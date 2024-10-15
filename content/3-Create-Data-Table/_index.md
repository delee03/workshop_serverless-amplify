+++
title = "Creating Data Table with DynamoDB and GraphQL API"
date = 2024
weight = 5
chapter = false
pre = "<b>4. </b>"
+++

**Content:**

-   [Creating Data Table with DynamoDB](#creating-data-table-with-dynamodb)
-   [Modify Lamda function to connect to the API](#modify-lamda-function-to-connect-to-the-api)

#### Creating Data Table with DynamoDB

In this section, you will create a data model to persist data using a GraphQL API and Amazon DynamoDB. You will use the AWS Amplify CLI to create a GraphQL API, define a data model, and deploy the API to the cloud.

1. Set up Amplify CLI by running the following command:  
   In your project directory:
   Navigate to the profilesapp folder, amplify/data/resource.ts and update the file with the following code, then save it.

![Update resource.ts](/images/workshop-setup/3_1_updateData.png?width=full)

```bash

import { type ClientSchema, a, defineData } from "@aws-amplify/backend";
import { postConfirmation } from "../auth/post-confirmation/resource";

const schema = a
  .schema({
    UserProfile: a
      .model({
        email: a.string(),
        profileOwner: a.string(),
      })
      .authorization((allow) => [
        allow.ownerDefinedIn("profileOwner"),
      ]),
  })
  .authorization((allow) => [allow.resource(postConfirmation)]);
export type Schema = ClientSchema<typeof schema>;

export const data = defineData({
  schema,
  authorizationModes: {
    defaultAuthorizationMode: "apiKey",
    apiKeyAuthorizationMode: {
      expiresInDays: 30,
    },
  },
});

```

2. Open a new terminal window, navigate to your app's root folder (profilesapp), and run the following command to deploy cloud resources to AWS:

![Install NPX in Amplify CLI](/images/workshop-setup/3.NPX.png?width=45pc)

```bash
npx ampx sandbox

```

This command is used to deploy the backend resources defined in your Amplify project to AWS. It will provision the necessary cloud resources, such as the GraphQL API and DynamoDB table, based on your project's configuration.

3.  Once the cloud sandbox has been fully deployed, you will see a success message in the terminal. The file _amplify-outputs.json_ will be generated and add to your project directory.

![Deploy Sandbox successfull](/images/workshop-setup/3.1_AddSandbox.png?width=full)

4. Open the new terminal window, navigate to the profilesapp folder, and run the following command to generate the GraphQL API:

For example, if you want to generate the GraphQL API, run the following command:  
`npx ampx generate graphql-client-code --out amplify/auth/post-confirmation/graphql`.

```bash

npx ampx generate graphql-client-code --out <path-to-post-confirmation-handler-dir>/graphql

```

![Generate GrapQL successfull](/images/workshop-setup/3.1_generateGrapQL1.png?width=full)

This command generates the GraphQL API client code based on the schema defined in the GraphQL API. The generated code will be used in the next section to interact with the GraphQL API from the frontend.  
Amplify will create the folder amplify/auth/post-confirmation/graphql where you will find the client code to connect to the GraphQL API.

#### Modify Lamda function to connect to the API

In your project directory: navigate to the amplify/auth/post-confirmation/handler.ts file and update the file with the following code, then save it.

![Update Handler.TS](/images/workshop-setup/2_1_updateHandlerTS.png?width=full)

```bash

import type { PostConfirmationTriggerHandler } from "aws-lambda";
import { type Schema } from "../../data/resource";
import { Amplify } from "aws-amplify";
import { generateClient } from "aws-amplify/data";
import { env } from "$amplify/env/post-confirmation";
import { createUserProfile } from "./graphql/mutations";

Amplify.configure(
  {
    API: {
      GraphQL: {
        endpoint: env.AMPLIFY_DATA_GRAPHQL_ENDPOINT,
        region: env.AWS_REGION,
        defaultAuthMode: "iam",
      },
    },
  },
  {
    Auth: {
      credentialsProvider: {
        getCredentialsAndIdentityId: async () => ({
          credentials: {
            accessKeyId: env.AWS_ACCESS_KEY_ID,
            secretAccessKey: env.AWS_SECRET_ACCESS_KEY,
            sessionToken: env.AWS_SESSION_TOKEN,
          },
        }),
        clearCredentialsAndIdentityId: () => {
          /* noop */
        },
      },
    },
  }
);

const client = generateClient<Schema>({
  authMode: "iam",
});

export const handler: PostConfirmationTriggerHandler = async (event) => {
  await client.graphql({
    query: createUserProfile,
    variables: {
      input: {
        email: event.request.userAttributes.email,
        profileOwner: `${event.request.userAttributes.sub}::${event.userName}`,
      },
    },
  });

  return event;
};

```

You have created a data table and configured a GraphQL API to persist data in an Amazon DynamoDB database. Then, you updated the Lambda function to use the API.
