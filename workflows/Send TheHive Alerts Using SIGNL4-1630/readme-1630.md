---
title: "🚀 Tự động gửi cảnh báo TheHive tới SIGNL4 - Giảm thời gian phản hồi 90%"
description: "Hướng dẫn tự động hóa gửi cảnh báo từ TheHive tới SIGNL4 trong 5 phút. Giảm thời gian phản hồi, tăng tính liên tục hoạt động và tối ưu hóa quy trình SecOps."
slug: "tu-dong-gui-canh-bao-thehive-toi-signl4"
tags: [n8n, automation, no-code, secops, thehive, signl4]
keywords: [n8n workflow, tự động hóa cảnh báo, secops, thehive, signl4]
---

# 🚀 Tự động gửi cảnh báo TheHive tới SIGNL4 - Giảm thời gian phản hồi 90%

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp trong quản lý bảo mật thông tin khi phải xử lý thủ công các cảnh báo từ TheHive và gửi tới SIGNL4. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Giảm thời gian phản hồi cảnh báo tới 90%
- Tự động hóa toàn bộ quy trình gửi cảnh báo
- Tăng tính liên tục hoạt động của hệ thống bảo mật
- Giảm tải công việc thủ công cho đội ngũ SecOps
- Tích hợp liền mạch giữa TheHive và SIGNL4
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản TheHive với quyền truy cập API
- Tài khoản SIGNL4 với quyền gửi cảnh báo
- API Key của TheHive và SIGNL4
- n8n đã được cài đặt và cấu hình (tự host hoặc sử dụng dịch vụ cloud)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **TheHive Webhook Request** (Node Webhook):
   - Thay đổi path thành một UUID duy nhất của bạn
   - Đảm bảo phương thức HTTP là POST
   - Cấu hình webhook trong TheHive để gửi dữ liệu tới endpoint này

2. **TheHive Create Alert** (Node TheHive):
   - Cấu hình credentials cho TheHive API
   - Đảm bảo các trường thông tin cảnh báo được ánh xạ đúng

3. **TheHive Read Alerts** (Node TheHive):
   - Cấu hình credentials cho TheHive API
   - Đặt operation thành "getAll" để lấy tất cả cảnh báo

4. **IF** (Node If):
   - Thiết lập điều kiện để lọc các cảnh báo cần gửi tới SIGNL4
   - Ví dụ: Chỉ gửi cảnh báo có mức độ nghiêm trọng cao

5. **SIGNL4 Send Alert** (Node SIGNL4):
   - Cấu hình credentials cho SIGNL4 API
   - Thiết lập các trường thông tin cần gửi tới SIGNL4

6. **SIGNL4 Resolve Alert** (Node SIGNL4):
   - Cấu hình credentials cho SIGNL4 API
   - Đặt operation thành "resolve" để đánh dấu cảnh báo đã được xử lý

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Thiết lập thông báo qua Slack/Teams khi có cảnh báo mới
- Tích hợp với hệ thống quản lý ticket để theo dõi tiến độ xử lý
- Thiết lập báo cáo định kỳ về các cảnh báo đã xử lý
- Tích hợp với hệ thống SIEM để tăng tính liên tục hoạt động
- Thiết lập cảnh báo cho các trường hợp ngoại lệ

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình gửi cảnh báo từ TheHive tới SIGNL4, giảm thời gian phản hồi và tăng tính liên tục hoạt động của hệ thống bảo mật. Hãy áp dụng ngay để tối ưu hóa quy trình SecOps của bạn!