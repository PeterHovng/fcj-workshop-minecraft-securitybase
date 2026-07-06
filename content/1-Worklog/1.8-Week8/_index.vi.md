---
title: "Worklog Tuần 8"
date: 2026-06-08
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Mục tiêu tuần 8:

* Triển khai hệ thống giám sát và phát hiện mối đe dọa cho Minecraft Server.
* Tích hợp Amazon GuardDuty với EventBridge và AWS Lambda.
* Tự động gửi cảnh báo bảo mật thông qua Amazon SNS.
* Kiểm thử luồng xử lý sự kiện bảo mật trên AWS.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2 | - Kích hoạt Amazon GuardDuty cho tài khoản AWS<br>- Tìm hiểu các loại Security Findings và cơ chế phát hiện mối đe dọa | 08/06/2026 | 08/06/2026 | https://www.youtube.com/@AWSStudyGroup https://cloudjourney.awsstudygroup.com/ |
| 3 | - Tạo AWS Lambda Function xử lý GuardDuty Findings<br>- Cấu hình IAM Role và quyền truy cập cho Lambda | 09/06/2026 | 09/06/2026 | https://www.youtube.com/@AWSStudyGroup https://cloudjourney.awsstudygroup.com/ |
| 4 | - Viết mã nguồn Lambda để xử lý Security Findings<br>- Kiểm tra log thực thi trên Amazon CloudWatch Logs | 10/06/2026 | 10/06/2026 | https://www.youtube.com/@AWSStudyGroup https://cloudjourney.awsstudygroup.com/ |
| 5 | - Tạo Amazon EventBridge Rule nhận sự kiện từ GuardDuty<br>- Liên kết EventBridge với Lambda Function | 11/06/2026 | 11/06/2026 | https://www.youtube.com/@AWSStudyGroup https://cloudjourney.awsstudygroup.com/ |
| 6 | - Tạo Amazon SNS Topic và Email Subscription<br>- Kiểm thử gửi Email cảnh báo khi phát hiện Security Findings | 12/06/2026 | 12/06/2026 | https://www.youtube.com/@AWSStudyGroup https://cloudjourney.awsstudygroup.com/ |
| 7 | - Kiểm thử toàn bộ quy trình GuardDuty → EventBridge → Lambda → SNS<br>- Điều chỉnh và tối ưu xử lý sự kiện | 13/06/2026 | 13/06/2026 | Personal Project Notes |
| CN | - Cập nhật tài liệu triển khai và sơ đồ kiến trúc hệ thống<br>- Chuẩn bị triển khai các thành phần Backup và Network Load Balancer trong tuần tiếp theo | 14/06/2026 | 14/06/2026 | Personal Notes, Udemy |

### Kết quả đạt được tuần 8:

* Kích hoạt thành công Amazon GuardDuty để giám sát các mối đe dọa trên tài khoản AWS.
* Triển khai AWS Lambda xử lý các Security Findings từ GuardDuty.
* Cấu hình thành công Amazon EventBridge để tự động kích hoạt Lambda khi có sự kiện bảo mật.
* Thiết lập Amazon SNS gửi Email cảnh báo đến quản trị viên khi phát hiện dấu hiệu tấn công.
* Hoàn thiện quy trình tự động hóa xử lý sự kiện bảo mật (SOAR) cho hệ thống Minecraft Security Based on AWS.