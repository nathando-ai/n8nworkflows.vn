---
title: "🚀 Gửi Bản Tin Thể Thao Hàng Tuần Tự Động Với AI: Reddit, GPT‑4o‑mini, Gemini & Outlook"
description: "Tự động thu thập tin thể thao từ Reddit, tổng hợp nội dung bằng AI và gửi newsletter qua Outlook mỗi tuần, không cần viết code."
slug: "gui-ban-tin-the-thao-hang-tuan-tu-dong-ai"
tags: [n8n, automation, no-code, AI, newsletter, sports]
keywords: [n8n workflow, tự động hóa, newsletter thể thao, AI content, Reddit, Outlook]
---

# 🚀 Gửi Bản Tin Thể Thao Hàng Tuần Tự Động Với AI: Reddit, GPT‑4o‑mini, Gemini & Outlook

Bạn đã từng mất hàng giờ mỗi tuần để **làm thủ công**:
- Đăng nhập Reddit, tìm kiếm các bài viết thể thao hot.
- Sao chép, dán, chỉnh sửa nội dung.
- Viết lại tiêu đề, tóm tắt, rồi gửi email cho danh sách người nhận.

Kết quả? **Thời gian tiêu tốn**, **độ chính xác không đồng đều**, và **rủi ro bỏ lỡ tin tức**.  
Workflow này sẽ **giải quyết toàn bộ** quy trình trên bằng cách:

1. **Tự động lấy bài viết thể thao mới nhất từ Reddit**.  
2. **AI (GPT‑4o‑mini + Gemini) tóm tắt, chỉnh sửa, cá nhân hoá** nội dung.  
3. **Gửi bản tin qua Outlook** vào đúng ngày/giờ đã định – **không cần can thiệp**.

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm thời gian**: Tự động thu thập và tổng hợp trong vài phút.  
- **Nội dung chuẩn xác, chuyên nghiệp**: AI xử lý ngôn ngữ, giảm lỗi chính tả và cải thiện phong cách.  
- **Cá nhân hoá**: Có thể chèn tên người nhận, khu vực, hoặc sở thích thể thao.  
- **Hoạt động liên tục**: Newsletter được gửi đúng lịch mà không cần giám sát.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **Tài khoản Reddit** + **API credentials** (Client ID, Client Secret, Refresh Token).  
- **API key OpenAI** (để sử dụng GPT‑4o‑mini).  
- **API key Google Gemini** (hoặc Vertex AI).  
- **Tài khoản Microsoft Outlook** (SMTP/Exchange) và **credentials** (email, password hoặc OAuth token).  
- **n8n** (cài đặt trên VPS hoặc Docker).  
- **Cron** (để kích hoạt workflow hàng tuần).  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file `weekly-sports-newsletter.json` (được đính kèm trong mục **Releases**).  
2. Mở n8n → **Workflows** → **Import** → Chọn file JSON → **Import**.  
3. Hoặc **Copy/Paste** nội dung JSON vào **Import from Clipboard**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌  
Dưới đây là danh sách các node quan trọng và cách cấu hình:

| Node | Mô tả | Tham số cần điền |
|------|------|------------------|
| **Cron (Weekly Trigger)** | Kích hoạt workflow mỗi tuần (ví dụ: Thứ Hai, 08:00). | - **Cron Expression**: `0 8 * * 1` (8h sáng thứ Hai). |
| **Reddit (Get Posts)** | Lấy các bài post mới nhất từ subreddit thể thao (e.g., r/sports, r/soccer). | - **Credentials**: Reddit API.<br>- **Subreddit**: `sports` (hoặc tùy chọn).<br>- **Limit**: `50`. |
| **Function (Filter Sports)** | Lọc chỉ những bài có từ khóa liên quan (football, basketball, tennis…). | ```js\nreturn items.filter(item => /football|basketball|tennis/i.test(item.json.title));``` |
| **OpenAI (GPT‑4o‑mini) – Summarize** | Tóm tắt nội dung mỗi post thành đoạn ngắn 2‑3 câu. | - **Credentials**: OpenAI API Key.<br>- **Model**: `gpt-4o-mini`.<br>- **Prompt**: `Summarize the following Reddit post in a concise, engaging paragraph suitable for a newsletter.` |
| **Google Gemini (Enhance)** | Cải thiện ngôn ngữ, thêm tiêu đề hấp dẫn, chèn emojis. | - **Credentials**: Gemini API Key.<br>- **Prompt**: `Rewrite the summary to be lively, add a catchy headline and appropriate emojis.` |
| **Outlook (Send Email)** | Gửi bản tin tới danh sách người nhận. | - **Credentials**: Outlook SMTP/OAuth.<br>- **To**: danh sách email (có thể lấy từ Google Sheet hoặc static).<br>- **Subject**: `🗞️ Bản Tin Thể Thao Tuần {date}`.<br>- **HTML Body**: chèn biến `{{$json["enhanced"]}}` (kết quả Gemini). |
| **Set (Prepare Email Body)** *(optional)* | Ghép các đoạn tóm tắt thành một email HTML. | - **Expression**: `items.map(i => i.json.enhanced).join("<hr/>")`. |

> **Lưu ý:**  
> - Đảm bảo **Credentials** được gán đúng cho từng node (đánh dấu màu xanh).  
> - Kiểm tra **Scope** của API (Reddit cần quyền `read`, OpenAI/Gemini cần `text:generate`).  
> - Nếu dùng **OAuth** cho Outlook, hãy tạo **App Registration** trên Azure AD và cấp quyền `Mail.Send`.

#### 3. Kích hoạt ⚡️
1. **Test run**: Nhấn **Execute Workflow** → Kiểm tra log từng node, chắc chắn không có lỗi.  
2. **Kiểm tra email mẫu**: Đảm bảo nội dung hiển thị đúng định dạng HTML.  
3. Khi mọi thứ ổn, bật **Active** (nút chuyển đổi ở góc trên bên phải). Workflow sẽ tự động chạy vào thời gian đã định.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo Slack/Telegram**: Thêm node Slack hoặc Telegram để gửi tin nhắn “Newsletter đã được gửi” tới kênh nội bộ.  
- **Lưu log vào Google Sheets**: Dùng node Google Sheets để ghi lại số lượng bài viết, thời gian gửi, tỷ lệ mở email (kết hợp với tracking pixel).  
- **Đa ngôn ngữ**: Sử dụng Gemini để dịch bản tin sang tiếng Anh, tiếng Tây Ban Nha, rồi gửi theo ngôn ngữ người nhận.  
- **A/B Testing tiêu đề**: Tạo 2 phiên bản tiêu đề, dùng node Random để gửi ngẫu nhiên, sau đó phân tích tỉ lệ mở qua Outlook analytics.  

### 📌 Kết luận
Với workflow này, **các sếp** sẽ không còn phải mất công tìm tin, viết bản tin, hay lo lắng về việc gửi trễ. Tất cả được tự động hoá 100% bằng n8n, AI và Outlook – **giải pháp nhanh, chính xác, và tiết kiệm chi phí**. Hãy triển khai ngay hôm nay, để mỗi tuần luôn có một bản tin thể thao chất lượng, thu hút độc giả và nâng cao thương hiệu của bạn! 🚀