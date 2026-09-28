---
title: "🚀 Tự Động Tạo Đề Xuất Bán Hàng AI với PandaDoc, ClickUp CRM & Gmail"
description: "Biến form sau cuộc gọi thành đề xuất PandaDoc cá nhân hoá, cập nhật ClickUp CRM và soạn email Gmail chỉ trong vài giây."
slug: "tu-dong-tao-de-xuat-ban-hang-ai-pandadoc-clickup-gmail"
tags: [n8n, automation, no-code, sales, proposal, AI]
keywords: [n8n workflow, tự động hóa, đề xuất bán hàng, PandaDoc, ClickUp CRM, Gmail draft, OpenAI]
---

# 🚀 Tự Động Tạo Đề Xuất Bán Hàng AI với PandaDoc, ClickUp CRM & Gmail

Bạn đã từng phải **ngồi hàng giờ** để viết lại nội dung đề xuất sau mỗi cuộc gọi bán hàng?  
Việc sao chép thông tin từ form, chỉnh sửa văn bản, tạo link PandaDoc, cập nhật CRM và cuối cùng soạn email **đòi hỏi thời gian và công sức** – thường dẫn đến sai sót và mất cơ hội.

**Workflow này** sẽ giải quyết toàn bộ quy trình **100 % không cần code**:
1. Nhận dữ liệu từ form Typeform ngay sau cuộc gọi.  
2. AI (OpenAI) tự động tạo nội dung đề xuất chuyên nghiệp.  
3. Gửi nội dung tới PandaDoc qua HTTP request để tạo bản đề xuất.  
4. Cập nhật Lead trong ClickUp CRM với tên công ty, link đề xuất và giá báo giá.  
5. Tạo bản nháp email trong Gmail, sẵn sàng gửi cho khách hàng.

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm thời gian**: Từ 30‑45 phút giảm còn < 5 phút.  
- **Độ chính xác cao**: Dữ liệu được truyền tự động, giảm lỗi nhập tay.  
- **Cá nhân hoá đề xuất**: AI viết nội dung dựa trên thông tin thực tế của khách hàng.  
- **Hoạt động liên tục**: Workflow chạy 24/7, không cần can thiệp thủ công.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **Typeform** (hoặc công cụ form tương tự) – API key và ID form.  
- **OpenAI** – API key (credential `openAiApi`).  
- **PandaDoc** – API token, ID template (được dùng trong node HTTP Request).  
- **ClickUp** – OAuth2 credentials (`clickUpOAuth2Api`) và các custom field:  
  - `Company Name`  
  - `Proposal URL`  
  - `Quote`  
- **Gmail** – OAuth2 credentials (`gmailOAuth2`).  
- **n8n** – Được cài đặt và có quyền truy cập internet để gọi API.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. **Tải file JSON** của workflow (từ trang gốc hoặc liên kết chia sẻ).  
2. Vào n8n → **Workflows** → **Import** → Chọn file JSON → **Import**.  
   *Hoặc* sao chép toàn bộ JSON và dán vào **Import from Clipboard**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Mô tả | Cấu hình cần thay đổi |
|------|------|-----------------------|
| **Sales Call Form** (Typeform Trigger) | Nhận dữ liệu form sau cuộc gọi. | - Chọn **Credential** `typeformApi`. <br> - Điền **Form ID** của form bạn đã tạo. |
| **Generate Proposal Copy** (OpenAI) | AI tạo nội dung đề xuất dựa trên dữ liệu form. | - Chọn **Credential** `openAiApi`. <br> - Tùy chỉnh **Prompt** nếu muốn thay đổi giọng điệu (casual, corporate, …). |
| **Create PandaDoc Proposal** (HTTP Request) | Gửi JSON tới PandaDoc để tạo bản đề xuất. | - **Method**: `POST` <br> - **URL**: `https://api.pandadoc.com/public/v1/documents` <br> - **Headers**: `Authorization: Bearer <YOUR_PANDADOC_TOKEN>` <br> - **Body**: Chỉnh sửa JSON để khớp với template của bạn (đặt biến `{{proposalCopy}}`, `{{clientName}}`, …). |
| **ClickUp** (Update) | Cập nhật trạng thái Lead trong ClickUp. | - Chọn **Credential** `clickUpOAuth2Api`. <br> - **Space ID**, **Folder ID**, **List ID** và **Task ID** (được truyền từ form). |
| **Add Company Name** (Set Custom Field) | Ghi tên công ty vào custom field. | - Chọn **Credential** `clickUpOAuth2Api`. <br> - **Custom Field ID** cho “Company Name”. |
| **Quote** (Set Custom Field) | Ghi giá báo giá vào custom field. | - Tương tự, chọn **Custom Field ID** cho “Quote”. |
| **Proposal URL** (Set Custom Field) | Ghi link PandaDoc vào custom field. | - Chọn **Custom Field ID** cho “Proposal URL”. |
| **Create a Draft** (Gmail) | Tạo bản nháp email cảm ơn kèm link đề xuất. | - Chọn **Credential** `gmailOAuth2`. <br> - **To**, **Subject**, **Body**: sử dụng biểu thức `{{$json["proposalUrl"]}}` để chèn link. |

> **Lưu ý:** Đảm bảo mọi **Custom Field ID** trong ClickUp được tạo trước và khớp chính xác với ID trong node.

#### 3. Kích hoạt ⚡️
1. **Test run**: Điền mẫu dữ liệu thử trong Typeform → Kiểm tra log của từng node trong n8n.  
2. Khi mọi thứ hoạt động ổn, bật **Active** ở góc phải của workflow.  
3. Theo dõi **Execution List** để chắc chắn không có lỗi.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo Slack/Telegram**: Thêm node `Slack` hoặc `Telegram` sau node Gmail để nhận thông báo “Draft ready”.  
- **Lưu log vào Google Sheets**: Dùng node `Google Sheets` để ghi lại thời gian tạo đề xuất, giúp đo lường hiệu suất.  
- **Tự động gửi email**: Thay đổi `resource: draft` thành `resource: send` nếu muốn email được gửi ngay sau khi tạo.  
- **PDF tự động**: Sử dụng node `PDF Generator` (hoặc PandaDoc webhook) để tải bản PDF về và lưu vào Dropbox/Google Drive.  
- **Đa ngôn ngữ**: Thêm tham số `language` vào prompt OpenAI để tạo đề xuất bằng tiếng Anh, tiếng Nhật, …  

### 📌 Kết luận
Với workflow này, **các sếp** sẽ không còn phải mất thời gian soạn đề xuất thủ công nữa. Chỉ cần một form ngắn sau cuộc gọi, AI sẽ lo phần nội dung, PandaDoc tạo tài liệu, ClickUp cập nhật thông tin và Gmail chuẩn bị email follow‑up. Hãy **import ngay**, cấu hình các credential và bắt đầu tự động hoá quy trình bán hàng của mình!

---