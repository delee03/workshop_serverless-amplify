+++
title = "Xây dựng hàm Serverless với AWS Lamda"
date = 2024
weight = 4
chapter = false
pre = "<b>3. </b>"
+++

#### Tạo 1 hàm Lambda

Trong phần này, bạn sẽ tạo một hàm Lambda được kích hoạt khi người dùng đăng ký vào ứng dụng. Hàm Lambda sẽ thu thập email của người dùng và lưu nó vào cơ sở dữ liệu.

Trong thư mục dự án của bạn:

1. Di chuyển đến thư mục profilesapp/amplify/auth
2. Tạo một thư mục mới bên trong thư mục amplify/auth và đặt tên là _**post-confirmation**_
3. Sau đó tạo 2 tệp trong thư mục _**post-confirmation**_, đặt tên là **resource.ts** và **handler.ts** tương ứng.
   ![Create Lambda Function](/images/workshop-setup/2_1_create_folder_post.png?width=full)

#### Cập nhật tệp resource.ts với mã sau, sau đó lưu lại:

![Update Resource.TS](/images/workshop-setup/2_1_updateResourceTS.png?width=full)

```bash
import { defineFunction } from '@aws-amplify/backend';

export const postConfirmation = defineFunction({
  name: 'post-confirmation',
});
```

#### Cập nhật tệp handler.ts với mã sau, sau đó lưu lại:

![Update Handler.TS](/images/workshop-setup/2_1_updateHandlerTS.png?width=full)

```bash
import type { PostConfirmationTriggerHandler } from "aws-lambda";

export const handler: PostConfirmationTriggerHandler = async (event) => {
  return event;
};
```

Bạn đã tạo thành công một hàm Lambda sử dụng Amplify. Hàm được đặt tên là post-confirmation và được kích hoạt khi người dùng đăng ký vào ứng dụng. Hàm trả về đối tượng sự kiện.
