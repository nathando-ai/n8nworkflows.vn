---
title: "🚀 Tự động tạo video AI với OpenAI Sora 2 và Google Drive bằng n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình tạo video bằng trí tuệ nhân tạo OpenAI Sora 2, kiểm tra trạng thái và lưu trữ trực tiếp lên Google Drive."
slug: "tu-dong-tao-video-ai-openai-sora-2-google-drive"
tags: [n8n, automation, no-code, openai, sora, google-drive, ai-video]
keywords: [n8n workflow, tự động hóa tạo video, openai sora 2, google drive automation, ai content creation]
---

# 🚀 Tự động tạo video AI với OpenAI Sora 2 và Google Drive

Việc sản xuất nội dung video ngắn cho TikTok, Reels hay YouTube Shorts thường tốn rất nhiều thời gian từ khâu lên ý tưởng, render video cho đến quản lý file. Khi làm thủ công, các sếp thường phải mất hàng giờ chờ đợi render, tải xuống rồi lại upload lên Google Drive để lưu trữ. 

Giải pháp dưới đây sẽ giúp các sếp tự động hóa 100% quy trình này: Chỉ cần điền prompt vào một Form, hệ thống sẽ gọi API OpenAI Sora 2 để tạo video, tự động kiểm tra trạng thái hoàn thành, tải xuống và lưu trữ gọn gàng kèm thumbnail lên Google Drive. Không cần biết lập trình, chỉ cần kéo thả và cấu hình!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Tự động hóa toàn bộ quy trình từ tạo yêu cầu đến lưu trữ file mà không cần thao tác thủ công.
- **Tích hợp thông minh:** Kết hợp linh hoạt giữa OpenAI Sora 2 API và Google Drive OAuth2.
- **Quản lý chuyên nghiệp:** Tự động tạo video, ảnh thumbnail và sắp xếp file gọn gàng trên Google Drive theo từng chiến dịch.
- **Hoạt động liên tục 24/7:** Form đầu vào tiện lợi giúp team marketing dễ dàng sử dụng mọi lúc mọi nơi.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Cloud hoặc Self-hosted).
- Tài khoản OpenAI có quyền truy cập API Sora 2 (`Settings`: chọn model `sora-2` hoặc `sora-2-pro`).
- Tài khoản Google Drive để cấu hình OAuth2 Credentials.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow hoặc sao chép toàn bộ mã JSON từ n8n và dán trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy trơn tru, các sếp cần cấu hình chính xác các node sau:

- **On form submission (`formTrigger`):** Thiết lập giao diện form đầu vào để người dùng nhập prompt, lựa chọn model (Sora 2 / Sora 2 Pro), kích thước, thời lượng và ảnh tham khảo (Reference).
- **Settings (`set`):** Cấu hình các tham số mặc định cho video:
  - *Model:* `sora-2` ($0.1/sec) hoặc `sora-2-pro` ($0.3 - $0.5/sec).
  - *Size:* Portrait (720x1280, 1024x1792) hoặc Landscape (1280x720, 1792x1024).
  - *Duration:* 4, 8, hoặc 12 giây (Mặc định: 4).
- **Create Video A / Create Video B (`httpRequest`):** Điền API Key của OpenAI và endpoint chính xác để gửi yêu cầu khởi tạo video dựa theo prompt.
- **Check Status & Wait (`httpRequest` & `wait`):** Node `Wait` sẽ tạm dừng luồng xử lý trong giây lát để chờ OpenAI render video, sau đó node `Check Status` gọi API kiểm tra trạng thái video.
- **Upload Video & Upload Thumbnail (`googleDrive`):** Kết nối tài khoản Google Drive thông qua `googleDriveOAuth2Api` để chọn thư mục đích lưu trữ video và ảnh thumbnail sau khi render thành công.
- **Completed & Failed (`form`):** Trả về thông báo thành công hoặc thất bại trực tiếp lên màn hình form của người gửi yêu cầu.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) bằng một prompt ngắn để kiểm tra kết nối API và Google Drive.
- Sau khi test thành công, gạt công tắc sang **Active** để đưa workflow vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo Telegram/Slack:** Thêm một node Telegram hoặc Slack ở cuối workflow để nhận thông báo ngay khi video được render xong và sẵn sàng trên Google Drive.
- **Lưu lịch sử vào Google Sheets:** Thêm node Google Sheets để lưu lại Prompt, ID video, thời gian tạo và link Google Drive nhằm quản lý kho content dễ dàng hơn.
- **Mở rộng đa nền tảng:** Tự động đăng tải video trực tiếp lên TikTok hoặc YouTube ngay sau khi upload thành công lên Google Drive.

### 📌 Kết luận
Với workflow tự động hóa OpenAI Sora 2 và Google Drive này, việc sản xuất video AI giờ đây trở nên tự động và chuyên nghiệp hơn bao giờ hết. Hãy "lên đồ" ngay cho hệ thống n8n của các sếp để tối ưu hóa hiệu suất làm content ngay hôm nay!