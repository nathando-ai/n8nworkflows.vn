---
title: "🚀 Tự động phân loại và chuyển tiếp ticket HubSpot sang Jira với cảnh báo SLA qua Slack"
description: "Workflow n8n tự động hóa quy trình xử lý ticket từ HubSpot sang Jira, với cảnh báo SLA qua Slack. Giảm thời gian phản hồi cho khách hàng VIP và tối ưu hóa quy trình hỗ trợ."
slug: "tu-dong-phan-loai-ticket-hubspot-jira-slack-sla"
tags: [n8n, automation, no-code, HubSpot, Jira, Slack, ticket management, AI]
keywords: [n8n workflow, tự động hóa ticket, quản lý ticket, HubSpot Jira, cảnh báo SLA, Slack]
---

# 🚀 Tự động phân loại và chuyển tiếp ticket HubSpot sang Jira với cảnh báo SLA qua Slack

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi xử lý ticket thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa 100% quy trình xử lý ticket từ HubSpot sang Jira
- Giảm thời gian phản hồi cho khách hàng VIP lên đến 80%
- Tăng tính chính xác trong phân loại ticket nhờ logic tự động
- Hoạt động liên tục 24/7 với cảnh báo SLA qua Slack
- Tiết kiệm thời gian nhân viên hỗ trợ lên đến 60%
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản HubSpot với quyền truy cập API
- Tài khoản Jira với quyền tạo task
- Tài khoản Slack với quyền gửi tin nhắn
- API keys cho HubSpot, Jira và Slack
- Quyền truy cập vào project Jira để tạo task
- Quyền truy cập vào channel Slack để nhận thông báo
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/12940)
2. Click vào nút "Download" để tải file JSON
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Every 10 Mins"**:
   - Đảm bảo lịch trình chạy đúng 10 phút/lần
   - Có thể điều chỉnh thời gian nếu cần

2. **Node "HubSpot: Search New Tickets"**:
   - Cấu hình credentials cho HubSpot
   - Đảm bảo query chỉ lấy ticket mới trong vòng 10 phút

3. **Node "HubSpot: Get Associations"**:
   - Cấu hình credentials cho HubSpot
   - Đảm bảo operation là "get" và resource là "ticket"

4. **Node "HubSpot: Get Contact Data"**:
   - Cấu hình credentials cho HubSpot
   - Đảm bảo lấy các trường dữ liệu quan trọng như Annual Revenue và Lifecycle Stage

5. **Node "Code: Calculate Severity"**:
   - Chỉnh sửa logic JavaScript nếu cần thay đổi tiêu chí phân loại
   - Đảm bảo các ngưỡng doanh thu và từ khóa rủi ro được cập nhật

6. **Node "Jira: Create Triage Ticket"**:
   - Cấu hình credentials cho Jira
   - Chỉnh sửa project ID và các trường dữ liệu cần thiết
   - Đảm bảo template mô tả ticket được định dạng đúng

7. **Node "Slack: Notify Channel"**:
   - Cấu hình credentials cho Slack
   - Chỉnh sửa channel ID và thông điệp cảnh báo

8. **Node "Jira: Get Latest Status"**:
   - Cấu hình credentials cho Jira
   - Đảm bảo operation là "get"

9. **Node "Slack: Send Alert"**:
   - Cấu hình credentials cho Slack
   - Chỉnh sửa channel ID và thông điệp cảnh báo cấp cao

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node, click vào nút "Activate" để kích hoạt workflow
2. Thử chạy workflow với dữ liệu mẫu để kiểm tra
3. Theo dõi kết quả trên Jira và Slack để đảm bảo workflow hoạt động đúng

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp với các công cụ khác**: Kết nối với Google Sheets để lưu trữ lịch sử ticket
2. **Cảnh báo nâng cao**: Thêm logic để cảnh báo khi ticket bị đóng mà không có phản hồi từ khách hàng
3. **Báo cáo định kỳ**: Tạo báo cáo hàng ngày về số lượng ticket đã xử lý và thời gian phản hồi trung bình
4. **Tích hợp với AI**: Sử dụng node AI để tự động phân loại ticket dựa trên nội dung

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quy trình xử lý ticket từ HubSpot sang Jira, với cảnh báo SLA qua Slack. Với việc áp dụng workflow này, các sếp có thể giảm thời gian phản hồi cho khách hàng VIP, tối ưu hóa quy trình hỗ trợ và tiết kiệm thời gian nhân viên. Hãy thử ngay để trải nghiệm sự khác biệt!