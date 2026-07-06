---
title: "Bản đề xuất"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Minecraft Security Based on AWS
## Giải pháp bảo mật, giám sát và tự động phản ứng cho Minecraft Server trên AWS

### 1. Tóm tắt điều hành

**Minecraft Security Based on AWS** là một dự án triển khai máy chủ Minecraft trên nền tảng Amazon Web Services (AWS), kết hợp các lớp bảo mật mạng, giám sát mối đe dọa và tự động phản ứng sự cố nhằm biến một game server thông thường thành một hệ thống có khả năng phòng thủ chủ động.

Dự án tập trung vào việc bảo vệ Minecraft Server trước các rủi ro phổ biến như quét cổng, tấn công brute-force SSH, lộ địa chỉ IP thật của máy chủ, phá hoại dữ liệu game và tấn công từ chối dịch vụ. Hệ thống sử dụng các dịch vụ AWS như **EC2, VPC, Security Group, AWS Systems Manager, Amazon GuardDuty, EventBridge, Lambda, SNS, CloudWatch, AWS Backup, Network Load Balancer và AWS Global Accelerator** để xây dựng một mô hình bảo mật hoàn chỉnh.

Điểm nổi bật của dự án là khả năng xây dựng một mô hình **SOAR (Security Orchestration, Automation and Response)** thu nhỏ: khi GuardDuty phát hiện hành vi bất thường, EventBridge sẽ kích hoạt Lambda để tự động chặn IP nguy hiểm và gửi cảnh báo đến người quản trị thông qua Email.

---

### 2. Ý tưởng & Mục tiêu (Tuyên bố vấn đề)

#### 2.1 Bối cảnh & Bài toán

*   **Mục đích hệ thống:**

    Dự án được xây dựng nhằm triển khai một máy chủ Minecraft có khả năng vận hành ổn định trên AWS, đồng thời được bảo vệ bằng nhiều lớp bảo mật khác nhau. Thay vì chỉ chạy server game đơn giản trên một máy ảo, hệ thống được thiết kế theo hướng bảo mật chủ động, có khả năng giám sát, phát hiện và phản ứng tự động trước các dấu hiệu tấn công.

*   **Đối tượng sử dụng:**

    Hệ thống hướng đến các nhóm người dùng sau:

    * Người quản trị máy chủ Minecraft muốn triển khai server an toàn trên Cloud.
    * Sinh viên hoặc học viên cần một dự án thực hành về AWS Security.
    * Nhóm học tập muốn mô phỏng quy trình phát hiện và phản ứng sự cố bảo mật trên môi trường thực tế.
    * Người chơi Minecraft cần kết nối đến server ổn định, bảo mật và ít bị gián đoạn.

*   **Vấn đề giải quyết:**

    Các máy chủ game public thường gặp nhiều rủi ro bảo mật như:

    * Lộ địa chỉ IP thật của máy chủ.
    * Bị quét cổng để tìm dịch vụ đang mở.
    * Bị brute-force SSH nếu mở port 22 ra Internet.
    * Bị tấn công DDoS hoặc flood traffic vào port game.
    * Bị phá hoại dữ liệu thế giới Minecraft.
    * Không có hệ thống cảnh báo hoặc phản ứng tự động khi có sự cố.

    Dự án giải quyết các vấn đề trên bằng cách triển khai nhiều lớp phòng thủ, bao gồm giới hạn cổng mạng, quản trị không cần SSH keypair, phát hiện mối đe dọa bằng GuardDuty, tự động chặn IP bằng Lambda, gửi cảnh báo bằng SNS và sao lưu dữ liệu định kỳ bằng AWS Backup.

---

#### 2.2 Mục tiêu cụ thể

