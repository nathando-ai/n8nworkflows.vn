---
title: "🚀 Tự động giám sát việc làm Upwork với Apify và nhận thông báo điện thoại qua ntfy"
description: "Hướng dẫn xây dựng workflow n8n tự động quét việc làm mới trên Upwork mỗi giờ qua Apify và gửi cảnh báo trực tiếp về điện thoại bằng ntfy hoàn toàn miễn phí."
slug: "giam-sat-viec-lam-upwork-apify-ntfy-n8n"
tags: [n8n, automation, no-code, apify, upwork, ntfy, web-scraping]
keywords: [n8n workflow, tự động hóa upwork, apify upwork scraper, ntfy notification, lọc việc làm upwork tự động]
---

# 🚀 Tự động giám sát việc làm Upwork với Apify và nhận thông báo điện thoại qua ntfy

Các sếp làm Freelancer trên Upwork chắc chắn hiểu cảm giác "ngồi canh" từng giây để săn các dự án mới phù hợp với kỹ năng của mình. Việc F5 trang web liên tục vừa tốn thời gian, mệt mỏi lại rất dễ bỏ lỡ các công việc "ngon ăn" vừa được đăng. 

Giải pháp là đây! Bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n tự động hoàn toàn: cứ mỗi giờ trong khung giờ hành chính ngày làm việc, hệ thống sẽ tự động quét các job mới nhất trên Upwork thông qua **Apify** và bắn thông báo (push notification) thẳng về điện thoại qua **ntfy.sh** mà không tốn một đồng chi phí phần mềm trung gian nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 săn job liên tục, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm tối đa thời gian:** Không cần F5 trang Upwork thủ công, hệ thống tự động làm việc 24/7.
- **Phản hồi siêu tốc:** Nhận thông báo việc làm mới ngay lập tức trên điện thoại, giúp ứng tuyển sớm nhất có thể.
- **Cá nhân hóa từ khóa:** Chỉ nhận thông báo các job thực sự liên quan đến kỹ năng (React, Python, Marketing, Design...).
- **Hoạt động hoàn toàn tự động:** Chạy ngầm định kỳ theo lịch trình cài đặt sẵn (Schedule Trigger).
:::

### Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống **n8n** đang hoạt động.
- Tài khoản **Apify** (có API Token và cấu hình Apify Actor dùng để scrape Upwork).
- Ứng dụng **ntfy** trên điện thoại (iOS/Android) hoặc truy cập [ntfy.sh](https://ntfy.sh/) để nhận thông báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy đoạn mã JSON của workflow hoặc tải file JSON, sau đó dán trực tiếp vào giao diện n8n Editor của mình. Workflow này gọn nhẹ chỉ gồm 4 nodes chính:
- **When Hourly on Weekdays** (`scheduleTrigger`)
- **Set Notification Parameters** (`set`)
- **Post Jobs to Upwork Scraper** (`httpRequest`)
- **Send NTFY Notification Post** (`httpRequest`)

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần cấu hình chính xác các node sau:

1. **Node `When Hourly on Weekdays` (Schedule Trigger):**
   - Cấu hình lại lịch chạy (Schedule) theo khung giờ hành chính hoặc múi giờ mong muốn của các sếp (ví dụ: chạy mỗi giờ từ thứ Hai đến thứ Sáu).

2. **Node `Set Notification Parameters` (Set):**
   - Thiết lập các tham số cấu hình runtime như: **Topic của ntfy** (để nhận thông báo trên điện thoại) và **Danh sách từ khóa (Keywords)** dùng cho việc tìm kiếm việc làm ở các bước sau.

3. **Node `Post Jobs to Upwork Scraper` (HTTP Request):**
   - **Credentials:** Cần cấu hình `httpBearerAuth` với **Apify API Token** của các sếp.
   - **Request Payload:** Điền đúng endpoint của Apify Actor chuyên scrape Upwork kèm theo các tham số tìm kiếm (truyền các từ khóa từ node Config sang).

4. **Node `Send NTFY Notification Post` (HTTP Request):**
   - Trỏ tới server ntfy và topic mà các sếp đã đăng ký (ví dụ: `https://ntfy.sh/ten_topic_bi_mat_cua_ban`).
   - Định dạng nội dung body thông báo (tiêu đề, nội dung job, link trực tiếp đến job trên Upwork) theo ý thích để hiển thị đẹp mắt nhất trên màn hình điện thoại.

#### 3. Kích hoạt ⚡️
- Bấm **Test workflow** để chạy thử nghiệm xem dữ liệu từ Apify có trả về đúng không và điện thoại đã nhận được thông báo qua ntfy chưa.
- Sau khi test thành công, bật công tắc **Active** để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Chat:** Ngoài ntfy, các sếp có thể nhân bản node thông báo để bắn thêm tin nhắn vào **Telegram Bot** hoặc **Slack** của nhóm.
- **Lưu trữ lịch sử:** Thêm một node **Google Sheets** hoặc **Airtable** để lưu lại danh sách các job đã quét, giúp dễ dàng tra cứu lại sau này.
- **Lọc thông minh bằng AI:** Kết hợp thêm các node AI (OpenAI / Anthropic) để phân tích mô tả công việc (Job Description) và đánh giá độ phù hợp trước khi gửi thông báo về điện thoại.

### 📌 Kết luận
Với workflow n8n cực kỳ tinh gọn này, các sếp đã có ngay một "trợ lý ảo" săn việc làm Upwork 24/7 mà không tốn một xu phí thuê tool ngoài. Hãy setup ngay hôm nay để trở thành một trong những freelancer ứng tuyển sớm nhất và chốt deal thành công nhé!