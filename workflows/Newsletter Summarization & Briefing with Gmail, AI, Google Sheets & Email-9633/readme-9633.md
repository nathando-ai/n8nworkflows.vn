---
title: "🚀 Tự động tóm tắt Newsletter & Gửi Briefing ngày bằng Gmail, AI Gemini, Google Sheets & Email"
description: "Giải pháp n8n kéo email newsletter, tách HTML, chia đoạn, tóm tắt bằng AI và gửi báo cáo HTML mỗi ngày – không cần viết code."
slug: "tu-dong-tom-tat-newsletter-gmail-ai-gemini"
tags: [n8n, automation, no-code, AI, email, google-sheets]
keywords: [n8n workflow, tự động hóa, tóm tắt newsletter, AI Gemini, Gmail, Google Sheets, email]
---

# 🚀 Tự động tóm tắt Newsletter & Gửi Briefing ngày

Bạn có bao giờ phải mở hòm thư, sao chép nội dung, dán vào Word, rồi tự mình viết bản tóm tắt cho đội ngũ?  
Việc này tốn hàng giờ, dễ bỏ sót thông tin quan trọng và luôn gây “đau đầu” cho các sếp khi muốn cập nhật nhanh các xu hướng, rủi ro hay cơ hội từ các bản tin.  

**Workflow này** sẽ tự động:

1. **Thu thập** ~10 newsletter mới nhất từ Gmail (theo query bạn định nghĩa).  
2. **Lọc sạch** HTML, loại bỏ tracking, style → chỉ còn plain‑text.  
3. **Chia nhỏ** nội dung thành các chunk an toàn token.  
4. **Ghi lại** từng chunk + metadata vào Google Sheets để lưu trữ và audit.  
5. **Dùng Google Gemini** (LLM) tạo bản tóm tắt ngắn gọn, nêu chủ đề, ảnh hưởng, hành động.  
6. **Xây dựng email HTML** chuyên nghiệp và **gửi** tới các bên liên quan.  

> **Kết quả:** 100 % tự động, không cần code, luôn chạy đúng giờ, giảm thời gian xử lý từ hàng giờ xuống vài phút.

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm thời gian**: Từ vài giờ xuống < 5 phút mỗi ngày.  
- **Độ chính xác cao**: Loại bỏ lỗi copy‑paste, giữ nguyên nội dung gốc.  
- **Báo cáo cá nhân hoá**: Nội dung tóm tắt, hành động rõ ràng, phù hợp từng bộ phận.  
- **Hoạt động liên tục**: Chạy tự động hàng ngày, không phụ thuộc vào con người.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **Tài khoản Gmail** có quyền **read** (hoặc label) các newsletter.  
- **API Key** của **Google Gemini** (hoặc OpenAI nếu muốn thay thế).  
- **Google Cloud Project** với **Google Sheets API** bật, và **OAuth2 credentials** cho n8n.  
- **SMTP server** (hoặc dịch vụ emailSend của n8n) để gửi email báo cáo.  
- **Google Sheet** (tạo trước) để lưu log các chunk.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Vào **n8n > Workflows** → **Import**.  
2. Chọn **Upload JSON** và tải file `newsletter-summarization.json` (được cung cấp kèm).  
3. Hoặc **Copy/Paste** nội dung JSON vào ô **Import from Clipboard** và nhấn **Import**.  

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Dưới đây là các node quan trọng và cách cấu hình chi tiết:

