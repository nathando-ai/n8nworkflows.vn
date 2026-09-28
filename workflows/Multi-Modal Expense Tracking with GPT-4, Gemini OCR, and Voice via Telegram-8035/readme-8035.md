---
title: "🚀 Quản lý tài chính cá nhân đa phương thức bằng AI với n8n, GPT-4, Gemini & Telegram"
description: "Xây dựng trợ lý tài chính thông minh trên Telegram hỗ trợ ghi chép chi tiêu qua văn bản, giọng nói (Voice) và hình ảnh hóa đơn (OCR) tự động đồng bộ Google Sheets."
slug: "quan-ly-tai-chinh-ca-nhan-ai-telegram-n8n"
tags: [n8n, automation, ai-agent, telegram, google-sheets, gpt-4]
keywords: [n8n workflow, trợ lý tài chính ai, telegram expense tracker, gpt-4 gemini ocr n8n, tự động hóa google sheets]
---

# 🚀 Trợ lý tài chính cá nhân thông minh tích hợp AI, Voice & OCR qua Telegram

Quản lý tiền bạc luôn là một "nỗi đau" thủ công: ghi chép sót hóa đơn, lười nhập liệu Excel mỗi cuối ngày, hay việc quy đổi ngoại tệ phức tạp. Bài toán này sẽ được giải quyết triệt để với workflow n8n tự động hóa 100%. 

Hệ thống biến con bot Telegram của các sếp thành một trợ lý tài chính đa năng (Multi-modal). Bot có thể đọc hiểu tin nhắn văn bản, chuyển giọng nói thành chữ nhờ **ElevenLabs**, trích xuất thông tin hóa đơn bằng **Google Gemini OCR**, sau đó phân tích và lưu trữ tự động vào **Google Sheets** bằng sức mạnh của **GPT-4**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Đa phương thức (Multi-modal):** Gửi text, gửi voice note hay chụp ảnh hóa đơn đều được xử lý gọn gàng.
- **Tự động hóa thông minh:** Phân loại ý định (ghi chép hay tra cứu), tự động quy đổi ngoại tệ, tính toán số dư và tổng chi tiêu theo ngày/tuần/tháng.
- **Không tốn sức:** Mọi dữ liệu tự động đồng bộ vào Google Sheets, không cần nhập liệu thủ công.
- **Hoạt động 24/7:** Bot trực sẵn trên Telegram, phản hồi nhanh chóng và thân thiện.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Cloud hoặc Self-hosted).
- Telegram Bot Token (tạo qua `@BotFather`).
- Google Sheets API Credentials (OAuth2).
- Azure OpenAI Credentials (có quyền truy cập mô hình GPT-4).
- ElevenLabs API Key (chuyển đổi giọng nói thành văn bản).
- API Key từ dịch vụ tỷ giá hối đoái (ví dụ: ExchangeRate-API).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ nguồn cung cấp hoặc copy toàn bộ JSON và dán trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Telegram Trigger & Send Message:** Kết nối tài khoản Telegram Bot của các sếp.
- **Google Sheets Tools (`Add_Expenses_Tool`, `Read_Rows_Tool`, `Total_Spent_Tool`, `Balance_Tool`, `Expenses_Tool`):** Cấu hình Google Sheets OAuth2 và liên kết với file Google Sheet quản lý tài chính chuẩn bị sẵn.
- **Azure OpenAI Models (`Intent Classification Model`, `Expense Parsing Model`, `Main Financial Assistant`):** Chọn credentials và cấu hình mô hình `gpt-4.1` (hoặc tương đương).
- **Convert Voice to Text (ElevenLabs):** Nhập API Key của ElevenLabs để xử lý file ghi âm từ Telegram.
- **Exchange_Rate:** Điền API Key lấy tỷ giá ngoại tệ.

**Cấu trúc Google Sheets chuẩn:**
1. Tab **`Expenses`**: Các cột gồm `Expense Date`, `Expense Description`, `Expense Amount (USD)`, `Expense Category`.
2. Tab **`Balance&Total_Spent`**: Điền số dư ban đầu tại ô `B3`. Các ô còn lại (`Current Balance`, `Total Spent by Day/Week/Month`) thiết lập sẵn công thức tính toán tự động.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (Test workflow) bằng cách gửi một tin nhắn mẫu tới bot Telegram.
- Bật công tắc **Active** để đưa workflow vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Báo cáo tự động:** Thêm node Cron (Schedule) để bot tự động gửi tổng kết chi tiêu mỗi tối lúc 21:00 qua Telegram.
- **Cảnh báo ngân sách:** Kết hợp node If để bot hú còi cảnh báo khi chi tiêu vượt quá hạn mức trong tuần.
- **Lưu trữ backup:** Tự động gửi file PDF tổng kết chi tiêu hàng tháng vào Google Drive hoặc email cá nhân.

### 📌 Kết luận
Workflow này là một minh chứng tuyệt vời cho việc ứng dụng AI Agents và kiến trúc MCP (Model Context Protocol) trong n8n nhằm tự động hóa các tác vụ tài chính hàng ngày. Hãy triển khai ngay hôm nay để tối ưu hóa thời gian và làm chủ tài chính cá nhân một cách thông minh nhất!