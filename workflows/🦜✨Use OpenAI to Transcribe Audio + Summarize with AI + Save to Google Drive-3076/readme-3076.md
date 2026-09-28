---
title: "🚀 Tự động chuyển đổi âm thanh thành văn bản, tóm tắt AI và lưu vào Google Drive"
description: "Workflow tự động lấy file âm thanh từ Google Drive, chuyển đổi sang văn bản bằng OpenAI Whisper, tạo báo cáo tóm tắt JSON và Markdown, sau đó lưu lại vào Google Drive và thông báo qua Gmail/Telegram."
slug: "tu-dong-chuyen-doi-am-thanh-thanh-van-ban-tom-tat-ai-google-drive"
tags: [n8n, automation, no-code, OpenAI, Google Drive, Gmail, Telegram, AI transcription]
keywords: [n8n workflow, tự động hóa, OpenAI Whisper, Google Drive, Gmail, Telegram, AI transcription, tóm tắt văn bản]
---

# 🚀 Tự động chuyển đổi âm thanh thành văn bản, tóm tắt AI và lưu vào Google Drive

Nhiều đội ngũ marketing, đào tạo hoặc hỗ trợ khách hàng thường phải xử lý hàng giờ bản ghi âm (phỏng vấn, webinar, cuộc gọi) rồi manually upload lên Google Drive, dùng công cụ ngoài để chuyển đổi sang text, sau đó tóm tắt và lưu lại. Quy trình này tốn thời gian, dễ xảy ra lỗi và thiếu tính nhất quán.  

Workflow **🦜✨Use OpenAI to Transcribe Audio + Summarize with AI + Save to Google Drive** giải quyết triệt để bài toán bằng cách tự động hoá toàn bộ luồng: từ khi một file âm thanh xuất hiện trong Google Drive → chuyển đổi sang văn bản bằng OpenAI Whisper → tạo báo cáo tóm tắt có cấu trúc (JSON & Markdown) → lưu tất cả các file kết quả lại vào Google Drive và thông báo cho người dùng qua Gmail hoặc Telegram. Tất cả đều chạy 100% trên n8n, không cần viết một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm giờ công**: Quy trình từ âm thanh → transcript → tóm tắt hoàn toàn tự động, giảm thiểu công việc thủ công lên tới 90%.
- **Chính xác cao**: Sử dụng mô hình Whisper của OpenAI để chuyển đổi âm thanh với độ chính xác ngành công nghiệp.
- **Báo cáo đa dạng**: Nhận đồng thời file transcript thô, báo cáo JSON có cấu trúc và bản Markdown dễ đọc.
- **Thông báo即时**: Gmail và Telegram thông báo ngay khi xử lý xong, kèm link trực tiếp tới file trên Google Drive.
- **Lưu trữ tập trung**: Tất cả kết quả được lưu tự động vào thư mục Google Drive đã chỉ định, dễ dàng tìm kiếm và lưu trữ lâu dài.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Google Drive** và **OAuth2 credential** (`googleDriveOAuth2Api`) để truy cập thư mục nguồn và lưu kết quả.
- **Tài khoản OpenAI** với API key (`openAiApi`) để sử dụng Whisper (transcribe) và các mô hình GPT cho tóm tắt/định dạng.
- **Tài khoản Gmail** (`gmailOAuth2`) để gửi email yêu cầu duyệt (human‑in‑the‑loop) và gửi kết quả cuối cùng.
- **Tài khoản Telegram** (`telegramApi`) để gửi tin nhắn thông báo (tùy chọn).
- **Thư mục Google Drive** chứa file âm thanh cần xử lý (định dạng .m4a được đề xuất, nhưng có thể thay đổi trong node Filter).
- Quyền truy cập để **tạo, đọc, cập nhật file** trong Google Drive (cả file text và nhị phân).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Sao chép toàn bộ JSON workflow từ trang n8n.io (nút **Export** → **Copy to Clipboard**) hoặc tải file JSON về.
2. Trong n8n Editor, chọn **Import** → **Upload file** hoặc **Paste** JSON vào ô nhập.
3. Nhấn **Import** – workflow sẽ xuất hiện với tên **🦜✨Use OpenAI to Transcribe Audio + Summarize with AI + Save to Google Drive**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần kiểm tra và cấu hình các node sau:

