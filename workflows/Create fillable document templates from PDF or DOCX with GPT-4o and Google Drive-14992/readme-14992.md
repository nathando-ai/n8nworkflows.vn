---
title: "🚀 Tự động tạo mẫu tài liệu có thể điền từ PDF/DOCX bằng GPT‑4o & Google Drive"
description: "Giải pháp n8n cho phép chuyển PDF hoặc DOCX thành mẫu tài liệu có thể điền, nhờ GPT‑4o trích xuất nội dung và Google Drive lưu trữ, giảm 100% công việc thủ công."
slug: "tu-dong-tao-mau-tai-lieu-tu-pdf-docx-bang-gpt4o-google-drive"
tags: [n8n, automation, no-code, AI, "Google Drive", "Document Processing"]
keywords: [n8n workflow, tự động tạo mẫu tài liệu, GPT-4o, Google Drive, trích xuất PDF, AI summarization]
---

# 🚀 Tự động tạo mẫu tài liệu có thể điền từ PDF/DOCX bằng GPT‑4o & Google Drive

Bạn đã từng phải mở từng file PDF/DOCX, sao chép nội dung, tạo form thủ công trong Google Docs hay Microsoft Word?  
Công việc này không chỉ tốn thời gian mà còn dễ gây lỗi, đặc biệt khi số lượng tài liệu lên hàng chục, hàng trăm.  

**Workflow này** sẽ tự động:

1. Nhận file PDF/DOCX qua webhook.  
2. Dùng **GPT‑4o** (OpenAI) để trích xuất nội dung, nhận dạng các trường cần điền (Tên, Ngày, Địa chỉ…).  
3. Tạo **Google Docs template** có các placeholder có thể điền ({{field}}).  
4. Lưu template vào **Google Drive** và trả về link cho người dùng.

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm thời gian**: Từ vài phút/đơn sang vài giây/đơn.  
- **Độ chính xác cao**: GPT‑4o nhận dạng trường dữ liệu tốt hơn so với việc copy‑paste thủ công.  
- **Tự động hoá liên tục**: Workflow chạy 24/7, không cần can thiệp người dùng.  
- **Dễ dàng chia sẻ**: Link Google Docs luôn luôn cập nhật, mọi người có thể truy cập ngay.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **Tài khoản OpenAI** với **API Key** (có quyền truy cập GPT‑4o).  
- **Google Cloud Project** bật Google Drive API, tạo **OAuth 2.0 Client ID** và cấp quyền `https://www.googleapis.com/auth/drive.file`.  
- **Webhook URL** (có thể dùng n8n Cloud hoặc tự host).  
- **n8n** (phiên bản mới nhất) đã cài đặt các node: `code`, `switch`, `webhook`, `stickyNote`, `googleDrive`, `httpRequest`, `word2text`, `langchain.agent`, `extractFromFile`, `respondToWebhook`, `lmChatOpenAi`.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập **n8n → Workflows → Import**.  
2. Tải file JSON từ link gốc: <https://n8n.io/workflows/14992>.  
3. Hoặc **Copy/Paste** toàn bộ JSON vào ô “Import from Clipboard”.  

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Công việc | Cấu hình cần chỉnh |
|------|-----------|--------------------|
| **Webhook** | Nhận file PDF/DOCX | - Chọn **HTTP Method**: `POST` <br> - Đặt **Response Mode**: `On Received` <br> - Lưu **Webhook URL** để gửi file từ hệ thống bên ngoài. |
| **Extract From File** | Trích xuất nội dung thô | - **File Property**: `binaryData` (đầu vào từ webhook). |
| **Word2Text** | Chuyển DOCX → Text (nếu file là DOCX) | - Không cần thay đổi, chỉ đảm bảo **Input** là `binaryData`. |
| **Code** (Node “Detect Fields”) | Dùng regex hoặc prompt để xác định các trường cần điền | - Thêm **Prompt**: “Identify placeholders such as Name, Date, Address … from the following text.” <br> - Chọn **Credentials**: OpenAI API Key. |
| **LM Chat OpenAI (GPT‑4o)** | Gọi GPT‑4o để nhận danh sách placeholder | - Model: `gpt-4o` <br> - Temperature: `0` (độ chính xác cao). |
| **Switch** | Kiểm tra loại file (PDF vs DOCX) | - Điều kiện: `{{ $json["mimeType"] === "application/pdf" }}` và `{{ $json["mimeType"] === "application/vnd.openxmlformats-officedocument.wordprocessingml.document" }}`. |
| **Google Drive** (Node “Create Template”) | Tạo Google Docs với placeholder | - **Operation**: `Create` <br> - **File Name**: `{{ $json["originalFileName"] }}_template` <br> - **Folder ID**: (điền ID thư mục lưu trữ). |
| **Respond To Webhook** | Trả về link tài liệu cho người gọi | - **Response Body**: `{ "templateUrl": "{{ $node["Google Drive"].json["webViewLink"] }}" }`. |
| **Sticky Note** | Ghi chú hướng dẫn (không ảnh hưởng workflow) | - Có thể bỏ qua hoặc để lại mô tả cho các bước. |

> **Lưu ý:** Mỗi node sử dụng **Credentials** phải được tạo trước trong n8n → Credentials. Đừng quên bật **OAuth consent screen** cho Google Drive để tránh lỗi “insufficient permissions”.

#### 3. Kích hoạt ⚡️
1. **Test run**: Gửi một file PDF/DOCX mẫu tới webhook (có thể dùng Postman hoặc curl).  
2. Kiểm tra log của các node, đặc biệt node **LM Chat OpenAI** và **Google Drive** để chắc chắn placeholder được tạo đúng.  
3. Khi mọi thứ ổn, bật **Active** ở góc phải của workflow.  

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack/Telegram**: Thêm node `Slack` hoặc `Telegram` để tự động gửi link template tới kênh làm việc.  
- **Lưu log chi tiết**: Dùng node `Write Binary File` để lưu bản sao PDF/DOCX và file text đã chuyển đổi vào một bucket S3 hoặc Google Cloud Storage.  
- **Báo cáo định kỳ**: Kết hợp `Cron` + `Google Sheets` để tổng hợp số lượng template đã tạo mỗi ngày/tuần.  
- **Tùy chỉnh Prompt**: Thêm các hướng dẫn chi tiết cho GPT‑4o (ví dụ: “Only extract fields that are likely to be filled by a user, ignore headings”).  

### 📌 Kết luận
Với workflow này, các sếp có thể **tự động hoá toàn bộ quy trình tạo mẫu tài liệu có thể điền** chỉ trong vài giây, giảm thiểu lỗi và tăng năng suất đội ngũ. Hãy triển khai ngay, kết nối webhook với hệ thống hiện tại và để n8n lo phần còn lại! 🚀