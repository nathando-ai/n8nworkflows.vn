---
title: "🚀 Tự động hóa kiểm tra PageSpeed Insights hàng loạt và xuất File CSV"
description: "Workflow n8n giúp phân tích điểm số Google PageSpeed Insights cho nhiều URL cùng lúc thông qua giao diện chat, tự động lọc link sống/chết và trả về file CSV hoàn chỉnh."
slug: "tu-dong-hoa-kiem-tra-pagespeed-insights-hang-loat"
tags: [n8n, automation, seo, google-pagespeed, chat-bot, productivity]
keywords: [n8n workflow, pagespeed insights automation, kiem tra seo hang loat, tu dong hoa n8n, google pagespeed api csv]
---

# 🚀 Tự động hóa kiểm tra PageSpeed Insights hàng loạt và xuất File CSV

Kiểm tra thủ công từng URL trên Google PageSpeed Insights và copy số liệu vào Excel là một ác mộng tốn hàng giờ đồng hồ của các anh em làm SEO, quản trị website hay team kỹ thuật. 

Workflow n8n này sinh ra để giải quyết triệt để vấn đề đó. Chỉ với một câu lệnh dán danh sách URL vào khung chat, hệ thống sẽ tự động validate, kiểm tra trạng thái hoạt động (online/offline), gọi Google PageSpeed API tuần tự để tránh lỗi Rate Limit, và trả về cho các sếp một file CSV chứa đầy đủ các chỉ số hiệu năng (Performance, SEO, Accessibility, Best Practices).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và xử lý các danh sách URL dài mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần click thủ công từng link, xử lý hàng chục URL chỉ trong vài phút.
- **Loại bỏ link "chết":** Tự động ping kiểm tra URL trước khi gọi API, tránh lãng phí tài nguyên và thời gian vào các trang lỗi 404 hoặc sập.
- **Dữ liệu trực quan, sạch sẽ:** Gom toàn bộ các chỉ số phức tạp từ Google thành các dòng dữ liệu phẳng gọn gàng và xuất ra file CSV sẵn sàng phân tích.
- **Giao diện Chat tiện lợi:** Tương tác trực tiếp qua khung chat n8n, nhận link tải file trực tiếp cực kỳ mượt mà.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Đã cấu hình Chat Trigger (hoặc sử dụng n8n Cloud / Self-hosted).
- **Google API Key:** Bắt buộc phải tạo một Google API Key miễn phí và cấu hình vào Credentials của node **PageSpeed API** để tránh bị giới hạn (rate limit) quá nhanh từ Google.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Copy toàn bộ mã JSON của workflow từ nguồn cung cấp và dán trực tiếp vào n8n Editor của các sếp, hoặc dùng tính năng Import từ file.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node `PageSpeed API` (HTTP Request):** 
  - Chọn hoặc tạo mới Credentials loại `Query Auth` (hoặc Header Auth tùy theo cấu hình Google API Key của sếp). 
  - Đảm bảo truyền đúng tham số API key để không gặp lỗi `429 Too Many Requests`.
- **Node `When chat message received` & `Final Chat`:** 
  - Cấu hình giao diện chat để bắt đầu nhập danh sách URL cần kiểm tra (`chatInput`).

#### 3. Kích hoạt ⚡️
- Bấm **Open chat** ở góc dưới canvas để test thử với 2-3 URL mẫu.
- Kiểm tra kết quả trả về và file CSV được tạo.
- Bật **Active** workflow để chính thức đưa vào vận hành.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram/Slack:** Thay vì trả kết quả qua khung chat n8n, các sếp có thể đổi node phản hồi thành gửi file CSV trực tiếp về nhóm Telegram hoặc Slack của team.
- **Lưu trữ tự động:** Kết hợp thêm node Google Sheets hoặc Airtable để lưu trữ lịch sử điểm số PageSpeed theo thời gian (tracking định kỳ hàng tuần/tháng).
- **Cảnh báo điểm số kém:** Thêm một nhánh IF sau bước trích xuất dữ liệu để nếu điểm Performance dưới 50 thì tự động bắn cảnh báo khẩn cấp cho dev.

### 📌 Kết luận
Workflow này là một "vũ khí" cực kỳ lợi hại cho các SEOer và Agency để audit website hàng loạt một cách chuyên nghiệp. Hãy triển khai ngay lên hệ thống n8n của các sếp để tối ưu hóa năng suất làm việc!