| Node | Cấu hình bắt buộc | Ghi chú |
|------|-------------------|---------|
| **Gmail User for Approval** | Chọn credential `gmailOAuth2`. Trong trường **Operation** chọn **Send And Wait**. Điền **To** (email người duyệt), **Subject** (ví dụ: “Xác nhận xử lý file âm thanh”), **Body** (có thể dùng biểu thức `{{ $json["fileName"] }}` để đưa tên file vào). | Node này tạo luồng Human‑in‑the‑Loop: workflow sẽ dừng tại đây cho tới khi người dùng trả lời email (phản hồi có chứa “approved” hoặc từ khóa bạn định). |
| **Set Config** | Thiết lập các biến toàn cục như `targetFolderId` (ID thư mục Google Drive nơi lưu kết quả), `allowedExtensions` (mặc định `.m4a`). | Bạn có thể thay đổi `targetFolderId` để lưu vào thư mục khác. |
| **Transcribe with OpenAI** | Chọn credential `openAiApi`. **Operation** = **Transcribe**, **Resource** = **Audio**. Trong trường **File Binary Data**, chọn output từ node **Download audio file** (thường là `binary`). | Đảm bảo mô hình được chọn là `whisper-1` (mặc định). |
| **Filter by .m4a extension** | Trong **Filter**, thiết lập điều kiện: `{{ $json["name"] }} ends with ".m4a"` (hoặc thay đổi extension nếu bạn dùng định dạng khác). | Node này chỉ cho qua file có phần mở rộng đúng; nếu bạn muốn xử lý nhiều loại, sửa điều kiện hoặc bỏ node này. |
| **Limit to last file** | Đặt **Limit** = **1** (giữ lại file mới nhất). | Nếu muốn xử lý batch, tăng limit hoặc bỏ node này. |
| **Download audio file** | Credential `googleDriveOAuth2Api`. **Operation** = **Download**. Chọn **File ID** từ output của node **Search Google Drive** (hoặc từ trigger nếu bắt đầu từ Google Drive Trigger). | Đảm bảo bạn đã chọn đúng trường chứa ID file. |
| **Search Google Drive** | Credential `googleDriveOAuth2Api`. **Resource** = **File/Folder**. Đặt **Query** để tìm file trong thư mục nguồn (ví dụ: `name contains ".m4a" and trashed = false`). | Điều chỉnh query nếu thư mục nguồn khác. |
| **Send Telegram Message** | Credential `telegramApi`. Điền **Chat ID** (có thể lấy từ bot) và **Text** (ví dụ: `🎧 File {{ $json["fileName"] }} đã được xử lý. Xem kết quả: {{ $json["driveLink"] }}`). | Tùy chọn – nếu không muốn thông báo qua Telegram, có thể disconnect node này. |
| **Send Gmail Message** | Credential `gmailOAuth2`. **Operation** = **Send Email**. Điền **To**, **Subject** (ex: “Kết quả xử lý âm thanh”), **HTML/Text** có thể dùng biểu thức để chèn link tới file JSON và Markdown. | Node này gửi báo cáo cuối cùng sau khi tất cả các đường xử lý hợp nhất. |
| **Email Content Formatter** | Credential `openAiApi`. Không cần thay đổi operation (mặc định là **Prompt**). Điền prompt để định dạng nội dung email (ví dụ: “Tóm tắt ngắn gọn về transcript sau đây: {{ $json[\"transcript\"] }}”). | Bạn có thể chỉnh prompt để thay đổi phong cách email. |
| **Summarize to Structured JSON** | Credential `openAiApi`. Prompt yêu cầu AI trả về JSON có các trường như `summary`, `keyPoints`, `actionItems`. | Đảm bảo JSON hợp lệ (n8n sẽ tự động parse nếu output là chuỗi JSON). |
| **Summarize to JSON** | Credential `openAiApi`. Tương tự node trên nhưng có thể dùng prompt khác nếu muốn định dạng khác. | Giữ riêng nếu cần hai phiên bản tóm tắt. |
| **Convert JSON to Markdown** | Credential `openAiApi`. Prompt: “Chuyển JSON sau thành báo cáo Markdown đẹp, có tiêu đề, danh sách và mã code nếu cần: {{ $json }}”. | Output sẽ là chuỗi Markdown. |
| **Get Filename for JSON** | Node **Set**. Thiết lập trường `jsonFileName` = `{{ $json["fileName"] }}.json`. | Đặt tên file JSON sẽ lưu. |
| **Get Filename for Markdown** | Node **Set**. Thiết lập trường `markdownFileName` = `{{ $json["fileName"] }}.md`. | Đặt tên file Markdown sẽ lưu. |
| **Save JSON file to Google Drive** | Credential `googleDriveOAuth2Api`. **Operation** = **Create From Text**. **File Name** = lấy từ node **Get Filename for JSON**. **Data** = output từ node **Summarize to JSON** (chuỗi JSON). **Folder ID** = `targetFolderId` (từ Set Config). | Lưu file JSON kết quả. |
| **Save Markdown file to Google Drive** | Tương tự, **Operation** = **Create From Text**, **File Name** từ **Get Filename for Markdown**, **Data** từ node **Convert JSON to Markdown**. | Lưu file Markdown. |
| **Get JSON File Meta** | Credential `googleDriveOAuth2Api`. **Resource** = **File/Folder**. Lấy **File ID** từ output node **Save JSON file to Google Drive** để lấy link condivise. | Dùng để tạo link sharing. |
| **Get Markdown File Meta** | Tương tự lấy meta cho file Markdown. |
| **Prepare Response JSON** | Node **Set**. Tạo đối tượng response bao gồm `jsonLink` (từ Get JSON File Meta), `markdownLink` (từ Get Markdown File Meta), `transcript` (từ node Transcribe with OpenAI). | Dùng để gửi trong email/Telegram. |
| **Prepare Response Markdown** | Node **Set**. Tạo chuỗi Markdown tóm tắt kết quả kèm link. |
| **Merge All Paths** | Node **Merge** (mode: **Append**). Đảm bảo tất cả các nhánh xử lý (JSON, Markdown, transcript raw) đều hội tụ vào đây trước khi gửi thông báo. |
| **Save Raw Transcript to Google Drive** | Credential `googleDriveOAuth2Api`. **Operation** = **Create From Text**. **File Name** = `{{ $json["fileName"] }}_transcript.txt`. **Data** = output từ node **Transcribe with OpenAI** (plain text). **Folder ID** = `targetFolderId`. | Lưu bản transcript thô để lưu trữ hoặc audit. |
| **Start Workflow** | Node **manualTrigger**. Cho phép chạy thử tay khi cần. |
| **On File Created Trigger** | Credential `googleDriveOAuth2Api**. Trigger khi file mới xuất hiện trong thư mục nguồn (được chỉ định trong node). Để bật tự động, hãy aktif workflow và để node này ở trạng thái **Active**. | Đây là điểm khởi động chính khi làm việc tự động. |

> **Lưu ý quan trọng**: Sau khi chỉnh các credential, hãy nhấn **Save** trên mỗi node rồi **Activate** workflow (góc trên bên phải). Để kiểm tra, bạn có thể upload một file .m4a test vào thư mục nguồn và quan sát workflow chạy qua từng bước.

#### 3. Kích hoạt ⚡️
- Sau khi cấu hình xong, nhấn **Activate Workflow**.
- Upload một file âm thanh mẫu (định dạng .m4a) vào thư mục Google Drive mà node **On File Created Trigger** đang lắng nghe.
- Quan sát Execution List: workflow sẽ dừng tại node **Gmail User for Approval** cho tới khi bạn trả lời email (ví dụ: trả