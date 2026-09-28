---
title: "🚀 Phân loại Email & Trích xuất Dữ liệu Ứng tuyển với GPT‑4o"
description: "Tự động phân loại email tuyển dụng và trích xuất thông tin cấu trúc từ CV PDF bằng GPT‑4o, giảm 90% thời gian xử lý hồ sơ."
slug: "phan-loai-email-trich-xuat-du-lieu-ung-tuyen-gpt4o"
tags: [n8n, automation, no-code, HR, AI]
keywords: [n8n workflow, tự động hóa, email classification, data extraction, GPT-4o, tuyển dụng]
---

# 🚀 Phân loại Email & Trích xuất Dữ liệu Ứng tuyển với GPT‑4o

Doanh nghiệp hiện đang phải **đối mặt với hàng trăm email ứng tuyển** mỗi ngày: đọc, phân loại, mở file CV, trích xuất thông tin cá nhân, kỹ năng… Tất cả đều **tiêu tốn thời gian và dễ gây sai sót**.  
Workflow này sẽ **tự động đọc email**, **phân loại** (ví dụ: “Ứng tuyển”, “Spam”, “Hỏi đáp”), **tải file đính kèm PDF**, và **trích xuất dữ liệu cấu trúc** (Tên, Email, Số điện thoại, Kỹ năng…) chỉ bằng **GPT‑4o** – không cần viết một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm 90% thời gian** so với xử lý thủ công.  
- **Độ chính xác cao** nhờ mô hình GPT‑4o phân loại và trích xuất.  
- **Dữ liệu chuẩn** (JSON) sẵn sàng nhập vào hệ thống HR (ATS, Google Sheet…).  
- **Hoạt động liên tục** 24/7, không bỏ lỡ bất kỳ email nào.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **Tài khoản IMAP** (Gmail, Outlook, hoặc máy chủ mail nội bộ) – để n8n đọc email.  
- **API Key OpenAI** (có quyền truy cập GPT‑4o).  
- **Quyền truy cập thư mục lưu file PDF** (n8n server cần có quyền ghi/đọc).  
- (Tùy chọn) **Công cụ lưu trữ dữ liệu** (Google Sheet, Airtable…) nếu muốn mở rộng.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập **n8n → Workflows → Import**.  
2. Tải file JSON của workflow (tải từ [link gốc](https://n8n.io/workflows/3457) hoặc sao chép nội dung JSON).  
3. Nhấn **Import** → Workflow sẽ xuất hiện trên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Dưới đây là **các node quan trọng** và cách cấu hình chi tiết:

| Node | Loại | Hướng dẫn cấu hình |
|------|------|-------------------|
| **Email trigger** | `emailReadImap` | - Chọn **Credentials → imap** (điền host, port, email, password). <br> - Thiết lập **Mailbox** (thường là `INBOX`). <br> - **Search Criteria**: `UNSEEN FROM "jobs@yourcompany.com"` hoặc tùy chỉnh. |
| **Classify email** | `textClassifier` (LangChain) | - Chọn **Model**: `gpt-4o`. <br> - **Prompt**: “Phân loại email này thành một trong các danh mục: 1️⃣ Ứng tuyển, 2️⃣ Spam, 3️⃣ Hỏi đáp, 4️⃣ Khác.” <br> - Đầu vào: `{{$json["subject"]}}` + `{{$json["body"]}}`. |
| **Extract variables - email & attachment** | `informationExtractor` (LangChain) | - Định nghĩa **Variables**: `email_from`, `email_subject`, `attachment_url`. <br> - Sử dụng **JSON Path** để lấy giá trị từ node **Email trigger**. |
| **Extract data from attachment** | `extractFromFile` (PDF) | - **Operation**: `pdf`. <br> - **File URL**: `{{$json["attachment_url"]}}`. <br> - Kết quả: `raw_text`. |
| **OpenAI Chat Model** (đầu tiên) | `lmChatOpenAi` | - **Credentials**: `openAiApi`. <br> - **Model**: `gpt-4o`. <br> - **Prompt**: “Từ đoạn văn bản CV dưới đây, trích xuất các trường: Họ và tên, Email, Số điện thoại, Kỹ năng chính, Kinh nghiệm làm việc.” <br> - Đầu vào: `{{$node["Extract data from attachment"].json["raw_text"]}}`. |
| **OpenAI Chat Model 2** (thứ hai) | `lmChatOpenAi` | - Dùng để **tóm tắt** nội dung CV hoặc **đánh giá mức độ phù hợp** với vị trí. <br> - Prompt mẫu: “Tóm tắt ngắn gọn (≤ 3 câu) về kinh nghiệm và kỹ năng của ứng viên này.” |
| **Workflow 2**, **Workflow 3**, **workflow 4** | `noOp` | Các node này là **placeholder**. Bạn có thể kéo chúng vào để **gửi dữ liệu tới Slack, Google Sheet, hoặc hệ thống ATS**. Đừng quên **kết nối** output của OpenAI Chat Model tới các node này. |

> **Lưu ý:** Sau khi cấu hình xong, **đừng quên bật “Execute Workflow”** để kiểm tra kết quả mẫu. Nếu có lỗi, kiểm tra lại **định dạng JSON Path** và **quyền truy cập file**.

#### 3. Kích hoạt ⚡️
1. **Test run** với một email mẫu (có file PDF đính kèm).  
2. Kiểm tra **output** của node “OpenAI Chat Model” – kết quả phải là JSON chứa các trường đã định nghĩa.  
3. Khi mọi thứ ổn, **bật “Active”** (Toggle ở góc phải) để workflow tự động chạy liên tục.

### ✍️ Mẹo & gợi ý nâng cao
- **Gửi thông báo Slack/Telegram**: Thêm node `Slack` hoặc `Telegram` sau “OpenAI Chat Model 2” để báo cho bộ phận tuyển dụng ngay khi có ứng viên phù hợp.  
- **Lưu trữ vào Google Sheet**: Dùng node `Google Sheets` để ghi mỗi hồ sơ thành một hàng, dễ dàng lọc và phân tích.  
- **Tự động tạo ticket** trong hệ thống ATS (Jira, Trello) bằng node `HTTP Request`.  
- **Lưu log**: Kết nối một node `Write Binary File` để lưu bản sao email và PDF vào S3/Drive cho mục đích audit.

### 📌 Kết luận
Với workflow **“Classify Emails & Extract Structured Data from Job Applications with GPT‑4o”**, các sếp có thể **tự động hoá toàn bộ quy trình nhận hồ sơ**, giảm tải công việc lặp đi lặp lại, đồng thời **đảm bảo dữ liệu chuẩn, nhanh chóng và chính xác**. Hãy **import ngay**, cấu hình các credentials và để n8n làm việc thay bạn – thời gian tuyển dụng sẽ nhanh hơn, chất lượng hồ sơ sẽ được nâng cao! 🚀