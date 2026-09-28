---
title: "🚀 Tự động lọc bài viết RSS mới nhất có kèm hình ảnh với n8n"
description: "Hướng dẫn chi tiết cách sử dụng n8n workflow để tự động quét nguồn RSS định kỳ, lọc bỏ các bài viết cũ, chỉ lấy bài viết mới và bóc tách hình ảnh minh họa."
slug: "tu-dong-loc-rss-moi-nhat-kem-hinh-anh-n8n"
tags: [n8n, automation, rss, content-curation, no-code]
keywords: [n8n workflow, lọc rss tự động, lấy ảnh từ rss, n8n rss feed, tự động hóa nội dung]
---

# 🚀 Tự động lọc bài viết RSS mới nhất có kèm hình ảnh với n8n

Việc theo dõi hàng loạt nguồn tin tức, blog hoặc website thủ công qua RSS tốn rất nhiều thời gian, đặc biệt là khi bạn chỉ muốn lấy các bài viết **mới xuất bản** và **bắt buộc phải có hình ảnh minh họa** để phục vụ việc chia sẻ lên mạng xã hội hoặc làm content curation. 

Nếu các sếp đang đau đầu vì phải lọc thủ công từng bài viết cũ rích hoặc bài viết chỉ toàn chữ, thì workflow n8n **"Get only new RSS with photo"** do tác giả *Vlad Knyzhnyk* xây dựng chính là "vị cứu tinh". Workflow này sẽ tự động hóa 100% quy trình: quét feed, lọc bài mới, bóc tách ảnh và sẵn sàng cung cấp dữ liệu sạch cho các bước tiếp theo mà không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Chạy ngầm định kỳ theo lịch trình đặt sẵn, không cần thao tác tay.
- **Chỉ lấy tin mới:** Loại bỏ hoàn toàn các bài viết cũ đã được xử lý trước đó nhờ cơ chế lọc thông minh.
- **Đảm bảo chất lượng nội dung:** Chỉ giữ lại các bài viết có kèm hình ảnh minh họa thực sự (bóc tách trực tiếp từ HTML của bài viết).
- **Linh hoạt tích hợp:** Dữ liệu sau khi lọc sạch có thể đẩy thẳng về Telegram, Slack, Google Sheets hoặc Auto-posting lên Facebook/Twitter.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống n8n đã hoạt động (Cloud hoặc Self-hosted).
- Đường dẫn **RSS Feed** của trang web mà các sếp muốn theo dõi.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ kho lưu trữ chính thức của n8n (ID: 1309) hoặc copy/paste trực tiếp đoạn mã JSON vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 5 nodes chính phối hợp nhịp nhàng với nhau. Các sếp cần chú ý cấu hình các node sau:

- **Cron (Node lịch trình):** 
  - Mặc định node này kích hoạt workflow chạy theo chu kỳ thời gian (ví dụ: mỗi giờ một lần). Các sếp có thể bấm vào node này để chỉnh lại tần suất quét tin theo nhu cầu thực tế của doanh nghiệp.
- **RSS Feed Read (Node đọc nguồn tin):**
  - Tại đây, các sếp cần dán đường dẫn **URL của RSS Feed** mà mình muốn theo dõi vào trường cấu hình.
- **Extract Image1 (Node HTML Extract):**
  - Node này chịu trách nhiệm quét nội dung HTML của bài viết để tìm và bóc tách đường dẫn hình ảnh (`<img>`). Đảm bảo rằng XPath hoặc CSS Selector trỏ đúng vào phần tử chứa ảnh trong feed của các sếp.
- **Filter RSS Data (Node Set):**
  - Dùng để chuẩn hóa dữ liệu đầu ra, gom nhóm các thông tin quan trọng như tiêu đề (Title), đường dẫn (Link), thời gian xuất bản (PubDate) và link ảnh (Image URL).
- **Only get new RSS1 (Node Function):**
  - Node chạy mã lệnh Javascript đơn giản có sẵn nhiệm vụ so sánh và ghi nhớ các bài viết đã quét, đảm bảo hệ thống **chỉ trả về các bài viết hoàn toàn mới** trong lần chạy gần nhất.

#### 3. Kích hoạt ⚡️
- Bấm nút **Execute Workflow** để test thủ công xem dữ liệu trả về có đúng tiêu chí (có link bài viết + có link ảnh) hay không.
- Nếu mọi thứ hiển thị xanh mướt, hãy gạt công tắc sang chế độ **Active** để hệ thống tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
Để workflow trở nên "lợi hại" hơn nữa, các sếp có thể mở rộng bằng cách nối thêm các node phía sau:
1. **Bắn thông báo:** Thêm node Telegram hoặc Slack để gửi ngay bài viết mới kèm hình ảnh về nhóm chat nội bộ.
2. **Lưu trữ dữ liệu:** Kết nối với Google Sheets hoặc Notion để lưu lại danh sách các bài viết đã tổng hợp làm tư liệu.
3. **Tự động đăng mạng xã hội:** Kết hợp với OpenAI (ChatGPT) để viết lại tóm tắt ngắn gọn rồi auto-post lên Fanpage Facebook hoặc LinkedIn.

### 📌 Kết luận
Workflow "Get only new RSS with photo" là một công cụ cực kỳ gọn nhẹ nhưng mang lại hiệu suất cao trong việc thu thập và lọc nội dung tự động. Hãy áp dụng ngay vào hệ thống n8n của các sếp để tiết kiệm hàng giờ đồng hồ mỗi ngày cho việc điểm tin thủ công!