+++
title = "Giới thiệu"
date = 2024
weight = 2
chapter = false
pre = "<b>1. </b>"
+++

#### Tổng quan

Trong workshop này, bạn sẽ học cách tạo một **ứng dụng web full-stack đơn giản** sử dụng **AWS Amplify**. Xuyên suốt workshop, bạn sẽ **xây dựng** và **host** một ứng dụng React **trên AWS**, sử dụng Amplify để **thêm tính năng xác thực**, **dữ liệu**, và **một hàm serverless** để thu thập email của người dùng đã đăng ký và lưu nó vào cơ sở dữ liệu. Sau đó, bạn sẽ triển khai một frontend cho ứng dụng của mình, **tích hợp với các tài nguyên đám mây** của bạn.

#### Lược đồ kiến trúc

Sơ đồ sau đây cung cấp một hình ảnh trực quan về các dịch vụ được sử dụng trong lab đơn giản này và cách chúng được kết nối. Ứng dụng này sử dụng **AWS Amplify, GraphQL API, AWS Lambda, và Amazon DynamoDB.**

Khi bạn đi qua workshop, bạn sẽ tìm hiểu chi tiết về các dịch vụ này và tìm thấy các tài nguyên giúp bạn nắm bắt chúng nhanh chóng.

![Architecture Application Schema](/images/workshop-setup/ArchitectureSystem.png?width=90pc)

#### Những gì bạn sẽ đạt được

**Host**: Xây dựng và triển khai một ứng dụng React trên mạng phân phối nội dung toàn cầu (CDN) của AWS.  
**Authenticate**: Thêm xác thực vào ứng dụng của bạn để kích hoạt chức năng đăng nhập và đăng xuất.  
**Database**: Tích hợp API thời gian thực, cơ sở dữ liệu và một hàm serverless.
**Function**: Triển khai một hàm lambda được kích hoạt khi người dùng đăng ký vào ứng dụng.

#### Yêu cầu

**1 tài khoản AWS:** với quyền quản trị viên  
**Nodejs and npm:** Đã cài đặt trên máy tính của bạn  
**Git & GitHub account:** Kiến thức cơ bản về Git và GitHub
**Visual Studio Code:** Đã cài đặt trên máy tính của bạn  
**Nếu bạn có tài khoản AWS FreeTier thì thật tuyệt vời**

{{% notice note%}}
Các tài khoản được tạo trong vòng 24 giờ qua có thể chưa có quyền truy cập vào các dịch vụ cần thiết cho lab này
{{% /notice%}}

#### Nội dung chính

1. [Giới thiệu](0-Introdution/)
2. [Tạo và Triển khai 1 ứng dụng web ReactJS](1-Create-A-Web-App/)
3. [Xây dựng hàm Serverless với AWS Lamda](2-Build-A-ServerlessFunction-Lamda/)
4. [Tạo data table với DynamoDB](3-Create-Data-Table/)
5. [Liên kết hàm Serverless đến ứng dụng Web](4-Link-ServerlessFunction-ToWebApp/)
6. [Thêm tính tương tác vào ứng dụng web](5-Add-Interactivity/)
7. [Dọn dẹp tài nguyên](6-CleanUp/)
 <!-- need to remove parenthesis for path in Hugo 0.88.1 for Windows-->