*   **Output mong muốn:**

    * Một Minecraft Server chạy trên Amazon EC2.
    * Hạ tầng mạng AWS gồm VPC, Public Subnet, Security Group và Network ACL.
    * Máy chủ được quản trị thông qua **AWS Systems Manager Session Manager**, không cần mở port SSH 22.
    * Hệ thống phát hiện xâm nhập sử dụng **Amazon GuardDuty**.
    * Hệ thống tự động phản ứng sử dụng **Amazon EventBridge + AWS Lambda**.
    * Cơ chế gửi cảnh báo qua Email bằng **Amazon SNS**.
    * Cơ chế sao lưu dữ liệu bằng **AWS Backup**.
    * Cơ chế che giấu IP thật của EC2 bằng **AWS Global Accelerator + Network Load Balancer**.
    * Tài liệu hướng dẫn triển khai, vận hành, demo và dọn dẹp tài nguyên.

*   **Tiêu chí đánh giá thành công:**

    * Minecraft Server có thể hoạt động và cho phép người chơi kết nối thông qua port 25565.
    * Security Group chỉ mở đúng port cần thiết cho Minecraft, không mở SSH public.
    * Người quản trị có thể truy cập EC2 bằng Session Manager.
    * GuardDuty có thể tạo finding hoặc sample finding để mô phỏng tấn công.
    * EventBridge kích hoạt Lambda khi có finding từ GuardDuty.
    * Lambda có thể thực hiện phản ứng tự động, ví dụ chặn IP hoặc ghi log xử lý.
    * SNS gửi được email cảnh báo đến người quản trị.
    * AWS Backup tạo được bản sao lưu định kỳ cho EC2.
    * Global Accelerator cung cấp IP tĩnh để người chơi kết nối, giúp hạn chế việc lộ IP thật của EC2.

---

#### 2.3 Phù hợp với chương trình

*   **Use-case gắn với AWS Security:**

    Dự án mô phỏng một tình huống thực tế trong lĩnh vực Cloud Security: triển khai dịch vụ public trên Internet và xây dựng hệ thống giám sát, phát hiện, phản ứng tự động khi có hành vi bất thường. Đây là một use-case phù hợp với các nội dung về AWS Networking, IAM, Monitoring, Threat Detection và Incident Response.

*   **Đúng trọng tâm Cloud:**

    Dự án sử dụng nhiều dịch vụ cốt lõi của AWS để thể hiện các nguyên tắc quan trọng trong điện toán đám mây:

    * **Security:** Bảo vệ hệ thống bằng Security Group, IAM, SSM và GuardDuty.
    * **Monitoring:** Theo dõi hoạt động bằng CloudWatch và GuardDuty.
    * **Automation:** Tự động phản ứng với EventBridge và Lambda.
    * **Resilience:** Sao lưu và khôi phục bằng AWS Backup.
    * **Availability:** Sử dụng Network Load Balancer và Global Accelerator để cải thiện khả năng truy cập.
    * **Cost Awareness:** Có quy trình tắt và xóa tài nguyên để tránh phát sinh chi phí.

*   **Giải pháp đề xuất:**

    Xây dựng một hệ thống Minecraft Server bảo mật trên AWS gồm:

    1.  **Game Server Layer:** Sử dụng Amazon EC2 chạy Ubuntu và PaperMC Minecraft Server.
    2.  **Network Security Layer:** Sử dụng VPC, Subnet, Security Group và NACL để kiểm soát traffic.
    3.  **Secure Administration Layer:** Sử dụng AWS Systems Manager Session Manager để quản trị EC2 mà không cần mở port SSH.
    4.  **Threat Detection Layer:** Sử dụng Amazon GuardDuty để phát hiện các hành vi đáng ngờ.
    5.  **Automated Response Layer:** Sử dụng EventBridge để nhận sự kiện GuardDuty và kích hoạt Lambda.
    6.  **Notification Layer:** Sử dụng Amazon SNS để gửi Email cảnh báo.
    7.  **Backup & Recovery Layer:** Sử dụng AWS Backup để sao lưu định kỳ dữ liệu máy chủ.
    8.  **DDoS Mitigation & IP Protection Layer:** Sử dụng AWS Global Accelerator kết hợp Network Load Balancer để che giấu IP thật của EC2.

