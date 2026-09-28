---
title: "🚀 Tự động hoá xử lý hóa đơn với Mistral OCR + GPT-4o-mini"
description: "Workflow tự động tải hóa đơn từ Google Drive, trích xuất văn bản bằng Mistral OCR, phân tích và cấu trúc dữ liệu hóa đơn bằng GPT-4o-mini, giúp doanh nghiệp tiết kiệm giờ công và giảm lỗi nhập liệu."
slug: "tu-dong-hoa-xu-ly-hoa-don-mistral-ocr-gpt4o-mini"
tags: [n8n, automation, no-code, AI, OCR, Google Drive, GPT-4o-mini, Mistral, Finance]
keywords: [n8n workflow, tự động hóa hóa đơn, Mistral OCR, GPT-4o-mini, trích xuất dữ liệu, Google Drive automation]
---

# 🚀 Tự động hoá xử lý hóa đơn với Mistral OCR + GPT-4o-mini

Nhiều doanh nghiệp vẫn phải xử lý hàng trăm hóa đơn mỗi tuần bằng cách tải file, sao chép văn bản vào bảng tính hoặc hệ thống kế toán – một công việc tốn thời gian, dễ sai sót và không thể mở rộng. Workflow **Automated Invoice Processing with Mistral OCR + GPT-4o-mini** thay đổi hoàn toàn quy trình này: từ khi một file hóa đơn mới xuất hiện trong Google Drive, hệ thống sẽ tự động tải xuống, trích xuất văn bản bằng Mistral OCR, sau đó sử dụng GPT-4o-mini để hiểu nội dung và xuất ra dữ liệu có cấu trúc (JSON) sẵn sàng để nhập vào ERP, Google Sheets hoặc bất kỳ hệ thống nào bạn muốn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm đến 80% thời gian** so với xử lý thủ công: từ vài phút xuống dưới 30 giây mỗi hóa đơn.
- **Độ chính xác cao**: Mistral OCR đạt >95% độ chính xác trên văn bản in, GPT-4o-mini giúp sửa lỗi và hiểu bối cảnh.
- **Dữ liệu sẵn sàng tích hợp**: JSON đầu ra có thể gửi trực tiếp tới Google Sheets, API kế toán hoặc hệ thống ERP qua webhook.
- **Hoạt động liên tục**: Trigger dựa trên Google Drive đảm bảo không bỏ lỡ bất kỳ file nào mới.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Google Drive** có quyền truy cập tới thư mục chứa hóa đơn (cần kết nối qua node Google Drive).
- **API Key Mistral OCR** (đăng ký tại [Mistral AI](https://mistral.ai/) và thêm vào Credentials typu “HTTP Request”).
- **API Key OpenAI** để sử dụng model `gpt-4o-mini` (thêm vào Credentials typu “OpenAI Chat Model”).
- (Tùy chọn) **Credentials cho đích xuất dữ liệu** như Google Sheets, Slack, Email… nếu bạn muốn mở rộng workflow sau bước parser.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Sao chép toàn bộ JSON workflow từ trang gốc (https://n8n.io/workflows/4331) hoặc tải file `.json` về.
2. Trong n8n Editor, chọn **Import** → **Upload file** hoặc dán JSON vào ô **Paste** → nhấn **Import**.
3. Workflow sẽ xuất hiện với tên **🧾 Automated Invoice Processing with Mistral OCR + GPT-4o-mini**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, bạn cần cấu hình các node sau để phù hợp với môi trường của mình:

| Node (tên chính xác) | Loại | Cần cấu hình |
|----------------------|------|--------------|
| **Google Drive Trigger: New Invoice Detection** | `googleDriveTrigger` | - Chọn **Folder** nơi bạn đặt hóa đơn mới.<br>- Đặt **Polling Interval** (ví dụ: 5 phút). |
| **Google Drive: Download Invoice** | `googleDrive` | - Chọn **Credential** Google Drive đã chuẩn bị.<br>- Đảm bảo **File ID** được lấy từ output của Trigger (node tự động map). |
| **Mistral OCR API: Extract Text** | `httpRequest` | - **Method**: `POST`.<br>- **URL**: `https://api.mistral.ai/v1/ocr` (hoặc endpoint mà bạn đã đăng ký).<br>- **Headers**: `Authorization: Bearer <YOUR_MISTRAL_API_KEY>`<br>- **Body**: gửi file binary từ node trước (thường là `{{ $binary.pdf }}` hoặc `{{ $binary.image }}`). |
| **Data Splitter: OCR Pages** | `splitOut` | - Chọn trường chứa kết quả OCR (thường là `text` hoặc `pages`).<br>- Đặt **Split By** thành `item` nếu mỗi trang là một phần tử. |
| **Field Extractor: Page Markdown** | `set` | - Tạo trường `page_markdown` = `{{ $json.text }}` (hoặc trường tương ứng từ OCR). |
| **Data Aggregator: Combine Pages** | `summarize` | - Chọn **Group By** để không nhóm (trang xử lý độc lập) hoặc để hợp nhất tất cả trang thành một chuỗi.<br>- Chọn **Concatenate** với dấu `\n\n` để tạo một văn bản đầy đủ. |
| **AI Agent: Structure Invoice Data** | `agent` | - Đặt **Tools** nếu muốn (ví dụ: công cụ tìm kiếm, nhưng thường không cần).<br>- Đảm bảo node này kết nối tới **AI Engine: GPT-4o-mini** làm model ngôn ngữ. |
| **AI Engine: GPT-4o-mini** | `lmChatOpenAi` | - Chọn **Credential** OpenAI API Key.<br>- Model: `gpt-4o-mini`.<br>- Temperature: `0.2` (để kết quả ổn định). |
| **JSON Parser: Invoice Structure** | `outputParserStructured` | - Định nghĩa **Schema** JSON mong muốn (ví dụ: `{ "invoice_number": "string", "date": "string", "total_amount": "number", "line_items": [{ "description": "string", "quantity": "number", "unit_price": "number" }] }`).<br>- Đảm bảo prompt trước node Agent yêu cầu trả về JSON đúng schema này. |
| **Convert invoice File to Base64** | `extractFromFile` | - Nếu bạn cần gửi file gốc tới một dịch vụ khác (ví dụ: lưu trữ hoặc gửi qua email), cấu hình node này để lấy file binary từ node **Google Drive: Download Invoice** và xuất ra Base64 string. |

> **Lưu ý quan trọng**: Sau khi thay đổi credentials hoặc endpoint, hãy nhấn **Save** trên mỗi node rồi thực hiện **Test Workflow** với một file hóa đơn mẫu để đảm bảo dữ liệu truyền qua các node đúng định dạng.

#### 3. Kích hoạt ⚡️
1. Chọn một file hóa đơn PDF hoặc ảnh mẫu, upload vào thư mục Google Drive bạn đã chỉ định ở Trigger.
2. Nhấn **Execute Workflow** (nút **Test Workflow**) để xem từng bước chạy.
3. Kiểm tra output của node **JSON Parser: Invoice Structure** – bạn nên thấy một đối tượng JSON đầy đủ các trường hóa đơn.
4. Nếu mọi thứ ổn, bật công tắc **Active** ở góc trên bên phải workflow để nó chạy tự động khi có file mới.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo Slack/Telegram**: Thêm node **Slack** hoặc **Telegram** sau JSON Parser để gửi thông báo khi có hóa đơn mới được xử lý kèm link tới file gốc và tóm tắt JSON.
- **Lưu trữ file đã xử lý**: Sau bước parser, dùng node **Google Drive** để di chuyển file vào thư mục “Processed” hoặc “Archive” để tránh xử lý lại.
- **Đẩy dữ liệu vào Google Sheets**: Sử dụng node **Google Sheets** để thêm mỗi hóa đơn như một hàng mới, giúp equipe kế toán xem và đối soát dễ dàng.
- **Gửi email tóm tắt hàng ngày**: Kết hợp node **Cron** (trigger mỗi sáng) với **HTTP Request** tới API nội bộ để tổng hợp tất cả hóa đơn trong ngày và gửi qua **Email Send**.
- **Thêm bước xác thực**: Nếu cần, chèn node **IF** sau JSON Parser để kiểm tra trường `total_amount` có vượt ngưỡng nhất định không; nếu có, tự động tạo task trong Asana/Trello để nhân viên kiểm tra thủ công.

### 📌 Kết luận
Workflow **Automated Invoice Processing with Mistral OCR + GPT-4o-mini** biến việc xử lý hóa đơn từ một công việc thủ công tốn thời gian thành một quy trình hoàn toàn tự động, chính xác và dễ mở rộng. Với chỉ một few clicks để cấu hình credentials và một lần import, các sếp có thể ngay lập tức tiết kiệm hàng giờ mỗi tuần, giảm lỗi nhập liệu và tập trung vào các hoạt động chiến lược hơn. Hãy áp dụng ngay hôm nay và trải nghiệm sức mạnh của AI + OCR trong tài chính!