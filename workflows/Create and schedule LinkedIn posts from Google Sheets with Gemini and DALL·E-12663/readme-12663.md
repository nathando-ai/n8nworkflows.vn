---
title: "🚀 Tự động tạo & lên lịch bài đăng LinkedIn từ Google Sheets với Gemini & DALL·E"
description: "Tự động lấy nội dung từ Google Sheets, sinh văn bản bằng Gemini, tạo hình ảnh DALL·E và đăng lên LinkedIn theo lịch định sẵn, không cần viết mã."
slug: "tao-bai-dang-linkedin-tu-google-sheets-voi-gemini-dalle"
tags: [n8n, automation, no-code, social-media, AI, LinkedIn, GoogleSheets]
keywords: [n8n workflow, tự động hóa, LinkedIn, Google Sheets, AI content generation, Gemini, DALL·E]
---

# 🚀 Tự động tạo & lên lịch bài đăng LinkedIn từ Google Sheets với Gemini & DALL·E

Bạn đã từng tốn hàng giờ đồng hồ để **copy‑paste** nội dung từ bảng tính, viết lại caption, tạo hình ảnh và cuối cùng mới đăng lên LinkedIn?  
Công việc này không chỉ mất thời gian mà còn dễ gây lỗi, không đồng nhất và **không thể mở rộng** khi số lượng bài đăng tăng lên.

**Workflow** này giải quyết toàn bộ quy trình:  
1️⃣ Lấy dữ liệu (tiêu đề, mô tả, hashtag…) từ **Google Sheets**.  
2️⃣ Dùng **Gemini** (LLM) để “tinh chỉnh” caption, tạo nội dung chuẩn SEO.  
3️⃣ Gọi **DALL·E** để tạo hình ảnh minh họa độc đáo.  
4️⃣ Đăng bài lên **LinkedIn** theo lịch đã định, tự động đánh dấu trạng thái đã đăng trong Sheet.  

Kết quả: **tự động 100%**, không cần viết code, giảm 80% thời gian soạn nội dung và luôn duy trì lịch đăng đều đặn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài phút/ bài xuống < 30 giây.  
- **Độ chính xác cao**: Caption và hình ảnh luôn đồng nhất, không còn lỗi copy‑paste.  
- **Cá nhân hoá nội dung**: Gemini tự động chèn tên công ty, CTA, hashtag phù hợp.  
- **Hoạt động liên tục**: Đăng bài theo lịch hằng ngày/tuần mà không cần can thiệp.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Google** với quyền **Google Sheets API** (OAuth2 hoặc Service Account).  
- **Google Sheet** chứa các cột: `Title`, `Description`, `Hashtags`, `Status` (đánh dấu “Posted”).  
- **API Key** của **Google Gemini** (hoặc OpenAI nếu dùng model Gemini‑compatible).  
- **API Key** của **OpenAI DALL·E** (image generation).  
- **LinkedIn Developer App** → **Client ID**, **Client Secret**, **Access Token** (được cấp quyền `r_liteprofile`, `w_member_social`).  
- **n8n** đã cài đặt các credentials trên (Google OAuth2, OpenAI, LinkedIn).  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Vào **n8n → Workflows → Import**.  
2. Tải file `linkedin-from-sheets.json` (được đính kèm trong phần **Resources**) hoặc **Copy/Paste** toàn bộ JSON vào ô **Import from Clipboard**.  
3. Nhấn **Import** → Workflow sẽ xuất hiện trong danh sách.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Vai trò | Cấu hình quan trọng cần chỉnh |
|------|---------|--------------------------------|
| **Schedule Trigger** | Kích hoạt workflow theo lịch (ví dụ: mỗi ngày 09:00). | Chọn **Cron** → `0 9 * * *` (hàng ngày 9h sáng). |
| **Google Sheets Trigger** | Kiểm tra thay đổi mới trong Sheet (tùy chọn). | Chọn **Spreadsheet ID**, **Worksheet Name**, **Trigger Column** (`Status`). |
| **Google Sheets (Read)** | Đọc các hàng chưa được đăng (`Status` = “Pending”). | Spreadsheet ID, Sheet Name, **Range**: `A2:E`. |
| **Split In Batches** | Xử lý từng hàng một để tránh rate‑limit. | Batch Size: `1`. |
| **If** | Kiểm tra `Status` có phải “Pending” không. | Condition: `{{$json["Status"]}}` **equals** `Pending`. |
| **Chain LLM (Gemini)** | Sinh caption dựa trên `Title` + `Description`. | Model: `gemini-pro` (hoặc `gpt‑4o`), **Prompt**: <br>```\nBạn là chuyên gia marketing. Viết một caption LinkedIn ngắn gọn, hấp dẫn, có CTA, dựa trên tiêu đề: "{{ $json["Title"] }}" và mô tả: "{{ $json["Description"] }}".\n``` |
| **OpenAI Image Generation (DALL·E)** | Tạo hình ảnh minh họa cho bài đăng. | Model: `dall-e-3`, **Prompt**: `{{ $json["Title"] }}` + “LinkedIn post illustration, professional, vibrant”. |
| **Upload Post (LinkedIn)** | Đăng bài lên LinkedIn kèm ảnh. | **Credentials**: LinkedIn OAuth2, **Content**: `{{ $node["Chain LLM"].json["text"] }}`, **Image URL**: `{{ $node["OpenAI Image Generation"].json["url"] }}`. |
| **Google Sheets (Update)** | Cập nhật cột `Status` thành “Posted”. | Spreadsheet ID, Sheet Name, **Row ID**: `{{$json["RowId"]}}`, **Values**: `{ "Status": "Posted" }`. |
| **NoOp / StickyNote** | Ghi chú, debug (không ảnh hưởng). | Không cần cấu hình. |

