---
title: "🚀 Tự động hóa thông báo bàn phím custom từ GeekHack lên Discord với n8n và PostgreSQL"
description: "Xây dựng hệ thống tự động quét RSS các bài đăng Interest Check và Group Buy mới nhất từ GeekHack, lưu trữ vào PostgreSQL và bắn thông báo trực quan kèm hình ảnh lên Discord."
slug: "tu-dong-hoa-geekhack-discord-postgres-n8n"
tags: [n8n, automation, discord, postgresql, rss, geekhack]
keywords: [n8n workflow, geekhack discord bot, tự động hóa rss, postgresql n8n, custom mechanical keyboard]
---

# 🚀 Tự động hóa thông báo GeekHack lên Discord với n8n & PostgreSQL

Các sếp trong hội mê bàn phím cơ (Custom Mechanical Keyboard) chắc hẳn đều quen thuộc với GeekHack - thánh địa của các kèo **Interest Check (IC)** và **Group Buy (GB)**. Tuy nhiên, việc F5 liên tục hay lướt forum thủ công để không bỏ lỡ các bộ keycap hay kit bàn phím hot thực sự tốn rất nhiều thời gian.

Giải pháp là gì? Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực xịn sò, tự động quét nguồn RSS của GeekHack, lọc các bài đăng mới, lưu lịch sử vào database PostgreSQL, crawl dữ liệu chi tiết kèm hình ảnh và bắn thẳng thông báo đẹp mắt lên kênh Discord của các sếp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Không bỏ lỡ kèo thơm:** Tự động bắt trọn mọi thread IC/GB mới xuất hiện trên GeekHack mà không cần canh me thủ công.
- **Tránh spam thông báo:** Sử dụng PostgreSQL làm bộ nhớ đệm (cache) để kiểm tra các thread đã được xử lý, đảm bảo 1 bài đăng chỉ bắn thông báo đúng 1 lần duy nhất.
- **Cập nhật trực quan:** Thông báo trên Discord hiển thị đầy đủ tiêu đề, nội dung tóm tắt từ tác giả và hình ảnh minh hoạ bắt mắt.
- **Vận hành tự động 24/7:** Chạy ngầm theo lịch trình (Schedule) hoặc tương tác linh hoạt qua form.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn sàng (Self-hosted hoặc Cloud).
- **Discord Webhook URL:** Để gửi tin nhắn thông báo vào kênh Discord chỉ định.
- **PostgreSQL Database:** Đã tạo sẵn bảng để lưu trữ trạng thái các thread (tránh thông báo trùng lặp).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và paste trực tiếp vào n8n Editor của mình. Workflow gồm 19 nodes được thiết kế mạch lạc từ khâu lấy dữ liệu RSS đến xử lý HTML và đẩy lên Discord.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần chú ý cấu hình các node cốt lõi sau:
- **Schedule Trigger:** Cài đặt chu kỳ quét (ví dụ: chạy mỗi 30 phút hoặc 1 tiếng một lần).
- **Interest Checks RSS & Group Buy RSS:** Trỏ tới đúng đường dẫn RSS feed của chuyên mục IC và GB trên GeekHack.
- **Check if Processed & Insert rows in a table (PostgreSQL):** Kết nối với database PostgreSQL của các sếp. Cần đảm bảo cấu trúc bảng có các trường lưu trữ ID hoặc Link thread để node `Check if Processed` nhận diện được bài viết cũ/mới.
- **Get geekhack page & Extract author message:** Node HTTP Request sẽ cào nội dung trang, kết hợp node HTML để bóc tách thông tin chi tiết và trích xuất lời nhắn của tác giả.
- **Send to discord:** Dán Discord Webhook URL của các sếp vào phần cấu hình HTTP Request để bot có quyền bắn tin nhắn.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Execute Workflow**) với một vài bản ghi mẫu để kiểm tra kết nối Database và Discord.
- Sau khi thấy tin nhắn đổ về Discord chuẩn chỉnh, các sếp bật công tắc **Active** để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Telegram/Slack:** Nếu hội nhóm của các sếp hoạt động trên Telegram hoặc Slack thay vì Discord, chỉ cần thay thế hoặc nhân bản node `Send to discord` sang node Telegram.
- **Báo cáo định kỳ:** Kết hợp thêm node Schedule để gửi bản tổng hợp (Digest) các kèo IC/GB nổi bật nhất trong tuần vào mỗi tối Chủ Nhật.
- **Lọc từ khóa thông minh:** Thêm node `If` hoặc tùy chỉnh code trong node `Filter New Threads` để chỉ thông báo khi bài viết chứa từ khóa mong muốn (ví dụ: "TKL", "Alice", "GMK",...).

### 📌 Kết luận
Với workflow n8n này, các sếp sẽ xây dựng được một "trợ lý ảo" săn đồ chơi phím cơ cực kỳ chuyên nghiệp, tiết kiệm thời gian và không bao giờ bỏ lỡ các Group Buy giới hạn. Triển khai ngay và tận hưởng thành quả thôi các sếp ơi!