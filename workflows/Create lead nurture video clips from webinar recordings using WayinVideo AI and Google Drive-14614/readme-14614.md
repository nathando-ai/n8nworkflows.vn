---
title: "🚀 Tự Động Hóa Tạo Video Clip Nuôi Dưỡng Lead Từ Webinar Với WayinVideo AI"
description: "Biến video webinar dài thành các clip ngắn hấp dẫn tự động bằng AI, lưu ngay vào Google Drive để gửi email marketing. Không cần cắt ghép thủ công."
slug: "tu-dong-hoa-tao-video-clip-nuoi-duong-lead-wayinvideo"
tags: [n8n, automation, no-code, wayinvideo, google-drive, lead-nurture]
keywords: [n8n workflow, tự động hóa video, wayinvideo api, lead nurture, google drive automation]
---

# 🚀 Tự Động Hóa Tạo Video Clip Nuôi Dưỡng Lead Từ Webinar Với WayinVideo AI

Các sếp có bao giờ cảm thấy đau đầu khi kết thúc một buổi webinar thành công, nhưng lại mất hàng giờ để cắt ghép video, tìm những khoảnh khắc "đỉnh" nhất để làm nội dung nuôi dưỡng lead (lead nurture)? Việc này không chỉ tốn thời gian mà còn dễ bỏ sót những đoạn nội dung giá trị cao.

Workflow này chính là giải pháp "chìa khóa trao tay" giúp các sếp tự động hóa 100% quy trình: Chỉ cần nhập link video webinar, hệ thống sẽ sử dụng **WayinVideo AI** để phân tích, trích xuất các đoạn clip ngắn nhất, hấp dẫn nhất, sau đó tự động tải xuống và lưu vào **Google Drive**. Các sếp chỉ việc lấy link để gửi email hoặc đăng lên mạng xã hội.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, đặc biệt là các tác vụ polling (kiểm tra kết quả) liên tục, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80-90% thời gian biên tập:** AI tự động tìm và cắt các đoạn highlight thay vì con người xem lại toàn bộ video.
- **Tăng tỷ lệ chuyển đổi:** Các clip ngắn, tập trung vào giá trị cốt lõi giúp lead dễ tiếp thu hơn so với video dài.
- **Quy trình liền mạch:** Từ nhận link webinar đến khi file video nằm sẵn trong thư mục Google Drive, không cần thao tác thủ công.
- **Đa dạng định dạng:** Có thể tùy chỉnh độ dài clip (15-30s hoặc 30-60s) và định dạng dọc/ngang tùy theo kênh phân phối.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản WayinVideo:** Cần có API Key (Bearer Token) từ dịch vụ WayinVideo.
2. **Tài khoản Google Drive:** Đã tạo sẵn thư mục (Folder) để lưu trữ các video clip.
3. **Credentials trong n8n:**
   - Tạo credential **Google Drive OAuth2**.
   - Chuẩn bị **API Key** của WayinVideo (sẽ điền trực tiếp vào node HTTP Request).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.
2. Chọn **Import from URL** hoặc **Import from File** (nếu các sếp đã tải file JSON về).
3. Dán link workflow gốc: `https://n8n.io/workflows/14614` hoặc chọn file JSON đã tải.
4. Sau khi import, các sếp sẽ thấy 8 nodes được kết nối sẵn theo luồng logic.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

Đây là phần quan trọng nhất. Các sếp cần kiểm tra kỹ các node sau:

**Node 1: `1. Form — Webinar URL + Details`**
- Đây là node tạo form nhập liệu. Các sếp có thể chỉnh sửa các trường dữ liệu (ví dụ: thêm trường "Tên khách hàng" nếu muốn cá nhân hóa).
- Đảm bảo form đang ở trạng thái **Active** để có thể lấy URL form chia sẻ.

**Node 2: `2. WayinVideo — Submit Clipping Task1`**
- **Hành động:** Gửi yêu cầu tạo clip lên API WayinVideo.
- **Cấu hình:**
  - Tìm phần **Headers** hoặc **Body** (tùy cấu trúc API).
  - Thay thế chuỗi `YOUR_WAYINVIDEO_API_KEY` bằng **API Key** thật của các sếp.
  - Kiểm tra tham số `target_duration`: Mặc định có thể là 30-60s. Nếu muốn clip ngắn cho TikTok/Reels, đổi sang `DURATION_15_30`.
  - Kiểm tra `enable_ai_reframe`: Đặt `true` nếu muốn AI tự căn khung hình dọc (9:16) cho mobile.

**Node 3: `3. Wait — 45 Seconds`**
- Node này chờ 45 giây trước khi kiểm tra kết quả lần đầu.
- **Lưu ý:** Nếu video webinar quá dài (trên 2 giờ), các sếp có thể tăng thời gian chờ lên 60-90 giây để tránh gọi API quá dày.