*   **Lợi ích và ROI (Hiệu quả đầu tư):**

    *   **Tăng cường bảo mật:** Server không mở port SSH public, giảm đáng kể nguy cơ brute-force.
    *   **Phản ứng nhanh:** Khi phát hiện hành vi bất thường, hệ thống có thể tự động xử lý thay vì chờ thao tác thủ công.
    *   **Giảm thiểu gián đoạn:** Backup định kỳ giúp khôi phục dữ liệu khi bị phá hoại hoặc lỗi hệ thống.
    *   **Dễ trình diễn:** Có thể demo bằng GuardDuty Sample Findings để mô phỏng tấn công mà không cần thực hiện tấn công thật.
    *   **Tối ưu chi phí học tập:** Hệ thống có thể tắt hoặc xóa tài nguyên sau khi demo để tránh phát sinh chi phí.

---

### 3. Kiến trúc giải pháp

Hệ thống được thiết kế theo mô hình bảo mật nhiều lớp, trong đó Minecraft Server được đặt trên EC2 và được bảo vệ bởi các thành phần mạng, giám sát, tự động hóa và sao lưu.

#### 3.1 Sơ đồ kiến trúc hệ thống

![Architecture](/images/2-Proposal/Architecture.png)

#### 3.2 Mô tả luồng kiến trúc

Người chơi sẽ không kết nối trực tiếp đến IP thật của EC2. Thay vào đó, người chơi kết nối đến IP tĩnh được cung cấp bởi **AWS Global Accelerator**. Traffic sau đó được chuyển đến **Network Load Balancer**, rồi tiếp tục chuyển đến EC2 đang chạy Minecraft Server trên port 25565.

Ở lớp bảo mật và giám sát, **Amazon GuardDuty** theo dõi các log và hành vi bất thường trong tài khoản AWS. Khi phát hiện finding, **Amazon EventBridge** sẽ nhận sự kiện và kích hoạt **AWS Lambda**. Lambda thực hiện hành động phản ứng như ghi log, chặn IP hoặc gửi cảnh báo. **Amazon SNS** được sử dụng để gửi Email thông báo đến người quản trị.

Đồng thời, **AWS Backup** đảm nhiệm việc sao lưu định kỳ máy chủ EC2 để phục vụ khôi phục khi có sự cố.

---

#### 3.3 Các dịch vụ AWS sử dụng

| Phân nhóm | Dịch vụ AWS | Lý do lựa chọn & Vai trò |
| :--- | :--- | :--- |
| **Compute** | Amazon EC2 | Chạy máy chủ Minecraft trên Ubuntu Server. EC2 đóng vai trò là thành phần xử lý chính của hệ thống game server. |
| **Game Server** | PaperMC / Minecraft Server | Cung cấp môi trường Minecraft Multiplayer để người chơi kết nối và tương tác. |
| **Networking** | Amazon VPC | Tạo môi trường mạng riêng biệt cho hệ thống, giúp kiểm soát subnet, route table và các lớp bảo mật mạng. |
| **Networking** | Public Subnet | Đặt EC2 và Load Balancer trong subnet có thể nhận traffic từ Internet theo đúng cấu hình bảo mật. |
| **Security** | Security Group | Chỉ mở port TCP 25565 cho Minecraft, không mở port 22 SSH public, giúp giảm nguy cơ brute-force. |
| **Security** | Network ACL | Bổ sung lớp kiểm soát traffic ở cấp subnet, hỗ trợ chặn IP khi cần thiết. |
| **Administration** | AWS Systems Manager Session Manager | Cho phép quản trị EC2 trực tiếp trên trình duyệt mà không cần keypair hoặc mở port SSH. |
| **Identity & Access** | IAM Role | Cấp quyền cho EC2 sử dụng Systems Manager và cấp quyền cho Lambda thực hiện hành động tự động. |
| **Threat Detection** | Amazon GuardDuty | Phát hiện các hành vi đáng ngờ như port scanning, SSH brute-force hoặc hoạt động bất thường trong tài khoản AWS. |
| **Event Routing** | Amazon EventBridge | Nhận sự kiện từ GuardDuty và định tuyến đến Lambda để xử lý tự động. |
| **Automation** | AWS Lambda | Thực hiện phản ứng tự động khi có cảnh báo, ví dụ chặn IP tấn công hoặc gửi cảnh báo. |
| **Notification** | Amazon SNS | Gửi Email cảnh báo đến người quản trị khi phát hiện sự cố bảo mật. |
| **Monitoring** | Amazon CloudWatch | Lưu trữ log, theo dõi hoạt động của Lambda và hỗ trợ kiểm tra kết quả khi demo. |
| **Backup** | AWS Backup | Tự động sao lưu máy chủ EC2, giúp khôi phục dữ liệu Minecraft khi bị lỗi hoặc bị phá hoại. |
| **Load Balancing** | Network Load Balancer | Phân phối traffic TCP port 25565 đến Minecraft Server, phù hợp với giao thức game ở tầng 4. |
| **Edge Networking** | AWS Global Accelerator | Cung cấp IP tĩnh toàn cầu, che giấu IP thật của EC2 và cải thiện khả năng truy cập của người chơi. |

