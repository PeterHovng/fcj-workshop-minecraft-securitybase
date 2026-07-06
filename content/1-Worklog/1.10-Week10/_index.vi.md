---
title: "Worklog Tuần 10"
date: 2026-06-22
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

### Mục tiêu tuần 10:

* Hoàn thiện kiến trúc **Minecraft Security Based on AWS**.
* Triển khai AWS Global Accelerator để cung cấp IP tĩnh và tối ưu kết nối.
* Kiểm thử toàn bộ luồng hoạt động của hệ thống.
* Hoàn thiện tài liệu kỹ thuật và chuẩn bị kết thúc project.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2 | - Tìm hiểu AWS Global Accelerator và cơ chế định tuyến toàn cầu<br>- Phân tích lợi ích khi sử dụng Global Accelerator cho Minecraft Server | 22/06/2026 | 22/06/2026 | https://www.youtube.com/@AWSStudyGroup https://cloudjourney.awsstudygroup.com/ |
| 3 | - Tạo AWS Global Accelerator<br>- Cấu hình Listener TCP Port 25565<br>- Kết nối Global Accelerator với Network Load Balancer | 23/06/2026 | 23/06/2026 | AWS Global Accelerator Documentation |
| 4 | - Kiểm thử kết nối Minecraft Server thông qua IP tĩnh của Global Accelerator<br>- Kiểm tra khả năng chuyển tiếp lưu lượng đến EC2 | 24/06/2026 | 24/06/2026 | Personal Project Notes |
| 5 | - Kiểm thử toàn bộ luồng hoạt động: Player → Global Accelerator → Network Load Balancer → EC2 Minecraft Server<br>- Kiểm tra cơ chế cảnh báo GuardDuty → EventBridge → Lambda → SNS | 25/06/2026 | 25/06/2026 | Personal Project Notes |
| 6 | - Tối ưu cấu hình hệ thống<br>- Hoàn thiện sơ đồ kiến trúc, tài liệu triển khai và hướng dẫn vận hành<br>- Rà soát chi phí các dịch vụ AWS đã sử dụng | 26/06/2026 | 26/06/2026 | AWS Well-Architected Framework |
| 7 | - Kiểm thử tổng thể lần cuối<br>- Khắc phục các lỗi còn tồn tại và tối ưu hiệu năng hệ thống<br>- Chuẩn bị demo project | 27/06/2026 | 27/06/2026 | Personal Project Notes |
| CN | - Cập nhật báo cáo và tài liệu project<br>- Chuẩn bị kế hoạch nghiệm thu và tổng kết project trong tuần tiếp theo | 28/06/2026 | 28/06/2026 | Personal Notes |

### Kết quả đạt được tuần 10:

* Triển khai thành công AWS Global Accelerator và tích hợp với Network Load Balancer.
* Người chơi có thể kết nối đến Minecraft Server thông qua địa chỉ IP tĩnh do Global Accelerator cung cấp.
* Kiểm thử thành công toàn bộ luồng hoạt động của hệ thống từ người chơi đến máy chủ và quy trình tự động xử lý sự kiện bảo mật.
* Hoàn thiện tài liệu triển khai, sơ đồ kiến trúc và hướng dẫn vận hành hệ thống.
* Project **Minecraft Security Based on AWS** cơ bản hoàn thành và sẵn sàng cho giai đoạn nghiệm thu, đánh giá và tổng kết.