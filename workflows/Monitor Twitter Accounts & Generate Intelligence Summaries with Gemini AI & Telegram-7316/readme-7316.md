---
title: "🚀 Tự động giám sát Twitter/X và phân tích tin tức bằng Gemini AI & Telegram"
description: "Hướng dẫn xây dựng hệ thống tự động theo dõi tài khoản Twitter, phân tích thông tin thông minh bằng Google Gemini AI và gửi báo cáo qua Telegram."
slug: "tu-dong-giam-sat-twitter-gemini-ai-telegram"
tags: [n8n, automation, no-code, twitter, gemini-ai, telegram, market-research]
keywords: [n8n workflow, tự động hóa twitter, gemini ai n8n, telegram bot n8n, market research automation]
---

# 🚀 Tự động giám sát Twitter/X và phân tích tin tức bằng Gemini AI & Telegram

Các sếp có đang tốn hàng giờ mỗi ngày để lướt Twitter/X nhằm cập nhật tin tức từ các KOLs, đối thủ cạnh tranh hay xu hướng thị trường không? Việc làm thủ công này cực kỳ mất thời gian, dễ bỏ lỡ thông tin quan trọng và gây xao nhãng.

Đừng lo, workflow n8n này sẽ giúp các sếp tự động hóa 100% quy trình: tự động quét tài khoản Twitter mục tiêu, sử dụng **Google Gemini AI** để phân tích, đánh giá mức độ quan trọng và gửi báo cáo tóm tắt trực tiếp về **Telegram** của các sếp! Không cần code phức tạp, setup một lần chạy mãi mãi.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian**: Không cần trực chờ trên Twitter, AI sẽ đọc và chắt lọc tin tức cốt lõi thay các sếp.
- **Phân tích thông minh**: Gemini AI tự động chấm điểm, phân loại và tóm tắt theo đúng prompt cấu hình riêng cho từng tài khoản.
- **Cảnh báo tức thì**: Nhận thông tin phân tích chất lượng cao qua Telegram ngay khi có bài viết mới đạt tiêu chuẩn.
- **Vận hành tự động 24/7**: Hệ thống tự động ghi nhớ mốc thời gian, không bỏ sót và không bị trùng lặp dữ liệu.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **n8n Instance**: Đã cài đặt sẵn sàng (Self-hosted hoặc Cloud).
- **PostgreSQL Database**: Nơi lưu cấu hình tài khoản Twitter và mốc thời gian cập nhật (`last_update_time`).
- **RSSHub Instance**: Dùng để chuyển đổi tài khoản Twitter thành RSS feed (có thể dùng public instance hoặc tự host).
- **Google Gemini API Key**: Tài khoản Google AI Studio để kết nối với node Gemini.
- **Telegram Bot Token & Chat ID**: Để gửi thông báo kết quả phân tích.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Copy toàn bộ JSON workflow từ n8n hoặc tải file JSON về, sau đó chọn **Import from File** hoặc dán trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các node trọng điểm sau đây:

- **Schedule Trigger**: Thiết lập khoảng thời gian chạy tự động (ví dụ: quét mỗi 15 phút hoặc 30 phút/lần).
- **Config (PostgreSQL)**: Kết nối tới cơ sở dữ liệu Postgres của các sếp và cấu hình truy vấn `executeQuery` để đọc bảng cấu hình tài khoản Twitter. Bảng mẫu gồm các cột: `id`, `twitter_account` (tên tài khoản không có dấu @), `last_update_time`, `prompt` (câu lệnh cho AI), và `note`.
- **RSS (RSSFeedRead)**: Trỏ URL đến instance RSSHub của các sếp theo cú pháp chuẩn của RSSHub cho mạng xã hội X (Twitter).
- **Filter New Tweets**: Node này lọc các bài đăng mới có thời gian (`IsoDate`) sau mốc `last_update_time` lấy từ database.
- **Analyze Tweet with AI (Google Gemini)**: Chọn credential Google Gemini, truyền nội dung tweet và câu lệnh `prompt` được lấy động từ cơ sở dữ liệu.
- **Parse AI Response & Filter by Level**: Xử lý chuỗi JSON trả về từ AI và lọc các bài viết đạt cấp độ quan trọng (ví dụ: `level` bằng 'A').
- **Update Latest Timestamp (PostgreSQL)**: Cập nhật lại mốc thời gian bài viết mới nhất vào database để lần chạy sau không bị lặp.
- **Send Telegram Message**: Điền Telegram Bot Token và Chat ID của các sếp để nhận thông báo.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử nghiệm (Test run) với dữ liệu mẫu xem hệ thống có mượt mà hay không.
- Sau khi kiểm tra mọi thứ đã chạy trơn tru, hãy gạt công tắc sang **Active** để workflow tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh nhận tin**: Ngoài Telegram, các sếp có thể nối thêm node Slack, Discord hoặc gửi Email tóm tắt hàng ngày.
- **Lưu trữ dữ liệu phân tích**: Thêm một node Postgres để lưu toàn bộ lịch sử phân tích của AI vào database phục vụ cho việc tra cứu, làm báo cáo thị trường (Market Research) dài hạn.
- **Đa dạng hóa nguồn tin**: Không chỉ Twitter, các sếp có thể kết hợp thêm RSS feed từ các trang báo công nghệ, blog uy tín vào cùng một luồng phân tích.

### 📌 Kết luận
Workflow này là một "vũ khí" cực mạnh cho các nhà quản lý, nhà nghiên cứu thị trường hay nhà sáng tạo nội dung muốn cập nhật tin tức chớp nhoáng mà không bị ngập chìm trong biển thông tin. Hãy triển khai ngay hôm nay để tối ưu hóa hiệu suất làm việc của các sếp nhé!