---
title: "🚀 Tự động phân loại & theo dõi email công ty bằng AI OpenRouter + Google Sheets"
description: "Workflow n8n tự động đọc email, dùng AI OpenRouter phân loại, lưu kết quả vào Google Sheets, giúp các sếp quản lý email nhanh chóng, chính xác và không cần viết code."
slug: "tu-dong-phan-loai-email-cong-ty-openrouter-google-sheets"
tags: [n8n, automation, no-code, AI, email, google-sheets]
keywords: [n8n workflow, tự động hóa, email classification, OpenRouter, Google Sheets, AI summarization]
---

# 🚀 Tự động phân loại & theo dõi email công ty bằng AI OpenRouter + Google Sheets

Các sếp thường phải **đọc hàng trăm email mỗi ngày**, lọc ra những yêu cầu quan trọng, gắn nhãn, rồi nhập thủ công vào bảng tính để theo dõi.  
Quá trình này tốn thời gian, dễ sai sót và không thể chạy 24/7.  

**Workflow này** sẽ:
- **Tự động đọc email** mới từ hộp thư IMAP.  
- **Gửi nội dung email** tới **OpenRouter AI** để phân loại (ví dụ: “Bảo trì”, “Yêu cầu hỗ trợ”, “Đề xuất”…).  
- **Lưu kết quả** (tiêu đề, người gửi, ngày, danh mục, nội dung tóm tắt) vào **Google Sheets**.  
- **Cập nhật số lần yêu cầu** cho mỗi danh mục, giúp các sếp nắm ngay khối lượng công việc.

