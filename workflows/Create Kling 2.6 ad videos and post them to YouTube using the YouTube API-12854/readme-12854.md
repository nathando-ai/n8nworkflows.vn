---
title: "🚀 Tự Động Tạo Video Quảng Cáo Kling 2.6 & Đăng Lên YouTube Với AI"
description: "Workflow n8n tự động sinh video quảng cáo dựa trên AI, tối ưu SEO và đăng trực tiếp lên YouTube chỉ trong vài phút."
slug: "tu-dong-tao-video-kling-2-6-youtube"
tags: [n8n, automation, no-code, content-creation, multimodal-ai, youtube]
keywords: [n8n workflow, tự động tạo video, YouTube API, AI video generation, content automation]
---

# 🚀 Tự Động Tạo Video Quảng Cáo Kling 2.6 & Đăng Lên YouTube Với AI

Bạn đã từng tốn hàng giờ đồng hồ để **lên kịch bản, tạo video, viết mô tả SEO và cuối cùng mới đăng lên YouTube**?  
Quá trình này không chỉ mất thời gian mà còn dễ gây sai sót, không đồng nhất và khó mở rộng.  

Workflow này sẽ **giải quyết toàn bộ chuỗi công việc**: từ nhập prompt, sinh nội dung AI, tạo video, tối ưu SEO, tới đăng tải lên YouTube – **tất cả 100 % không cần viết code**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80 % thời gian**: không còn phải quay, chỉnh sửa video thủ công.  
- **SEO chuẩn**: mô tả, tiêu đề, tag được AI tối ưu ngay khi tạo.  
- **Đăng tự động 24/7**: video xuất hiện trên kênh YouTube ngay khi workflow hoàn tất.  
- **Mở rộng dễ dàng**: chỉ cần thay đổi prompt, workflow tái sử dụng cho mọi chiến dịch.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Google** với quyền **YouTube Data API** (API Key & OAuth 2.0 credentials).  
- **Google Sheets**: bảng tính để lưu trữ prompt, từ khóa và kết quả.  
- **OpenRouter API Key** (hoặc bất kỳ LLM hỗ trợ OpenRouter).  
- **FAL.AI API Key** (để tạo video dựa trên prompt).  
- **n8n** đã cài đặt (Self‑hosted hoặc n8n.cloud).  
- **Kết nối internet ổn định** để tải video từ FAL.AI.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n → **Workflows** → **Import**.  
2. Chọn **Import from JSON** và tải file `Create_Kling_2.6_Ad_Videos.json` (được cung cấp kèm).  
3. Hoặc **Copy/Paste** nội dung JSON vào ô **Import JSON** và nhấn **Import**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Mô tả | Cấu hình cần chỉnh |
|------|------|--------------------|
| **Type Prompt** (formTrigger) | Form để nhập nội dung quảng cáo (prompt). | Đặt **Form Fields**: `title`, `description`, `targetAudience`… |
| **Store Data** (googleSheets) | Lưu prompt và kết quả vào Google Sheet. | Chọn **Credentials** Google Sheets → **Spreadsheet ID** → **Sheet Name** (ví dụ: `Kling_Ads`). |
| **AI Brain** (lmChatOpenRouter) | Gọi LLM để sinh nội dung video. | Chọn **Credentials** OpenRouter → **Model** (ví dụ: `gpt-4o`). |
| **Get Keywords** (code) | Trích xuất từ khóa SEO từ nội dung. | Không cần thay đổi, nhưng có thể tùy chỉnh regex nếu muốn. |
| **YT Video SEO** (agent) | Tối ưu tiêu đề, mô tả, tag cho YouTube. | Đảm bảo **Agent Prompt** chứa các biến `{title}`, `{keywords}`. |
| **Videography** (chainLlm) | Gửi yêu cầu tới FAL.AI để tạo video. | Chọn **Credentials** FAL.AI → **API Key**. |
| **Download Video** (httpRequest) | Tải video đã tạo về n8n. | Đảm bảo **Response Format** = `File`. |
| **Fetch Video Credentials** (httpRequest) | Lấy URL video tạm thời từ FAL.AI. | Kiểm tra **Header Authorization**. |
| **Post on YouTube** (youTube) | Đăng video lên kênh YouTube. | Chọn **Credentials** YouTube → **OAuth2** → Điền **Title**, **Description**, **Tags** (được truyền từ node trước). |
| **Wait 5 mins** (wait) | Đợi FAL.AI xử lý video. | Thời gian chờ có thể giảm/ tăng tùy tốc độ API. |
| **Structured Output** (outputParserStructured) | Định dạng dữ liệu trả về từ LLM. | Kiểm tra **Schema** để khớp với các trường cần dùng. |
| **Make FAL.AI Request** (httpRequest) | Gửi prompt tới FAL.AI để tạo video. | Đặt **Method** = `POST`, **Body** chứa `prompt`, `style`, `duration`. |

> **Lưu ý:** Mỗi node sử dụng **Credentials** riêng; hãy tạo chúng trong **Settings → Credentials** trước khi cấu hình node.

#### 3. Kích hoạt ⚡️
1. **Test run**: Nhấn **Execute Workflow** → nhập dữ liệu mẫu qua form. Kiểm tra log từng node để chắc chắn không lỗi.  
2. Khi mọi thứ ổn, bật **Active** (nút chuyển đổi ở góc trên bên phải).  
3. Đặt **Trigger** (formTrigger) lên **Webhook** nếu muốn tích hợp với website hoặc CRM.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối Slack/Telegram**: Thêm node `Slack` hoặc `Telegram` sau node `Post on YouTube` để thông báo ngay khi video được đăng.  
- **Lưu log chi tiết**: Dùng node `Google Sheets` hoặc `Airtable` để ghi lại `videoId`, `URL`, `thời gian đăng`.  
- **Báo cáo định kỳ**: Thêm `Cron` trigger (hàng tuần) + `Google Slides` để tự động tạo báo cáo thống kê lượt xem, tương tác.  
- **A/B Testing tiêu đề**: Tạo 2‑3 tiêu đề trong node `YT Video SEO`, dùng node `If` để đăng ngẫu nhiên, sau đó đo hiệu suất.  

### 📌 Kết luận
Với workflow này, các sếp có thể **tự động hoá toàn bộ quy trình tạo video quảng cáo Kling 2.6**, tối ưu SEO và đăng lên YouTube chỉ trong vài phút. Không còn lo lắng về thời gian biên tập, sai sót mô tả hay việc phải chạy tay từng bước. Hãy **import ngay**, cấu hình các credentials cần thiết và để n8n làm việc cho bạn! 🚀