---

### 4. Triển khai kỹ thuật

#### Các giai đoạn triển khai

Dự án được triển khai theo các giai đoạn chính sau:

1.  **Thiết lập mạng an toàn (VPC & Security Group):**

    * Tạo VPC riêng cho project.
    * Tạo Public Subnet.
    * Cấu hình Internet Gateway.
    * Tạo Security Group chỉ mở port TCP 25565.
    * Không mở port SSH 22 ra Internet.
    * Bật Auto-assign Public IPv4 cho subnet nếu cần.

2.  **Triển khai Minecraft Server & quản trị không dùng Keypair:**

    * Tạo EC2 Ubuntu.
    * Không sử dụng keypair truyền thống.
    * Gán IAM Role có policy `AmazonSSMManagedInstanceCore`.
    * Kết nối vào EC2 thông qua AWS Systems Manager Session Manager.
    * Cài đặt Java.
    * Tải và cấu hình PaperMC Minecraft Server.
    * Tạo user riêng tên `minecraft` để chạy server, không chạy bằng quyền root.
    * Chạy server ở chế độ nền bằng `screen`.

3.  **Thiết lập hệ thống phát hiện xâm nhập:**

    * Bật Amazon GuardDuty.
    * Theo dõi findings trong GuardDuty.
    * Sử dụng sample findings để phục vụ demo tấn công giả lập.

4.  **Thiết lập tự động phản ứng với Lambda & EventBridge:**

    * Tạo Lambda function xử lý sự kiện bảo mật.
    * Cấp quyền IAM cần thiết cho Lambda.
    * Tạo EventBridge Rule nhận sự kiện GuardDuty Finding.
    * Kết nối EventBridge với Lambda.
    * Kiểm tra log thực thi trong CloudWatch Logs.

5.  **Thiết lập sao lưu thảm họa với AWS Backup:**

    * Tạo Backup Vault.
    * Tạo Backup Plan.
    * Cấu hình backup theo giờ.
    * Gán EC2 Minecraft Server vào Backup Plan.
    * Thiết lập retention period để tự động xóa backup cũ.

6.  **Che giấu IP thật và kháng DDoS với Global Accelerator + NLB:**

    * Tạo Target Group cho port TCP 25565.
    * Tạo Network Load Balancer.
    * Gắn EC2 Minecraft Server vào Target Group.
    * Tạo AWS Global Accelerator.
    * Trỏ Global Accelerator đến Network Load Balancer.
    * Sử dụng IP tĩnh của Global Accelerator để người chơi kết nối.

7.  **Cấu hình thông báo Email:**

    * Tạo SNS Topic.
    * Tạo Email Subscription.
    * Xác nhận subscription trong Email.
    * Cập nhật Lambda để gửi cảnh báo qua SNS.

8.  **Quy trình vận hành và dọn dẹp tài nguyên:**

    * Bật Minecraft Server bằng chuỗi lệnh an toàn.
    * Kiểm tra trạng thái server bằng `screen` hoặc log.
    * Tắt server an toàn bằng lệnh `stop`.
    * Dọn dẹp Global Accelerator, NLB, EC2, Lambda, EventBridge, SNS, GuardDuty và AWS Backup sau khi hoàn thành project.

