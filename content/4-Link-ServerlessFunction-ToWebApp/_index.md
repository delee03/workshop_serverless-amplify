+++
title = "Link Serverless function to Web Application"
date = 2024
weight = 6
chapter = false
pre = "<b>5. </b>"
+++

In this section, you will update the Amplify Auth resources to use the Lambda function you created in the previous module as an Amazon Cognito post confirmation invocation. When the user completes the sign up, the function will use the GraphQL API and capture the user’s email into the DynamoDB table.

<!-- **Content:**

-   [Verify your account information](#verify-your-account-information)
-   [Create a support case with AWS Support](#create-a-support-case-with-aws-support) -->

#### Set up Amplify Auth

1. Your auth resource is configured allowing the user to sign up using email, but you need to update the resource to invoke the previously created postConfirmation function when the user signs up.

![Update Auth](/images/workshop-setup/4_1_UpdateResource1.png?width=full)

Add the following code to the `amplify/auth/resource.ts` file:

```bash
import { defineAuth } from '@aws-amplify/backend';
import { postConfirmation } from './post-confirmation/resource';

export const auth = defineAuth({
  loginWith: {
    email: true,
  },
  triggers: {
    postConfirmation
  }
});
```

<!-- {{% notice note%}}
You can create support requests with AWS Support even if your account is not activated.
{{% /notice%}} -->

2. The sandbox will automatically get updated and redeployed once the file is updated. If the sandbox is not running, you can run the following command in a new terminal window to start it.

```bash
npx ampx sandbox

```

3. Once the cloud sandbox has been fully deployed, your terminal will display a confirmation message and the amplify_outputs.json file will be generated/updated and added to your profilesapp project.

![Amplify Outputs](/images/workshop-setup/4.1_CheckSandboxRunning.png?width=full)

You used Amplify to configure auth and configured the Lambda function to be invoked when the user signs in to the app.
