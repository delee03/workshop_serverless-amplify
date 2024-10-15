+++
title = "Liên kết hàm Serverless đến ứng dụng Web"
date = 2024
weight = 6
chapter = false
pre = "<b>5. </b>"
+++

Trong phần này, Bạn sẽ cập nhật tài nguyên Amplify Auth để sử dụng hàm Lambda mà bạn đã tạo trong phần trước dưới dạng lệnh gọi trên Amazon Cognito. Khi người dùng hoàn tất đăng ký, hàm này sẽ sử dụng API GraphQL và ghi lại email của người dùng vào bảng DynamoDB.

<!-- **Content:**

-   [Verify your account information](#verify-your-account-information)
-   [Create a support case with AWS Support](#create-a-support-case-with-aws-support) -->

#### Set up Amplify Auth

1. Tài nguyên xác thực của bạn được cấu hình cho phép người dùng đăng ký bằng email, nhưng bạn cần cập nhật tài nguyên để gọi hàm postConfirmation đã tạo trước đó khi người dùng đăng ký.

![Update Auth](/images/workshop-setup/4_1_UpdateResource1.png?width=full)

Thêm đoạn code sau đây vào file `amplify/auth/resource.ts`:

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

2. Sandbox sẽ tự động được cập nhật và triển khai lại khi tệp được cập nhật. Nếu sandbox không chạy, bạn có thể chạy lệnh sau trong cửa sổ terminal mới để khởi động nó.

```bash
npx ampx sandbox

```

3. Khi sandbox trên đám mây đã được triển khai hoàn toàn, terminal của bạn sẽ hiển thị thông báo xác nhận và tệp amplify_outputs.json sẽ được tạo/cập nhật và thêm vào dự án profilesapp của bạn.

![Amplify Outputs](/images/workshop-setup/4.1_CheckSandboxRunning.png?width=full)

Bạn đã sử dụng Amplify để cấu hình xác thực và cấu hình hàm Lambda để được gọi khi người dùng đăng nhập vào ứng dụng.
