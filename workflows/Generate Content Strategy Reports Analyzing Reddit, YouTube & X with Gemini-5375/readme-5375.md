---
title: "🚀 Tự động phân tích xu hướng nội dung từ Reddit, YouTube & X bằng Gemini AI trong n8n"
description: "Xây dựng chiến lược nội dung đỉnh cao với workflow n8n tự động cào dữ liệu từ Reddit, YouTube, X (Twitter), dùng Gemini AI lọc và tổng hợp thành báo cáo HTML chuyên nghiệp gửi qua Gmail."
slug: "tu-dong-phan-tich-xu-huong-noi-dung-reddit-youtube-x-gemini"
tags: [n8n, automation, gemini-ai, market-research, reddit, youtube, twitter]
keywords: [n8n workflow, phan tich xu huong, content strategy, gemini ai, reddit scraping, youtube api, tu dong hoa n8n]
---

# 🚀 Tự động phân tích xu hướng nội dung từ Reddit, YouTube & X bằng Gemini AI

Các sếp có bao giờ cảm thấy đuối sức khi phải liên tục "đào bới" các nền tảng mạng xã hội như Reddit, YouTube hay X (Twitter) để tìm kiếm ý tưởng viết bài, nghiên cứu thị trường hay bắt trend không? Việc đọc hàng trăm bình luận, xem chục video và tổng hợp thủ công ngốn vô số thời gian mà hiệu quả lại không đều.

Đừng lo, workflow n8n cực kỳ xịn sò này sẽ giúp các sếp tự động hóa 100% quy trình đó! Hệ thống sẽ thay các sếp cào dữ liệu từ 3 mạng xã hội lớn, sử dụng **Google Gemini AI** để lọc nội dung rác, phân tích chuyên sâu và tự động xuất ra một bản báo cáo chiến lược nội dung hoàn chỉnh gửi thẳng vào Gmail hoặc Feishu của các sếp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian nghiên cứu:** Không cần lướt mạng xã hội hàng giờ, AI sẽ tổng hợp những xu hướng nóng hổi nhất.
- **Lọc sạch nhiễu (Noise reduction):** Sử dụng AI Pre-filtering để loại bỏ các bài đăng kém chất lượng, chỉ giữ lại nội dung thực sự có giá trị.
- **Báo cáo chuyên sâu chuẩn SEO/Content:** Nhận ngay báo cáo dạng HTML trực quan qua Gmail hoặc tin nhắn nhóm qua Feishu/Webhook.
- **Lưu trữ tự động:** Toàn bộ dữ liệu phân tích được đồng bộ thẳng vào Google Sheets để tra cứu bất cứ lúc nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động mượt mà, các sếp cần chuẩn bị sẵn các tài khoản và API sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google Gemini API Key** (hoặc cấu hình qua LangChain LM Chat Google Gemini).
- **Reddit API / Credentials** (OAuth2).
- **Twitter / X API Credentials** (hoặc các dịch vụ bên thứ ba như Apify, ScrapingBee, TwitterAPI tùy chọn).
- **YouTube API Key / HTTP Query Auth**.
- **Google Sheets & Gmail Credentials** (OAuth2).
- **Feishu Webhook** (Nếu muốn nhận thông báo qua group chat).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow này, vào giao diện n8n Editor, chọn **New workflow** -> Nhấn tổ hợp `Ctrl + V` (hoặc `Cmd + V`) để dán toàn bộ các nodes lên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Vì workflow này có tới 31 nodes, các sếp cần chú ý cấu hình kỹ các điểm sau để chạy không bị lỗi:

- **Form Trigger & Analysis Parameters**: Nơi các sếp nhập từ khóa (keywords) hoặc chủ đề cần nghiên cứu thị trường. Hãy kiểm tra lại cấu hình form đầu vào.
- **Reddit: Search Posts, YouTube: Search Videos & X: Search Tweets**: 
  - Cấu hình lại các API credentials tương ứng cho từng nền tảng.
  - *Lưu ý về X (Twitter):* Workflow có chuẩn bị sẵn các lựa chọn như `Apify`, `ScrapingBee` hoặc `twitterapi` nếu các sếp không dùng official X API (do quota miễn phí của X khá hạn chế). Hãy chọn phương án phù hợp với tài nguyên của mình.
- **Pre-filter Content & Deep Analysis (Gemini AI nodes)**: 
  - Kết nối node với credentials của `Google Palm/Gemini API`.
  - Có thể tinh chỉnh System Prompt trong các node `AI Pre-filtering` và `AI Deep Analysis` để AI trả về kết quả đúng với văn phong và nhu cầu cụ thể của doanh nghiệp.
- **Archive Data (Google Sheets)**:
  - Chọn file Google Sheets và chỉ định đúng Sheet Name để workflow tự động ghi log dữ liệu phân tích (`append`).
- **Send HTML Report (Gmail) & Send Feishu Card**:
  - Cấu hình tài khoản Gmail gửi đi và điền đúng Webhook URL của Feishu Group Chat (nếu các sếp muốn nhận thông báo qua nhóm chat công ty).

#### 3. Kích hoạt ⚡️
- Nhấn nút **Test workflow** bằng cách điền thử một từ khóa vào Form Trigger để kiểm tra từng luồng dữ liệu (Data flow).
- Sau khi thấy dữ liệu chạy thông suốt từ đầu đến cuối và nhận được email báo cáo, các sếp bấm nút **Active** ở góc trên cùng bên phải để bật chế độ tự động chạy 24/7.

---

### ✍️ Mẹo & gợi ý nâng cao
- **Đa dạng hóa kênh nhận tin:** Ngoài Gmail và Feishu, các sếp có thể thay thế hoặc bổ sung node `Slack` hoặc `Telegram Bot` để gửi báo cáo chiến lược trực tiếp vào nhóm chat làm việc.
- **Lập lịch tự động (Schedule Trigger):** Thay vì dùng `Form Trigger` thủ công, các sếp có thể gắn thêm node `Schedule Trigger` để hệ thống tự động chạy báo cáo xu hướng vào mỗi sáng thứ Hai hàng tuần.
- **Kết hợp Notion:** Thêm node Notion vào cuối luồng để tự động tạo một trang "Content Strategy Report" lưu trữ tri thức cho team Marketing.

### 📌 Kết luận
Workflow **Generate Content Strategy Reports analyzing Reddit, YouTube & X with Gemini** là một "vũ khí" cực kỳ lợi hại cho các Marketer, Content Creator và các nhà nghiên cứu thị trường. Hãy triển khai ngay lên hệ thống n8n của các sếp để tối ưu hóa thời gian và luôn dẫn đầu xu hướng nội dung trong ngành!