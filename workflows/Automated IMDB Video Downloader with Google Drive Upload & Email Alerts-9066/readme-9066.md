---
title: "🎬 [Tự Động Hạ Video IMDB Sang Google Drive Và Gửi Email Thông Báo - Không Cần Code!]"
description: "Workflow tự động hóa hoàn chỉnh giúp các sếp tải video từ IMDB (trailer, phim, clip) chỉ với 1 link, tự động upload lên Google Drive và gửi email thông báo kết quả. Giúp tiết kiệm thời gian lên đến 90% so với cách làm thủ công."
slug: "tieu-dong-hua-video-imdb-sang-google-drive"
tags: [n8n, automation, no-code, google-drive, email-notification, content-creation]
keywords: [tự động hóa video imdb, download video từ imdb, google drive tự động, email thông báo download video, workflow n8n content creation]
---

# 🚀 **Tự Động Hạ Video IMDB Sang Google Drive Và Gửi Email Thông Báo - Không Cần Code!**

## **😩 Nỗi Đau Của Các Sếp Khi Làm Thủ Công**
Các sếp trong ngành **content creation**, **marketing**, hoặc **giáo dục** thường phải đối mặt với việc:
- **Tốn thời gian** để tìm kiếm và tải video từ IMDB (trailer, phim, clip) một cách thủ công.
- **Khó quản lý** nhiều file video trên máy tính hoặc cloud, dẫn đến rối loạn và mất mát dữ liệu.
- **Không biết kết quả** download thành công hay thất bại, phải check lại nhiều lần.
- **Không có cách tự động hóa** để gửi thông báo cho đồng nghiệp hoặc khách hàng khi video sẵn sàng.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tải video từ IMDB chỉ với 1 link** (không cần đăng nhập).
✅ **Tự động upload lên Google Drive** với quyền chia sẻ tự động.
✅ **Gửi email thông báo** kết quả (thành công/thất bại) ngay lập tức.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian lên đến 90%** so với cách làm thủ công.
- **Tránh mất file** nhờ tự động backup lên Google Drive.
- **Cá nhân hóa thông báo** với email chi tiết (link download, lỗi nếu có).
- **Hoạt động liên tục** mà không cần can thiệp của con người.
- **Dễ dàng mở rộng** cho nhiều người dùng với form submission.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Drive** (đã cấp quyền OAuth2 cho n8n).
2. **Tài khoản email SMTP** (để gửi thông báo thành công/thất bại).
   - Ví dụ: Gmail (SMTP của Google), SendGrid, hoặc Mailgun.
