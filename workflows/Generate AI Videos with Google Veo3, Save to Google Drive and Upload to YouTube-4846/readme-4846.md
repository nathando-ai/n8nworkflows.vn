---
title: "🚀 Tự động tạo video AI với Google Veo3, lưu Google Drive và đăng YouTube"
description: "Hướng dẫn xây dựng hệ thống tự động hóa hoàn toàn quy trình tạo video AI bằng Google Veo3, tối ưu tiêu đề qua OpenAI, lưu trữ trên Google Drive và đăng lên YouTube từ Google Sheets."
slug: "tu-dong-tao-video-ai-google-veo3-google-drive-youtube"
tags: [n8n, automation, ai-video, google-veo3, youtube, google-sheets, open-ai]
keywords: [n8n workflow, tạo video ai, google veo3, tự động đăng youtube, google drive automation, open ai gpt-4o]
---

# 🚀 Tự động hóa toàn diện quy trình tạo video AI với Google Veo3, lưu Google Drive và đăng YouTube

Các sếp có đang cảm thấy mệt mỏi khi phải tốn hàng giờ liền để lên ý tưởng prompt, chờ render video AI, tải xuống, viết tiêu đề rồi lại thủ công upload lên YouTube không? Quy trình sản xuất nội dung video thủ công này ngốn rất nhiều thời gian và năng lượng.

Đừng lo, bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n cực kỳ mạnh mẽ, tự động hóa từ A-Z: Lấy yêu cầu từ Google Sheets -> Gọi API tạo video AI (Google Veo3 qua Fal.ai) -> Kiểm tra trạng thái -> Lưu file vào Google Drive -> Dùng OpenAI tạo tiêu đề tối ưu -> Tự động upload lên YouTube và cập nhật ngược lại kết quả vào Google Sheets!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Từ khâu nhận prompt đến khi video xuất hiện trên kênh YouTube mà không cần can thiệp thủ công.
- **Quản lý tập trung:** Biến Google Sheets thành bảng điều khiển (Dashboard) trực quan để quản lý danh sách video, prompt và link kết quả.
- **Tối ưu SEO tự động:** Sử dụng OpenAI (GPT-4o) để sinh tiêu đề video hấp dẫn, chuẩn SEO thu hút lượt xem.
- **Hoạt động bền bỉ:** Kết hợp giữa `Schedule Trigger` và cơ chế kiểm tra trạng thái (`If`, `Wait 60 sec.`, `Get status`) giúp xử lý các video render nặng mà không bị timeout.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google Account:** Dùng cho Google Sheets và Google Drive (Credentials: `googleSheetsOAuth2Api`, `googleDriveOAuth2Api`).
- **Fal.ai Account:** Để gọi API Google Veo3 tạo video (Lấy API Key tại [fal.ai](https://fal.ai/)).
- **OpenAI Account:** Để tạo tiêu đề video tự động (Credentials: `openAiApi`).
- **Upload-Post Account:** Dịch vụ hỗ trợ quản lý và upload video lên mạng xã hội (Lấy API Key tại [app.upload-post.com](https://app.upload-post.com/) - miễn phí 10 uploads/tháng).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng file JSON của workflow này, copy và paste trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 15 nodes được thiết kế chặt chẽ. Các sếp cần cấu hình chính xác các điểm sau:

- **Google Sheets Nodes (`Get new video`, `Update result`, `Update Youtube URL`):** 
  - Tạo một Google Sheet mẫu dựa theo [Link mẫu của tác giả](https://docs.google.com/spreadsheets/d/1pcoY9N_vQp44NtSRR5eskkL5Qd0N0BGq7Jh_4m-7VEQ/edit?usp=sharing).
  - Cột `PROMPT`: Nhập mô tả chi tiết video muốn tạo.
  - Cột `DURATION`: Thời lượng video.
  - Cột `VIDEO`: Để trống, hệ thống sẽ tự điền link khi hoàn thành.
  - Kết nối tài khoản Google Sheets thông qua OAuth2 trong n8n.

- **Fal.ai API Nodes (`Create Video`, `Get status`, `Get Url Video`, `HTTP Request`):**
  - Sử dụng Authentication kiểu `Header Auth`.
  - Thiết lập Name: `Authorization` và Value: `Key YOURAPIKEY` (với `YOURAPIKEY` là API key lấy từ Fal.ai).

- **OpenAI Node (`Generate title`):**
  - Chọn credential OpenAI API và cấu hình model phù hợp (như `gpt-4o`) để tạo tiêu đề video bắt tai.

- **YouTube Upload Node (`HTTP Request` - Upload/Post API):**
  - Cấu hình Header Auth với Name: `Authorization` và Value: `Apikey YOUR_API_KEY_HERE` (lấy từ Upload-Post).
  - Điền Profile name quản lý mạng xã hội của các sếp vào tham số `YOUR_USERNAME` (ví dụ: `test1`, `test2`).

- **Google Drive Node (`Upload Video`):**
  - Kết nối tài khoản Google Drive để lưu trữ bản sao của video được tạo ra trước khi đẩy lên YouTube.

#### 3. Kích hoạt ⚡️
- Bấm **"Test workflow"** (`When clicking ‘Test workflow’`) bằng một dòng dữ liệu mẫu trong Google Sheets để kiểm tra toàn bộ luồng chạy.
- Sau khi test thành công, bật **Active workflow** và cấu hình `Schedule Trigger` (khuyến nghị đặt khoảng thời gian chạy định kỳ là 5 phút/lần để kiểm tra và xử lý video mới).

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo Telegram/Slack:** Thêm node gửi tin nhắn thông báo mỗi khi video được tạo thành công hoặc khi xảy ra lỗi API.
- **Mở rộng đa nền tảng:** Tận dụng Upload-Post API để nhân bản video tự động đăng lên TikTok, Instagram Reels hoặc Facebook Shorts cùng lúc.
- **Lưu log lỗi:** Thêm nhánh xử lý lỗi (`Error Trigger`) để ghi nhận lại các prompt bị lỗi render vào mộtsheet riêng biệt giúp dễ dàng kiểm tra.

### 📌 Kết luận
Với workflow n8n tích hợp AI Veo3 này, các sếp đã có thể tự động hóa hoàn toàn một "studio sản xuất video mini" chạy ngầm 24/7. Hãy áp dụng ngay để tối ưu hóa hiệu suất làm marketing và tiết kiệm hàng đống thời gian!