---
title: "🚀 Tự động tạo và upload file llms.txt cho website chuẩn GEO tối ưu AI với ScrapegraphAI"
description: "Hướng dẫn sử dụng workflow n8n tự động cào dữ liệu website, tổng hợp bằng AI Agent và upload file llms.txt lên FTP chuẩn SEO và GEO."
slug: "tu-dong-tao-upload-llms-txt-website-geo-optimization-scrapegraphai"
tags: [n8n, automation, scrapegraphai, openai, ftp, geo-optimization]
keywords: [n8n workflow, llms.txt generator, scrapegraphai, geo optimization, ai agent ftp upload]
keywords: [n8n workflow, llms.txt generator, scrapegraphai, geo optimization, ai agent ftp upload]
---

# 🚀 Tự động tạo và upload file llms.txt cho website tối ưu GEO với ScrapegraphAI

Chào các sếp! Việc tối ưu hóa cho các công cụ tìm kiếm tích hợp AI (GEO - Generative Engine Optimization) đang trở thành xu hướng sống còn cho mọi website. Tuy nhiên, việc thủ công soạn thảo và cập nhật file `llms.txt` cho toàn bộ cấu trúc website tốn rất nhiều thời gian và công sức. 

Workflow n8n này sẽ giải quyết triệt để bài toán đó: Tự động crawl toàn bộ website, sử dụng AI thông minh để phân tích nội dung từng trang, tạo file `llms.txt` chuẩn cú pháp và tự động đẩy lên server qua FTP mà không cần động tay viết code một dòng nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Quét toàn bộ website, gom link nội bộ và tổng hợp thành file `llms.txt` chuẩn định dạng của `llmstxt.org`.
- **Cá nhân hóa bằng AI:** AI Agent kết hợp mô hình OpenAI và ScrapegraphAI tool tự động đọc hiểu từng URL, trích xuất tiêu đề, mô tả chính xác tuyệt đối khôngaaa bịa đặt nội dung.
- **Đẩy file tự động:** Chuyển đổi dữ liệu Markdown sang tệp nhị phân và upload thẳng lên server/hosting thông qua FTP.
- **Tiết kiệm thời gian:** Thay vì mất hàng giờ đồng hồ rà soát link và viết mô tả, hệ thống hoàn thành toàn bộ chỉ sau vài phút chạy lệnh thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và credentials sau trong n8n:
- **ScrapegraphAI API:** Dùng cho các node Smart Crawler và Smart Scraper.
- **OpenAI API:** Dùng cho node OpenAI Chat Model (hỗ trợ các model như `gpt-4o-mini` hoặc tùy chỉnh).
- **FTP Credentials:** Thông tin kết nối FTP (Host, User, Password, Port) của website để upload file kết quả.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow này, dán trực tiếp vào giao diện n8n Editor (hoặc import file JSON) để khởi tạo toàn bộ 12 nodes bao gồm Trigger, Agent, Crawler và FTP.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà theo đúng tên miền và hệ thống của các sếp, hãy chú ý cấu hình các node quan trọng sau:
- **Set domain:** Điền tên miền website mục tiêu của các sếp vào node này (Lưu ý: **Không** bao gồm tiền tố `https://` hay `http://`).
- **Wait (Chờ):** Tùy chỉnh khoảng thời gian chờ dựa trên quy mô lớn nhỏ của website để ScrapegraphAI crawler quét xong toàn bộ link nội bộ.
- **LLMS.txt Agent & OpenAI Chat Model:** Kiểm tra lại credentials của OpenAI. Các sếp có thể tinh chỉnh Prompt trong Agent nếu muốn thay đổi văn phong, ngôn ngữ (Tiếng Việt/Tiếng Anh) hoặc phân loại section theo ý muốn.
- **Upload to FTP:** Kiểm tra lại credentials FTP và đường dẫn lưu file tại ô path (ví dụ: `=/public_html/llms.txt` hoặc thư mục gốc tùy chọn). Đảm bảo tên file đầu ra là `llms.txt`.

#### 3. Kích hoạt ⚡️
- Nhấn nút **‘Execute workflow’** từ node `When clicking ‘Execute workflow’` để test chạy thử với dữ liệu thực tế.
- Kiểm tra kết quả trên thư mục FTP của server xem file `llms.txt` đã xuất hiện chưa.
- Sau khi test thành công, bật trạng thái **Active** để sẵn sàng sử dụng bất cứ lúc nào.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo Telegram/Slack:** Thêm một node Telegram hoặc Slack ở cuối luồng để nhận thông báo thành công hoặc cảnh báo lỗi ngay khi file `llms.txt` được upload lên server.
- **Lên lịch tự động (Cron):** Thay thế node `Manual Trigger` bằng `Schedule Trigger` để tự động cập nhật file `llms.txt` hàng tuần hoặc hàng tháng, giúp website luôn đồng bộ với các nội dung mới xuất bản.
- **Quản lý lịch sử:** Lưu lại nội dung file vào Google Sheets hoặc Notion để theo dõi sự thay đổi cấu trúc trang qua từng lần cập nhật.

### 📌 Kết luận
Việc tối ưu GEO cho website chưa bao giờ dễ dàng đến thế với sự trợ giúp của n8n và ScrapegraphAI. Hãy áp dụng ngay workflow này để giúp website của các sếp thân thiện hơn với các AI Crawler trong kỷ nguyên tìm kiếm thông minh!