3. **API Key của RapidAPI** (để lấy thông tin video từ IMDB).
   - **Lấy API Key miễn phí tại [RapidAPI](https://rapidapi.com/)** (tìm kiếm "IMDB Video Downloader").
4. **Form submission** (có thể là Google Form, Typeform, hoặc form đơn giản trên website).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [đây](https://n8n.io/workflows/9066) (hoặc copy JSON từ link trên).
- Mở **n8n Editor** → Nhấn **"Import"** → Dán JSON và nhấn **"Import"**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **9 node chính**, các sếp cần chú ý cấu hình sau:

##### **🔹 Node 1: "On form submission" (formTrigger)**
- **Chức năng:** Khởi động workflow khi người dùng submit form (ví dụ: Google Form).
- **Cấu hình:**
  - Nếu sử dụng **Google Form**, các sếp cần:
    1. Tạo một form với trường **"IMDB Video URL"** (dạng text).
    2. Cấu hình **Webhook** trong Google Form để gửi dữ liệu đến n8n.
    3. **Lưu ý:** Nếu không dùng Google Form, có thể thay bằng **form trên website** hoặc **Typeform**.

##### **🔹 Node 2 & 3: "Fetch IMDB Video Info" & "Check API Response Status" (httpRequest + if)**
- **Chức năng:** Gửi yêu cầu API để lấy thông tin video từ IMDB.
- **Cấu hình:**
  - **API Endpoint:** `https://imdb-video-downloader.p.rapidapi.com/download` (hoặc endpoint tương tự từ RapidAPI).
  - **Headers:**
    ```json
    {
      "x-rapidapi-key": "API_KEY_CỦA_BẠN",
      "x-rapidapi-host": "imdb-video-downloader.p.rapidapi.com"
    }
    ```
  - **Body (JSON):**
    ```json
    {
      "url": "{{ $node["On form submission"].json["imdb_url"] }}"
    }
    ```
  - **Node "if":**
    - **Condition:** `{{ $json["status"] === 200 }}`
    - Nếu thành công → tiếp tục node **Download Video File**.
    - Nếu thất bại → chuyển sang node **Failure Notification Email**.

##### **🔹 Node 4: "Download Video File" (httpRequest)**
- **Chức năng:** Tải video từ link được API trả về.
- **Cấu hình:**
  - **URL:** `{{ $json["download_url"] }}` (trích từ response API).
  - **Headers:**
    ```json
    {
      "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36"
    }
    ```
  - **Response Format:** Chọn **"Binary"** để tải file video.

##### **🔹 Node 5 & 6: "Upload Video to Google Drive" & "Google Drive Set Permission" (googleDrive)**
- **Chức năng:** Upload video vào Google Drive và chia sẻ link.
- **Cấu hình:**
  - **Credentials:** Chọn **"googleDriveOAuth2Api"** (đã cấu hình trước).
  - **File:** Chọn **"Binary Data"** từ node **Download Video File**.
  - **Folder:** Chọn **"Root"** (hoặc folder cụ thể).
  - **Permission:** Chọn **"Anyone with the link"** (để người dùng có thể truy cập).
  - **Node "Set Permission":**
    - **Resource:** Chọn file vừa upload.
    - **Permission:** `"viewer"` (cho phép xem và tải).

##### **🔹 Node 7 & 8: "Success/Failure Notification Email" (emailSend)**
- **Chức năng:** Gửi email thông báo kết quả.
- **Cấu hình:**
  - **Credentials:** Chọn **"smtp"** (đã cấu hình trước).
  - **Email thành công:**
    - **Subject:** `"Video đã tải thành công! Link: {{ $json["file"]["webViewLink"] }}"`
    - **Body:**
      ```html
      <p>Xin chào,</p>
      <p>Video của bạn đã được tải thành công và đã được upload lên Google Drive.</p>
      <p><a href="{{ $json["file"]["webViewLink"] }}">Truy cập video tại đây</a></p>
      <p>Trân trọng,</p>
      <p>Hệ thống tự động hóa</p>
      ```
  - **Email thất bại:**
    - **Subject:** `"Lỗi khi tải video: {{ $json["error"] }}"`
    - **Body:**
      ```html
      <p>Xin lỗi, quá trình tải video thất bại.</p>
      <p>Lỗi: {{ $json["error"] }}</p>
      <p>Vui lòng kiểm tra lại URL hoặc liên hệ admin.</p>
      ```

##### **🔹 Node 9: "Processing Delay" (wait)**
- **Chức năng:** Thêm thời gian chờ (nếu cần) trước khi gửi email thất bại.
- **Cấu hình:**
  - Thời gian chờ: **5 giây** (để cho phép retry nếu cần).

---

#### **3. Kích Hoạt ⚡️**
- **Test Run:** Nhấn **"Run"** để thử với một URL mẫu (ví dụ: `https://www.imdb.com/video/imdb/vi0000000/`).
- **Active Workflow:** Sau khi kiểm tra thành công, nhấn **"Active"** để workflow hoạt động liên tục.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết hợp với Slack/Telegram:**
   - Thay vì email, các sếp có thể gửi thông báo thành công/thất bại lên **Slack** hoặc **Telegram** bằng node `slackSend` hoặc `telegramSend`.
   - **Cách làm:** Thêm node `slackSend` sau `emailSend` và cấu hình webhook từ Slack.

2. **Lưu log vào Google Sheets:**
   - Thêm node `googleSheets` để ghi lại lịch sử download (URL, thời gian, trạng thái).
   - **Ưu điểm:** Dễ dàng theo dõi và báo cáo.

3. **Gửi báo cáo định kỳ:**
   - Sử dụng node `dateTime` + `set` để tạo báo cáo hàng tuần/month về số lượng video tải thành công/thất bại.
   - **Cách làm:** Thêm node `dateTime` để lấy ngày tháng, sau đó gửi email tổng hợp.

4. **Tự động chia sẻ với nhiều người:**
   - Thay vì chỉ chia sẻ với người submit, các sếp có thể **chia sẻ link Google Drive cho nhiều người** bằng cách thêm node `googleDrive` với quyền `"editor"`.
   - **Áp dụng:** Dành cho nhóm làm content hoặc marketing team.

5. **Cài đặt trên VPS để hoạt động 24/7:**
   - Để workflow chạy liên tục, các sếp nên **self-host n8n trên VPS** (không phụ thuộc vào n8n.io free).
   - **👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)**
   - **👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)**
:::

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn chỉnh** cho các sếp muốn tự động hóa việc tải video từ IMDB, upload lên Google Drive và nhận thông báo ngay lập tức. **Không cần code, không cần kỹ thuật**, chỉ cần cấu hình theo hướng dẫn trên.

**Hành động ngay:**
1. **Import workflow** vào n8n của mình.
2. **Cấu hình các credentials** (Google Drive, SMTP, API Key).
3. **Test với một URL** và bắt đầu tự động hóa!
4. **Mở rộng** với các tính năng nâng cao như Slack, Google Sheets, hoặc báo cáo tự động.

**🚀 Cùng tự động hóa công việc của mình ngay hôm nay!** 🚀