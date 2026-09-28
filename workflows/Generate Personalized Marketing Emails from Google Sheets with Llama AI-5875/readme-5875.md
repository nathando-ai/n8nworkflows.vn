---
title: "🚀 Tự động tạo và gửi email marketing cá nhân hóa từ Google Sheets bằng Llama AI trong n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa chiến dịch email marketing, kết hợp Google Sheets và Llama AI để tạo nội dung cá nhân hóa 100%."
slug: "tao-email-marketing-ca-nhan-hoa-google-sheets-lama-ai"
tags: [n8n, automation, no-code, ai, google-sheets, gmail, ollama]
keywords: [n8n workflow, tự động hóa email marketing, Llama AI, Google Sheets, Gmail automation, AI Agent n8n]
---

# 🚀 Tự động hóa Email Marketing cá nhân hóa với Llama AI và Google Sheets

Các chiến dịch email marketing thủ công thường tốn rất nhiều thời gian, nhàm chán và tỷ lệ chuyển đổi thấp do nội dung chung chung, thiếu sự cá nhân hóa cho từng khách hàng. 

Giải pháp tuyệt vời cho các sếp đây: Workflow n8n tự động hoàn toàn hóa quy trình này! Hệ thống sẽ lấy thông tin ưu đãi từ **Google Sheets**, kết hợp với danh sách khách hàng, sử dụng sức mạnh của **Llama AI (Ollama)** để viết nội dung siêu cá nhân hóa và tự động gửi đi qua **Gmail** mà không cần tốn một giọt mồ hôi nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn phải ngồi soạn từng email hay copy-paste thủ công thông tin khách hàng.
- **Cá nhân hóa đỉnh cao:** AI tự động phân tích dữ liệu từng khách hàng để viết nội dung đúng "pain point" của họ.
- **Tự động hóa 24/7:** Kích hoạt ngay khi có chương trình khuyến mãi mới hoặc cập nhật từ Google Sheets.
- **Chuyên nghiệp & Chính xác:** Gửi trực tiếp qua tài khoản Gmail cá nhân/doanh nghiệp một cách mượt mà.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google Sheets:** Chuẩn bị 2 bảng dữ liệu:
  - *Sheet 1:* Chứa chi tiết chương trình khuyến mãi/ưu đãi (Marketing Offer Details).
  - *Sheet 2:* Chứa thông tin danh sách khách hàng (Client Information).
- **Ollama:** Đã cài đặt mô hình Llama (ví dụ: `llama3.2`) để AI xử lý nội dung.
- **Gmail Account:** Kết nối OAuth2 để gửi email.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trên n8n Editor, sau đó copy toàn bộ mã JSON của workflow này và dán trực tiếp vào giao diện làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy trơn tru, các sếp cần cấu hình chính xác các node sau:

- **Track Offer Sheet Updates (Sheet 1):** 
  - Kết nối tài khoản Google thông qua `googleSheetsTriggerOAuth2Api`.
  - Chọn đúng file Google Sheet và Sheet chứa thông tin chương trình khuyến mãi. Node này đóng vai trò là "ngòi nổ" kích hoạt workflow khi có offer mới.
- **Fetch Client List (Sheet 2):**
  - Cấu hình credentials Google Sheets (`googleApi`).
  - Trỏ tới file chứa danh sách khách hàng để lấy thông tin tên, email, sở thích...
- **Llama 3.2 - Promo Content Model:**
  - Kết nối với Ollama Server của các sếp (`ollamaApi`).
  - Đảm bảo tham số model được điền chính xác (ví dụ: `llama3.2-16000:latest`).
- **Generate Marketing Content with AI (Agent):**
  - Kiểm tra lại system prompt để AI hiểu rõ cách kết hợp dữ liệu từ Sheet 1 và Sheet 2 nhằm tạo ra mẫu email hấp dẫn nhất.
- **Format Personalized Email (Code):**
  - Node JavaScript này giúp bóc tách kết quả từ AI, định dạng lại tiêu đề và nội dung HTML sạch sẽ trước khi gửi.
- **Send Marketing Email to Client (Gmail):**
  - Kết nối credentials `gmailOAuth2`.
  - Map trường `Email` từ dữ liệu khách hàng vào mục "To", đồng thời đưa tiêu đề và nội dung đã được định dạng từ các bước trước vào email.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** chạy thử với một dòng dữ liệu mẫu để kiểm tra xem Gmail có nhận được email nháp/gửi đi hay chưa.
- Nếu mọi thứ mượt mà, hãy gạt công tắc sang **Active** để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm bước thông báo:** Gắn thêm node Telegram hoặc Slack ở cuối workflow để báo cáo về máy ngay khi gửi thành công email cho khách hàng.
- **Lưu lịch sử:** Thêm một node Google Sheets phụ để ghi lại trạng thái "Đã gửi email" vào ngay dòng dữ liệu của khách hàng, tránh gửi trùng lặp.
- **Đa dạng hóa mô hình:** Có thể thay thế Llama bằng OpenAI (GPT-4o) hoặc Anthropic (Claude) tùy thuộc vào chi phí và nhu cầu nội dung của doanh nghiệp.

### 📌 Kết luận
Workflow tích hợp Llama AI và Google Sheets này là vũ khí cực kỳ lợi hại giúp các sếp tối ưu hóa phễu chăm sóc khách hàng bằng AI. Hãy cài đặt ngay để nâng tầm chuyên nghiệp cho hoạt động marketing của doanh nghiệp!