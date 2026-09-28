---
title: "🚀 Tự động Kiểm định Influencer và Đánh giá Brand Safety với AI trên n8n"
description: "Xây dựng hệ thống tự động kiểm tra tài khoản Instagram, phát hiện follow ảo, phân tích tỷ lệ tương tác và quét rủi ro thương hiệu bằng OpenAI."
slug: "tu-dong-kiem-dinh-influencer-brand-safety-n8n"
tags: [n8n, automation, no-code, instagram, openai, influencer-marketing]
keywords: [n8n workflow, kiểm định influencer, brand safety, apify instagram scraper, openai n8n]
---

# 🚀 Tự động Kiểm định Influencer và Đánh giá Brand Safety với AI

Các sếp làm Influencer Marketing chắc chắn đã từng đau đầu khi hợp tác với những KOL/KOLs có lượng follow khủng nhưng tương tác lẹt đẹt (mua follow ảo), hoặc vô tình dính phốt phát ngôn tục tĩu, quảng cáo cho đối thủ cạnh tranh. Việc check tay từng profile, đọc hàng chục bài viết cũ vừa tốn thời gian lại dễ bỏ sót rủi ro.

Giải pháp đây rồi! Workflow n8n này sẽ tự động hóa 100% quy trình: nhận thông tin từ form, cào dữ liệu Instagram qua Apify, tính toán tỷ lệ tương tác thực tế, dùng AI để quét nội dung xem có an toàn cho thương hiệu hay không, sau đó gửi báo cáo về Slack và lưu log vào Google Sheets.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Thay vì mất 30 phút/influencer để check thủ công, hệ thống chỉ mất chưa tới 1 phút để trả về kết quả toàn diện.
- **Phát hiện "bẫy" follow ảo:** Tự động tính toán Engagement Rate và gắn nhãn "Suspicious" nếu số liệu bất thường (quá thấp hoặc cao một cách phi lý do bot).
- **Bảo vệ danh tiếng thương hiệu (Brand Safety):** AI OpenAI sẽ quét toàn bộ caption gần nhất để tìm từ ngữ nhạy cảm, phốt, hoặc nhắc đến đối thủ cạnh tranh.
- **Lưu trữ & Báo cáo minh bạch:** Tự động cập nhật kết quả vào Google Sheets và bắn thông báo trực tiếp lên kênh Slack của team.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow này "lên đồ" mượt mà, các sếp cần chuẩn bị sẵn:
- **Tài khoản Apify:** Để cào dữ liệu profile và bài viết Instagram (cần có API Token).
- **Tài khoản OpenAI:** API Key để sử dụng mô hình LLM phân tích nội dung.
- **Google Sheets:** File Google Sheet để lưu thông tin yêu cầu và kết quả kiểm định.
- **Slack Workspace:** Kênh Slack để nhận thông báo báo cáo tự động (cần có Slack OAuth2/Webhook).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy mã JSON của workflow này, vào giao diện n8n Editor chọn **Add workflow** -> Dấu ba chấm (...) ở góc trên bên phải -> **Import from JSON** và dán vào là xong.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy trơn tru, các sếp cần cấu hình chính xác các node sau:

- **Influencer Audit Form:** Node kích hoạt dạng Form. Các sếp có thể tùy chỉnh các trường đầu vào (username Instagram, tên đối thủ cạnh tranh cần check...) phù hợp với nhu cầu thực tế của team.
- **Store Audit Request:** Kết nối tài khoản Google Sheets của các sếp. Chọn đúng File ID và Sheet Name để lưu thông tin yêu cầu ban đầu của các sếp.
- **Apify Instagram Scraper:** Điền Apify API Token và cấu hình để cào profile cùng 30 bài viết gần nhất của influencer.
- **Calculate Engagement Rate:** Node Code (JavaScript) có sẵn nhiệm vụ tính toán tỷ lệ tương tác trung bình và gắn cờ cảnh báo nếu số liệu bất thường. Các sếp có thể giữ nguyên logic hoặc tùy chỉnh công thức tính toán.
- **AI Content Safety Audit:** Kết nối node OpenAI bằng API Key của các sếp. Kiểm tra lại prompt để đảm bảo AI tập trung quét đúng các tiêu chí Brand Safety mà doanh nghiệp quan tâm (ngôn từ gây tranh cãi, nhắc đến đối thủ, đánh giá tâm trạng...).
- **Send Audit Report to Slack:** Kết nối tài khoản Slack và chọn channel nhận thông báo (ví dụ: `#marketing-team` hoặc `#brand-safety`).
- **Store Audit Results:** Node Google Sheets tiếp theo dùng để lưu kết quả phân tích chi tiết của AI và chỉ số tương tác vào bảng tính.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng một username Instagram bất kỳ qua form.
- Kiểm tra xem dữ liệu đã đổ về Google Sheets và Slack chưa.
- Nếu mọi thứ mượt mà, bật nút **Active** ở góc trên cùng bên phải để đưa workflow vào hoạt động chính thức 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Ngoài Slack, các sếp có thể nối thêm node Telegram hoặc Email để gửi báo cáo trực tiếp cho cấp quản lý.
- **Tự động hóa hàng loạt:** Thay vì dùng Form thủ công, các sếp có thể kết nối workflow này với một danh sách Influencer dài ngoằng trên Google Sheets để hệ thống tự động quét định kỳ hàng tuần.
- **Lưu lịch sử kiểm duyệt:** Tách bảng Google Sheets thành các sheet riêng biệt cho "Đạt" và "Cần xem xét lại" để dễ dàng lọc danh sách hợp tác sau này.

### 📌 Kết luận
Workflow kiểm định Influencer tự động này là thứ vũ khí tối tân giúp các agency và brand manager loại bỏ hoàn toàn rủi ro truyền thông, tối ưu hóa ngân sách marketing. Triển khai ngay hôm nay để bảo vệ uy tín thương hiệu của các sếp nào!