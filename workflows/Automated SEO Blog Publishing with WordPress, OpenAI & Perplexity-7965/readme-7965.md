---
title: "🚀 Tự động xuất bản blog SEO với WordPress, OpenAI & Perplexity"
description: "Workflow tự động tạo nội dung, hình ảnh, đăng bài lên WordPress, đồng bộ lên Google Sheets, giảm thời gian thủ công và tăng chất lượng SEO."
slug: "tuy-dong-xuat-ban-blog-seo-voi-wordpress-openai-perplexity"
tags: [n8n, automation, no-code, seo, ai, wordpress]
keywords: [n8n workflow, tự động hóa, SEO blog, WordPress automation, AI content creation]
---

# 🚀 Tự động xuất bản blog SEO với WordPress, OpenAI & Perplexity

Bạn đang phải mất hàng giờ viết bài, tìm hình ảnh, đăng lên WordPress và cập nhật bảng tính? Workflow này sẽ giúp bạn **tự động hoá toàn bộ quy trình** từ lập kế hoạch nội dung, tạo bài viết, sinh hình ảnh, đăng lên WordPress, cho tới ghi nhận vào Google Sheets – **không cần viết một dòng code**.

:::info[Hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ 4‑6 giờ viết bài → 15 phút tự động.  
- **Chính xác & nhất quán**: Prompt chuẩn, cấu trúc bài viết, tiêu đề SEO được tối ưu.  
- **Cá nhân hóa**: Dựa vào dữ liệu trong Google Sheets, mỗi bài được tùy chỉnh theo chủ đề, từ khóa.  
- **Hoạt động liên tục**: Được lên lịch tự động, không lo bỏ lỡ deadline.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
| Dịch vụ | API Key / Credential | Ghi chú |
|---------|----------------------|---------|
| **WordPress** | `WordPress API` (OAuth hoặc Application Password) | Đăng nhập vào cài đặt WordPress → Users → Application Passwords |
| **OpenAI** | `OPENAI_API_KEY` | Dùng cho các node `lmChatOpenAi`, `openAi` |
| **Perplexity** | `PERPLEXITY_API_KEY` | Dùng cho node `perplexityTool` |
| **Google Sheets** | `Google Sheets API` (OAuth 2.0) | Dùng cho node `googleSheets` |
| **Cloudinary** | `CLOUDINARY_CLOUD_NAME`, `CLOUDINARY_API_KEY`, `CLOUDINARY_API_SECRET` | Dùng cho node `httpRequest` upload hình ảnh |
| **Pexels** | `PEXELS_API_KEY` | Dùng cho node `httpRequest` lấy hình ảnh |
| **Google Gemini** | `GOOGLE_GEMINI_API_KEY` | Dùng cho node `googleGemini` |
| **n8n Credentials** | Tạo credentials tương ứng trong n8n (WordPress, OpenAI, Perplexity, Google, Cloudinary, Pexels, Gemini) | Đảm bảo mỗi node được gán đúng credential |
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON từ link gốc hoặc copy toàn bộ JSON.  
2. Mở n8n → **Workflows** → **Import** → **Upload file** hoặc **Paste JSON**.  
3. Nhấn **Import** và workflow sẽ xuất hiện trong danh sách.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Mô tả | Cài đặt cần chỉnh |
|------|-------|-------------------|
| **Schedule Trigger** | Lên lịch chạy workflow (hàng ngày/tuần) | Chọn `Cron` hoặc `Interval` phù hợp |
| **Get data databse (Google Sheets)** | Lấy danh sách chủ đề, từ khóa | Đặt `Spreadsheet ID`, `Range` (ví dụ: `Sheet1!A2:B`) |
| **Content planer (agent)** | Xác định prompt tổng quát cho AI | Đặt `Prompt` (ví dụ: “Generate article outline for topic …”) |
| **OpenAI Chat Model** | Tạo nội dung chi tiết | Chọn model (gpt‑4‑o-mini), thiết lập `Temperature`, `Max Tokens` |
| **Perplexity** | Kiểm tra nội dung, lấy phản hồi | Đặt `Prompt` và `Model` (perplexity‑2) |
| **Generate an image (Google Gemini / OpenAI)** | Sinh hình ảnh chủ đề | Đặt `Prompt` (ví dụ: “High‑resolution image of …”) |
| **Post image Cloudinary2** | Upload hình ảnh lên Cloudinary | Gán credential Cloudinary, đặt `URL` và `Body` (Base64) |
| **Set Output Image** | Lưu URL hình ảnh vào biến | Đặt `Image URL` từ node trước |
| **Set Image on Wordpress Post1/2** | Đính kèm hình ảnh vào bài viết | Đặt `Media ID` từ node upload |
| **Create a post (WordPress)** | Đăng bài lên WordPress | Gán credential WordPress, điền `Title`, `Content`, `Excerpt`, `Categories`, `Tags` |
| **Append or update row in sheet** | Ghi nhận trạng thái, URL bài viết | Đặt `Spreadsheet ID`, `Range`, `Values` |
| **Limit** | Giới hạn số bài viết mỗi lần chạy | Đặt `Limit` (ví dụ: 3 bài) |
| **Aggregate** | Kết hợp dữ liệu từ nhiều item | Đặt `Mode` (e.g., `Merge`) |
| **Set input data/credintenials** | Chuẩn bị dữ liệu đầu vào cho các node | Đặt `Variables` (topic, keyword, etc.) |
| **Split Out / Split In Batches** | Xử lý từng item riêng lẻ | Đảm bảo `Batch Size` phù hợp (ví dụ: 1) |
| **Structured Output Parser1** | Phân tích output từ AI | Đặt `Schema` (JSON) |
| **OpenAI 4.1 mini4/5** | Kiểm tra và chỉnh sửa nội dung | Đặt `Prompt` (ví dụ: “Proofread the article”) |
| **Write query too pexels / image AI generator** | Tạo query cho Pexels hoặc AI generator | Đặt `Prompt` (ví dụ: “Find image of …”) |
| **Download Image form Pexels** | Tải hình ảnh từ Pexels | Gán credential Pexels, đặt `URL` |
| **upload image to wordpress / wordpress1** | Upload media lên WordPress | Gán credential WordPress, đặt `Body` (Base64) |
| **Set Image on Wordpress Post1/2** | Đặt hình ảnh làm featured image | Đặt `Media ID` |
| **Generate an image2/3** | Sử dụng OpenAI hoặc Gemini để tạo hình ảnh bổ sung | Đặt `Prompt` và `Model` |

> **Lưu ý**: Mỗi node cần được gán credential đúng loại. Nếu chưa tạo credential, vào **Credentials** → **New Credential** → chọn loại tương ứng.

#### 3. Kích hoạt ⚡️
1. **Test run**: Chạy workflow với dữ liệu mẫu (đảm bảo các node không bị lỗi).  
2. Kiểm tra kết quả:  
   - Bài viết xuất hiện trên WordPress.  
   - Hình ảnh được upload và gắn vào bài.  
   - Dữ liệu được ghi vào Google Sheets.  
3. Khi mọi thứ ổn, bật **Active** (đánh dấu xanh) để workflow tự động chạy theo lịch.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo Slack**: Thêm node `Slack` để gửi tin nhắn khi bài viết được đăng.  
- **Lưu log vào Google Sheets**: Dùng node `Append or update row in sheet` để ghi lại thời gian, tiêu đề, trạng thái.  
- **Đăng bài định kỳ**: Sử dụng `Schedule Trigger` với cron `0 8 * * *` để đăng bài vào 8h sáng mỗi ngày.  
- **Tùy chỉnh prompt**: Thêm `meta tags`, `SEO keywords` vào prompt của OpenAI để bài viết tối ưu hơn.  
- **Sử dụng Gemini cho hình ảnh**: Nếu muốn hình ảnh chất lượng cao, chuyển node `Generate an image` sang `googleGemini`.  

### 📌 Kết luận
Workflow **Automated SEO Blog Publishing with WordPress, OpenAI & Perplexity** giúp bạn **tối ưu hoá toàn bộ chuỗi công việc** từ ý tưởng đến bài đăng, giảm thiểu công sức và thời gian. Hãy **cài đặt ngay** để tập trung vào chiến lược nội dung thay vì công việc thủ công. Nếu có bất kỳ câu hỏi hay muốn tùy chỉnh thêm, đừng ngần ngại liên hệ với tác giả: `kontakt@lumizone.pl`. Happy automating!