---
title: "🚀 Tự Động Theo Dõi Kênh YouTube Yêu Thích Qua RSS và Nhận Thông Báo Thông Minh"
description: "Xây dựng hệ thống tự động theo dõi video mới từ các kênh YouTube yêu thích qua RSS, xử lý thông tin bằng AI và gửi thông báo qua Telegram hoặc Gmail."
slug: "tu-dong-theo-doi-kenh-youtube-qua-rss-va-nhan-thong-bao"
tags: [n8n, automation, youtube, rss, ai, telegram, gmail]
keywords: [n8n workflow, theo dõi youtube tự động, rss youtube, thông báo telegram, gửi email tự động n8n]
---

# 🚀 Tự Động Theo Dõi Kênh YouTube Yêu Thích Qua RSS và Nhận Thông Báo Thông Minh

Các sếp có đang tốn quá nhiều thời gian để lướt YouTube, kiểm tra thủ công xem các kênh yêu thích đã ra video mới hay chưa? Hay các sếp là nhà sáng tạo nội dung/marketer cần theo dõi sát sao đối thủ nhưng lại bỏ lỡ các xu hướng mới? Việc cập nhật thủ công cực kỳ tốn thời gian và dễ bỏ sót thông tin quan trọng.

Giải pháp ở đây chính là workflow n8n cực kỳ xịn sò được thiết kế bởi chuyên gia Joseph LePage. Workflow này sẽ tự động hóa toàn bộ quy trình: quét RSS feed của các kênh YouTube, lọc video mới trong khoảng thời gian nhất định, dùng AI tổng hợp và gửi thông báo trực quan đến Telegram hoặc Gmail của các sếp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Không cần tự tay kiểm tra từng kênh YouTube mỗi ngày.
- **Đa kênh thông báo:** Nhận ảnh thu nhỏ (thumbnail), tiêu đề và link trực tiếp qua Telegram hoặc Email (gửi từng email riêng lẻ hoặc 1 email tổng hợp).
- **Ứng dụng AI mạnh mẽ:** Sử dụng OpenAI (GPT-4o-mini) thông qua các node `Create Email per Video` và `Create One Email for All Videos` để tối ưu hóa nội dung email thông báo cực kỳ chuyên nghiệp.
- **Linh hoạt cấu hình:** Dễ dàng nhập danh sách kênh YouTube mong muốn thông qua form (`On form submission`) hoặc sử dụng bộ kênh mặc định.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động mượt mà, các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **n8n instance** (Self-hosted hoặc Cloud).
- **YouTube Data API Key** (để lấy thông tin chi tiết video).
- **OpenAI API Key** (cho các node xử lý nội dung LangChain).
- **Tài khoản Gmail** (với quyền OAuth2 để gửi email).
- **Telegram Bot Token & Chat ID** (để nhận tin nhắn thông báo).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Các sếp tải file JSON của workflow từ nguồn gốc hoặc copy đoạn JSON được cung cấp.
- Trong giao diện n8n Editor, chọn **Add workflow** -> Nhấp vào dấu 3 chấm ở góc trên bên phải -> **Import from File / Clipboard** và dán JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình các thành phần sau để workflow chạy đúng ý muốn:
- **Node Credentials:** 
  - Kết nối `OpenAI Chat Model` / `OpenAI Chat Model1` với OpenAI API Credential của sếp.
  - Kết nối `Multiple Emails` / `Single Email` với tài khoản Gmail qua OAuth2.
  - Kết nối node `Telegram` với Telegram Bot API.
- **Node `Get YouTube Video Details` (HTTP Request):** Điền `GOOGLE_API_KEY` của các sếp vào phần header hoặc query parameters theo hướng dẫn trên canvas của workflow.
- **Node `On form submission` & `Default YouTube Channel Ids` / `YouTube Channel Ids`:** Cấu hình danh sách ID kênh YouTube mà các sếp muốn theo dõi.
- **Node `Get New Videos` (Filter):** Kiểm tra lại điều kiện lọc thời gian video mới (mặc định trong vòng 3 ngày gần nhất, các sếp có thể thay đổi tùy nhu cầu).

#### 3. Kích hoạt ⚡️
- Nhấn nút **‘Test workflow’** (hoặc dùng node `When clicking ‘Test workflow’` và `On form submission`) để chạy thử nghiệm xem dữ liệu có đổ về Telegram và Gmail chính xác không.
- Sau khi test thành công, gạt công tắc **Active** ở góc trên bên phải để workflow tự động chạy theo lịch trình từ node `Every Day` (Schedule Trigger).

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh nhận thông báo:** Thay vì chỉ Telegram và Gmail, các sếp có thể kết nối thêm node Slack hoặc Discord để đội ngũ cùng cập nhật thông tin.
- **Lưu trữ dữ liệu:** Thêm node Google Sheets hoặc Airtable vào sau bước lọc video để lưu lại lịch sử các video đã được thông báo, tránh bị trùng lặp.
- **Tùy chỉnh Prompt AI:** Tinh chỉnh prompt trong các node LangChain (`Create Email per Video`) để email tổng hợp có phong cách viết đúng ý sếp nhất (hài hước, trang trọng, tóm tắt ngắn gọn...).

### 📌 Kết luận
Workflow "Monitor Favorite YouTube Channels Through RSS feeds and Receive Notifications" là một công cụ tuyệt vời giúp các sếp tiết kiệm hàng giờ đồng hồ mỗi tuần. Hãy thiết lập ngay hôm nay để không bỏ lỡ bất kỳ xu hướng hay nội dung giá trị nào từ các nhà sáng tạo yêu thích!