> **Kết quả:** Tiết kiệm hàng giờ công mỗi tuần, giảm lỗi nhập liệu, và có báo cáo thời gian thực.

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm thời gian**: Không còn phải mở email, copy‑paste, nhập dữ liệu thủ công.  
- **Độ chính xác cao**: AI phân loại dựa trên ngữ cảnh, giảm lỗi gán nhãn sai.  
- **Theo dõi liên tục**: Google Sheets cập nhật ngay khi email mới đến, mọi người có thể xem real‑time.  
- **Dễ mở rộng**: Thêm Slack/Telegram thông báo, báo cáo định kỳ chỉ bằng vài node.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **Tài khoản IMAP** (Gmail, Outlook, ...). Cần `host`, `port`, `username`, `password`.  
- **Google Cloud Project** với **Google Sheets API** bật, tạo **OAuth2 credentials** (hoặc Service Account) và chia sẻ sheet cho tài khoản này.  
- **OpenRouter API key** (đăng ký tại https://openrouter.ai).  
- **Google Sheet** đã tạo sẵn với các cột: `Timestamp`, `From`, `Subject`, `Category`, `Summary`, `Request Count`.  
- **n8n** (cài đặt trên VPS hoặc n8n.cloud).  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON của workflow (đính kèm hoặc từ link gốc).  
2. Vào **n8n → Workflows → Import** → Chọn file JSON → **Import**.  
3. Hoặc mở **n8n Editor**, nhấn **+** → **Import from Clipboard**, dán toàn bộ JSON và **Save**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Cấu hình cần chỉnh | Ghi chú |
|------|-------------------|---------|
| **Email Trigger (IMAP)** | - **Credentials**: IMAP account <br> - **Mailbox**: `INBOX` (hoặc thư mục tùy chỉnh) <br> - **Search criteria**: `UNSEEN` để chỉ lấy email chưa đọc | Đảm bảo tài khoản có quyền IMAP. |
| **Get row(s) in sheet** | - **Credentials**: Google Sheets <br> - **Spreadsheet ID** <br> - **Sheet Name**: `Categories` (chứa danh sách danh mục) | Dùng để kiểm tra danh mục đã tồn tại chưa. |
| **AI Agent** | - **Credentials**: OpenRouter API Key <br> - **Model**: `meta-llama/llama-3.1-8b` (hoặc model bạn muốn) <br> - **Prompt**: “Phân loại email này vào một trong các danh mục: …” | Prompt có thể tùy chỉnh để phù hợp ngôn ngữ công ty. |
| **Find Category** (Google Sheets) | - **Spreadsheet ID** <br> - **Sheet Name**: `Categories` <br> - **Range**: `A:B` (Category ↔︎ Description) | Trả về ID danh mục nếu đã tồn tại. |
| **If** | - **Condition**: `{{ $json["categoryFound"] === true }}` (có danh mục) | Điều hướng luồng: **Có** → Cập nhật count, **Không** → Thêm mới. |
| **Edit Fields** (Set) | - **Fields**: `category`, `summary`, `requestCount` (đặt giá trị mặc định) | Định dạng dữ liệu trước khi ghi vào sheet. |
| **Update Request Count** (Google Sheets) | - **Spreadsheet ID** <br> - **Sheet Name**: `Categories` <br> - **Row ID**: từ node **Find Category** <br> - **Column**: `Request Count` → `+1` | Tăng số lần yêu cầu cho danh mục đã có. |
| **Append row in sheet** (Google Sheets) | - **Spreadsheet ID** <br> - **Sheet Name**: `Emails` <br> - **Values**: `Timestamp, From, Subject, Category, Summary, Request Count` | Lưu bản ghi email mới. |
| **oAI OSS** (lmChatOpenRouter) | - **Credentials**: OpenRouter API Key <br> - **Model**: cùng model ở **AI Agent** <br> - **Prompt**: “Hãy tóm tắt nội dung email và đưa ra danh mục phù hợp.” | Node này thực hiện **summarization + classification**. |
| **Category & Request** (outputParserStructured) | - **Schema**: `{ "category": "string", "summary": "string" }` | Trích xuất dữ liệu có cấu trúc từ phản hồi AI. |

> **⚠️ Lưu ý:** Sau khi cấu hình credentials, chạy **Test** từng node để chắc chắn nhận được dữ liệu mong muốn trước khi bật workflow.

#### 3. Kích hoạt ⚡️
1. Nhấn **Execute Workflow** với một email mẫu để kiểm tra toàn bộ luồng.  
2. Kiểm tra Google Sheet: có dòng mới, category được cập nhật đúng?  
3. Khi mọi thứ ổn, bật **Active** (nút chuyển đổi ở góc phải). Workflow sẽ tự động chạy mỗi khi email mới tới.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo Slack/Telegram**: Thêm node **Slack** hoặc **Telegram** sau node `Append row in sheet` để gửi tin nhắn “📧 Email mới được phân loại: *{{ $json.category }}*”.  
- **Lưu log chi tiết**: Dùng node **Write Binary File** để ghi toàn bộ payload vào file log trên server, giúp debug khi AI trả về kết quả không mong muốn.  
- **Báo cáo định kỳ**: Kết hợp node **Cron** + **Google Sheets → Get All** → **HTML Email** để gửi báo cáo tổng hợp số email mỗi danh mục mỗi tuần.  
- **Kiểm soát chi phí AI**: Thêm node **If** kiểm tra `{{ $json.tokensUsed > 500 }}` → gửi cảnh báo nếu tiêu thụ token quá cao.

### 📌 Kết luận
Với workflow **“Categorize and Track Company Emails with OpenRouter AI and Google Sheets”**, các sếp có thể **tự động hoá toàn bộ quy trình xử lý email** chỉ trong vài phút thiết lập, không cần viết một dòng code nào.  
Hãy **import ngay**, cấu hình các credentials, và để n8n làm việc cho bạn 24/7 – tiết kiệm thời gian, giảm lỗi và luôn có cái nhìn tổng quan về khối lượng công việc qua Google Sheets.  

**Áp dụng ngay hôm nay, các sếp sẽ thấy sự khác biệt!**