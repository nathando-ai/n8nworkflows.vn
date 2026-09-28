---
title: "🚀 Tự Động Tạo Đề Xuất Bán Hàng AI với Claude & PDF Noodle"
description: "Workflow n8n kết nối CRM, AI Claude và PDF Noodle để tạo đề xuất bán hàng dạng PDF và gửi email tự động, giảm 80% thời gian soạn thảo."
slug: "tu-dong-tao-de-xuat-ban-hang-ai-claude-pdf-noodle"
tags: [n8n, automation, no-code, AI, PDF, CRM]
keywords: [n8n workflow, tự động hóa, AI proposal, Claude, PDF Noodle, CRM integration]
---

# 🚀 Tự Động Tạo Đề Xuất Bán Hàng AI với Claude & PDF Noodle

Bạn đã từng phải **soạn đề xuất bán hàng** thủ công, sao chép dữ liệu từ CRM sang tài liệu, rồi lại phải định dạng lại, kiểm tra lỗi và cuối cùng mới gửi email?  
Quá trình này **tiêu tốn hàng giờ**, dễ sai sót và khiến cơ hội bán hàng bị trễ.  

Workflow **“Generate AI sales proposals using Anthropic Claude, PDF Noodle and your CRM”** giải quyết 100% công việc trên **không cần viết một dòng code nào**:  
- Nhận dữ liệu khách hàng từ CRM qua webhook.  
- Dùng **Claude Sonnet** (Anthropic) để tạo nội dung đề xuất chuyên nghiệp.  
- Chuyển nội dung thành **PDF** bằng **PDF Noodle**.  
- Gửi PDF đính kèm qua **Gmail** ngay lập tức.  

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm thời gian**: Từ 30‑60 phút giảm còn < 2 phút mỗi đề xuất.  
- **Độ chính xác cao**: Dữ liệu CRM được truyền thẳng, không còn lỗi copy‑paste.  
- **Cá nhân hoá**: AI tạo nội dung phù hợp từng khách hàng dựa trên thông tin CRM.  
- **Hoạt động liên tục**: Workflow chạy tự động 24/7, không cần can thiệp thủ công.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **Tài khoản PDF Noodle** – tạo tại: https://app.pdfnoodle.com/auth/sign-up  
- **API key Anthropic** (Claude Sonnet) – thêm vào credentials `anthropicApi` trong n8n.  
- **Google OAuth2** (Gmail) – tạo credential `gmailOAuth2` với quyền gửi email.  
- **CRM** có khả năng gọi webhook POST (đường dẫn `/ai-proposal`).  
- **n8n** (cài đặt self‑hosted hoặc cloud) với các node: `set`, `gmail`, `webhook`, `stickyNote`, `pdforge`, `httpRequest`, `agent`, `lmChatAnthropic`, `outputParserStructured`.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. **Tải file JSON** của workflow (từ trang gốc https://n8n.io/workflows/13232).  
2. Vào n8n → **Workflows** → **Import** → **Upload JSON** hoặc **Paste JSON** vào ô.  
3. Nhấn **Import** → Workflow sẽ xuất hiện trong danh sách.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Công việc | Cấu hình cần chỉnh |
|------|-----------|--------------------|
| **Webhook** | Nhận dữ liệu từ CRM | - `Path`: `ai-proposal` <br> - `HTTP Method`: `POST` |
| **Fields Mapping** (Set) | Định dạng lại dữ liệu CRM | - Thêm các trường cần thiết (e.g., `clientName`, `company`, `dealSize`, `contactEmail`). |
| **AI Agent** | Điều phối luồng AI | - Không cần credentials, chỉ kết nối tới **Anthropic Chat Model**. |
| **Anthropic Chat Model** | Tạo nội dung đề xuất | - Chọn **Credential** `anthropicApi`.<br> - Model: `claude-sonnet-4-5-20250929`. |
| **Structured Output Parser** | Chuyển output AI thành JSON có cấu trúc | - Định nghĩa schema (title, bullet points, pricing, CTA). |
| **Generate PDF synchronously** (pdforge) | Tạo PDF từ template | - Credential `pdforgeApi`.<br> - Chọn **Template ID** (được tạo trên PDF Noodle).<br> - Map các biến từ output parser vào template. |
| **Download PDF binary** (HTTP Request) | Lấy file PDF dưới dạng binary | - Method: `GET` <br> - URL: `{{$node["Generate PDF synchronously"].json["pdfUrl"]}}` <br> - `Response Format`: `File`. |
| **Send a message** (Gmail) | Gửi email kèm PDF | - Credential `gmailOAuth2`. <br> - `To`: `{{$json["contactEmail"]}}` <br> - `Subject`: `Proposal for {{$json["clientName"]}}`. <br> - `Attachments`: `{{$node["Download PDF binary"].binary["data"]}}`. |

> **Lưu ý:** Đảm bảo các **credentials** đã được tạo và **kết nối** đúng trong n8n → **Credentials**. Nếu chưa có, tạo mới trước khi lưu workflow.

#### 3. Kích hoạt ⚡️
1. **Test run**: Gửi một payload mẫu từ CRM (hoặc dùng công cụ Postman) tới `https://<your-n8n-domain>/webhook/ai-proposal`.  
2. Kiểm tra log từng node, xác nhận PDF được tạo và email được gửi.  
3. Khi mọi thứ ổn, bật **Active** ở góc phải của workflow.  

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối Slack/Telegram**: Thêm node `Slack` hoặc `Telegram` sau node `Send a message` để thông báo nội bộ khi đề xuất đã gửi.  
- **Lưu log vào Google Sheet**: Dùng node `Google Sheets` để ghi lại thời gian gửi, khách hàng, và trạng thái.  
- **Báo cáo định kỳ**: Sử dụng node `Cron` + `Google Slides` để tổng hợp số lượng đề xuất đã gửi trong tuần/tháng.  
- **Tùy chỉnh template PDF**: Tạo nhiều template trên PDF Noodle (ví dụ: “Enterprise”, “SMB”) và dùng **IF** node để chọn template dựa trên `dealSize`.  

### 📌 Kết luận
Với workflow này, các sếp có thể **tự động hoá toàn bộ quy trình tạo và gửi đề xuất bán hàng** chỉ trong vài giây, giảm thiểu lỗi và tăng tốc độ phản hồi khách hàng. Hãy **import ngay**, cấu hình các credentials cần thiết và để AI làm việc cho bạn! 🚀