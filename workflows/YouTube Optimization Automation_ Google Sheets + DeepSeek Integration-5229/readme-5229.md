---
title: "🚀 Tự động tối ưu YouTube: Kết nối Google Sheets + DeepSeek AI"
description: "Giải pháp tự động tạo tiêu đề và mô tả chuẩn SEO cho video YouTube bằng Google Sheets và mô hình ngôn ngữ DeepSeek, giảm 90% thời gian soạn nội dung."
slug: "tu-dong-toi-uu-youtube-google-sheets-deepseek"
tags: [n8n, automation, no-code, youtube, ai, google-sheets]
keywords: [n8n workflow, tự động hóa, YouTube SEO, DeepSeek, Google Sheets]
---

# 🚀 Tự động tối ưu YouTube: Kết nối Google Sheets + DeepSeek AI

Bạn đã từng mất hàng giờ để viết tiêu đề và mô tả chuẩn SEO cho mỗi video YouTube?  
Việc làm thủ công không chỉ tốn thời gian mà còn dễ gây lỗi, không đồng nhất và khó mở rộng.  
Workflow **YouTube Optimization Automation** sẽ tự động lấy dữ liệu từ Google Sheets, dùng mô hình DeepSeek tạo tiêu đề & mô tả chuẩn SEO, rồi cập nhật lại ngay vào sheet – **100% không cần viết code**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài phút xuống chỉ vài giây cho mỗi video.  
- **Độ chính xác cao**: AI tạo tiêu đề, mô tả dựa trên từ khóa SEO thực tế.  
- **Nhất quán & cá nhân hoá**: Mẫu nội dung đồng nhất, dễ tùy chỉnh qua Google Sheets.  
- **Hoạt động liên tục**: Workflow chạy tự động, không cần can thiệp thủ công.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Google** với quyền truy cập Google Sheets (OAuth2).  
- **API Key DeepSeek** (đăng ký tại https://deepseek.com).  
- **Google Sheet** chứa các cột: `Video ID`, `Keyword`, `Title (output)`, `Description (output)`.  
- **n8n** đã cài đặt (Self‑hosted hoặc Cloud).  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Vào **n8n > Workflows > Import**.  
2. Tải file JSON của workflow (được đính kèm trong phần **Resources**) hoặc copy toàn bộ JSON và dán vào ô **Import from Clipboard**.  
3. Nhấn **Import** → workflow sẽ xuất hiện trong danh sách.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Dưới đây là các node quan trọng và cách cấu hình:

| Node | Mô tả | Cấu hình cần chỉnh |
|------|------|--------------------|
| **When clicking ‘Execute workflow’** | Manual trigger để khởi động workflow. | Không cần thay đổi. |
| **Get row(s) in sheet** | Lấy dữ liệu video (Video ID, Keyword) từ Google Sheet. | - **Credentials**: `googleSheetsOAuth2Api`.<br>- **Spreadsheet ID**: ID của sheet chứa danh sách video.<br>- **Range**: ví dụ `Sheet1!A2:C` (cột A: Video ID, B: Keyword). |
| **HTTP Request** | Gửi request tới API YouTube (nếu cần lấy thông tin video). | - **Method**: `GET`.<br>- **URL**: `https://www.googleapis.com/youtube/v3/videos`.<br>- **Query Parameters**: `id={{$json["Video ID"]}}&part=snippet&key=YOUR_YOUTUBE_API_KEY`.<br>- **Authentication**: API Key. |
| **Code** | Xử lý dữ liệu thô, chuẩn hoá từ YouTube API. | - **Language**: JavaScript.<br>- **Code**: (được cung cấp trong workflow, không cần thay đổi). |
| **DeepSeek Chat Model** | Gọi mô hình DeepSeek để tạo nội dung. | - **Credentials**: `deepSeekApi`.<br>- **Model**: `deepseek-chat` (hoặc model mới nhất).<br>- **Prompt**: Được truyền từ node **New Title Generating** / **New Description Generating**. |
| **Merge** | Gộp kết quả tiêu đề và mô tả từ các chain LLM. | - **Mode**: `Pass Through` (đảm bảo cả 2 output được giữ). |
| **Update row in sheet1** | Cập nhật tiêu đề và mô tả mới vào Google Sheet. | - **Credentials**: `googleSheetsOAuth2Api`.<br>- **Spreadsheet ID**: giống như node “Get row(s)”.<br>- **Range**: vị trí dòng cần cập nhật (sử dụng `Row ID` từ node trước).<br>- **Values**: `Title (output)` và `Description (output)`. |
| **Code1** | Định dạng tiêu đề (cắt ngắn, thêm ký tự). | - **Language**: JavaScript.<br>- **Code**: tùy chỉnh nếu muốn thêm tiền tố/suffix. |
| **Code2** | Định dạng mô tả (thêm hashtag, CTA). | - **Language**: JavaScript.<br>- **Code**: tùy chỉnh theo nhu cầu marketing. |
| **Aggregate** | Gom lại các trường dữ liệu để gửi tới Google Sheet. | - **Operation**: `Append` hoặc `Merge` tùy mục tiêu. |
| **New Title Generating** (chainLlm) | Chuỗi LLM tạo tiêu đề SEO. | - **Prompt**: “Tạo tiêu đề YouTube ngắn gọn, chứa từ khóa **{{Keyword}}**, tối đa 60 ký tự, hấp dẫn người xem.” |
| **New Description Generating** (chainLlm) | Chuỗi LLM tạo mô tả SEO. | - **Prompt**: “Viết mô tả YouTube khoảng 150‑200 từ, bao gồm từ khóa **{{Keyword}}**, có 3‑4 câu mở đầu hấp dẫn và CTA cuối cùng.” |

> **⚠️ Lưu ý:** Đảm bảo các **Credentials** đã được tạo trong n8n → Credentials trước khi gán vào node. Nếu chưa có, vào **Credentials > New Credential**, chọn loại tương ứng và nhập API Key/ OAuth token.

#### 3. Kích hoạt ⚡️
1. Nhấn **Execute Workflow** để chạy thử với 1‑2 video mẫu.  
2. Kiểm tra Google Sheet: tiêu đề và mô tả mới đã được ghi lại đúng vị trí.  
3. Khi mọi thứ ổn, bật **Active** (nút chuyển đổi ở góc trên bên phải) để workflow tự động chạy mỗi khi bạn nhấn **Execute** hoặc tích hợp thêm trigger (cron, webhook, v.v.).

### ✍️ Mẹo & gợi ý nâng cao
- **Tự động hoá định kỳ**: Thêm node **Cron** để chạy mỗi ngày, tự động xử lý video mới được thêm vào sheet.  
- **Thông báo Slack/Telegram**: Sau khi cập nhật sheet, dùng node **Slack** hoặc **Telegram** gửi tin nhắn báo cáo cho team.  
- **Lưu log chi tiết**: Kết nối **Google Cloud Logging** hoặc **Airtable** để lưu lịch sử tiêu đề, mô tả và phản hồi AI.  
- **A/B Testing**: Tạo 2 chain LLM (phiên bản tiêu đề A & B), sau đó dùng node **Merge** + **HTTP Request** tới YouTube API để cập nhật tiêu đề thử nghiệm và đo lường hiệu suất.

### 📌 Kết luận
Với workflow **YouTube Optimization Automation**, các sếp có thể biến việc soạn tiêu đề & mô tả YouTube thành một quy trình tự động, nhanh chóng và chuẩn SEO chỉ trong vài giây. Hãy triển khai ngay hôm nay, kết hợp với các công cụ báo cáo để tối ưu hoá hiệu suất kênh YouTube của bạn! 🚀