---

#### Yêu cầu chuẩn bị (Prerequisites)

*   **Tài nguyên & Công cụ:**

    * Tài khoản AWS có quyền tạo EC2, VPC, IAM, Lambda, EventBridge, SNS, GuardDuty, CloudWatch, AWS Backup, NLB và Global Accelerator.
    * Máy tính có cài Minecraft Java Edition để kiểm tra kết nối server.
    * Trình duyệt web để truy cập AWS Console.
    * Kiến thức cơ bản về Linux command line.

*   **Kiến thức nền tảng:**

    * VPC Networking: Subnet, Route Table, Internet Gateway, Security Group.
    * EC2 và IAM Role.
    * AWS Systems Manager Session Manager.
    * Amazon GuardDuty và CloudWatch Logs.
    * Lambda và EventBridge.
    * SNS Email Notification.
    * Backup và Disaster Recovery.
    * Khái niệm DDoS và bảo vệ IP thật của server.

---

### 5. Lộ trình & Mốc triển khai

*   **Tuần 1: Xây dựng hạ tầng lõi & Minecraft Server**

    * Thiết kế VPC, Subnet, Internet Gateway và Security Group.
    * Tạo EC2 Ubuntu chạy Minecraft Server.
    * Cấu hình IAM Role cho Systems Manager.
    * Truy cập EC2 bằng Session Manager thay vì SSH.
    * Cài đặt Java và PaperMC.
    * Tạo user `minecraft` để chạy server an toàn.
    * Kiểm tra kết nối Minecraft từ máy client.

*   **Tuần 2: Bảo mật, giám sát, tự động hóa & nghiệm thu**

    * Bật Amazon GuardDuty.
    * Tạo Lambda function để xử lý sự kiện bảo mật.
    * Tạo EventBridge Rule để kết nối GuardDuty với Lambda.
    * Cấu hình SNS gửi Email cảnh báo.
    * Cấu hình AWS Backup cho EC2.
    * Tạo Network Load Balancer và Global Accelerator.
    * Demo sample findings của GuardDuty.
    * Kiểm tra CloudWatch Logs và Email cảnh báo.
    * Viết tài liệu vận hành, demo và dọn dẹp tài nguyên.

---

### 6. Ước tính ngân sách

Việc ước tính chi phí giúp đánh giá khả năng triển khai thực tế của hệ thống trên nền tảng AWS. Chi phí dưới đây được tính theo bảng giá tham khảo của AWS khu vực **Asia Pacific (Singapore)** và chỉ mang tính chất ước lượng. Thực tế có thể thay đổi tùy theo thời gian sử dụng, lưu lượng truy cập và tài nguyên được cấp phát.

#### 6.1. Môi trường Workshop / Hướng dẫn

| STT | Dịch vụ AWS | Cấu hình & Tham số tính toán | Chi phí/Tháng |
| :--- | :--- | :--- | :--- |
| 1 | Amazon EC2 | 1 instance `t3.medium`, Ubuntu Server, chạy Minecraft Server | ~ $30.37 |
| 2 | Amazon EBS | 20GB gp3 SSD Storage | ~ $1.60 |
| 3 | Amazon GuardDuty | Phân tích CloudTrail, DNS Logs và VPC Flow Logs ở quy mô nhỏ | ~ $3.00 |
| 4 | AWS Lambda | Tự động xử lý và chặn IP, dưới 1 triệu requests/tháng | ~ $0.00 |
| 5 | Amazon EventBridge | Rule kết nối GuardDuty Finding đến Lambda | ~ $0.00 |
| 6 | Amazon SNS | Gửi Email cảnh báo bảo mật cho quản trị viên | ~ $0.00 |
| 7 | Amazon CloudWatch | Lưu trữ log và monitoring khoảng 5GB logs/tháng | ~ $2.50 |
| 8 | AWS Backup | Backup EC2 mỗi giờ, retention 7 ngày | ~ $2.50 |
| 9 | Network Load Balancer | 1 TCP Network Load Balancer cho port 25565 | ~ $16.20 |
| 10 | AWS Global Accelerator | 1 Accelerator cung cấp IP tĩnh toàn cầu | ~ $18.25 |
| 11 | VPC, IAM, Security Groups, NACL, Systems Manager | Các dịch vụ nền tảng và quản trị bảo mật | $0.00 |
| **Tổng** | **Ước tính chi phí hàng tháng** | | **~ $74.42** |

