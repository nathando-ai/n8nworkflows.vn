---
title: "🚀 Tự động trích xuất tài liệu từ Dropbox bằng DocuPipe & gửi Slack"
description: "Workflow n8n tự động phát hiện file mới trên Dropbox, dùng AI DocuPipe trích xuất dữ liệu và đẩy kết quả ngay vào kênh Slack, giảm thời gian xử lý tài liệu."
slug: "trich-xuat-tai-lieu-dropbox-docupipe-slack"
tags: [n8n, automation, no-code, docupipe, dropbox, slack, ai]
keywords: [n8n workflow, tự động hóa, docupipe, dropbox, slack, trích xuất tài liệu]
---

# 🚀 Tự động trích xuất tài liệu từ Dropbox bằng DocuPipe & gửi Slack

Bạn đã bao giờ phải **mở từng file trên Dropbox, sao chép dữ liệu ra Excel, rồi thủ công nhập vào hệ thống**?  
Quá trình này tốn thời gian, dễ sai sót và khiến các sếp luôn lo lắng về độ chính xác của dữ liệu.  
Workflow này sẽ **tự động phát hiện file mới**, gửi chúng tới **DocuPipe AI** để trích xuất thông tin có cấu trúc, rồi **đẩy kết quả ngay vào Slack** – mọi thứ diễn ra 100 % không cần viết code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài phút/đơn sang chỉ vài giây tự động.  
- **Độ chính xác cao**: AI DocuPipe giảm lỗi nhập liệu thủ công.  
- **Cập nhật tức thời**: Kết quả được gửi ngay vào Slack, mọi người luôn nắm bắt.  
- **Hoạt động liên tục**: Workflow chạy mỗi phút, không bỏ sót tài liệu nào.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Dropbox** + **OAuth2 token** (được tạo trong n8n > Credentials > Dropbox OAuth2 API).  
- **Tài khoản DocuPipe** và **API Key** (trong DocuPipe > Settings > General).  
- **Workspace Slack** với **bot token** (OAuth2) và quyền `chat:write`.  
- **Schema trích xuất** đã cấu hình trong DocuPipe (ví dụ: “Invoice”, “Receipt”).  
- **n8n** (cài đặt self‑hosted hoặc cloud) với **Community Node** `n8n-nodes-docupipe` đã được cài.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. **Tải file JSON** của workflow (được cung cấp ở phần cuối).  
2. Vào n8n → **Workflows** → **Import** → Chọn file JSON → **Import**.  
   *Hoặc* copy toàn bộ JSON, vào **New Workflow**, nhấn **Import from Clipboard**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Cấu hình cần chỉnh | Ghi chú |
|------|-------------------|--------|
| **Check Every Minute** (`scheduleTrigger`) | Không cần thay đổi, chạy mỗi phút. | |
| **List Dropbox Folder** (`dropbox`) | - **Credentials**: `dropboxOAuth2Api` <br> - **Operation**: `list` <br> - **Resource**: `folder` <br> - **Folder Path**: Đường dẫn thư mục cần giám sát (ví dụ: `/Invoices`). | Đảm bảo tài khoản có quyền đọc thư mục. |
| **Filter New Files** (`if`) | Thiết lập **Condition** để chỉ cho phép file **mới** (ví dụ: `{{$json[".tag"] === "file" && $json["client_modified"] > $now.minus({ minutes: 2 }).toISO()}}`). | Điều kiện tùy thuộc vào cách bạn muốn xác định “mới”. |
| **Download File from Dropbox** (`dropbox`) | - **Operation**: `download` <br> - **Resource**: `file` <br> - **Path**: `={{ $json.path_display }}` (được lấy từ node trước). | |
| **Upload File & Extract Data** (`docuPipe`) | - **Credentials**: `docuPipeApi` <br> - **Operation**: `uploadAndExtract` <br> - **Resource**: `extraction` <br> - **File**: `{{$binaryData}}` (binary từ node download) <br> - **Schema ID**: Chọn schema đã tạo trên DocuPipe. | |
| **Extraction Complete** (`docuPipeTrigger`) | Không cần chỉnh, node này là webhook nhận thông báo hoàn thành từ DocuPipe. | Khi import, n8n sẽ tự tạo URL webhook; sao chép URL này vào **DocuPipe > Webhooks** nếu cần. |
| **Get Extracted Data** (`docuPipe`) | - **Operation**: `getResult` <br> - **Resource**: `extraction` <br> - **Extraction ID**: `={{ $json.id }}` (được trả về từ trigger). | |
| **Format Slack Message** (`code`) | Dán đoạn JavaScript dưới đây (đã chuẩn sẵn) để tạo tin nhắn dạng markdown: ```js\nconst data = $json;\nlet text = `*📄 Kết quả trích xuất:*\\n`;\nObject.entries(data).forEach(([key, value]) => {\n  text += `• *${key}*: ${value}\\n`;\n});\nreturn [{ json: { text } }];\n``` | Đảm bảo node trả về `json.text`. |
| **Set Channel & Message** (`set`) | - **Field** `channel`: ID hoặc tên kênh Slack (ví dụ: `#invoices`). <br> - **Field** `text`: `{{$node["Format Slack Message"].json["text"]}}`. | |
| **Post Results to Slack** (`slack`) | - **Credentials**: `slackOAuth2Api` <br> - **Channel**: `{{$json["channel"]}}` <br> - **Message**: `{{$json["text"]}}`. | Kiểm tra bot đã được mời vào kênh. |

#### 3. Kích hoạt ⚡️
1. **Test run**: Chọn **Execute Workflow** → **Run Once** → Đặt một file mẫu vào thư mục Dropbox đã chỉ định.  
2. Kiểm tra **Logs** của các node để chắc chắn dữ liệu được tải, trích xuất và gửi Slack thành công.  
3. Khi mọi thứ ổn, bật **Active** (nút chuyển đổi ở góc trên bên phải) để workflow chạy liên tục.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm bước lưu log**: Dùng node **Google Sheets** hoặc **Airtable** để ghi lại mỗi lần trích xuất, giúp audit và phân tích.  
- **Thông báo đa kênh**: Sao chép node Slack, thay đổi `channel` để gửi cùng một tin nhắn tới **Telegram** hoặc **Microsoft Teams**.  
- **Xử lý lỗi**: Thêm node **IF** sau `Upload File & Extract Data` để kiểm tra `statusCode` và gửi cảnh báo lỗi qua Slack nếu có.  
- **Tự động xóa file**: Sau khi trích xuất thành công, dùng node **Dropbox → Delete** để dọn dẹp thư mục nguồn, tránh trùng lặp.  

### 📌 Kết luận
Với workflow này, các sếp có thể **tự động hoá toàn bộ quy trình thu thập, trích xuất và báo cáo dữ liệu tài liệu** chỉ trong vài giây, giảm tải công việc thủ công và tăng độ tin cậy. Hãy **import ngay**, cấu hình các credentials và để n8n làm việc cho bạn! 🚀