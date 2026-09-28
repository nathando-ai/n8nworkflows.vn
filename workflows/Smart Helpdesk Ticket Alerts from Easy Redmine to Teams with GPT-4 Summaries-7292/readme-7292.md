---
title: "🚀 Tự động hóa Ticket từ Easy Redmine sang Teams với Tóm tắt AI GPT-4"
description: "Hướng dẫn tự động gửi thông báo ticket mới từ Easy Redmine sang Microsoft Teams với tóm tắt AI, tiết kiệm thời gian xử lý và nâng cao hiệu suất hỗ trợ khách hàng."
slug: "tu-dong-hoa-ticket-easy-redmine-sang-teams-voi-ai-gpt-4"
tags: [n8n, automation, no-code, easy-redmine, microsoft-teams, ai-agent]
keywords: [n8n workflow, tự động hóa ticket, easy redmine, microsoft teams, ai tóm tắt]
---

# 🚀 Tự động hóa Ticket từ Easy Redmine sang Teams với Tóm tắt AI GPT-4

[Các sếp đang làm việc với hệ thống Easy Redmine và Microsoft Teams sẽ gặp khó khăn khi phải theo dõi và xử lý các ticket mới thủ công. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình từ nhận ticket đến gửi thông báo sang Teams với tóm tắt AI, giúp tiết kiệm thời gian và nâng cao hiệu suất hỗ trợ khách hàng.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian xử lý ticket: Tự động nhận và xử lý ticket mới ngay khi chúng được tạo.
- Tăng cường thông tin ticket: Tóm tắt nội dung ticket bằng AI để dễ dàng hiểu và xử lý.
- Trung tâm hóa thông tin: Gửi thông báo ticket mới đến Microsoft Teams, giúp toàn bộ team dễ dàng theo dõi và phản hồi.
- Tăng hiệu suất làm việc: Giảm thời gian chờ đợi và tăng tốc độ xử lý ticket, đặc biệt là trong các tình huống khẩn cấp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Easy Redmine với quyền truy cập API.
- Tài khoản Microsoft Teams với quyền truy cập API.
- API Key từ OpenAI để sử dụng mô hình GPT-4.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow này vào n8n, các sếp có thể làm theo các bước sau:

1. Truy cập vào n8n Editor.
2. Chọn "Import from URL" và nhập URL sau: [https://n8n.io/workflows/7292](https://n8n.io/workflows/7292).
3. Hoặc, tải file JSON từ liên kết trên và chọn "Import from File".

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **Node "Catch Easy Webhook - New Issue Created"**:
  - Đảm bảo rằng webhook URL trong node này đã được cấu hình đúng với URL của n8n.
  - Cấu hình webhook trong Easy Redmine để gửi yêu cầu POST đến URL này khi có ticket mới được tạo.

- **Node "Get a new ticket by ID"**:
  - Cấu hình credentials cho Easy Redmine API.
  - Đảm bảo rằng node này được cấu hình để lấy ticket mới theo ID.

- **Node "OpenAI Chat Model"**:
  - Cấu hình credentials cho OpenAI API.
  - Chọn mô hình GPT-4 để sử dụng cho việc tóm tắt nội dung ticket.

- **Node "MS Teams message to Support channel"**:
  - Cấu hình credentials cho Microsoft Teams API.
  - Chọn kênh Teams phù hợp để gửi thông báo.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu để đảm bảo rằng workflow hoạt động đúng.
- Bật Active workflow để bắt đầu tự động hóa quy trình.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack để gửi thông báo ticket mới đến cả Slack và Teams.
- Lưu log các ticket đã xử lý để theo dõi và phân tích hiệu suất hỗ trợ.
- Gửi báo cáo định kỳ về số lượng ticket đã xử lý và thời gian trung bình xử lý.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình từ nhận ticket đến gửi thông báo sang Teams với tóm tắt AI, tiết kiệm thời gian và nâng cao hiệu suất hỗ trợ khách hàng. Hãy áp dụng ngay để trải nghiệm sự tiện lợi và hiệu quả của tự động hóa!