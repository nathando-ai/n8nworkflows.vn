---
title: "🚀 Tự động cải thiện Website Accessibility với GPT-4o & Google Sheets"
description: "Workflow n8n tự động quét trang web, phát hiện hình ảnh thiếu thẻ alt hoặc alt quá ngắn, sử dụng GPT-4o Vision sinh mô tả chính xác và cập nhật lại Google Sheets – Giải pháp SEO & Accessibility 'set up xong quên' cho Marketer & Dev."
slug: "tu-dong-cai-thien-accessibility-gpt4o-google-sheets"
tags: [n8n, automation, no-code, ai, seo, accessibility, gpt-4o, google-sheets]
keywords: [n8n workflow, tự động hóa seo, website accessibility, alt text generator, gpt-4o vision, google sheets automation]
---

# 🚀 Tự động cải thiện Website Accessibility với GPT-4o & Google Sheets

Việc kiểm tra thủ công hàng trăm trang web để đảm bảo mọi thẻ `<img>` đều có `alt text` mô tả chính xác là cơn ác mộng của bất kỳ SEO Specialist hay Developer nào. Thiếu alt text không chỉ làm giảm điểm **Accessibility (WCAG)** mà còn khiến Google Bot "mù" trước nội dung hình ảnh – mất điểm SEO to lớn.

