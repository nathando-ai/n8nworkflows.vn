---
title: "🚀 Tự Động Theo Dõi Xu Hướng Mạng Xã Hội (Reddit, Instagram, TikTok) với Apify và n8n"
description: "Xây dựng hệ thống tự động cào dữ liệu, chấm điểm tương tác đa nền tảng (Reddit, Instagram, TikTok) qua Apify và gửi báo cáo HTML chi tiết qua Gmail."
slug: "tu-dong-theo-doi-xu-huong-mang-xa-hoi-reddit-instagram-tiktok-apify-n8n"
tags: [n8n, automation, apify, social-media, marketing, ai]
keywords: [n8n workflow, social media monitoring, apify scraper, reddit instagram tiktok, tu dong hoa marketing]
---

# 🚀 Tự Động Theo Dõi Xu Hướng Mạng Xã Hội Đa Nền Tảng với n8n & Apify

Các sếp làm marketing, nghiên cứu thị trường hoặc phát triển sản phẩm chắc chắn hiểu rõ nỗi đau: Việc ngồi mò mẫm từng từ khóa, hashtag trên **Reddit, Instagram và TikTok** mỗi ngày để xem đối thủ đang làm gì, xu hướng nào đang viral thực sự ngốn quá nhiều thời gian và công sức. Dữ liệu thì phân mảnh, việc tổng hợp thành một báo cáo hoàn chỉnh lại càng nhiêu khê.

Đừng lo, workflow n8n này sinh ra để giải quyết triệt để vấn đề đó! Hệ thống sẽ tự động hóa 100% quy trình cào dữ liệu, tính điểm tương tác thông minh, tổng hợp xếp hạng và gửi bảng dashboard HTML trực quan thẳng đến hộp thư Gmail của các sếp định kỳ.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Không cần tốn một phút thủ công nào để lướt mạng xã hội tìm trend.
- **Chấm điểm chuyên sâu:** Áp dụng thuật toán tính điểm riêng biệt cho từng nền tảng (tính đến upvotes, comments, shares, views...).
- **Đánh giá đa nền tảng:** Gộp top nội dung từ Reddit, Instagram và TikTok vào một bảng xếp hạng duy nhất.
- **Báo cáo chuyên nghiệp:** Nhận ngay email HTML trực quan, đầy đủ link gốc bài viết để đội ngũ dễ dàng nghiên cứu và lên chiến lược content.
:::

### 📦 Các thành phần chính trong Workflow (15 Nodes)
- **Schedule Trigger:** Lên lịch chạy tự động định kỳ.
- **Apify Integration (`httpRequest` + `wait`):** Gửi yêu cầu cào dữ liệu đến Apify cho 3 nền tảng (Reddit, Instagram, TikTok) và chờ kết quả trả về.
- **Xử lý dữ liệu (`code`):** Các node *Sort Reddit*, *Sort Instagram*, *Sort TikTok* và *Classement global* thực hiện chấm điểm, lọc top 10 bài viết xuất sắc nhất mỗi nền tảng và gộp thành bảng xếp hạng tổng thể (Top 15).
- **Send a message (`gmail`):** Gửi dashboard phân tích chi tiết qua Gmail.

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Self-hosted hoặc Cloud).
- **Tài khoản Apify:** Cần có API Token để kết nối các Actor cào dữ liệu Reddit, Instagram và TikTok.
- **Tài khoản Gmail/Google Workspace:** Đã cấu hình Credentials OAuth2 để n8n có thể gửi email tự động.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ n8n template hoặc copy trực tiếp mã JSON, sau đó paste vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Schedule Trigger:** Cấu hình lại khung giờ chạy mong muốn (ví dụ: Chạy mỗi tuần một lần vào thứ Hai sáng sớm).
- **Các node `Reddit Post`, `Insta Post`, `Tiktok Post` (httpRequest):** 
  - Cần cài đặt `Credentials` loại `HTTP Header Auth` trỏ tới Apify API Token của các sếp.
  - Cấu hình body JSON gửi đi trỏ đúng Actor Apify tương ứng kèm từ khóa/hashtag cần theo dõi (ví dụ: *"trottinette"*).
- **Các node `Reddit Get`, `Insta Get`, `Tiktok Get` (httpRequest):** Dùng để lấy kết quả từ dataset của Apify sau khi chạy xong.
- **Send a message (Gmail):** Chọn đúng Credentials Gmail OAuth2 đã liên kết để gửi báo cáo.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (**Execute Workflow**) để kiểm tra luồng dữ liệu từ Apify đổ về các node Code và Gmail có mượt mà không.
- Sau khi test thành công, bật công tắc **Active** để hệ thống tự động chạy ngầm.

---

### ✍️ Mẹo & gợi ý nâng cao
- **Đa kênh thông báo:** Ngoài gửi Gmail, các sếp có thể nối thêm node **Slack** hoặc **Telegram** để bắn nhanh thông báo tóm tắt trend vào nhóm chat của team content.
- **Lưu trữ dữ liệu lịch sử:** Thêm node **Google Sheets** hoặc **Airtable** để lưu lại toàn bộ lịch sử điểm số bài viết theo thời gian, giúp phân tích sự dịch chuyển của xu hướng dài hạn.
- **Tích hợp AI (LLM):** Kết nối thêm node OpenAI/Claude để tự động viết tóm tắt (AI Summary) những điểm nổi bật nhất từ các bài viết viral trước khi gửi mail cho sếp lớn.

### 📌 Kết luận
Việc bắt kịp xu hướng trên mạng xã hội không còn là bài toán cảm tính hay tốn hàng giờ cày cuốc thủ công. Với workflow kết hợp n8n và Apify này, các sếp đã sở hữu ngay một "trợ lý AI" đắc lực tự động quét, đo lường và báo cáo toàn cảnh thị trường mỗi ngày. Lên đồ ngay thôi nào các sếp!