---
title: "🚀 Tự động giao sản phẩm sau mua & Upsell với JotForm, Google Drive, Gemini"
description: "Giải pháp không code tự động chia sẻ file, ghi nhận đơn hàng, tạo email cảm ơn AI và gửi ngay sau khi khách hàng hoàn tất mua hàng trên JotForm."
slug: "tu-dong-giao-san-pham-sau-mua-upsell-jotform-google-drive-gemini"
tags: [n8n, automation, no-code, email-marketing, ai]
keywords: [n8n workflow, tự động hóa, giao sản phẩm, email AI, JotForm, Google Gemini]
---

# 🚀 Tự động giao sản phẩm sau mua & Upsell với JotForm, Google Drive, Gemini

Khi khách hàng mua hàng qua form trực tuyến, **các sếp** thường phải thực hiện một loạt công việc thủ công: tải file lên Drive, chia sẻ link, nhập dữ liệu vào bảng tính, viết email cảm ơn, rồi mới bấm gửi.  
Quá trình này tốn thời gian, dễ sai sót và mất đi cơ hội upsell ngay khi khách còn “nóng”.  

Workflow **Automated Post-Purchase Product Delivery & Upsell** giúp **tự động 100 %** các bước trên mà không cần viết một dòng code nào. Khi khách hàng hoàn tất mua hàng trên JotForm, hệ thống sẽ:

1. **Chia sẻ file sản phẩm** từ Google Drive ngay lập tức.  
2. **Ghi nhận đơn hàng** vào Google Sheet để quản lý và phân tích.  
3. **AI Gemini** tạo email cảm ơn cá nhân hoá, kèm đề xuất upsell.  
4. **Gửi email** tự động qua Gmail tới khách hàng.

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm thời gian**: Loại bỏ công việc nhập liệu và gửi email thủ công.  
- **Độ chính xác 100 %**: Không còn lỗi sai địa chỉ email hay link file.  
- **Cá nhân hoá & Upsell**: Email AI đề xuất sản phẩm liên quan, tăng doanh thu trung bình mỗi đơn hàng.  
- **Hoạt động liên tục**: Workflow chạy 24/7, không phụ thuộc vào giờ làm việc.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **Tài khoản JotForm** + API key (`jotFormApi`).  
- **Google Drive** và **Google Sheets**: cấp quyền OAuth2 (`googleApi`, `googleSheetsOAuth2Api`).  
- **Gmail**: tài khoản Gmail với OAuth2 (`gmailOAuth2`).  
- **Google Gemini (Palm)**: API key (`googlePalmApi`).  
- **Google Sheet** đã tạo sẵn để lưu đơn hàng (ID và tên sheet).  
- **File sản phẩm** đã lưu trên Google Drive (ID hoặc tên).  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n → **Workflows** → **Import**.  
2. Chọn **Upload JSON** và tải file JSON của workflow (hoặc copy/paste nội dung JSON vào ô).  
3. Nhấn **Import**, workflow sẽ xuất hiện trên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Cấu hình cần chỉnh | Ghi chú |
|------|-------------------|---------|
| **JotForm Trigger** | - Chọn **Credential** `jotFormApi`.<br>- Nhập **Form ID** của form mua hàng. | Khi khách hàng submit form, node sẽ kích hoạt workflow. |
| **Share file** (Google Drive) | - Credential `googleApi`.<br>- **Operation**: `share` (đã mặc định).<br>- **File ID**: ID của file sản phẩm.<br>- **Email**: `{{$json["email"]}}` (lấy từ dữ liệu JotForm).<br>- **Role**: `reader` hoặc `writer` tùy nhu cầu. | Đảm bảo file đã chia sẻ công khai cho người nhận. |
| **Append or update row in sheet** (Google Sheets) | - Credential `googleSheetsOAuth2Api`.<br>- **Spreadsheet ID** và **Sheet Name**.<br>- **Values**: map các trường JotForm (Tên, Email, Sản phẩm, Ngày mua...). | Dùng để lưu lịch sử đơn hàng, hỗ trợ báo cáo. |
| **AI Agent** | - **Prompt**: “Viết một email cảm ơn khách hàng {{name}} đã mua {{product}}. Đề xuất upsell sản phẩm {{related_product}}.” (có thể tùy chỉnh).<br>- **Input**: dữ liệu từ JotForm (name, email, product). | Node này sẽ truyền prompt tới Gemini. |
| **Google Gemini Chat Model** | - Credential `googlePalmApi`.<br>- **Model**: `gemini-pro` (hoặc phiên bản mới nhất).<br>- **Temperature**: 0.7 (độ sáng tạo). | Đảm bảo quota API đủ. |
| **Structured Output Parser** | - **Schema**: JSON schema mô tả cấu trúc email (subject, body, upsell_link).<br>- **Input**: output từ Gemini. | Giúp tách riêng tiêu đề và nội dung email. |
| **Send a message** (Gmail) | - Credential `gmailOAuth2`.<br>- **To**: `{{$json["email"]}}`.<br>- **Subject**: `{{$json["subject"]}}` (từ parser).<br>- **Body**: `{{$json["body"]}}` (HTML hoặc plain). | Kiểm tra quota gửi mail của Gmail. |

> **⚠️ Lưu ý:** Đảm bảo các trường JSON (`email`, `name`, `product`, …) khớp với tên trường trong JotForm. Nếu tên trường khác, chỉnh lại mapping trong node **Append or update row in sheet** và **AI Agent**.

#### 3. Kích hoạt ⚡️
1. **Test run**: Nhấn **Execute Workflow** → nhập dữ liệu mẫu (hoặc thực hiện một submission thực tế trên JotForm).  
2. Kiểm tra: file đã được chia sẻ, dòng mới xuất hiện trong Sheet, email được gửi và nội dung AI hợp lý.  
3. Khi mọi thứ ổn, bật **Active** (nút chuyển đổi ở góc trên bên phải) để workflow tự động chạy 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối Slack/Telegram**: Thêm node Slack để thông báo nội bộ mỗi khi có đơn hàng mới.  
- **Lưu log chi tiết**: Dùng Google Cloud Logging hoặc một Sheet phụ để ghi lại thời gian chạy, lỗi API.  
- **Báo cáo định kỳ**: Thêm node Google Sheets → Google Docs → Gmail để gửi báo cáo doanh thu hàng tuần.  
- **Upsell tự động**: Sử dụng thêm node **HTTP Request** để tạo coupon code và đính kèm trong email.  

### 📌 Kết luận
Với workflow này, các sếp có thể **tự động hoá toàn bộ quy trình giao sản phẩm và upsell** ngay sau khi khách hàng mua hàng, giảm thiểu công sức, tăng độ chính xác và tối đa hoá doanh thu. Hãy **import ngay**, cấu hình các credential và bắt đầu trải nghiệm tự động hoá không giới hạn! 🚀