---
title: "💰 Tự động hóa tài chính cá nhân với AI Agent qua Slack & Google Sheets"
description: "Workflow n8n giúp theo dõi tài chính cá nhân thông qua Slack, tự động cập nhật Google Sheets và sử dụng AI để phân tích giao dịch."
slug: "tu-dong-hoa-tai-chinh-ca-nhan-voi-ai-agent-qua-slack-google-sheets"
tags: [n8n, automation, no-code, personal-finance, ai-chatbot]
keywords: [n8n workflow, tự động hóa tài chính, AI agent, Google Sheets, Slack]
---

# 💰 Tự động hóa tài chính cá nhân với AI Agent qua Slack & Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa việc theo dõi tài chính hàng ngày.
- Chính xác: AI phân tích và xử lý giao dịch một cách chính xác.
- Cá nhân hóa: Theo dõi tài chính cá nhân theo cách riêng của bạn.
- Hoạt động liên tục: Nhận nhắc nhở hàng ngày và cập nhật tự động.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Slack với bot token.
- Google Sheets với 3 tab: Balances, Transactions, Debts.
- API key của Google Gemini.
- Cơ sở dữ liệu PostgreSQL.
- Instance n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/10056](https://n8n.io/workflows/10056).
2. Nhấn nút "Import" và chọn "Import from URL".
3. Dán URL vào ô nhập liệu và nhấn "OK".

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Google Sheets**: Cần cấu hình credentials `googleSheetsOAuth2Api` và điền ID của Google Sheet.
- **Slack**: Cần cấu hình credentials `slackApi` và điền channel ID.
- **Google Gemini**: Cần cấu hình credentials `googlePalmApi` và điền API key.
- **PostgreSQL**: Cần cấu hình credentials `postgres` và điền thông tin kết nối.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack để nhận thông báo và tương tác.
- Lưu log các giao dịch để theo dõi lịch sử.
- Gửi báo cáo định kỳ qua email hoặc Slack.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa việc theo dõi tài chính cá nhân một cách hiệu quả và chính xác. Hãy áp dụng ngay để tiết kiệm thời gian và tăng hiệu suất làm việc.