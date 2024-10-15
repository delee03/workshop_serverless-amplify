+++
title = "Tạo và triển khai ứng dụng Web với ReactJS"
date = 2024-10-14T00:38:32+07:00
weight = 3
chapter = false
pre = "<b>2. </b>"
+++

**Nội dung:**

-   [Tạo 1 ứng dụng ReactJS mới](#1-tạo-1-ứng-dụng-reactjs-mới)
-   [Khởi tạo 1 Github Repository](#2-khởi-tạo-1-github-repository)
-   [Tải các Amplify packages](#3-tải-các-amplify-packages)
-   [Triển khai ứng dụng web với AWS Amplify](#4-triển-khai-ứng-dụng-web-với-aws-amplify)

#### Tạo 1 ứng dụng ReactJS mới

Trong phần này, bạn sẽ tạo một ứng dụng React và triển khai nó lên Cloud sử dụng AWS Amplify.
AWS Amplify cung cấp một quy trình CI/CD dựa trên Git để xây dựng, triển khai và lưu trữ các ứng dụng web đơn trang hoặc các trang tĩnh với backend. Khi được kết nối với một kho Git, Amplify xác định các thiết lập xây dựng cho cả framework frontend và bất kỳ tài nguyên backend nào đã được cấu hình, và tự động triển khai các cập nhật với mỗi lần commit code.

Bạn sẽ bắt đầu bằng việc tạo một ứng dụng React mới và đẩy nó lên một kho GitHub. Sau đó, bạn sẽ kết nối kho này với dịch vụ lưu trữ web của AWS Amplify và triển khai nó lên một mạng phân phối nội dung (CDN) có sẵn toàn cầu được lưu trữ trên miền amplifyapp.com.

### 1. Tạo 1 ứng dụng ReactJS mới

Bước 1: Mở trình quản lý tệp của bạn, tạo một thư mục mới và đặt tên là <<Your-Project-Amplify>>, sau đó mở Visual Studio Code với thư mục vừa tạo và mở terminal trong VS Code. Chạy lệnh sau để tạo một ứng dụng React mới sử dụng Vite và React:

```bash
npm create vite@latest profilesapp -- --template react
cd profilesapp
npm install
npm run dev

```

![Create a Web Application](/images/workshop-setup/1.1_KhoiTaoDuAn.png?width=full)

Bước 2: Trong cửa sổ Terminal, chọn và mở đường dẫn có cổng 5173 để xem 1 ứng dụng React + Vite.

![Create a Web Application](/images/workshop-setup/RunLocalhost.png?width=full)

### 2. Khởi tạo 1 Github Repository

Trong bước này, bạn sẽ tạo một kho GitHub và lưu mã của bạn vào kho này. Bạn sẽ cần một tài khoản GitHub để hoàn thành bước này, nếu bạn chưa có tài khoản, [đăng ký tại đây](https://github.com/).

{{% notice warning%}}
Nếu bạn chưa từng sử dụng GitHub trên máy tính của mình, hãy làm theo [các bước này](https://docs.github.com/en/authentication/connecting-to-github-with-ssh) trước khi tiếp tục.

{{% /notice%}}

Bước 1: Mở một tab trình duyệt mới và điều hướng đến [GitHub tại https://github.com](https://github.com/)

Bước 2: Đăng nhập vào tài khoản GitHub của bạn.

Bước 3: Chọn **+** ở góc phải của trang home và chọn **New repository**.

Bước 4: Ở phần **Repository name** , điền tên repo `profile_app`.

![Create a Repository with Github](/images/workshop-setup/1.2_CreateRepository.png?width=full)

Mở mã nguồn của bạn đã khởi tạo trong Bước trước, nhấp chuột phải vào `profilesapp` và chọn `Open in Integrated Terminal`, sau đó chạy các lệnh sau để khởi tạo git và đẩy ứng dụng lên kho GitHub mới:

![Open Terminal Correctly in VS Code](/images/workshop-setup/1.3_Mo_Dung_TerminalDuAn_CaiAmplify.png?width=full)

{{% notice note%}}
Lưu ý: thay thế GitHub URL trong câu lệnh trên bằng GitHub URL của bạn.
{{% /notice%}}

**Chạy câu lệnh sau trong terminal để đẩy code lên Github:**

```bash
    git init
    git add .
    git commit -m "first commit"
    git remote add origin https://github.com/<your-username>/profile_app
    git branch -M main

    git push -u origin main
```

### 3. Tải các Amplify packages

1. Mở một cửa sổ terminal mới, điều hướng đến thư mục gốc của ứng dụng của bạn (profilesapp) mở trong Integrated Terminal bằng cách nhấp chuột phải vào tệp _package.json_, mục đích là điều hướng chính xác đến thư mục gốc, và chạy lệnh sau:

![Open Terminal Correctly to Install Amplify in VS Code](/images/workshop-setup/1.3_Mo_Dung_TerminalDuAn_CaiAmplify-Copy.png?width=full)

**Chạy lệnh sau Amplify CLI:**

```bash
npm create amplify@latest -y

```

2. Chạy lệnh trước đó sẽ tạo một dự án Amplify nhỏ bên trong trong thư mục của ứng dụng.

![Install Successfull Amplify](/images/workshop-setup/1.3_TaiAmplifySuccess.png?width=full)

3. Trong cửa sổ Terminal của bạn, chạy lệnh sau để đẩy các thay đổi lên GitHub:

```bash
git add .
git commit -m "Add Amplify installed"
git push
```

Nếu bạn đã đẩy thành công các thay đổi lên GitHub, bạn sẽ thấy thông báo sau trong terminal:

![Push Changed filed to Github](/images/workshop-setup/1.3_PushCode.png?width=full)

### 4. Triển khai ứng dụng web với AWS Amplify

1. Đăng nhập vào bảng điều khiển quản lý AWS trong một cửa sổ trình duyệt mới, và mở bảng điều khiển AWS Amplify tại [https://console.aws.amazon.com/amplify/](https://console.aws.amazon.com/amplify/).

![Image of AWS Amplify Service](/images/workshop-setup/Amplify_Service.png?width=full)

<!-- ![Install Successfull Amplify](/images/workshop-setup/1.3_TaiAmplifySuccess.png?width=full) -->

2. Chọn **Deploy** tại chính giữa cửa sổ màn hình.

![Image of AWS Amplify Console](/images/workshop-setup/1.4_Deploy_With_Amplify.png?width=full)

3. Trên trang Bắt đầu xây dựng với Amplify, cho mục Triển khai ứng dụng của bạn, **chọn GitHub**, và chọn **Next**.

![Choose Github to Deploy](/images/workshop-setup/1.4_DeployOnGithub1.png?width=full)

4. Tiếp theo, xác thực với GitHub bằng cách chọn **Authorize AWS Amplify**.

![Athourize with Github](/images/workshop-setup/1_4_Authorization.png?width=35pc)

5. Chọn kho lưu trữ bạn muốn triển khai trên Amplify, xác thực với GitHub bằng cách chọn **Only selected repositories** (bạn có thể chọn tất cả các kho lưu trữ, trong trường hợp này tôi chọn Only selected repositories) và chọn **Dự án của bạn: Profile_app** sau đó nhấp vào **Install & Authorize**.

![Athourize with Github](/images/workshop-setup/1_4_SelectRepositoryCreated.png?width=40pc)

6. Bạn sẽ tự động được chuyển hướng về cửa sổ Amplify console, chọn **the repository**, **main branch** mà bạn muốn deploy, sau đó chọn **Next**.
   ![Select Repository Uploaded](/images/workshop-setup/1_4_SelectRepository.png?width=full)

7. Giữ nguyên cài đặt mặc định và chọn **Next**.
   ![Default Setting Config](/images/workshop-setup/1_4_ConfigDefault.png?width=full)

8. Xem lại các thay đổi và nhấn **Save and deploy**

![Review Setting and deploy](/images/workshop-setup/1_4_Review.png?width=full)

**AWS Amplify** sẽ xây dựng mã nguồn của bạn và triển khai ứng dụng của bạn tại _https://...amplifyapp.com_, và mỗi lần bạn đẩy mã lên git, phiên bản triển khai của bạn sẽ được cập nhật tự động. Quá trình triển khai ứng dụng ReactJS của bạn có thể mất đến 5 phút.

9. Một khi xây dựng hoàn tất, bạn có thể chọn **Visit deployed URL** và xem website của mình trực tiếp trên môi trường Internet.

![Deploy Successfull](/images/workshop-setup/1_4_DeploySuccess.png?width=full)

10. Bây giờ bạn có thể xem ứng dụng ReactJS đã triển khai của mình trên bảng điều khiển AWS Amplify. Bạn có thể xem tên miền và trạng thái của việc triển khai.
    Nếu bạn thấy màn hình như này, **bạn đã triển khai dự án thành công** ứng dụng ReactJS trên AWS Amplify.

![Deploy Website](/images/workshop-setup/1_4_SuccessfulDeploy1.png?width=full)

**Good job** Bạn đã triển khai một ứng dụng React trên AWS Cloud bằng cách tích hợp với GitHub và sử dụng AWS Amplify. Với AWS Amplify, bạn có thể liên tục triển khai ứng dụng của mình trên Cloud và lưu trữ nó trên một CDN có sẵn toàn cầu.
