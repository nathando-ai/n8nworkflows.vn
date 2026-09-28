---
title: "🚀 Tự động phân tích hình ảnh Instagram với Apify, OpenAI GPT và Google Sheets trong n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động cào dữ liệu bài viết Instagram bằng Apify, phân tích hình ảnh đa phương thức bằng AI và lưu kết quả vào Google Sheets."
slug: "tu-dong-phan-tich-hinh-anh-instagram-apify-openai-google-sheets"
tags: [n8n, automation, no-code, instagram-scraper, openai, google-sheets]
keywords: [n8n workflow, tự động hóa instagram, apify instagram scraper, openai vision n8n, google sheets automation]
---

# 🚀 Tự động phân tích hình ảnh Instagram với Apify, OpenAI GPT và Google Sheets

Các sếp có bao giờ mất hàng giờ đồng hồ để nghiên cứu đối thủ, tổng hợp hình ảnh bài viết trên Instagram và phân tích xu hướng thị giác (visual trends) thủ công? Công việc này không chỉ tẻ nhạt mà còn cực kỳ mất thời gian khi phải làm với danh sách dài các tài khoản.

Đừng lo, bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ mạnh mẽ do chuyên gia **Robert Breen** thiết kế. Giải pháp này giúp tự động hóa 100% quy trình: lấy danh sách tài khoản từ Google Sheet, cào dữ liệu hình ảnh qua Apify, sử dụng OpenAI Vision (GPT) để phân tích thị giác và trả về nhữnginsight đắt giá mà không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Kéo dữ liệu bài đăng và hình ảnh mới nhất từ bất kỳ tài khoản Instagram nào chỉ với một cú click.
- **Phân tích hình ảnh thông minh (Multimodal AI):** Khai thác sức mạnh của OpenAI để mổ xẻ, đánh giá nội dung hình ảnh, màu sắc, phong cách bài đăng của đối thủ hoặc KOLs.
- **Quản lý tập trung:** Dữ liệu đầu vào lấy từ Google Sheets và kết quả phân tích được đồng bộ hóa mạch lạc, sẵn sàng cho các báo cáo chiến lược.
- **Tiết kiệm 90% thời gian:** Thay vì thao tác thủ công từng hình ảnh, hệ thống chạy ngầm hàng loạt một cách mượt mà.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google Account** (có file Google Sheets chứa cột `user` gồm các username Instagram cần phân tích).
- **Apify Account & API Token** (để sử dụng dịch vụ cào dữ liệu Instagram Profile Scraper).
- **OpenAI API Key** (với mô hình hỗ trợ Vision như GPT-4o, GPT-4o-mini hoặc GPT-5 cấu hình sẵn).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ n8n template (ID: 8068) và import trực tiếp vào giao diện n8n Editor của mình thông qua tính năng **Import from File** hoặc copy/paste trực tiếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm các node chính sau đây cần được cấu hình chuẩn xác:

- **Node `Get Google Sheet` (Google Sheets):**
  - Chọn credential loại `Google Sheets OAuth2 API`.
  - Chỉ định đúng **Spreadsheet** và **Worksheet** (ví dụ: bảng "Multi Scraper") có chứa cột `user` liệt kê các tài khoản Instagram mục tiêu.
- **Node `Scrape Details` (HTTP Request):**
  - Cấu hình credential loại `HTTP Query Auth`, thêm query parameter với `token=<YOUR_APIFY_TOKEN>` lấy từ Apify Console.
  - URL được thiết lập sẵn: `https://api.apify.com/v2/acts/apify~instagram-profile-scraper/run-sync-get-dataset-items`.
  - Body request sẽ tự động truyền biến `usernames: ["{{$json.user}}"]` từ dòng dữ liệu của Google Sheet.
- **Node `OpenAI Chat Model` & `AI Agent` (OpenAI):**
  - Tạo credential loại `OpenAI API` và dán API Key của các sếp vào.
  - Trong cấu hình model, chọn các dòng mô hình thị giác mạnh mẽ (như `gpt-4o`, `gpt-4o-mini` hoặc `gpt-5` tùy theo thiết lập của workflow).
- **Các node hỗ trợ khác (`Filter`, `Split Out`, `HTTP Request`):** Kiểm tra lại đường dẫn luồng dữ liệu (data flow) đảm bảo hình ảnh binary được trích xuất và đẩy vào AI Agent chính xác.

#### 3. Kích hoạt ⚡️
- Nhấn nút **`When clicking ‘Execute workflow’`** (`manualTrigger`) để test chạy thử với dữ liệu mẫu từ Google Sheets.
- Kiểm tra kết quả trả về ở các node AI Agent.
- Khi mọi thứ chạy trơn tru, hãy chuyển trạng thái workflow sang **Active** để đưa vào vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
Để khai thác tối đa sức mạnh của workflow này, các sếp có thể mở rộng thêm:
- **Tích hợp thông báo:** Nối thêm node **Slack** hoặc **Telegram** để gửi ngay báo cáo phân tích hình ảnh vào nhóm chat khi AI chạy xong.
- **Lưu trữ kết quả tự động:** Thay vì chỉ hiển thị trên n8n, hãy cấu hình đẩy ngược kết quả phân tích của AI vào một cột mới trong Google Sheet hoặc cơ sở dữ liệu như Airtable/Notion.
- **Định kỳ chạy tự động:** Thay thế node `manualTrigger` bằng `Schedule Trigger` để hệ thống tự động quét và phân tích đối thủ mỗi tuần/mỗi tháng một lần.

### 📌 Kết luận
Workflow *Instagram Visual Analysis* là một "vũ khí" lợi hại cho các nhà làm Marketing, nghiên cứu thị trường và cácagency sáng tạo nội dung. Hy vọng hướng dẫn chi tiết này giúp các sếp tự tay thiết lập thành công hệ thống tự động hóa của riêng mình. Chúc các sếp thao tác mượt mà và hẹn gặp lại ở các bài hướng dẫn tiếp theo!