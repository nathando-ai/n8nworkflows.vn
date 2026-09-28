---
title: "🚀 Tự Động Tổng Hợp và Đánh Giá Tin Tức Công Nghệ từ RSS với OpenAI, Google Sheets và Slack"
description: "Hướng dẫn xây dựng workflow n8n tự động cào tin RSS, lọc bài viết mới, dùng AI chấm điểm và tạo nội dung chia sẻ lên Slack, đồng thời lưu lịch sử chống trùng lặp."
slug: "tu-dong-tong-hop-tin-tuc-cong-nghe-rss-openai-slack"
tags: [n8n, automation, ai-summarization, openai, slack, google-sheets, rss]
keywords: [n8n workflow, tự động hóa tin tức, openai n8n, google sheets deduplication, slack automation, rss feed n8n]
---

# 🚀 Tự Động Tổng Hợp và Đánh Giá Tin Tức Công Nghệ từ RSS với OpenAI, Google Sheets và Slack

Các sếp làm trong ngành công nghệ, marketing hay sáng tạo nội dung có bao giờ thấy mệt mỏi khi phải liên tục "lướt web", đọc hàng chục trang tin mỗi ngày để tìm kiếm những bài viết giá trị nhằm chia sẻ lên mạng xã hội hoặc nội bộ team không? Việc này cực kỳ tốn thời gian mà lại dễ bỏ sót các xu hướng nổi bật.

Đừng lo, bài viết này sẽ hướng dẫn các sếp thiết lập một **AI Tech Insight Engine** hoàn chỉnh trên n8n. Workflow này sẽ tự động hóa 100% quy trình: cào tin từ RSS (như TechCrunch), lọc bài viết rác, dùng OpenAI để chấm điểm độ đổi mới (innovation score) và viết nội dung tóm tắt (tweet/digest), sau đó tự động gửi những tin "nóng" nhất lên Slack và lưu trữ vào Google Sheets để tránh trùng lặp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không cần thủ công lọc tin, AI sẽ thay bạn đọc, đánh giá và tóm tắt nội dung.
- **Nội dung chất lượng cao:** Chỉ chọn lọc những bài viết có điểm số từ AI $\ge$ 8/10, đảm bảo thông tin mang tính đột phá và chuyên môn cao.
- **Chống trùng lặp thông minh:** Tự động kiểm tra Google Sheets để loại bỏ ngay lập tức những bài đã từng đăng.
- **Tự động hóa hoàn toàn:** Chạy định kỳ theo lịch (Schedule Trigger) và đẩy thẳng kết quả vào kênh Slack của team.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **OpenAI API Key:** Để sử dụng node `AI - Score & Generate Tweet` phân tích và viết nội dung.
- **Google Sheets Account:** Tạo sẵn một file Google Sheets để lưu trữ lịch sử bài viết (chống trùng lặp và tracking).
- **Slack Account / Workspace:** Kết nối node `Send to Slack Channel` để nhận thông báo tin tức.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ kho lưu trữ chính thức của n8n (Workflow ID: `14702`) hoặc copy đoạn mã JSON tương ứng và dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình các node quan trọng sau đây để workflow chạy trơn tru:

- **Schedule Trigger:** Thiết lập lịch chạy mong muốn (ví dụ: chạy mỗi sáng lúc 8:00 AM).
- **Fetch RSS - TechCrunch:** Thay đổi URL RSS feed nếu các sếp muốn theo dõi các trang tin công nghệ khác (như The Verge, Wired, AI News...).
- **Check Google sheet & Log to Google Sheet:** Kết nối tài khoản Google Sheets thông qua OAuth2, trỏ tới file Google Sheets chuẩn bị sẵn và map đúng các cột dữ liệu (Link, Tiêu đề, Điểm AI, Ngày đăng...).
- **AI - Score & Generate Tweet:** Kết nối `openAiApi` credentials. Kiểm tra lại prompt trong node này để đảm bảo AI chấm điểm theo đúng tiêu chí mong muốn và viết nội dung (tweet/digest) đúng văn phong của team.
- **Filter - Score ≥ 8:** Tùy chỉnh mức điểm lọc (Threshold). Nếu muốn nhiều tin hơn, có thể hạ xuống $\ge 7$, hoặc tăng lên $\ge 9$ nếu chỉ muốn lọc những tin cực kỳ xuất sắc.
- **Send to Slack Channel:** Cấu hình tài khoản Slack (`slackApi`) và chọn đúng kênh (Channel) mà các sếp muốn bot bắn tin vào.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử nghiệm thủ công với dữ liệu mẫu xem hệ thống có hoạt động mượt mà từ đầu đến cuối không.
- Kiểm tra kết quả trên Google Sheets và kênh Slack.
- Nếu mọi thứ đã xanh mướt (success), các sếp chỉ cần gạt công tắc **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa dạng hóa kênh nhận tin:** Ngoài Slack, các sếp có thể nhân bản node cuối cùng và kết nối thêm Telegram Bot, Discord Webhook hoặc tự động đăng trực tiếp lên Twitter/X.
- **Tinh chỉnh Prompt AI:** Thêm yêu cầu AI phân loại tin theo từng lĩnh vực cụ thể (AI, Cybersecurity, Cloud, Startup...) để tiện gắn thẻ (tags).
- **Báo cáo tuần/tháng:** Tạo thêm một nhánh định kỳ tổng hợp các bài viết đã lưu trong Google Sheets để gửi báo cáo tuần về xu hướng công nghệ cho sếp lớn.

### 📌 Kết luận
Với workflow n8n kết hợp OpenAI và Google Sheets này, việc điểm tin công nghệ hàng ngày không còn là gánh nặng. Hãy "lên đồ" ngay cho hệ thống tự động hóa của mình để luôn dẫn đầu các xu hướng công nghệ mới nhất nhé các sếp!