---
title: "🚀 Tự động hóa bản tin tổng hợp Reddit (Reddit Digest) lên Telegram, Discord & Slack bằng AI Gemini"
description: "Hướng dẫn chi tiết xây dựng workflow n8n tự động cào dữ liệu Reddit, lọc nội dung bằng AI Gemini và gửi bản tin tóm tắt hàng ngày đến Telegram, Discord hoặc Slack."
slug: "tao-ban-tin-reddit-tu-dong-voi-n8n-gemini"
tags: [n8n, automation, ai, reddit, gemini, telegram, discord, slack]
keywords: [n8n workflow, tự động hóa reddit, ai curation gemini, tóm tắt tin tức reddit, telegram bot n8n]
---

# 🚀 Tự động hóa bản tin tổng hợp Reddit (Reddit Digest) lên Telegram, Discord & Slack bằng AI Gemini

Các sếp có đang tốn hàng giờ mỗi ngày để lướt Reddit tìm kiếm xu hướng, ý tưởng nội dung hay tin tức công nghệ? Việc tổng hợp thủ công này vừa tốn thời gian, vừa dễ bỏ lỡ thông tin quan trọng.

Giải pháp đây rồi! Workflow n8n này sẽ tự động hóa 100% quy trình: cào bài viết từ các subreddit yêu thích, sử dụng AI (Google Gemini) thông minh để lọc spam, chọn lọc nội dung chất lượng cao và phân phối bản tin đẹp mắt trực tiếp đến Telegram, Discord hoặc Slack của các sếp. Hoàn toàn không cần code!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần lướt Reddit thủ công, bản tin tự động cập nhật đúng giờ hẹn.
- **AI chọn lọc thông minh:** AI tự động loại bỏ rác, nội dung trùng lặp và chọn ra các bài viết giá trị nhất theo từ khóa trọng tâm.
- **Đa nền tảng:** Gửi đồng thời hoặc tùy chọn đến Telegram, Discord hay Slack.
- **Hoạt động bền bỉ 24/7:** Chạy tự động theo lịch trình đặt sẵn nhờ Schedule Trigger.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Phiên bản 1.0 trở lên (Self-hosted hoặc Cloud).
- **Google Gemini API Key:** Dùng cho node AI Content Curator (có tier miễn phí tại [Google AI Studio](https://makersuite.google.com/app/apikey)).
- **Tài khoản kênh nhận tin (Tùy chọn nền tảng các sếp muốn dùng):**
  - **Telegram:** Bot Token (lấy từ `@BotFather`) và Chat ID.
  - **Discord:** Webhook URL của kênh Discord.
  - **Slack:** OAuth Token và quyền truy cập kênh.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này từ n8n template hoặc copy toàn bộ JSON và dán trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình các node cốt lõi sau để workflow chạy mượt mà:
- **📅 Schedule Trigger (Daily 9 AM):** Đặt lịch thời gian gửi bản tin (mặc định 9h sáng mỗi ngày). Có thể đổi biểu thức Cron nếu muốn chạy tần suất khác (ví dụ: `0 */6 * * *` cho mỗi 6 tiếng).
- **⚙️ Configuration:** Node này cực kỳ quan trọng. Các sếp cần chỉnh sửa:
  - `subreddits`: Danh sách các chuyên mục muốn theo dõi (cách nhau bởi dấu phẩy, ví dụ: `AI_Agents,MachineLearning,Python`).
  - `min_upvotes`: Ngưỡng upvote tối thiểu để lọc bài chất lượng (mặc định 10).
  - `focus_keywords`: Từ khóa trọng tâm để AI ưu tiên.
- **Google Gemini Flash 2.0 (AI Model):** Thêm Credentials bằng cách nhập Google Gemini API Key.
- **📱 Send to Telegram / 💬 Send to Discord / 💼 Send to Slack:** Bật node tương ứng với nền tảng các sếp muốn nhận tin, sau đó điền Bot Token/Webhook URL/Channel ID. Nhớ chuột phải vào node và chọn **Enable** vì mặc định chúng có thể đang tắt.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử nghiệm và kiểm tra kết quả đổ về kênh chat.
- Nếu mọi thứ hiển thị đẹp đẽ, gạt công tắc sang **Active** để bật chế độ tự động 24/7.

### ✍️ Nâng cấp & Gợi ý mở rộng
- **Gửi Email báo cáo:** Nối thêm node "Send Email" vào sau node kiểm tra dữ liệu để nhận bản tin qua hòm thư cá nhân.
- **Lưu trữ lịch sử:** Kết nối thêm cơ sở dữ liệu (PostgreSQL, Supabase, Google Sheets) để lưu lại các bài viết đã gửi phục vụ nghiên cứu xu hướng (Market Research) sau này.
- **Tùy biến Prompt AI:** Vào node `🤖 AI Content Curator` để điều chỉnh giọng văn, phong cách tóm tắt (ngắn gọn, hài hước, hoặc chuyên sâu).

### 📌 Kết luận
Workflow tự động hóa tổng hợp Reddit này là trợ đắc lực cho các content creator, marketer và các "tín đồ" công nghệ muốn nắm bắt xu hướng nhanh chóng mà không bị ngập chìm trong biển thông tin. Cài đặt ngay hôm nay để tối ưu hóa năng suất cho bản thân và đội ngũ nhé các sếp!