> **Lưu ý:**  
> - Đảm bảo **Credentials** được gán đúng cho mỗi node (Google, OpenAI, LinkedIn).  
> - Kiểm tra **quota** của Gemini và DALL·E để tránh bị giới hạn khi chạy hàng loạt.  
> - Nếu muốn **đánh dấu ngày đăng** trong Sheet, thêm cột `PostedAt` và cập nhật giá trị `{{ $now }}` trong node **Google Sheets (Update)**.

#### 3. Kích hoạt ⚡️
1. Nhấn **Execute Workflow** lần đầu với dữ liệu mẫu để kiểm tra.  
2. Kiểm tra LinkedIn: bài viết đã xuất hiện chưa, hình ảnh đúng không.  
3. Khi mọi thứ ổn, bật **Active** (nút chuyển đổi ở góc trên bên phải). Workflow sẽ tự động chạy theo lịch đã định.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp Slack/Telegram**: Thêm node **Slack** hoặc **Telegram** để gửi thông báo “Bài đăng đã lên LinkedIn” cho team.  
- **Lưu log chi tiết**: Dùng node **HTTP Request** gửi dữ liệu tới Google Cloud Logging hoặc một Google Sheet “Log”.  
- **Báo cáo định kỳ**: Thêm **Schedule Trigger** (hàng tuần) + **Google Sheets** để tổng hợp số lượng bài đã đăng, tương tác, và gửi email báo cáo.  
- **A/B Testing**: Tạo 2 phiên bản caption (đổi Prompt) và dùng node **If** để ngẫu nhiên chọn một trong hai trước khi đăng.  

### 📌 Kết luận
Với workflow này, các sếp có thể **tự động hoá toàn bộ quy trình tạo nội dung LinkedIn** chỉ bằng một Google Sheet. Không còn lo lắng về việc quên đăng, nội dung không đồng nhất hay mất thời gian soạn thảo. Hãy **import ngay**, cấu hình các credentials và để n8n làm việc thay bạn – để bạn có thể tập trung vào chiến lược và sáng tạo! 🚀