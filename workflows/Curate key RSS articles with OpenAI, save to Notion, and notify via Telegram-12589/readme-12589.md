---
title: "🚀 Tự động hóa điểm tin công nghệ RSS với OpenAI, lưu vào Notion và thông báo Telegram"
description: "Hướng dẫn xây dựng workflow n8n tự động tổng hợp tin tức RSS từ TechCrunch, Dev.to, The Verge, dùng AI phân tích, lọc bài viết quan trọng lưu vào Notion và gửi thông báo qua Telegram."
slug: "tu-dong-hoa-diem-tin-rss-openai-notion-telegram"
tags: [n8n, automation, openai, notion, telegram, rss]
keywords: [n8n workflow, tự động hóa rss, openai tóm tắt tin tức, lưu notion tự động, thông báo telegram]
keywords: [n8n workflow, tự động hóa rss, openai tóm tắt tin tức, lưu notion tự động, thông báo telegram]
---

# 🚀 Tự động hóa điểm tin công nghệ RSS với OpenAI, lưu vào Notion và thông báo Telegram

Các sếp có đang tốn hàng giờ mỗi ngày để lướt các trang tin công nghệ (TechCrunch, Dev.to, The Verge...) nhằm tìm kiếm thông tin hữu ích cho công việc hoặc nghiên cứu thị trường? Việc đọc thủ công này vừa mất thời gian, vừa dễ bỏ lỡ các xu hướng quan trọng.

Giải pháp ở đây là gì? Workflow n8n này sẽ thay các sếp làm toàn bộ quy trình: Tự động gom tin, dùng AI (OpenAI) đọc hiểu, chấm điểm mức độ quan trọng, lọc ra những bài "đáng đồng tiền bát gạo" nhất, lưu gọn gàng vào Notion và bắn thông báo ngay lập tức qua Telegram. Tất cả hoàn toàn tự động 100% không cần code!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không còn phải mở hàng chục tab trình duyệt để đọc báo công nghệ mỗi sáng.
- **AI chọn lọc thông minh:** OpenAI tự động tóm tắt, trích xuất ý chính, phân loại và chấm điểm ưu tiên (từ 0-100) cho từng bài viết.
- **Cơ sở tri thức tự động (Notion):** Lưu trữ toàn bộ bài viết chất lượng cao vào Notion database một cách ngăn nắp, không bị trùng lặp.
- **Cập nhật tức thì (Telegram):** Nhận ngay các thông báo tóm tắt tin tức quan trọng trực tiếp qua chat Telegram để nắm bắt xu hướng nhanh chóng.
- **Dọn dẹp thông minh:** Tự động lưu trữ (archive) các bài viết cũ hơn 30 ngày để giữ database luôn gọn gàng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản sau:
- **n8n Instance:** Đã cài đặt sẵn (Self-hosted hoặc Cloud).
- **OpenAI API Key:** Để chạy node AI Content Analysis phân tích và chấm điểm bài viết.
- **Notion Integration & Database:** Tạo sẵn một Database trong Notion để lưu trữ bài viết với các trường (properties) phù hợp (Tiêu đề, URL, Tóm tắt, Điểm số, Ngày tháng...).
- **Telegram Bot Token & Chat ID:** Tạo một Bot thông qua `@BotFather` trên Telegram và lấy Chat ID để nhận thông báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow này, sau đó vào giao diện n8n Editor, chọn **Add workflow** -> bấm dấu `...` ở góc trên bên phải -> chọn **Import from Clipboard** và dán vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 16 nodes được thiết kế mạch lạc. Các sếp cần chú ý cấu hình các điểm mấu chốt sau:

- **Các node RSS (`RSS TechCrunch`, `RSS Dev.to`, `RSS The Verge`):** Mặc định đang lấy nguồn từ 3 trang công nghệ lớn. Các sếp có thể thay thế hoặc thêm bớt URL nguồn RSS tùy theo nhu cầu lĩnh vực của mình (Marketing, Tài chính, Crypto, v.v.).
- **Các node Notion (`Get Existing Articles`, `Save to Notion`, `Archive Old Articles`, `Get Old Articles`):** Cần kết nối với tài khoản Notion của các sếp và trỏ chính xác vào **Database ID** nơi lưu trữ bài viết.
- **Node AI Content Analysis (`AI Content Analysis`):** Node này sử dụng HTTP Request để gọi trực tiếp OpenAI API. Các sếp nhớ cấu hình **Credential** loại Header Auth hoặc Bearer Token với OpenAI API Key của mình, đồng thời kiểm tra lại prompt và model (khuyên dùng `gpt-4o-mini` hoặc `gpt-4o` để tối ưu chi phí và chất lượng).
- **Node Priority Filter (`Priority Filter (≥60)`):** Mặc định workflow sẽ lọc các bài viết có điểm số đánh giá từ `60` trở lên. Các sếp có thể tăng giảm ngưỡng này trong cấu hình điều kiện của node IF.
- **Node Telegram Notification (`Telegram Notification`):** Cần kết nối Telegram Bot Credential và điền chính xác `Chat ID` của cá nhân hoặc group nhận tin.
- **Trigger:** Mặc định workflow sử dụng `Manual Trigger` để test. Sau khi test ổn định, các sếp nhớ thay thế bằng **Schedule Trigger** (ví dụ chạy tự động 2 lần/ngày sáng và chiều).

#### 3. Kích hoạt ⚡️
- Bấm nút **Execute Workflow** để chạy thử nghiệm thủ công với dữ liệu mẫu từ các nguồn RSS.
- Kiểm tra xem Notion đã nhận được bài viết và Telegram đã bắn thông báo chưa.
- Nếu mọi thứ mượt mà, gạt công tắc sang **Active** để hệ thống tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Ngoài Telegram, các sếp có thể nối thêm node Slack, Discord hoặc Email để gửi bản tin tóm tắt (Newsletter) tự động hàng tuần cho đội ngũ.
- **Tùy biến Prompt AI:** Yêu cầu OpenAI dịch sang tiếng Việt hoàn toàn, hoặc viết lại theo giọng văn hài hước, châm biếm tùy sở thích.
- **Lưu log & Thống kê:** Kết hợp thêm Google Sheets để lưu vết số lượng bài viết thu thập được mỗi ngày phục vụ việc phân tích hiệu suất nội dung.

### 📌 Kết luận
Tự động hóa việc điểm tin công nghệ chưa bao giờ dễ dàng đến thế với sức mạnh kết hợp giữa n8n, OpenAI và Notion. Hãy áp dụng ngay workflow này để giải phóng thời gian đọc tin thủ công và cập nhật tri thức mỗi ngày một cách thông minh nhất! Chúc các sếp thao tác thành công!