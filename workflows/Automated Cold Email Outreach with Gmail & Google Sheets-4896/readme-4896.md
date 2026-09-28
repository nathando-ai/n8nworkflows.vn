---
title: "🚀 Tự động gửi email cold outreach với Gmail & Google Sheets – Giải pháp marketing 100% no-code"
description: "Giải quyết việc gửi email cold outreach thủ công, lặp đi lặp lại bằng một workflow n8n đơn giản, tiết kiệm thời gian và giảm sai sót."
slug: "tuyendung-gmail-google-sheets-automation"
tags: [n8n, automation, no-code, marketing, cold-email]
keywords: [n8n workflow, tự động hóa, cold email, Gmail, Google Sheets]
---

# 🚀 Tự động gửi email cold outreach với Gmail & Google Sheets – Giải pháp marketing 100% no-code

Bạn đang phải mất hàng giờ mỗi ngày để gửi email cold outreach cho danh sách leads? Bạn lo lắng về sai sót khi nhập dữ liệu thủ công, hoặc muốn gửi email một cách cá nhân hóa nhưng không muốn viết code? Workflow này sẽ giúp bạn **tự động** lấy danh sách leads từ Google Sheets, gửi email cá nhân hóa qua Gmail, và cập nhật trạng thái ngay trong sheet – hoàn toàn không cần viết code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động gửi hàng trăm email mỗi ngày mà không cần thao tác thủ công.
- **Chính xác & nhất quán**: Đảm bảo mỗi email được gửi đúng đối tượng, đúng nội dung cá nhân hóa.
- **Cập nhật trạng thái ngay lập tức**: Khi email được gửi, trạng thái “Sent” được ghi lại ngay trong Google Sheet.
- **Tự động hóa 24/7**: Workflow chạy theo lịch, không phụ thuộc vào giờ làm việc của bạn.
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
| Thành phần | Mô tả | Yêu cầu |
|------------|-------|---------|
| **Google Sheet** | Tập tin chứa danh sách leads | Cột: `Email`, `Name`, `Status` (có thể trống lúc bắt đầu) |
| **Gmail account** | Tài khoản Gmail dùng để gửi email | Cần bật **OAuth2** và cấp quyền gửi email |
| **n8n credentials** | Credentials cho Gmail & Google Sheets | Tạo trong n8n: `Gmail OAuth2`, `Google Sheets OAuth2` |
| **Node version** | n8n v1.0+ | Đảm bảo cài đặt n8n đúng phiên bản |
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON của workflow từ [link gốc](https://n8n.io/workflows/4896) hoặc copy nội dung JSON.
2. Trong n8n Editor, chọn **Import** → **JSON** → dán nội dung hoặc tải file.
3. Nhấn **Import** và workflow sẽ xuất hiện trong danh sách workflow của bạn.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích từng node quan trọng:

| Node | Tên trong workflow | Cấu hình cần chỉnh |
|------|--------------------|---------------------|
| **Schedule Trigger** | `Schedule Trigger` | - Thời gian chạy (ví dụ: `0 9 * * *` – 9h sáng hàng ngày).<br>- Đặt `Timezone` phù hợp. |
| **Batch Processing of Leads** | `Batch Processing of Leads` | - `Batch size` (định số leads mỗi lần gửi, ví dụ: `10`). |
| **Send Personalized Email** | `Send Personalized Email` | - **Credentials**: Chọn `Gmail OAuth2` đã tạo.<br>- **To**: `{{ $json["Email"] }}`.<br>- **Subject**: `Hi {{ $json["Name"] }}, ...`.<br>- **Body**: Nội dung email, có thể dùng HTML. |
| **Fetch Leads** | `Fetch Leads` | - **Credentials**: Chọn `Google Sheets OAuth2`.<br>- **Spreadsheet ID**: ID của Google Sheet.<br>- **Range**: Ví dụ: `Sheet1!A:C` (cột Email, Name, Status). |
| **Update Lead Status** | `Update Lead Status` | - **Credentials**: `Google Sheets OAuth2`.<br>- **Spreadsheet ID**: ID của Google Sheet.<br>- **Range**: Cột Status (ví dụ: `Sheet1!C2:C`).<br>- **Value**: `Sent` hoặc `Failed` tùy theo kết quả gửi. |

> **Lưu ý**: Đảm bảo Google Sheet có quyền truy cập cho tài khoản OAuth2 của bạn. Nếu chưa, chia sẻ sheet với email của OAuth2.

### 3. Kích hoạt ⚡️
1. **Test run**: Chạy workflow với dữ liệu mẫu (bấm “Execute Workflow”) để kiểm tra xem email có được gửi và trạng thái có được cập nhật không.
2. **Bật Active**: Khi mọi thứ ổn, chuyển workflow sang trạng thái **Active** để nó tự động chạy theo lịch.

## ✍️ Mẹo & gợi ý nâng cao
- **Slack/Telegram notifications**: Thêm node Slack hoặc Telegram để nhận thông báo khi email được gửi thành công hoặc thất bại.
- **Logging**: Sử dụng node `Set` hoặc `Write Binary Data` để ghi log vào Google Sheet hoặc Cloud Storage.
- **Thêm điều kiện**: Dùng node `If` để chỉ gửi email cho leads chưa được gửi (`Status` = `Pending`).
- **Tùy chỉnh nội dung**: Sử dụng `HTML` trong Gmail node để tạo email đẹp, kèm logo, CTA.

## 📌 Kết luận
Workflow này giúp các sếp **đưa công việc cold outreach lên một tầm cao mới**: tự động, chính xác, và dễ dàng quản lý. Hãy thử ngay, điều chỉnh theo nhu cầu và mở rộng thêm các tính năng như thông báo, báo cáo định kỳ. Bạn sẽ thấy thời gian dành cho marketing tăng lên, còn công việc thủ công giảm xuống. 🚀

---