*Lưu ý:* Chi phí hạ tầng cloud có thể giảm đáng kể xuống dưới **$40.00/tháng** trong môi trường học tập bằng cách:

*   Sử dụng EC2 `t3.micro` hoặc `t2.micro` thay vì `t3.medium` khi chỉ demo với ít người chơi.
*   Chỉ bật EC2 trong thời gian thực hành và Stop Instance khi không sử dụng.
*   Tắt AWS Global Accelerator khi không cần trình diễn tính năng che giấu IP hoặc chống DDoS.
*   Xóa các bản backup cũ sau khi kết thúc buổi thực hành.
*   Tận dụng AWS Free Tier cho Lambda, EventBridge, SNS và CloudWatch.

#### 6.2. Môi trường Thực tế

| STT | Dịch vụ AWS | Cấu hình & Tham số tính toán | Chi phí/Tháng |
| :--- | :--- | :--- | :--- |
| 1 | Amazon EC2 | 1 instance `t3.large`, Ubuntu Server, Production Minecraft Server | ~ $60.74 |
| 2 | Amazon EBS | 50GB gp3 SSD Storage | ~ $4.00 |
| 3 | Amazon GuardDuty | Giám sát và phát hiện mối đe dọa liên tục | ~ $10.00 |
| 4 | AWS Lambda | Tự động phản ứng và chặn IP độc hại | ~ $0.50 |
| 5 | Amazon EventBridge | Event routing giữa GuardDuty và Lambda | ~ $1.00 |
| 6 | Amazon SNS | Email notification service | ~ $0.50 |
| 7 | Amazon CloudWatch | Monitoring, dashboard và log storage | ~ $8.00 |
| 8 | AWS Backup | Backup định kỳ, retention 30 ngày | ~ $10.00 |
| 9 | Network Load Balancer | 1 Production NLB cho Minecraft TCP traffic | ~ $16.20 |
| 10 | AWS Global Accelerator | 1 Production Global Accelerator | ~ $18.25 |
| 11 | VPC, IAM, Security Groups, NACL, Systems Manager | Các dịch vụ nền tảng và quản trị bảo mật | $0.00 |
| **Tổng** | **Ước tính chi phí hàng tháng** | | **~ $129.19** |

---

### 7. Đánh giá rủi ro

#### Ma trận rủi ro

| Rủi ro xác định | Khả năng xảy ra | Mức độ ảnh hưởng | Chiến lược giảm thiểu & Phòng ngừa |
| :--- | :--- | :--- | :--- |
| **Brute-force SSH vào máy chủ** | Trung bình | Cao | Không mở port 22 ra Internet. Quản trị máy chủ thông qua AWS Systems Manager Session Manager. |
| **Lộ địa chỉ IP thật của EC2** | Trung bình | Cao | Sử dụng AWS Global Accelerator kết hợp Network Load Balancer để người chơi kết nối qua IP tĩnh thay vì IP EC2. |
| **Port scanning hoặc reconnaissance** | Trung bình | Trung bình | Bật Amazon GuardDuty để phát hiện hành vi quét cổng và gửi finding cho EventBridge. |
| **Tấn công DDoS vào Minecraft Server** | Trung bình | Cao | Sử dụng Global Accelerator và Network Load Balancer để giảm rủi ro truy cập trực tiếp vào EC2. |
| **Phá hoại dữ liệu world Minecraft** | Trung bình | Cao | Cấu hình AWS Backup sao lưu định kỳ EC2, retention 7 ngày hoặc 30 ngày tùy môi trường. |
| **Lambda chặn nhầm IP hợp lệ** | Thấp | Trung bình | Kiểm tra kỹ logic xử lý finding, ghi log đầy đủ trong CloudWatch và có quy trình khôi phục rule khi cần. |
| **Chi phí AWS phát sinh ngoài ý muốn** | Trung bình | Trung bình | Dừng hoặc xóa tài nguyên sau demo. Xóa Global Accelerator, NLB, EC2, Backup Vault và tắt GuardDuty khi không dùng. |
| **Chạy Minecraft Server bằng quyền root** | Trung bình | Cao | Tạo user riêng `minecraft` và chạy server bằng user hạn chế quyền thay vì root. |

