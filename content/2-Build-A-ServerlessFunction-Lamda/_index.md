+++
title = "Build Serverless function with AWS Lamda"
date = 2024
weight = 4
chapter = false
pre = "<b>3. </b>"
+++

#### Create a Lambda function

In this section, you will create a Lambda function that is triggered when a user signs up for the application. The Lambda function will capture the user's email and save it in the database.

In you project directory:

1. Navigate to the profilesapp/amplify/auth folder
2. Create a new folder inside the amplify/auth folder and name it _**post-confirmation**_
3. Then create 2 files inside the _**post-confirmation**_ folder, name them **resource.ts** and **handler.ts** respectively.
   ![Create Lambda Function](/images/workshop-setup/2_1_create_folder_post.png?width=full)

#### Update the resource.ts file with the following code, then save it.:

![Update Resource.TS](/images/workshop-setup/2_1_updateResourceTS.png?width=full)

```bash
import { defineFunction } from '@aws-amplify/backend';

export const postConfirmation = defineFunction({
  name: 'post-confirmation',
});
```

#### Update the hanlder.ts file with the following code, then save it.:

![Update Handler.TS](/images/workshop-setup/2_1_updateHandlerTS.png?width=full)

```bash
import type { PostConfirmationTriggerHandler } from "aws-lambda";

export const handler: PostConfirmationTriggerHandler = async (event) => {
  return event;
};
```

You have defined a Lambda function using Amplify. The function is named post-confirmation and is triggered when a user signs up for the application. The function returns the event object.
