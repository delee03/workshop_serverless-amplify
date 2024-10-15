+++
title = "Triển khai giao diện người dùng"
date = 2024
weight = 3
chapter = false
pre = "<b>6.3. </b>"
+++

1. Điều hướng đến tệp profilesapp/src/main.jsx và cập nhật nó với mã sau. Sau đó, lưu tệp.

![Cập nhật App.JSX](/images/workshop-setup/5_Root.png?width=full)

```typescript
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App.jsx";
import "./index.css";
import { Authenticator } from "@aws-amplify/ui-react";

ReactDOM.createRoot(document.getElementById("root")).render(
    <React.StrictMode>
        <Authenticator>
            <App />
        </Authenticator>
    </React.StrictMode>
);
```

Bạn đã cập nhật tệp main.jsx để bao gồm thành phần Authenticator từ thư viện Amplify UI. Thành phần Authenticator cung cấp một tập hợp các thành phần giao diện người dùng xác thực được xây dựng sẵn mà bạn có thể sử dụng để tạo luồng đăng ký và đăng nhập cho ứng dụng của mình.

2. Mở tệp profilesapp/src/App.jsx và cập nhật nó với mã sau. Sau đó, lưu tệp.

Mã bắt đầu bằng cách cấu hình thư viện Amplify với tệp cấu hình khách hàng (amplify_outputs.json). Sau đó, nó tạo ra một khách hàng dữ liệu bằng cách sử dụng hàm generateClient(). Ứng dụng sẽ sử dụng khách hàng dữ liệu để lấy dữ liệu hồ

```typescript
import { useState, useEffect } from "react";
import {
    Button,
    Heading,
    Flex,
    View,
    Grid,
    Divider,
} from "@aws-amplify/ui-react";
import { useAuthenticator } from "@aws-amplify/ui-react";
import { Amplify } from "aws-amplify";
import "@aws-amplify/ui-react/styles.css";
import { generateClient } from "aws-amplify/data";
import outputs from "../amplify_outputs.json";
/**
 * @type {import('aws-amplify/data').Client<import('../amplify/data/resource').Schema>}
 */

Amplify.configure(outputs);
const client = generateClient({
    authMode: "userPool",
});

export default function App() {
    const [userprofiles, setUserProfiles] = useState([]);
    const { signOut } = useAuthenticator((context) => [context.user]);

    useEffect(() => {
        fetchUserProfile();
    }, []);

    async function fetchUserProfile() {
        const { data: profiles } = await client.models.UserProfile.list();
        setUserProfiles(profiles);
    }

    return (
        <Flex
            className="App"
            justifyContent="center"
            alignItems="center"
            direction="column"
            width="70%"
            margin="0 auto"
        >
            <Heading level={1}>My Profile</Heading>

            <Divider />

            <Grid
                margin="3rem 0"
                autoFlow="column"
                justifyContent="center"
                gap="2rem"
                alignContent="center"
            >
                {userprofiles.map((userprofile) => (
                    <Flex
                        key={userprofile.id || userprofile.email}
                        direction="column"
                        justifyContent="center"
                        alignItems="center"
                        gap="2rem"
                        border="1px solid #ccc"
                        padding="2rem"
                        borderRadius="5%"
                        className="box"
                    >
                        <View>
                            <Heading level="3">{userprofile.email}</Heading>
                        </View>
                    </Flex>
                ))}
            </Grid>
            <Button onClick={signOut}>Sign Out</Button>
        </Flex>
    );
}
```

3. Mở một cửa sổ terminal mới, điều hướng đến thư mục gốc của dự án của bạn (profilesapp), và chạy lệnh sau để khởi chạy ứng dụng:

```bash
npm run dev
```

4. Chọn đường dẫn localhost với cổng 5173 để mở ứng dụng Vite + React .

![Local Host](/images/workshop-setup/RunLocalhost.png?width=full)

5. Chọn **Create Account tab**, đăng kí tải khoản bằng cách nhập **địa chỉ email address và a password**. Sau đó, **choose Create Account**.

![Local Host Website](/images/workshop-setup/5_Localhost1.png?width=full)

6. Bạn sẽ nhận được mã xác minh được gửi đến email của bạn. Nhập mã xác minh để đăng nhập vào ứng dụng.

![Local Host Website](/images/workshop-setup/5_3_DienCodeOTP.png?width=full)

![Local Host Website](/images/workshop-setup/5_3_CodeEmail.png?width=full)

7. Khi đã đăng nhập, ứng dụng sẽ hiển thị địa chỉ email của bạn và một nút Đăng Xuất.

![Local Host Website](/images/workshop-setup/5_3_LoginSuccessful.png?width=full)

Như bạn có thể thấy, bạn có thể đăng nhập vào ứng dụng và xem thông tin hồ sơ của mình tại localhost.

8. Bây giờ, bạn có thể đẩy các thay đổi lên kho lưu trữ GitHub của mình bằng cách chạy các lệnh sau trong terminal:

```bash
git add -A
git commit -m "Thêm tính tương tác vào ứng dụng web hiển thị thông tin hồ sơ người dùng"
git push

```

9. AWS Amplify tự động xây dựng mã nguồn của bạn và triển khai ứng dụng của bạn tại _https://...amplifyapp.com_, và trên mỗi lần git push, phiên bản triển khai của bạn sẽ được cập nhật. Chọn nút **Visit deployed URL** để xem ứng dụng web của bạn đang chạy trực tiếp, bạn có thể sử dụng tab **Host** để triển khai ứng dụng của mình lên mạng phân phối nội dung toàn cầu (CDN) của AWS và xem nó trực tuyến trong Amplify Console.

![Automatically](/images/workshop-setup/5_End_AutoDeploy.png?width=full)

Bạn có thể đăng nhập vào ứng dụng và xem thông tin hồ sơ của mình tại URL đã triển khai của bạn.

![ Host Website](/images/workshop-setup/DangNhapThanhCong1.png?width=full)

Bạn đã triển khai thành công giao diện người dùng cho ứng dụng web của mình. Bây giờ bạn có thể xem thông tin hồ sơ của mình và đăng xuất khỏi ứng dụng.

10. Bây giờ, bạn có thể truy cập vào bảng DynamoDB của mình để xem dữ liệu đã được lưu khi bạn đăng ký.

Bước 1: Mở AWS Management Console, chuyển hướng đến DynamoDB console.
bạn có thể thấy 2 table được tạo bởi Amplify CLI.

![ DynamoDB](/images/workshop-setup/5_KiemTraDynamoDB.png?width=full)

Bước 2: Chọn tab**Expolore items** , sau đó chọn table **UserProfile** để xem dữ liệu người dùng đã đăng kí.

![Record User Info](/images/workshop-setup/EndXemRecordAccount1.png?width=full)
