+++
title = "Thiết lập Tài Khoản AWS"
date = 2021
weight = 1
chapter = false
+++

# Tạo tài khoản AWS đầu tiên

#### Tổng quan
Trong workshop này, bạn sẽ hướng dẫn người tham gia cách sử dụng **AWS Amplify** để xây dựng một **ứng dụng web serverless** với sự hỗ trợ của Generative AI thông qua **Amazon Bedrock** và mô hình nền **Claude 3 Sonnet**. Người dùng sẽ có thể nhập danh sách nguyên liệu, và ứng dụng sẽ tự động tạo ra những công thức nấu ăn ngon dựa trên các nguyên liệu đã nhập. Ứng dụng này bao gồm một giao diện người dùng dựa trên HTML để nhập nguyên liệu và một backend web app để yêu cầu công thức nấu ăn được tạo bởi AI.

#### Tài khoản AWS (AWS Account)
**Tài khoản AWS** là phương tiện để bạn có thể truy cập và sử dụng những tài nguyên và dịch vụ của AWS. Theo mặc định, mỗi tài khoản AWS sẽ có một *root user*. *Root user* có toàn quyền với tài khoản AWS của bạn, và quyền hạn của root user không thể bị giới hạn. Nếu bạn mới sử dụng tài khoản AWS lần đầu tiên, bạn sẽ truy cập vào tài khoản dưới danh nghĩa của *root user*.

{{% notice note %}}
Chính vì quyền hạn của **root user** không thể bị giới hạn, AWS khuyên bạn không nên sử dụng trực tiếp *root user* cho bất kỳ công tác nào. Thay vào đó, bạn nên tạo ra một *IAM User* và trao quyền quản trị cho *IAM User* đó để dễ dàng quản lý và giảm thiểu rủi ro.
{{% /notice %}}

#### MFA (Multi-factor Authentication)
**MFA** là một tính năng được sử dụng để gia tăng bảo mật của tài khoản AWS. Nếu MFA được kích hoạt, bạn sẽ phải nhập mã OTP (One-time Password) mỗi lần bạn đăng nhập vào tài khoản AWS.

#### IAM Group 
**IAM Group**  là một công cụ quản lý người dùng (*IAM User*) của AWS. Một IAM Group có thể chứa nhiều IAM User. Các IAM User ở trong một IAM Group đều hưởng chung quyền hạn mà IAM Group đó được gán cho.

#### IAM User
**IAM User** là một đơn vị người dùng của AWS. Khi bạn đăng nhập vào AWS, bạn sẽ phải đăng nhập dưới danh nghĩa của một IAM User. Nếu bạn mới đăng nhập vào AWS lần đầu tiên, bạn sẽ đăng nhập dưới danh nghĩa của *root user* (tạm dịch là người dùng gốc). Ngoài *root user* ra, bạn có thể tạo ra nhiều IAM User khác để cho phép người khác truy cập **dài hạn** vào tài nguyên AWS trong tài khoản AWS của bạn.


#### AWS Support
**AWS Support** là một đơn vị cung cấp các dịch vụ hỗ trợ khách hàng của AWS.


#### Nội dung chính

1. [Tạo tài khoản AWS](1-create-new-aws-account/)
2. [Thiết lập MFA cho tài khoản AWS (Root)](2-mfa-setup-for-aws-user-(root)/)
3. [Tài khoản và Nhóm Admin](3-create-admin-user-and-group/)
4. [Hỗ trợ Xác thực Tài khoản](4-verify-new-account/)