---
title: "🚀 Tự động chuyển tiếp đánh giá Facebook tiêu cực lên Slack và tạo Ticket Supabase"
description: "Hướng dẫn thiết lập workflow n8n tự động bắt đánh giá Facebook Page tiêu cực (≤ 2 sao), gửi cảnh báo qua Slack và tạo ticket hỗ trợ trên Supabase để xử lý kịp thời."
slug: "tu-dong-chuyen-tiep-danh-gia-facebook-tieu-cuc-slack-supabase"
tags: [n8n, automation, facebook, slack, supabase, ticket-management]
keywords: [n8n workflow, tự động hóa đánh giá facebook, facebook review webhook, slack alert, supabase ticket]
---

# 🚀 Tự động chuyển tiếp đánh giá Facebook tiêu cực lên Slack và tạo Ticket Supabase

Trong kinh doanh online, việc phản hồi chậm trễ các đánh giá tiêu cực (1-2 sao) trên Fanpage Facebook có thể "giết chết" uy tín thương hiệu trong chớp mắt. Tuy nhiên, việc phải ngồi canh trực page 24/7 để lọc review xấu rồi thủ công copy qua nhóm chat nội bộ hay tạo ticket trên hệ thống là cực hình tốn thời gian.

Giải pháp là gì? Workflow n8n này sẽ tự động hóa 100% quy trình: ngay khi có khách hàng để lại đánh giá từ 2 sao trở xuống, hệ thống sẽ lập tức tóm bắt, gửi tin nhắn cảnh báo đỏ lửa vào Slack cho đội ngũ Support, đồng thời tự động tạo một ticket trên Supabase để tracking tiến độ xử lý mà không cần con người nhúng tay vào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phản ứng tức thì (Real-time Alert):** Đội ngũ CSKH nhận được cảnh báo ngay lập tức trên Slack khi có review tiêu cực, không bỏ sót bất kỳ khách hàng nào.
- **Tự động hóa Ticket Management:** Tự động tạo bản ghi trên Supabase để theo dõi trạng thái xử lý khiếu nại, đo lường KPI đội ngũ Support.
- **Cơ chế Fallback thông minh:** Nếu hệ thống database gặp lỗi khi tạo ticket, n8n sẽ tự động kích hoạt cảnh báo phụ để đảm bảo không có sự cố nào bị "chìm xuồng".
- **Tiết kiệm 100% thời gian thủ công:** Không cần nhân sự ngồi lướt Fanpage kiểm tra đánh giá mỗi ngày.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn sàng (Cloud hoặc Self-hosted).
- **Tài khoản Facebook Page / Webhook Provider:** Nguồn cấp dữ liệu đánh giá (Webhook).
- **Slack Workspace:** Đã tạo bot/App và có quyền gửi tin nhắn vào kênh channel chỉ định.
- **Supabase Project:** Đã tạo bảng (table) để lưu trữ các support ticket/case.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trên n8n, sau đó copy toàn bộ mã JSON của template hoặc import trực tiếp file JSON vào trình biên tập n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 7 nodes chính được cấu hình mạch lạc. Các sếp cần chú ý tùy chỉnh các điểm sau:

- **Facebook Page Review Trigger (Webhook):** 
  - Cấu hình endpoint path là `facebook-reviews` với phương thức `POST`. 
  - Kết nối nguồn Webhook từ Facebook Page hoặc qua các bên trung gian cấp phát dữ liệu review.
- **Global Configuration (Set):** 
  - Node này đóng vai trò chuẩn hóa dữ liệu đầu vào (lấy các trường như rating, nội dung review, tên người đánh giá, tên page). Các sếp cần điều chỉnh lại field mapping trong node này nếu cấu trúc payload webhook của sếp khác biệt so với mặc định.
- **Check Negative Review (≤ 2 Stars) (If):** 
  - Thiết lập điều kiện lọc: Chỉ cho phép các luồng dữ liệu có số sao `Rating <= 2` đi tiếp. Các đánh giá 3-4-5 sao sẽ được bỏ qua.
- **Slack – New Negative Review Alert & Slack – Case Creation Failed Alert (Slack):** 
  - Kết nối `slackApi` credentials của sếp.
  - Chọn kênh Slack channel (ví dụ: `#cskh-alerts`, `#support-urgent`) để nhận thông báo khẩn cấp.
- **Create Support Case (Supabase) & Check Case Creation Failure (Supabase / If):** 
  - Kết nối `supabaseApi` credentials.
  - Trỏ tới đúng tên bảng (Table Name) chứa dữ liệu support tickets trên cơ sở dữ liệu Supabase của sếp.
  - Nhánh `Check Case Creation Failure` sẽ kiểm tra xem việc ghi dữ liệu vào Supabase có thành công hay không; nếu thất bại sẽ bắn cảnh báo phụ sang Slack.

#### 3. Kích hoạt ⚡️
- Thực hiện **Test workflow** bằng cách gửi một payload giả lập (mock data) có số sao `<= 2` qua Webhook để kiểm tra luồng chạy từ Slack đến Supabase.
- Kiểm tra kết quả trên kênh Slack và bảng Supabase xem dữ liệu đã được đẩy chuẩn xác chưa.
- Gạt công tắc sang **Active** để đưa hệ thống vào vận hành tự động thực tế.

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống tối ưu hơn nữa, các sếp có thể mở rộng workflow với các ý tưởng sau:
- **Tích hợp AI Summarization (OpenAI / Claude):** Thêm một node AI trước khi gửi tin nhắn lên Slack để phân tích tâm lý khách hàng (Sentiment Analysis) và gợi ý sẵn câu trả lời mẫu cho nhân viên CSKH.
- **Gửi cảnh báo sang Telegram:** Nếu team không dùng Slack, có thể thay thế bằng node Telegram để nhận thông báo qua chat cá nhân hoặc nhóm Telegram.
- **Báo cáo định kỳ:** Kết hợp thêm node Schedule Trigger để thống kê số lượng review tiêu cực trong tuần/tháng và gửi báo cáo tổng kết vào sáng thứ Hai hàng tuần.

### 📌 Kết luận
Việc xử lý khủng hoảng truyền thông từ những đánh giá 1-2 sao trên Facebook chưa bao giờ dễ dàng và nhanh chóng đến thế. Hãy cài đặt ngay workflow này để bảo vệ uy tín thương hiệu và nâng cao trải nghiệm khách hàng ngay hôm nay các sếp nhé!