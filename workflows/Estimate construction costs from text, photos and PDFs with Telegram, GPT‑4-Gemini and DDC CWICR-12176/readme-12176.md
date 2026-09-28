---
title: "🚀 Ước tính chi phí xây dựng tự động từ Văn bản, Hình ảnh và PDF với n8n, AI & DDC CWICR"
description: "Hướng dẫn cài đặt workflow n8n cực khủng tích hợp Telegram, OpenAI, Gemini và Qdrant để tự động bóc tách khối lượng và tính toán chi phí xây dựng từ ảnh chụp, bản vẽ PDF với cơ sở dữ liệu 55,000+ định mức."
slug: "uoc-tinh-chi-phi-xay-dung-tu-dong-n8n-telegram-ai"
tags: [n8n, automation, ai, construction, telegram, openai, qdrant, vector-search]
keywords: [n8n workflow, ước tính chi phí xây dựng, ai construction estimation, ddc cwicr, qdrant vector search, tự động hóa n8n]
---

# 🚀 Ước tính chi phí xây dựng tự động từ Văn bản, Hình ảnh và PDF với n8n, AI & DDC CWICR

Các kỹ sư định lượng (QS), nhà thầu và chủ đầu tư thường xuyên phải đối mặt với nỗi đau: Mất hàng giờ để đo bóc khối lượng thủ công từ bản vẽ PDF, đọc bản vẽ mặt bằng từ ảnh chụp và tra cứu hàng ngàn đơn giá xây dựng. 

Workflow n8n "khủng" với 91 nodes này chính là giải pháp tự động hóa 100% toàn bộ quy trình trên thông qua trợ lý ảo Telegram tích hợp AI đa năng (OpenAI GPT-4, Gemini 2.0 Flash) và cơ sở dữ liệu định mức xây dựng khổng lồ **DDC CWICR (55,000+ rates)**.

:::info[Gợi ý hạ tầng cho n8n]
Vì workflow này có xử lý file nặng (ảnh, PDF nhiều trang) và gọi nhiều API AI phức tạp, để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Nhận yêu cầu, bóc tách ảnh/PDF và tính toán chi phí trực tiếp qua chat Telegram.
- **AI Thị giác thông minh**: Hỗ trợ Gemini 2.0 Flash hoặc GPT-4 Vision để phân tích ảnh công trình hoặc mặt bằng PDF cực kỳ chính xác.
- **Tra cứu Vector thông minh (RAG)**: Kết hợp OpenAI Embedding và Qdrant Vector DB với hơn 55,000 định mức xây dựng.
- **Đa ngôn ngữ & Xuất báo cáo đa dạng**: Hỗ trợ 9 ngôn ngữ (DE, EN, RU, ES, FR, IT, PL, PT, UK) và xuất file báo cáo ra Excel, PDF, HTML chuyên nghiệp.
:::

---

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị sẵn:
- **Telegram Bot Token**: Tạo qua [@BotFather](https://t.me/BotFather).
- **OpenAI API Key**: Dùng cho text embedding và xử lý ngôn ngữ.
- **Gemini API Key**: Dùng cho Vision AI phân tích ảnh/PDF (hoặc dùng GPT-4 Vision).
- **Qdrant Vector Database**: URL và API Key chứa cơ sở dữ liệu định mức xây dựng (hoặc chạy local/VPS).
:::

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Copy toàn bộ mã JSON của workflow và paste trực tiếp vào n8n Editor của các sếp, hoặc import file JSON thông qua giao diện n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần chú ý cấu hình các thành phần trọng yếu sau:

- **Node `🔑 TOKEN` (Set node)**: 
  Điền đầy đủ thông tin token và các API key vào cấu hình JSON của node này:
  ```json
  {
    "bot_token": "YOUR_BOT_TOKEN",
    "AI_PROVIDER": "gemini",
    "GEMINI_API_KEY": "YOUR_KEY",
    "OPENAI_API_KEY": "YOUR_KEY",
    "QDRANT_URL": "http://...",
    "QDRANT_API_KEY": "YOUR_KEY"
  }
  ```
- **Node `Telegram Trigger` & Các node gửi tin nhắn (`📤 Send PDF`, `📤 Send Excel`, `📤 Send HTML`)**:
  - Tạo Credentials loại **Telegram API** trong n8n bằng Bot Token lấy từ `@BotFather`.
  - Liên kết credential này vào `Telegram Trigger` và các node gửi tài liệu tương ứng.

#### 3. Kích hoạt ⚡️
- Gửi thử lệnh `/start` tới bot Telegram của các sếp để kiểm tra kết nối Webhook.
- Bật công tắc **Active** cho workflow để bắt đầu vận hành tự động 24/7.

---

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo**: Có thể tích hợp thêm node Slack hoặc Discord để gửi bản bóc tách khối lượng về kênh chung của dự án.
- **Lưu lịch sử báo cáo**: Kết nối thêm Google Sheets hoặc PostgreSQL node để lưu lại lịch sử các lần ước tính chi phí của khách hàng/nhân sự.
- **Tối ưu tốc độ AI**: Sử dụng Gemini 2.0 Flash làm Vision Provider chính để tối ưu hóa tốc độ phản hồi và chi phí gọi API so với các mô hình khác.

---

### 📌 Kết luận
Workflow này là một cỗ máy tự động hóa hoàn hảo dành cho ngành xây dựng và kỹ thuật, giúp tiết kiệm đến 90% thời gian đo bóc khối lượng và tra cứu định mức. Hãy áp dụng ngay vào quy trình kinh doanh hoặc dự án của các sếp để tạo ra lợi thế cạnh tranh vượt trội!