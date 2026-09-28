---
title: "🚀 Tự động trích xuất phụ đề YouTube (Transcript) qua Google Sheets hoặc Webhook với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động lấy transcript video YouTube hàng loạt từ Google Sheets hoặc gọi trực tiếp qua Webhook API một cách nhanh chóng."
slug: "tu-dong-trich-xuat-phu-de-youtube-google-sheets-webhook-n8n"
tags: [n8n, automation, youtube, google-sheets, webhook, ai-tools]
keywords: [n8n workflow, trích xuất youtube transcript, tự động hóa google sheets, youtube transcript api, no-code automation]
---

# 🚀 Tự động trích xuất phụ đề YouTube (Transcript) qua Google Sheets hoặc Webhook với n8n

Việc nghiên cứu nội dung, phân tích đối thủ hay tổng hợp kiến thức từ hàng loạt video YouTube thủ công thực sự tốn rất nhiều thời gian. Các sếp có bao giờ cảm thấy mệt mỏi khi phải vừa xem video, vừa ghi chép hoặc tìm cách copy phụ đề? 

Workflow n8n này sinh ra để giải quyết triệt để vấn đề đó! Với sự kết hợp thông minh giữa **Google Sheets** và **Webhook API**, hệ thống sẽ tự động hóa 100% quy trình lấy transcript (phụ đề) từ bất kỳ video YouTube nào, trích xuất đầy đủ thông tin metadata và lưu trữ gọn gàng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Tự động lấy phụ đề hàng loạt thay vì copy-paste thủ công từng video.
- **Linh hoạt đa kênh:** Hỗ trợ cả 2 phương thức: Tự động quét Google Sheets hoặc gọi API trực tiếp qua Webhook.
- **Metadata đầy đủ:** Không chỉ lấy text phụ đề, workflow còn trả về tiêu đề video, tên kênh, ngày đăng, thời lượng và danh mục.
- **Xử lý thông minh:** Tự động nhận diện chuẩn các định dạng link YouTube khác nhau (`youtube.com`, `youtu.be`, `embed`) và xử lý mượt mà.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **YouTube Transcript API:** Tài khoản hoặc API key từ dịch vụ cung cấp transcript (như youtube-transcript.io).
- **Google Account:** Tài khoản Google để kết nối Google Sheets (dành cho luồng tự động hóa qua Sheet).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ n8n hoặc sao chép mã nguồn JSON và paste trực tiếp vào trình soạn thảo n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow được chia thành 2 nhánh xử lý độc lập. Các sếp cần cấu hình kỹ các node sau:

- **Node `Monitor Google Sheet for URLs` (googleSheetsTrigger):** 
  - Cấu hình kết nối Google OAuth2.
  - Chọn file Google Sheet và Sheet Name dùng để nhập danh sách URL YouTube đầu vào.
- **Nodes `Fetch Video Transcript Data (Sheets)` & `Fetch Video Transcript Data (Webhook)` (httpRequest):** 
  - Cấu hình credentials cho **YouTube Transcript API**. Đảm bảo endpoint và API Key chính xác để gọi dữ liệu.
- **Nodes xử lý Code (`Extract YouTube Video ID`, `Parse Transcript Text`):** 
  - Các node này đã được viết sẵn logic JavaScript để bóc tách ID video từ mọi định dạng URL và làm sạch nội dung transcript. Các sếp chỉ cần giữ nguyên hoặc tùy chỉnh nếu muốn định dạng lại text.
- **Node `Save Transcript to Sheet` (googleSheets):** 
  - Kết nối tài khoản Google Sheets và chọn file đích để lưu kết quả trả về (Tiêu đề video, Transcript, Metadata...).
- **Node `Webhook Trigger (Direct Input)` (webhook):** 
  - Kiểm tra đường dẫn path (mặc định là `extract-youtube-transcript`) và phương thức `POST` nếu muốn tích hợp gọi API từ bên ngoài (Bubble, Webflow, n8n khác...).

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (Test execution) bằng cách thêm 1 link YouTube vào Google Sheet hoặc gửi 1 request POST qua Postman/cURL đến Webhook.
- Kiểm tra kết quả trả về và bật công tắc **Active** để workflow chính thức vận hành tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp AI tóm tắt:** Nối thêm node OpenAI / Claude vào sau bước `Parse Transcript` để tự động tạo tóm tắt (Summary) hoặc trích xuất ý chính của video.
- **Gửi thông báo:** Thêm node Telegram hoặc Slack để nhận thông báo ngay khi workflow xử lý xong một video mới.
- **Lưu trữ database:** Thay vì chỉ lưu Google Sheets, các sếp có thể kết nối với Airtable, Notion hoặc Supabase để xây dựng một thư viện kiến thức video quy mô lớn.

### 📌 Kết luận
Workflow trích xuất YouTube Transcript này là trợ thủ đắc lực cho những ai làm content creator, nghiên cứu thị trường, SEO hoặc xây dựng ứng dụng AI. Hãy cài đặt ngay lên hệ thống n8n của các sếp để tối ưu hóa năng suất làm việc từ hôm nay!