**Node 4: `4. WayinVideo — Poll Clip Results`**
- **Hành động:** Kiểm tra trạng thái xử lý của task.
- **Cấu hình:**
  - Tương tự Node 2, đảm bảo **API Key** đã được điền đúng.
  - Node này sẽ được gọi lặp lại (loop) cho đến khi có kết quả.

**Node 5: `5. If — Clips Ready Check`**
- **Logic:** Kiểm tra xem API đã trả về trạng thái "Completed" chưa.
- **Cấu hình:**
  - **True Branch:** Chuyển sang Node 6 (Xử lý kết quả).
  - **False Branch:** Quay lại Node 3 (Chờ tiếp).
  - ⚠️ **Cảnh báo quan trọng:** Workflow gốc có rủi ro **vòng lặp vô hạn** nếu API lỗi hoặc link video không hợp lệ. Các sếp nên thêm một node **Set** (đếm số lần retry) và một node **If** thứ hai để giới hạn số lần kiểm tra (ví dụ: tối đa 10-15 lần). Nếu vượt quá, chuyển sang nhánh "Error" để gửi thông báo lỗi.

**Node 6: `6. Code — Extract Clips Array1`**
- **Hành động:** Dùng JavaScript để tách mảng các clip từ response của API.
- **Cấu hình:** Thường không cần chỉnh sửa gì đặc biệt, nhưng các sếp có thể kiểm tra code để đảm bảo nó lấy đúng trường dữ liệu chứa link video (ví dụ: `clips` hoặc `results`).

**Node 7: `7. HTTP — Download Clip File`**
- **Hành động:** Tải file video thực tế từ link mà API cung cấp.
- **Cấu hình:** Đảm bảo node này nhận đúng link từ Node 6.

**Node 8: `8. Google Drive — Upload Clip1`**
- **Hành động:** Upload file video vừa tải lên Google Drive.
- **Cấu hình:**
  - Chọn **Credential**: Chọn credential **Google Drive OAuth2** đã tạo.
  - **Folder ID**: Thay thế `YOUR_GOOGLE_DRIVE_FOLDER_ID` bằng ID thư mục đích.
    - *Cách lấy ID:* Mở thư mục trong Google Drive, nhìn vào URL. Phần sau `/folders/` chính là Folder ID.
  - **File Name**: Có thể cấu hình để đặt tên file tự động dựa trên tên webinar hoặc thời gian.

#### 3. Kích hoạt ⚡️
1. **Test Run:**
   - Nhấn vào Node 1 (Form) và chọn **Execute Node**.
   - Một form sẽ hiện ra. Điền một link video YouTube hoặc file video công khai bất kỳ.
   - Nhấn **Submit**.
   - Quan sát workflow chạy: Nó sẽ chờ 45s, kiểm tra, và cuối cùng upload file lên Drive.
2. **Bật Active:**
   - Sau khi test thành công, nhấn nút **Active** ở góc trên bên phải.
   - Copy **Form URL** từ Node 1 để chia sẻ cho team hoặc nhúng vào trang web.

### ✍️ Mẹo & gợi ý nâng cao
- **Tự động gửi Email:** Sau Node 8 (Upload Drive), các sếp có thể thêm node **Gmail** hoặc **Mailchimp** để tự động gửi link video clip cho lead ngay khi video được tạo xong. Đây là cách "nuôi dưỡng" lead cực kỳ hiệu quả.
- **Cảnh báo lỗi:** Như đã đề cập, hãy thêm cơ chế đếm số lần retry. Nếu sau 15 lần kiểm tra (khoảng 11 phút) mà vẫn chưa có kết quả, hãy gửi thông báo qua **Slack** hoặc **Telegram** để các sếp biết link video có vấn đề.
- **Đa dạng nội dung:** Tạo nhiều workflow hoặc thêm logic phân nhánh để tạo 2 phiên bản: 1 clip ngắn 15s (cho Social Media) và 1 clip dài 60s (cho Email/Website).
- **Lưu Log:** Thêm node **Google Sheets** để ghi lại lịch sử: Link webinar gốc, thời gian tạo, link các clip đã tạo. Giúp các sếp dễ dàng theo dõi hiệu quả nội dung.

### 📌 Kết luận
Việc biến một video webinar dài lê thê thành các "viên ngọc quý" ngắn gọn để tiếp cận khách hàng là một lợi thế cạnh tranh lớn. Với workflow này, các sếp không cần phải là chuyên gia video editing, chỉ cần có một chút kiến thức về n8n và API, các sếp đã có thể tự động hóa toàn bộ quy trình tạo nội dung video.

Hãy thử ngay workflow này để giải phóng thời gian biên tập và tập trung vào chiến lược marketing của mình! 🚀