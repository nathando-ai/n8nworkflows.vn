---
title: "🚀 Tự động tóm tắt bài viết Hot trên Reddit và gửi báo cáo qua Gmail bằng AI GPT-4o Mini"
description: "Hướng dẫn cài đặt workflow n8n tự động quét các subreddit mục tiêu mỗi ngày, lọc bài viết nổi bật, tóm tắt nội dung bằng AI qua OpenRouter và gửi bản tin tổng hợp (Digest) qua Gmail."
slug: "tu-dong-tom-tat-reddit-gui-gmail-gpt-4o-mini"
tags: [n8n, automation, reddit, gmail, gpt-4o-mini, openrouter, ai-agent, market-research]
keywords: [n8n workflow, tự động hóa reddit, tóm tắt bài viết reddit, gpt-4o mini n8n, gửi gmail tự động, market research automation]
---

# 🚀 Tự động tóm tắt bài viết Hot trên Reddit và gửi báo cáo qua Gmail bằng AI GPT-4o Mini

Việc theo dõi các xu hướng, thảo luận nổi bật trên Reddit để làm nghiên cứu thị trường (Market Research) hay cập nhật tin tức công nghệ ngốn rất nhiều thời gian nếu làm thủ công. Các sếp thường phải lướt qua hàng tá subreddit, đọc từng bình luận dài dòng để chắt lọc thông tin hữu ích.

Workflow n8n này sẽ giải quyết triệt để vấn đề đó: tự động quét các bài viết "Hot" trong 24 giờ qua, lọc theo tương tác (score > 30), sử dụng sức mạnh của **GPT-4o Mini (qua OpenRouter)** để tóm tắt nội dung bài viết kèm các bình luận chính, sau đó tổng hợp thành một bản tin (Digest) gọn gàng và gửi thẳng vào hộp thư Gmail của các sếp mỗi ngày.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm hàng giờ lướt web:** Tự động hóa toàn bộ quá trình thu thập và chắt lọc thông tin từ Reddit.
- **Nắm bắt insight nhanh chóng:** AI (GPT-4o Mini) tự động tóm tắt ngắn gọn các chủ đề nóng kèm theo các bình luận sắc sảo nhất.
- **Báo cáo định kỳ tiện lợi:** Nhận một email tổng hợp (Digest) đẹp mắt qua Gmail mỗi ngày đúng giờ hẹn.
- **Tùy biến linh hoạt:** Dễ dàng thay đổi danh sách subreddit, chủ đề quan tâm hoặc bộ lọc tương tác chỉ với vài cú click.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **Tài khoản Reddit API:** Để lấy dữ liệu bài viết và bình luận (`redditOAuth2Api`).
- **Tài khoản OpenRouter API:** Để kết nối với mô hình `openai/gpt-4o-mini` (`openRouterApi`).
- **Tài khoản Google/Gmail:** Để xác thực và gửi email tự động (`gmailOAuth2`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ nguồn gốc hoặc copy/paste trực tiếp mã JSON vào n8n Editor để bắt đầu.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 30 nodes được chia thành luồng chính và luồng phụ (Sub-workflow), các sếp cần chú ý cấu hình kỹ các điểm sau:

- **Schedule: Daily run:** Mở node này để cấu hình thời gian chạy tự động hàng ngày. Đảm bảo đã kiểm tra lại **Workflow Settings → Timezone** cho đúng múi giờ Việt Nam (UTC+7).
- **Set Topic, Subreddits and Email Address:** Đây là node cực kỳ quan trọng, các sếp cần điền đúng các thông số:
  - `topic`: Tên chủ đề bản tin (Ví dụ: `AI & Automation`, `Investing`).
  - `subreddits`: Mảng các subreddit muốn theo dõi (Ví dụ: `["n8n", "artificial", "SaaS"]`).
  - `email`: Địa chỉ Gmail nhận báo cáo.
- **Filter: Last 24h & Score > 30:** Node này giúp lọc ra các bài viết đăng trong vòng 24 giờ qua và có số điểm tương tác (score) lớn hơn 30. Các sếp có thể tăng/giảm ngưỡng score này tùy theo quy mô của subreddit.
- **GPT-4o mini (lmChatOpenRouter):** Cấu hình kết nối OpenRouter API Key và chọn model `openai/gpt-4o-mini` để tối ưu chi phí mà vẫn đảm bảo chất lượng tóm tắt.
- **Send Digest (Gmail):** Kết nối tài khoản Gmail cá nhân/doanh nghiệp để workflow có quyền gửi email báo cáo.

#### 3. Kích hoạt ⚡️
- Chạy thử thủ công (Test run) với một vài subreddit nhỏ để kiểm tra dữ liệu chảy qua các node `List Hot Posts`, `Summarize Threads` và `Send Digest`.
- Sau khi kiểm tra email nhận được hiển thị chính xác, hãy bật công tắc **Active** để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Telegram/Slack:** Ngoài việc gửi Gmail, các sếp có thể nhân bản luồng gửi và kết nối thêm node Telegram để nhận thông tin tóm tắt ngay trên điện thoại theo thời gian thực.
- **Lưu trữ vào Google Sheets:** Thêm node Google Sheets trước bước tóm tắt để lưu lại toàn bộ dữ liệu bài viết Reddit phục vụ cho việc nghiên cứu xu hướng dài hạn.
- **Giới hạn số lượng bài viết:** Nếu subreddit quá sôi nổi khiến email quá dài, hãy gắn thêm một node **Limit** trước khi đưa vào phần tóm tắt của AI.

### 📌 Kết luận
Workflow tự động hóa từ Reddit đến Gmail sử dụng GPT-4o Mini là một trợ lý đắc lực cho các nhà sáng tạo nội dung, marketer và lập trình viên muốn tự động hóa việc nghiên cứu thị trường. Hãy triển khai ngay hôm nay để tối ưu hóa thời gian và không bỏ lỡ bất kỳ xu hướng nào trên mạng xã hội!