---

#### Kế hoạch dự phòng (Contingency Plan)

*   **Trường hợp Minecraft Server bị lỗi hoặc bị phá hoại dữ liệu:**

    Sử dụng AWS Backup để khôi phục lại EC2 hoặc dữ liệu world từ bản sao lưu gần nhất. Với backup theo giờ, mức mất dữ liệu tối đa có thể được giới hạn trong khoảng dưới 1 giờ đối với môi trường demo.

*   **Trường hợp phát hiện IP độc hại:**

    GuardDuty tạo finding, EventBridge kích hoạt Lambda, Lambda thực hiện phản ứng tự động và gửi cảnh báo thông qua SNS. Người quản trị có thể kiểm tra chi tiết sự kiện trong CloudWatch Logs.

*   **Trường hợp hệ thống bị lỗi trong lúc demo:**

    Có thể sử dụng GuardDuty Sample Findings để tạo sự kiện mô phỏng thay vì chờ tấn công thật. Điều này giúp quá trình báo cáo ổn định và tránh phụ thuộc vào điều kiện bên ngoài.

*   **Trường hợp phát sinh chi phí không mong muốn:**

    Thực hiện quy trình dọn dẹp tài nguyên theo thứ tự: Global Accelerator, Network Load Balancer, Target Group, EC2, Lambda, EventBridge, SNS, GuardDuty, AWS Backup và các rule NACL tùy chỉnh.

---

### 8. Các Luồng Xử Lý Hệ Thống & Đặc Điểm Kỹ Thuật

Hệ thống áp dụng kiến trúc bảo mật nhiều lớp kết hợp tự động hóa phản ứng sự cố. Các luồng xử lý chính bao gồm luồng người chơi kết nối vào game, luồng quản trị an toàn, luồng phát hiện tấn công, luồng tự động phản ứng và luồng sao lưu khôi phục dữ liệu.

#### 8.1 Các Luồng Xử Lý Cốt Lõi (Core Processing Flows)

*   **Luồng người chơi kết nối vào Minecraft Server:**

    Người chơi sử dụng IP tĩnh do AWS Global Accelerator cung cấp để kết nối đến Minecraft Server. Traffic TCP port 25565 được chuyển qua Global Accelerator đến Network Load Balancer, sau đó đến EC2 đang chạy Minecraft Server. Cách này giúp hạn chế việc công khai IP thật của EC2.

*   **Luồng quản trị an toàn:**

    Người quản trị không sử dụng SSH keypair và không mở port 22. Thay vào đó, quản trị viên truy cập EC2 thông qua AWS Systems Manager Session Manager trên AWS Console. Cơ chế này giảm rủi ro bị brute-force SSH và loại bỏ nhu cầu quản lý file `.pem`.

*   **Luồng phát hiện xâm nhập:**

    Amazon GuardDuty phân tích log và hành vi trong tài khoản AWS để phát hiện các dấu hiệu bất thường như port scanning, brute-force hoặc hoạt động đáng ngờ. Khi có finding, GuardDuty gửi sự kiện đến EventBridge.

*   **Luồng tự động phản ứng sự cố:**

    EventBridge Rule nhận GuardDuty Finding và kích hoạt AWS Lambda. Lambda xử lý thông tin sự kiện, trích xuất IP nghi vấn nếu có, thực hiện hành động phản ứng như chặn IP, ghi log hoặc gửi cảnh báo. Kết quả xử lý được ghi lại trong CloudWatch Logs để phục vụ kiểm tra.

