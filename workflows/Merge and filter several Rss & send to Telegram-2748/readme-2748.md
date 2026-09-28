---
title: "🚀 Tự động tổng hợp, lọc tin tức từ nhiều nguồn RSS và gửi về Telegram bằng n8n"
description: "Hướng dẫn cài đặt workflow n8n tự động lấy tin từ nhiều nguồn RSS feed, gộp, lọc nội dung theo điều kiện và gửi thông báo trực quan định kỳ về Telegram."
slug: "tu-dong-tong-hop-loc-tin-rss-gui-telegram-n8n"
tags: [n8n, automation, no-code, telegram, rss, marketing]
keywords: [n8n workflow, tự động hóa RSS, gửi RSS về Telegram, lọc tin tức tự động, n8n RSS feed]
---

# 🚀 Tự động tổng hợp, lọc tin tức từ nhiều nguồn RSS và gửi về Telegram

Các sếp làm nội dung, marketing hay cập nhật tin tức chắc chắn đều gặp tình trạng phải "ngụp lặn" giữa hàng tá trang web, blog và bản tin RSS mỗi ngày để tìm kiếm thông tin hữu ích. Việc kiểm tra thủ công vừa tốn thời gian, vừa dễ bỏ lỡ các tin tức nóng hổi.

Giải pháp là đây! Workflow n8n này sẽ tự động hóa 100% quy trình: kéo tin từ nhiều nguồn RSS khác nhau, gộp chung, lọc các bài viết mới/phù hợp và đóng gói thành một danh sách Markdown gọn gàng gửi thẳng về Telegram của các sếp. Hoàn toàn không cần viết code phức tạp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không cần mở nhiều tab trình duyệt để check tin tức nữa.
- **Cập nhật liên động 24/7:** Chạy tự động theo lịch trình (Schedule) được thiết lập sẵn.
- **Nội dung chọn lọc:** Chỉ nhận những bài viết thực sự quan tâm nhờ bộ lọc (Filter) thông minh.
- **Giao diện trực quan:** Tin tức được định dạng Markdown gọn gàng, bấm vào là đọc ngay trên Telegram.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Telegram Bot:** Một Bot Telegram đã được tạo qua `@BotFather` và đã lấy được **Bot Token**, cùng với **Chat ID** của nhóm hoặc kênh nhận tin.
- **Nguồn RSS Feeds:** Danh sách các đường link RSS của các trang web/blog các sếp muốn theo dõi.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow (hoặc tải file) và import trực tiếp vào n8n Editor của mình. Workflow sẽ hiển thị sơ đồ gồm 10 nodes phối hợp nhịp nhàng.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà theo ý muốn, các sếp cần cấu hình chính xác các node sau dựa theo ghi chú gốc từ tác giả *Sherlockes*:

- **Schedule Trigger:** Thiết lập mốc thời gian muốn nhận tin (ví dụ: chạy mỗi sáng lúc 8h hoặc mỗi 4 tiếng một lần).
- **RSS Olimpo & RSS Torrent (Node RSS Feed Read):** 
  * *Lưu ý từ tác giả:* "In these nodes you have to modify the urls of the rss feeds to be consulted."
  * Các sếp cần thay thế URL mặc định bằng đường dẫn RSS thực tế của các trang tin tức mà mình muốn theo dõi. Có thể nhân bản thêm node RSS nếu cần lấy từ nhiều nguồn hơn.
- **Edit Fields & Edit Fields1 (Node Set):** Dùng để chuẩn hóa các trường dữ liệu (tiêu đề, link, ngày tháng) từ các nguồn RSS khác nhau về cùng một định dạng chung.
- **Merged Rss & Sort:** Gộp các luồng tin từ các nguồn lại với nhau và sắp xếp theo thứ tự thời gian mới nhất.
- **Filter (Node Filter):** 
  * *Lưu ý từ tác giả:* "Here the maximum age of the elements that we are going to show is defined" và "Adjust the regular expression to achieve the desired result".
  * Các sếp cấu hình điều kiện lọc (ví dụ: chỉ lấy các bài viết xuất bản trong vòng 24 giờ qua, hoặc chứa từ khóa liên quan đến ngành nghề).
- **Markdown list (Node Code):** Chuyển đổi danh sách các bài viết đã lọc thành định dạng văn bản Markdown đẹp mắt để hiển thị trên Telegram.
- **Telegram (Node Telegram):** 
  * Kết nối tài khoản bằng **Telegram API Credentials** (nhập Bot Token).
  * Điền **Chat ID** vào phần thông số để gửi tin nhắn đến đúng nhóm hoặc tài khoản cá nhân.

#### 3. Kích hoạt ⚡️
- Bấm **Test workflow** để chạy thử xem tin tức có được kéo về và gửi vào Telegram thành công hay không.
- Nếu mọi thứ mượt mà, gạt công tắc sang **Active** để workflow tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp AI tóm tắt:** Thêm một node AI (OpenAI / Anthropic) trước khi gửi sang Telegram để nhờ AI tóm tắt ngắn gọn 3 ý chính của mỗi bài báo.
- **Đa kênh thông báo:** Nhân bản node Telegram thành node Slack hoặc Discord nếu team làm việc trên các nền tảng chat khác.
- **Lưu trữ lịch sử:** Kết nối thêm node Google Sheets để lưu lại danh sách các tin tức đã gửi, tiện cho việc tra cứu sau này.

### 📌 Kết luận
Với workflow n8n tổng hợp RSS và gửi Telegram này, các sếp sẽ xây dựng được một "trợ lý tin tức" tự động hoàn toàn miễn phí, giúp bắt kịp xu hướng thị trường mỗi ngày mà không tốn một giọt mồ hôi. Lên đồ và áp dụng ngay thôi nào các sếp!