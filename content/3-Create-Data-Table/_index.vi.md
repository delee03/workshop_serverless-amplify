+++
title = "Tạo Data Table với DynamoDB và GraphQL API"
date = 2024
weight = 5
chapter = false
pre = "<b>4. </b>"
+++

**Nội dung:**

-   [Khởi tạo Data Table với DynamoDB](#Tạo-Data-Table-với-DynamoDB)
-   [Cập nhật Lamda function để kết nối tới API](#Cập-nhật-Lamda-function-để-kết-nối-tới-API)

#### Tạo Data Table với DynamoDB

Trong phần này, bạn sẽ tạo một mô hình dữ liệu để lưu trữ dữ liệu bằng cách sử dụng GraphQL API và Amazon DynamoDB. Bạn sẽ sử dụng AWS Amplify CLI để tạo một GraphQL API, định nghĩa một mô hình dữ liệu, và triển khai API lên đám mây.

1. Mở terminal, di chuyển đến thư mục dự án của bạn (profilesapp), và chạy lệnh sau để tạo một mô hình dữ liệu và triển khai API GraphQL:

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

2. Chạy lệnh sau để triển khai tài nguyên backend được xác định trong dự án Amplify của bạn lên AWS. Nó sẽ cung cấp các tài nguyên đám mây cần thiết, chẳng hạn như GraphQL API và bảng DynamoDB, dựa trên cấu hình của dự án của bạn.

![Install NPX in Amplify CLI](/images/workshop-setup/3.NPX.png?width=45pc)

```bash
npx ampx sandbox

```

3.  Sau khi sandbox đám mây đã được triển khai hoàn tất, bạn sẽ thấy một thông báo thành công trong terminal. Tệp _amplify-outputs.json_ sẽ được tạo và thêm vào thư mục dự án của bạn.

![Deploy Sandbox successfull](/images/workshop-setup/3.1_AddSandbox.png?width=full)

4. Mở cửa sổ terminal mới, điều hướng đến thư mục profilesapp, và chạy lệnh sau để tạo GraphQL API:

Ví dụ, nếu bạn muốn tạo GraphQL API, hãy chạy lệnh sau:  
`npx ampx generate graphql-client-code --out amplify/auth/post-confirmation/graphql`.

```bash

npx ampx generate graphql-client-code --out <path-to-post-confirmation-handler-dir>/graphql

```

![Generate GrapQL successfull](/images/workshop-setup/3.1_generateGrapQL1.png?width=full)

Lệnh này tạo mã client API GraphQL dựa trên schema được định nghĩa trong API GraphQL. Mã được tạo ra sẽ được sử dụng trong phần tiếp theo để tương tác với API GraphQL từ frontend.  
Amplify sẽ tạo thư mục `amplify/auth/post-confirmation/graphql` nơi bạn sẽ tìm thấy mã client để kết nối với API GraphQL.

#### Cập nhật Lamda function để kết nối tới API

Trong thư mục dự án của bạn: điều hướng đến tệp `amplify/auth/post-confirmation/handler.ts` và cập nhật tệp với mã sau, sau đó lưu lại.

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

Bạn đã tạo một bảng dữ liệu và cấu hình một API GraphQL để lưu trữ dữ liệu trong cơ sở dữ liệu Amazon DynamoDB. Sau đó, bạn đã cập nhật hàm Lambda để sử dụng API.
