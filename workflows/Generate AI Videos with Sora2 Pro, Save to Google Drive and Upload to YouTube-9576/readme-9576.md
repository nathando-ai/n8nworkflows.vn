---
title: "🚀 Tự động hóa sản xuất video AI với Sora2 Pro, Google Drive và YouTube"
description: "Hướng dẫn xây dựng workflow n8n tự động tạo video bằng Sora2 Pro từ Google Sheets, lưu trữ vào Google Drive, tối ưu tiêu đề bằng OpenAI và tự động đăng lên YouTube."
slug: "tu-dong-hoa-tao-video-ai-sora2-pro-google-drive-youtube"
tags: [n8n, automation, no-code, ai-video, youtube-automation, google-sheets]
keywords: [n8n workflow, sora2 pro, tự động tạo video ai, upload youtube tự động, google drive automation]
---

# 🚀 Tự động hóa sản xuất video AI với Sora2 Pro, Google Drive và YouTube

Các sếp có đang cảm thấy quá tải khi mỗi ngày phải nghĩ ý tưởng, viết prompt, tạo video AI, tải về rồi lại thủ công up lên Google Drive và kênh YouTube không? Việc này ngốn vô số thời gian và dễ làm gián đoạn sự tập trung.

Workflow n8n này chính là giải pháp tự động hóa 100% không cần code (No-code), giúp các sếp quản lý toàn bộ quy trình chỉ từ một bảng Google Sheets duy nhất. Hệ thống sẽ tự động lấy prompt, gọi API tạo video từ **Sora2 Pro** (thông qua fal.ai), kiểm tra trạng thái, lưu video vào **Google Drive**, nhờ OpenAI tối ưu tiêu đề và **tự động xuất bản lên YouTube**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không sợ sập, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Chỉ cần nhập prompt và thời lượng vào Google Sheets, hệ thống lo phần còn lại.
- **Tiết kiệm 90% thời gian:** Không còn cảnh download/upload thủ công từng video hàng ngày.
- **Tối ưu hóa SEO video:** Sử dụng OpenAI để sinh tiêu đề hấp dẫn tự động trước khi đẩy lên YouTube.
- **Vận hành liên tục 24/7:** Kết hợp Schedule Trigger để hệ thống tự động sản xuất nội dung đều đặn theo lịch trình.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API sau:
1. **Google Sheets & Google Drive:** Tài khoản Google và [mẫu Google Sheet quản lý prompt](https://docs.google.com/spreadsheets/d/1pcoY9N_vQp44NtSRR5eskkL5Qd0N0BGq7Jh_4m-7VEQ/edit?usp=sharing).
2. **fal.ai Account:** Để lấy API Key gọi dịch vụ tạo video Sora2 Pro.
3. **OpenAI API Key:** Dành cho node **Generate title** tạo tiêu đề video thông minh.
4. **Upload-Post API:** Dịch vụ hỗ trợ đăng video lên mạng xã hội ([Đăng ký tài khoản tại đây](https://www.upload-post.com/?linkId=lp_144414&sourceId=n3witalia&tenantId=upload-post-app) - miễn phí 10 lượt upload/tháng).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow này, dán trực tiếp vào n8n Editor của mình hoặc import file JSON thông qua giao diện n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 15 nodes được thiết kế chặt chẽ. Các sếp cần cấu hình chính xác các điểm sau:

- **Google Sheets Nodes (`Get new video`, `Update result`, `Update Youtube URL`):** Kết nối tài khoản Google Sheets của các sếp, trỏ tới file Google Sheet quản lý nội dung. Cột cần chú ý: `PROMPT` (mô tả video), `DURATION` (độ dài video) và cột `VIDEO` (lưu kết quả trả về).
- **Node `Create Video` & `Get status` (HTTP Request):** 
  - Cấu hình **Header Auth** với API Key lấy từ [fal.ai](https://fal.ai/).
  - Định dạng: 
    - Name: `Authorization`
    - Value: `Key YOURAPIKEY` (Thay `YOURAPIKEY` bằng key thực tế).
- **Node `Generate title` (OpenAI):** Thêm OpenAI API Credentials và thiết lập prompt yêu cầu AI tạo tiêu đề video thu hút dựa trên nội dung đầu vào.
- **Node `Upload Video` (Google Drive):** Kết nối tài khoản Google Drive OAuth2 để hệ thống tự động tải file video về kho lưu trữ cá nhân.
- **Node `HTTP Request` (Phần Upload YouTube qua Upload-Post):**
  - Cấu hình **Auth Header**:
    - Name: `Authorization`
    - Value: `Apikey YOUR_API_KEY_HERE` (Lấy từ trang quản lý API của [Upload-Post](https://www.upload-post.com/?linkId=lp_144414&sourceId=n3witalia&tenantId=upload-post-app)).
  - Thiết lập profile tài khoản mạng xã hội của các sếp (`YOUR_USERNAME` như `test1` hoặc `test2` đã tạo trên nền tảng).

#### 3. Kích hoạt ⚡️
- Bấm **Test workflow** để chạy thử một hàng dữ liệu từ Google Sheets và kiểm tra xem video có được tạo thành công không.
- Bật **Schedule Trigger** (khuyên dùng chu kỳ 5 phút/lần hoặc tùy chỉnh theo nhu cầu) để hệ thống tự động quét sheet và xử lý video mới.
- Bật công tắc **Active** góc trên cùng bên phải để workflow chính thức vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm một node Telegram hoặc Slack vào cuối chuỗi để nhận thông báo ngay khi video được upload thành công lên YouTube.
- **Log lỗi chuyên nghiệp:** Thêm nhánh `Error Trigger` để ghi lại các lỗi phát sinh (ví dụ: lỗi gọi API Sora2 Pro quá hạn mức) vào một sheet riêng biệt để dễ kiểm tra.
- **Mở rộng nền tảng:** Ngoài YouTube, các sếp có thể tận dụng Upload-Post để đẩy đồng thời video lên TikTok, Instagram Reels hoặc Facebook.

### 📌 Kết luận
Workflow tự động hóa Sora2 Pro kết hợp Google Drive và YouTube này là chìa khóa giúp các nhà sáng tạo nội dung và Marketer tối ưu hóa năng suất, giải phóng hoàn toàn sức lao động khỏi các tác vụ thủ công. Hãy triển khai ngay hôm nay để biến ý tưởng thành video triệu view một cách tự động!