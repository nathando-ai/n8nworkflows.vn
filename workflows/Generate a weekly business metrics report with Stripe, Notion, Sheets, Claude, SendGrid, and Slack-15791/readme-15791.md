---
title: "🚀 Tự động hóa báo cáo kinh doanh hàng tuần với Stripe, Notion, Google Sheets và Claude AI"
description: "Xây dựng hệ thống tự động tổng hợp dữ liệu doanh thu từ Stripe, CRM Notion, Google Sheets và nhờ Claude AI viết báo cáo điều hành gửi qua SendGrid và Slack mỗi sáng thứ Hai."
slug: "tu-dong-hoa-bao-cao-kinh-doanh-hang-tuan-stripe-notion-claude"
tags: [n8n, automation, ai, stripe, notion, google-sheets, claude, sendgrid, slack]
keywords: [n8n workflow, bao cao kinh doanh tu dong, stripe automation, claude ai report, sendgrid email, tich hop n8n]
---

# 🚀 Tự động hóa báo cáo kinh doanh hàng tuần với Stripe, Notion và Claude AI

Các sếp có đang tốn hàng giờ mỗi sáng thứ Hai để "gom" dữ liệu từ Stripe (doanh thu), Notion (deal sales), Google Sheets (vận hành) rồi ngồi viết báo cáo tuần gửi sếp lớn hoặc đội ngũ? Công việc thủ công này vừa nhàm chán, dễ sai sót lại vừa lãng phí thời gian quý giá.

Giải pháp đây rồi! Workflow n8n siêu việt này sẽ thay các sếp làm tất cả: tự động lấy dữ liệu, nhờ **Claude AI** phân tích và viết báo cáo điều hành cực kỳ chuyên nghiệp, sau đó gửi thẳng qua **SendGrid** (email HTML đẹp mắt) và thông báo qua **Slack**. 100% tự động, không cần đụng tay!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 3-5 giờ mỗi tuần:** Không còn phải thủ công copy-paste số liệu từ nhiều nguồn khác nhau.
- **Báo cáo AI thông minh:** Claude Sonnet 4 phân tích sâu về hiệu suất doanh thu, sức khỏe pipeline và điểm nhấn vận hành như một chuyên gia tài chính thực thụ.
- **Giao diện HTML chuyên nghiệp:** Email báo cáo gửi đi có thiết kế thẻ KPI, bảng phân tách giai đoạn deal rõ ràng, đẹp mắt.
- **Cảnh báo lỗi tự động:** Tích hợp Error Trigger sẵn sàng gửi email cảnh báo nếu có bất kỳ sự cố nào xảy ra trong quá trình chạy.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance** (phiên bản Cloud hoặc Self-hosted).
- Tài khoản và API Key của **Anthropic (Claude)**.
- Tài khoản **Stripe** (với quyền lấy dữ liệu charge/revenue).
- Tài khoản **Notion** và quyền truy cập Deals Database.
- **Google Sheets** chứa số liệu vận hành (Ops Metrics).
- Tài khoản **SendGrid** để gửi email tự động.
- **Slack App / Bot Token** để nhận thông báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy trực tiếp mã nguồn JSON.
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File / Clipboard** và dán vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình các biến môi trường (Environment Variables) hoặc trực tiếp trên các node sau:
- **Anthropic Chat Model**: Kết nối credentials `anthropicApi` và chọn model `claude-sonnet-4-20250514`.
- **GSheets: Ops Metrics**: Kết nối Google Sheets OAuth2 credential, trỏ tới `GSHEETS_SPREADSHEET_ID`, `GSHEETS_SHEET_NAME`, và `GSHEETS_LAST_ROW_RANGE`.
- **Send via SendGrid** & **Send Error Email**: Kết nối SendGrid credential, cấu hình biến email gửi đi (`REPORT_EMAIL_FROM`, `REPORT_EMAIL_TO`, `REPORT_ALERT_EMAIL`).
- **Slack: Report Sent**: Kết nối Slack credential và điền `SLACK_CHANNEL_ID`.
- **Stripe & Notion**: Đảm bảo thiết lập đúng biến môi trường `STRIPE_SECRET_KEY`, `NOTION_API_KEY`, và `NOTION_DEALS_DB_ID`.
- **Every Monday at 08:00**: Kiểm tra lại múi giờ của các sếp (`REPORT_TIMEZONE`, ví dụ: `Asia/Ho_Chi_Minh` thay vì mặc định UTC) thông qua node **Compute Date Windows**.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** để test thử nghiệm với dữ liệu hiện tại.
- Kiểm tra email, Slack xem báo cáo đã hiển thị chuẩn chỉnh chưa.
- Gạt nút **Active** trên góc phải màn hình để bật chế độ chạy tự động hàng tuần.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Thay vì chỉ gửi Slack, các sếp có thể nối thêm node Telegram để nhận bản tóm tắt nhanh trên điện thoại.
- **Lưu trữ lịch sử:** Thêm một node Google Sheets ở cuối workflow để ghi lại lịch sử các bản báo cáo đã gửi kèm thời gian thực thi.
- **Tùy chỉnh Prompt của Claude:** Các sếp có thể chỉnh sửa prompt trong node `Claude: Write Executive Narrative` để điều chỉnh văn phong (trang trọng hơn, hài hước hơn hoặc tập trung sâu vào một chỉ số cụ thể).

### 📌 Kết luận
Một hệ thống báo cáo tự động chuẩn "quân đội" giúp các sếp nắm bắt toàn bộ bức tranh tài chính và vận hành doanh nghiệp ngay đầu tuần mà không tốn một giọt mồ hôi. Hãy triển khai ngay hôm nay để tối ưu hóa thời gian quản trị của mình!