| Node | Loại | Cấu hình cần chỉnh |
|------|------|--------------------|
| **Schedule Trigger** | scheduleTrigger | - **Cron**: `0 8 * * *` (chạy mỗi ngày 08:00) – tùy chỉnh thời gian. |
| **Gmail** | gmail | - **Operation**: `Get All` <br> - **Query**: `label:Newsletter newer_than:1d` (hoặc `from:news@company.com`). <br> - **Max Results**: `10`. |
| **Parse HTML-Code** | code | - **Language**: JavaScript. <br> - **Code**: Loại bỏ thẻ `<script>`, `<style>`, các tracking pixel, và trả về `plainText`. (Mặc định đã có, chỉ cần kiểm tra). |
| **Split in Chunks** | code | - **Language**: JavaScript. <br> - **Code**: Chia `plainText` thành các chunk ≤ 1500 token (hoặc tùy chỉnh `CHUNK_SIZE`). <br> - **Output**: `chunkId`, `text`. |
| **Set Table Fields** | set | - **Fields**: `date`, `source`, `subject`, `chunkId`, `text`. <br> - **Values**: Lấy từ các node trước (e.g., `{{$json["date"]}}`). |
| **Append Row** | googleSheets (operation: append) | - **Spreadsheet ID**: ID của Google Sheet lưu log. <br> - **Sheet Name**: `RawChunks` (hoặc tùy chỉnh). <br> - **Values**: Map các trường từ node **Set Table Fields**. |
| **Memory3** | memoryBufferWindow | - **Size**: `20` (giữ 20 chunk gần nhất). <br> - **Memory Key**: `newsletterMemory`. |
| **Google Gemini Chat Model** | lmChatGoogleGemini | - **Model**: `gemini-pro` (hoặc model bạn có). <br> - **System Prompt**: *“Bạn là chuyên gia Public Affairs. Tóm tắt nội dung newsletter, nêu các chủ đề chính, ảnh hưởng EU/DE, rủi ro, cơ hội và đề xuất hành động.”* <br> - **Temperature**: `0.3`. <br> - **Max Tokens**: `800`. |
| **Public Affairs Consultant** | code | - **Language**: JavaScript. <br> - **Code**: Gọi **Google Gemini** với **Memory3** làm input, trả về `summary`. (Kiểm tra biến `{{$node["Memory3"].json["..."]}}`). |
| **Structure HTML-Mail** | code | - **Language**: JavaScript. <br> - **Code**: Xây dựng HTML email: tiêu đề, TL;DR, danh sách bullet, nguồn. Sử dụng biến `{{$node["Public Affairs Consultant"].json["summary"]}}`. |
| **Google Spreadsheet** | googleSheets (resource: spreadsheet) | - **Spreadsheet ID**: ID của sheet “Digest”. <br> - **Operation**: `Update` (nếu muốn lưu bản tóm tắt). |
| **Send email** | emailSend | - **To**: `director@company.com` (hoặc danh sách). <br> - **Subject**: `Daily Public Affairs Digest – {{ $now.format("YYYY-MM-DD") }}`. <br> - **HTML**: Dùng output của **Structure HTML-Mail**. <br> - **Attachments**: (tuỳ chọn). |

> **Lưu ý:** Đảm bảo mỗi node **Credentials** được gán đúng (Gmail, Google Sheets, Gemini, SMTP). Nếu chưa có, tạo mới trong **n8n > Credentials** và chọn **OAuth2** hoặc **API Key** tương ứng.

#### 3. Kích hoạt ⚡️
1. **Test run**: Nhấn **Execute Workflow** → kiểm tra log từng node, đặc biệt là **Parse HTML-Code**, **Split in Chunks**, và **Public Affairs Consultant**.  
2. Nếu mọi thứ trả về kết quả mong muốn, bật **Active** (nút chuyển đổi góc phải).  
3. Kiểm tra hộp thư nhận **email** để xác nhận format và nội dung.  

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối Slack/Telegram**: Thêm node **Slack** hoặc **Telegram** sau node **Send email** để gửi thông báo nhanh.  
- **Lưu log chi tiết**: Thêm một **Google Sheets** khác để ghi lại `summary`, `tokenUsage`, và `runtime`.  
- **Báo cáo định kỳ**: Dùng **Cron** khác (ví dụ: mỗi tuần) để tổng hợp các digest trong Google Sheet và gửi báo cáo tổng hợp.  
- **Thay đổi Prompt**: Đổi `System Prompt` thành “Legal Analyst” hoặc “ESG Analyst” để tái sử dụng workflow cho các lĩnh vực khác.  

### 📌 Kết luận
Với workflow **Newsletter Summarization & Briefing**, các sếp có thể “đánh bại” công việc thủ công, nhận bản tóm tắt chất lượng cao mỗi ngày và tập trung vào quyết định chiến lược. Hãy import ngay, cấu hình các credentials, bật chạy và cảm nhận sức mạnh của tự động hoá không code! 🚀