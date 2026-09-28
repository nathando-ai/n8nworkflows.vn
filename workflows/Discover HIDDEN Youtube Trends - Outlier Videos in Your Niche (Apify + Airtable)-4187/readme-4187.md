---
title: "🚀 Khám Phá Xu Hướng YouTube Ẩn Giấu: Tự Động Tìm Video Triệu View Với n8n, Apify & Airtable"
description: "Hướng dẫn xây dựng workflow n8n tự động quét từ khóa ngách trên YouTube qua Apify, phân tích nội dung bằng AI Mistral Cloud và lưu trữ kết quả chuyên nghiệp vào Airtable."
slug: "kham-pha-xu-huong-youtube-an-giau-voi-n8n-apify-airtable"
tags: [n8n, automation, no-code, youtube, apify, airtable, ai]
keywords: [n8n workflow, tu dong hoa youtube, apify youtube scraper, airtable automation, ai phan tich video youtube, mistral cloud n8n]
---

# 🚀 Khám Phá Xu Hướng YouTube Ẩn Giấu: Tự Động Tìm Video Triệu View Với n8n, Apify & Airtable

Các sếp có đang tốn hàng giờ mỗi tuần chỉ để lướt YouTube tìm ý tưởng nội dung, phân tích xem vì sao video của đối thủ lại viral? Việc nghiên cứu thị trường (Market Research) thủ công vừa mất thời gian, lại dễ bỏ sót các video "outlier" (video có lượng view vượt trội so với số lượngsub thực tế của kênh).

Đừng lo nữa các sếp! Bài viết này sẽ hướng dẫn chi tiết cách thiết lập một **Workflow n8n hoàn toàn tự động** giúp "săn" các xu hướng ẩn giấu trên YouTube, sử dụng AI để tóm tắt cấu trúc video và tự động đồng bộ toàn bộ dữ liệu vào Airtable.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [End đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Định kỳ hàng tuần, hệ thống tự động quét từ khóa và cập nhật video mới nhất vào Airtable.
- **Săn video Outlier chính xác:** Tính toán tự động chỉ số VSC Ratio (Views/Subs & Comments/Views) để tìm ra các video bùng nổ view thực sự.
- **Phân tích nội dung bằng AI:** Sử dụng Mistral Cloud AI để làm sạch và tổng hợp cấu trúc kịch bản video.
- **Lưu trữ chuyên nghiệp:** Quản lý toàn bộ thông tin (Link, Tiêu đề, Kênh, Thumbnail, Views, Subs...) gọn gàng ngay trên Airtable.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **Apify Account:** Tài khoản Apify để lấy API Token dùng cho việc cào dữ liệu YouTube.
- **Mistral AI Account:** API Key của Mistral Cloud để chạy node AI phân tích kịch bản.
- **Airtable Account:** Base quản lý dữ liệu YouTube với các trường (Fields) tương ứng.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và paste trực tiếp vào giao diện n8n Editor, hoặc import file JSON tải từ nguồn chính thức.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần chú ý cấu hình các node sau:

- **Schedule Trigger:** Chọn tần suất chạy mong muốn (Ví dụ: Chạy hàng tuần). *Lưu ý: Nếu thay đổi tần suất, nhớ cập nhật lại tham số `dateFilter` tương ứng trong node `Create Videos Dataset`.*
- **Setup Keywords:** Nhập các từ khóa liên quan đến ngách sản phẩm/nội dung mà các sếp muốn theo dõi. Nếu thay đổi số lượng từ khóa, nhớ cập nhật biến `searchQueries` trong node `Create Videos Dataset`.
- **Create Videos Dataset & HTTP Request Nodes:** 
  - Trong các trường URL của node HTTP Request, thay thế `[YOUR_API_TOKEN]` bằng API Token thực tế của tài khoản Apify.
  - Tham khảo thêm [Apify API Documentation](https://docs.apify.com/api/v2/getting-started) nếu gặp khó khăn khi cấu hình payload.
- **Mistral Cloud Chat Model:** Kết nối thông tin xác thực (Credentials) với `mistralCloudApi` bằng API Key của các sếp.
- **Airtable Node:** 
  - Kết nối Credentials với `airtableTokenApi`.
  - Cấu hình đúng Base và Table đích. 
  - Đặc biệt, đối với trường **Thumbnail** (Attachment), n8n yêu cầu định dạng mảng URL dạng: 
    `{{ [{ "url": $json.thumbnail}] }}`

#### 3. Kích hoạt ⚡️
- Chạy thử thủ công (Test step-by-step hoặc Execute Workflow) với dữ liệu mẫu để kiểm tra xem dữ liệu có đổ về Airtable chính xác hay chưa.
- Sau khi mọi thứ chạy trơn tru, bật công tắc **Active workflow** để hệ thống tự động làm việc thay các sếp.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Thêm node Telegram hoặc Slack ở cuối workflow để bắn thông báo ngay lập tức về máy mỗi khi có một video "outlier" triệu view xuất hiện trong ngách.
- **Mở rộng nguồn dữ liệu:** Không chỉ YouTube, các sếp có thể kết hợp thêm Apify Actor để quét TikTok hoặc Instagram Reels với cùng logic tính toán chỉ số tương tác.
- **Tự động hóa kịch bản:** Dùng kết quả phân tích cấu trúc từ AI (Text Synthesis) để làm đầu vào cho LLM viết kịch bản video mới cho kênh của mình.

### 📌 Kết luận
Workflow này là một "vũ khí bí mật" giúp các Content Creator và Data Marketer tiết kiệm hàng chục giờ nghiên cứu thủ công mỗi tuần. Hãy triển khai ngay trên hệ thống n8n của các sếp để luôn đi đầu xu hướng ngách của mình nhé!