Workflow này được thiết kế để **giải quyết triệt để bài toán đó**: Tự động quét URL → Trích xuất toàn bộ ảnh + alt text hiện tại → Lọc ra ảnh thiếu/alt quá ngắn → Gọi **GPT-4o Vision** "nhìn" ảnh sinh mô tả ngữ nghĩa → Cập nhật kết quả vào **Google Sheets** để team Dev/Content review và deploy.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian audit**: Quét hàng trăm URL chỉ trong vài phút thay vì hàng giờ làm thủ công.
- **Chuẩn WCAG & SEO**: Alt text do GPT-4o sinh ra giàu ngữ cảnh, mô tả chính xác nội dung hình ảnh.
- **Quy trình đóng vòng lặp**: Dữ liệu thô → Phân tích AI → Output có cấu trúc (Google Sheets) sẵn sàng cho Dev implement.
- **Chi phí gần như bằng 0**: Chỉ tốn chi phí API OpenAI (vài cent/lần chạy) + n8n self-hosted free.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI IMPORT]
- **Tài khoản n8n** (Self-hosted khuyến nghị hoặc Cloud).
- **Google Cloud Project** đã bật **Google Sheets API** & **Google Drive API** + OAuth Credentials.
- **File Google Sheets** mẫu (có thể để trống, workflow sẽ ghi header tự động).
- **OpenAI API Key** có quyền truy cập model **GPT-4o** (hoặc `gpt-4o-mini` để tiết kiệm chi phí).
- Danh sách **URL trang web** cần audit (điền vào node `Page Link`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON workflow từ [n8n.io/workflows/3640](https://n8n.io/workflows/3640) hoặc copy raw JSON.
2. Trên n8n Editor: **Workflows → Import → Chọn file / Paste JSON**.
3. Đổi tên workflow dễ nhớ: `SEO - Auto Alt Text Generator`.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Mở workflow lên, các sếp **bắt buộc** cấu hình 5 node sau:

| Node (Tên hiển thị) | Loại | Hành động cấu hình chi tiết |
| :--- | :--- | :--- |
| **Page Link** | `Set` | **Sửa giá trị `url`** thành link trang web cần audit. <br>💡 *Mẹo: Dùng Expression `{{ $json.url }}` nếu truyền từ Webhook/Form sau này.* |
| **Download HTML** | `HTTP Request` | Kiểm tra **Method: GET**, URL trỏ đến `{{ $json.url }}`. Bật **Response Format: Text** (để lấy HTML thô). |
| **Get Images urls with altText** | `Code` | **KHÔNG CẦN SỬA CODE** (logic đã sẵn: parse HTML, lấy `src` & `alt` của mọi `<img>`). Chỉ cần đảm bảo node chạy sau `Download HTML`. |
| **Download Results** | `Google Sheets` | **Credentials**: Chọn OAuth2 Google Sheets đã tạo.<br>**Operation**: `Read` (hoặc `Get All` tùy version).<br>**Spreadsheet ID/URL**: Dán link file Sheet của sếp.<br>**Sheet Name**: Tên tab (vd: `RawData`).<br>**Options**: Bật `Header Row: 1`. |
| **altLength < 50** | `If` | Điều kiện lọc: `{{ $json.altText.length < 50 }}` (hoặc check `altText` rỗng). Node này quyết định ảnh nào gửi lên GPT-4o. |
| **Generate altText** | `OpenAI` | **Credentials**: OpenAI API Key.<br>**Resource**: `Image` → **Operation**: `Analyze`.<br>**Model**: `gpt-4o` (hoặc `gpt-4o-mini`).<br>**Image**: Chọn `Binary Data` hoặc `URL` (map từ `imageUrl` của node Code).<br>**Prompt**: *Đã có sẵn prompt tối ưu trong workflow, nhưng các sếp có thể tùy chỉnh:*<br>`"Hãy mô tả chi tiết nội dung hình ảnh này bằng tiếng Việt, tập trung vào thông tin chính, văn bản trong ảnh (nếu có) và bối cảnh. Độ dài 50-120 ký tự, phù hợp cho thẻ alt HTML."` |
| **Update Results** | `Google Sheets` | **Operation**: `Update`.<br>**Key Column**: `imageUrl` (hoặc cột unique ID).<br>**Map field**: `altText` ← `{{ $json.choices[0].message.content }}` (output của OpenAI). |
| **Store Results** | `Google Sheets` | **Operation**: `Append` (dùng để log lịch sử chạy). Cấu hình tương tự `Download Results` nhưng ghi vào tab `History`. |

> ⚠️ **Lưu ý quan trọng về Node `Loop Over Items` (`SplitInBatches`)**:
> Workflow dùng node này để xử lý **từng ảnh một** (batch size = 1) tránh lỗi Rate Limit của OpenAI. Các sếp **KHÔNG NÊN TẮT** node này. Nếu muốn chạy nhanh hơn, có thể tăng `Batch Size` lên 5-10 nhưng phải thêm node `Wait` (1-2s) giữa các batch.

#### 3. Kích hoạt ⚡️
1. Click **Test workflow** (node `When clicking ‘Test workflow’`).
2. Kiểm tra tab **Executions**: Xem log node `Get Images urls...` có ra danh sách ảnh không? Node `If` có phân luồng đúng không?
3. Mở Google Sheets kiểm tra cột `altText` đã được điền bởi GPT-4o chưa.
4. Nếu ổn → Bật nút **Active** (góc trên phải) để chạy theo lịch (Cron) hoặc gọi qua Webhook.

### ✍️ Mẹo & gợi ý nâng cao
- 🔗 **Kết hợp Webhook + Form**: Thay `Manual Trigger` bằng `Webhook` → Tạo Google Form/Typeform nhập URL → Tự động trigger workflow cho khách hàng/đội ngũ Content.
- 📊 **Báo cáo Slack/Telegram**: Thêm node `Slack`/`Telegram` sau `Store Results` gửi tin nhắn: *"✅ Đã audit xong `{{ $json.url }}`: Cập nhật `{{ $itemsUpdated }}` alt text mới."*
- 🛡️ **Validate trước khi Deploy**: Thêm node `Function`/`IF` check độ dài alt text mới > 100 ký tự → Cảnh báo review thủ công (tránh AI lan man).
- 🖼️ **Xử lý ảnh Lazy-load/Background**: Node `Code` hiện tại chỉ parse `<img src>`. Các sếp có thể mở rộng regex để bắt `data-src`, `srcset` hoặc `style="background-image: url(...)"`.
- 💰 **Tối ưu chi phí**: Dùng `gpt-4o-mini` cho batch lớn, chỉ dùng `gpt-4o` cho ảnh phức tạp (biểu đồ, infographic).

### 📌 Kết luận
Vài click chuột, một chút cấu hình API – các sếp đã sở hữu một **"nhân viên AI Audit Accessibility"** làm việc 24/7 không ngỉ, không lương, không phàn nàn. Workflow này không chỉ giúp web đạt chuẩn WCAG 2.1 AA mà còn bơm thêm "nhiên liệu" ngữ nghĩa cho Google Bot index hình ảnh tốt hơn – **SEO On-page thực sự "chân ái"**.

👉 **Import ngay hôm nay**, chạy test 1 URL và xem GPT-4o "mô tả ảnh" ngầu như thế nào. Đừng quên share kết quả cho team Dev/Content nhé!

---
*Workflow gốc bởi [Samir Saci](https://www.linkedin.com/in/samir-saci/) | Tutorial chi tiết: [YouTube](https://www.youtube.com/watch?v=LwTIro6Rapk)*