*   **Luồng cảnh báo Email:**

    Sau khi Lambda xử lý sự kiện, Amazon SNS gửi Email cảnh báo đến quản trị viên. Nội dung cảnh báo có thể bao gồm loại mối đe dọa, thời gian phát hiện, IP nguồn và hành động đã thực hiện.

*   **Luồng sao lưu và khôi phục:**

    AWS Backup tự động tạo bản sao lưu EC2 theo lịch định kỳ. Khi server gặp sự cố, bị phá hoại hoặc dữ liệu world bị lỗi, người quản trị có thể khôi phục từ backup gần nhất để giảm thiểu mất mát dữ liệu.

---

#### 8.2 Đặc Điểm Kiến Trúc (Architectural Strengths)

*   **Bảo mật theo chiều sâu (Defense in Depth):**

    Hệ thống không dựa vào một lớp bảo mật duy nhất mà kết hợp nhiều lớp: Security Group, NACL, IAM, SSM, GuardDuty, Lambda, SNS và Backup. Điều này giúp tăng khả năng chống chịu trước nhiều loại rủi ro khác nhau.

*   **Không mở SSH public:**

    Việc quản trị EC2 bằng Session Manager giúp loại bỏ rủi ro phổ biến khi mở port SSH 22 ra Internet. Đây là một điểm mạnh quan trọng trong thiết kế bảo mật của project.

*   **Tự động hóa phản ứng sự cố:**

    Sự kết hợp giữa GuardDuty, EventBridge và Lambda tạo thành mô hình SOAR thu nhỏ. Hệ thống không chỉ phát hiện sự cố mà còn có khả năng phản ứng tự động.

*   **Khả năng khôi phục sau sự cố:**

    AWS Backup giúp bảo vệ dữ liệu Minecraft World trước các rủi ro như lỗi hệ thống, thao tác sai hoặc phá hoại trong game.

*   **Che giấu IP thật của máy chủ:**

    Global Accelerator và NLB giúp người chơi kết nối qua IP tĩnh thay vì IP public trực tiếp của EC2. Điều này giúp giảm nguy cơ attacker nhắm trực tiếp vào máy chủ gốc.

*   **Dễ demo và kiểm chứng:**

    GuardDuty Sample Findings cho phép tạo tình huống tấn công giả lập, giúp chứng minh luồng phát hiện và phản ứng tự động một cách ổn định trong buổi báo cáo.

---

### 9. Kết quả kỳ vọng

*   **Cải tiến kỹ thuật:**

    * Minecraft Server được triển khai thành công trên AWS EC2.
    * Người chơi có thể kết nối vào server thông qua port 25565.
    * Máy chủ không mở SSH public, giảm nguy cơ brute-force.
    * GuardDuty phát hiện được các hành vi đáng ngờ hoặc sample findings.
    * EventBridge kích hoạt Lambda tự động khi có finding.
    * Lambda ghi nhận sự kiện, thực hiện phản ứng và gửi cảnh báo.
    * SNS gửi Email cảnh báo đến người quản trị.
    * AWS Backup tạo bản sao lưu định kỳ phục vụ khôi phục dữ liệu.
    * Global Accelerator và NLB hỗ trợ che giấu IP thật của EC2.

*   **Giá trị lâu dài:**

    * Xây dựng được một mô hình bảo mật Cloud thực tế, dễ mở rộng cho các loại game server hoặc dịch vụ public khác.
    * Áp dụng được các nguyên tắc quan trọng của AWS Security như Least Privilege, Defense in Depth, Secure Administration và Automated Incident Response.
    * Tạo nền tảng để phát triển thêm các tính năng nâng cao như dashboard giám sát, cảnh báo qua Discord/Telegram, tự động snapshot world riêng biệt, hoặc triển khai server bằng container trên ECS/Fargate.
    * Cung cấp một project có tính thực tiễn cao, phù hợp để đưa vào portfolio cá nhân hoặc báo cáo môn học về Cloud Computing và Cybersecurity.

---