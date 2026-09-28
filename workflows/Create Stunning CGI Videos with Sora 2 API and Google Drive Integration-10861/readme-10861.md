---
title: "🎬 Tự Động Hóa Sáng Tạo Video CGI Đẹp Mắt với Sora 2 API + Google Drive - Không Cần Code!"
description: "Tự động hóa quy trình tạo video CGI chuyên nghiệp từ khung cảnh văn bản (prompt) đến chia sẻ ngay trên Google Drive chỉ trong vài phút. Giảm thời gian sản xuất 90% và nâng cao chất lượng nội dung marketing cho doanh nghiệp."
slug: "tieu-dong-hoa-tao-video-cgi-sora-2-google-drive"
tags: [n8n, automation, no-code, ai-generative, content-creation, google-drive, sora-ai]
keywords: [tự động hóa video cgi, sora 2 api, google drive automation, tạo video từ prompt, no-code workflow, tự động hóa marketing]
---

# 🚀 **Tự Động Hóa Tạo Video CGI Đẹp Mắt với Sora 2 API + Google Drive**

### **Giải Phóng Tay Các Sếp!**
Hãy tưởng tượng: chỉ với một **bài viết ngắn** (hoặc prompt) từ các sếp, hệ thống tự động tạo ra **video CGI chuyên nghiệp**, sau đó **tải lên Google Drive** và **gửi link ngay cho khách hàng** – **không cần biên tập, không cần kỹ sư AI, không cần code!**

Workflow này **tích hợp Sora 2 API** (mô hình AI tiên tiến của Meta) với **Google Drive** để tự động hóa toàn bộ quy trình từ **nghĩ ra ý tưởng** đến **chia sẻ video hoàn chỉnh** – **tiết kiệm thời gian lên đến 90%** so với cách làm thủ công!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ **ngày làm thủ công** xuống còn **vài phút** cho mỗi video.
- **Chất lượng chuyên nghiệp**: Video CGI **đẹp mắt, động như thật**, phù hợp cho quảng cáo, training video, hoặc nội dung marketing.
- **Tự động chia sẻ**: Video **tự động tải lên Google Drive** và **gửi link qua email** cho khách hàng/ký giả.
- **Hoạt động liên tục**: Không cần can thiệp người dùng – **chạy 24/7** mà không lo lỗi.
- **Cá nhân hóa**: Mỗi video đều **được tạo riêng** từ prompt của các sếp, không cần sao chép.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Sora 2 API**:
   - Đăng ký API key từ [Sora Developer Portal](https://sora.ai/) (nếu chưa có).
   - **Lưu ý**: Sora 2 hiện đang trong **phases closed beta**, các sếp cần liên hệ Meta hoặc đối tác để được cấp API key.

2. **Tài khoản Google Drive OAuth 2.0**:
   - Cài đặt **Google Drive API** và tạo **OAuth 2.0 credentials** trong [Google Cloud Console](https://console.cloud.google.com/).
   - **Quyền cần cấp**: `https://www.googleapis.com/auth/drive.file` (để upload và chia sẻ file).

3. **Tài khoản SMTP (để gửi email thông báo)**:
   - Các sếp có thể dùng **Gmail SMTP** (mặc định) hoặc **dịch vụ email doanh nghiệp** như SendGrid, Mailgun.
   - **Cần cấu hình**:
     - Host: `smtp.gmail.com`
     - Port: `465` (hoặc `587` cho TLS)
     - Username/Password: **App Password** (nếu dùng Gmail, cần bật **2FA** và tạo mật khẩu ứng dụng).

4. **Form Submission (để kích hoạt workflow)**:
   - Các sếp có thể dùng **Google Form**, **Typeform**, hoặc **n8n Form Trigger** để người dùng nhập **prompt** (ví dụ: *"Một cảnh quảng cáo cho sản phẩm xanh lá cây, phong cách futuristic"*).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể **import workflow** từ file JSON hoặc **copy/paste JSON** vào **n8n Editor**:
1. Tải file JSON từ [link gốc](https://n8n.io/workflows/10861) hoặc **sao chép toàn bộ mã JSON** từ trang này.
2. Trong **n8n Editor**, nhấn **Import Workflow** và dán JSON vào.
3. **Kích hoạt workflow** bằng cách bật **Active** ở góc trên bên phải.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này **phức tạp** vì liên quan đến **API Sora 2** và **Google Drive**, nên các sếp **cần chú ý các node sau**:

##### **A. Node "On form submission" (formTrigger)**
- **Cấu hình**:
  - Chọn **Google Form** hoặc **n8n Form Trigger** làm nguồn kích hoạt.
  - **Trường cần bắt buộc**: `prompt` (để gửi cho Sora API).
  - **Lưu ý**: Nếu dùng **Google Form**, các sếp cần **cấu hình Webhook** để n8n nhận được dữ liệu.

##### **B. Node "Sora API Processor" (httpRequest)**
- **Cấu hình API Request**:
  - **Method**: `POST`
  - **URL**: `https://api.sora.ai/v1/tasks` (hoặc URL chính thức từ Sora).
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer YOUR_SORA_API_KEY",
      "Content-Type": "application/json"
    }
    ```
  - **Body (JSON)**:
    ```json
    {
      "prompt": "{{$node["On form submission"].json["prompt"]}}",
      "task_type": "video",
      "duration": 5  // (giây, tùy chỉnh)
    }
    ```
  - **Lưu ý**:
    - **Không bỏ qua API key** – nếu thiếu, API sẽ trả về lỗi.
    - **Prompt phải rõ ràng** (ví dụ: *"Một cảnh quảng cáo cho sản phẩm xanh lá cây, phong cách futuristic, chất lượng 4K"*).

##### **C. Node "Condition: Check Prediction Id" (if)**
- **Cấu hình**:
  - **If**: `$node["Sora API Processor"].json["prediction_id"]` **không tồn tại** → **gửi email lỗi**.
  - **Else**: Tiếp tục xử lý.
  - **Lưu ý**: Nếu API trả về `prediction_id` trống, workflow sẽ **tự động gửi email thông báo lỗi** (xem phần **Email Error Handling** dưới đây).

##### **D. Node "Wait for API Response" & "Wait for Task to Complete" (wait)**
- **Thời gian chờ**:
  - **60 giây** sau khi gọi API (để Sora xử lý).
  - **60 giây** sau đó để **check status** của task.
  - **Lưu ý**: Nếu video dài (ví dụ: 10 giây), các sếp có thể **tăng thời gian chờ** (ví dụ: 120 giây).

##### **E. Node "API Request: Check Task Status" (httpRequest)**
- **Cấu hình**:
  - **Method**: `GET`
  - **URL**: `https://api.sora.ai/v1/tasks/{{$node["Sora API Processor"].json["prediction_id"]}}`
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer YOUR_SORA_API_KEY"
    }
    ```
  - **Lưu ý**: **Không thay đổi URL** – nếu sai, API sẽ trả về lỗi 404.

##### **F. Node "Condition: Task Output Status" (switch)**
- **Cấu hình**:
  - **Case 1**: `status === "completed"` → **tải video và upload lên Google Drive**.
  - **Case 2**: `status === "failed"` → **gửi email lỗi**.
  - **Case 3**: `status === "processing"` → **chờ tiếp (vòng lặp)**.
  - **Lưu ý**:
    - Nếu task **failed**, workflow sẽ **tự động gửi email thông báo** (xem phần **Email Error Handling**).
    - Nếu task **processing**, workflow sẽ **chờ 60 giây** rồi check lại.

##### **G. Node "Download Video" (httpRequest)**
- **Cấu hình**:
  - **Method**: `GET`
  - **URL**: `{{$node["API Request: Check Task Status"].json["output_url"]}}`
  - **Headers**: Không cần thêm (nếu API yêu cầu, thêm `Authorization`).
  - **Lưu ý**:
    - **Output URL** được lấy từ **API response** của Sora.
    - **File video** sẽ được **tải về tạm thời** trước khi upload lên Google Drive.

##### **H. Node "Upload File to Google Drive" (googleDrive)**
- **Cấu hình**:
  - **Action**: `uploadFile`
  - **File**: `$node["Download Video"].json["body"]` (file video đã tải về).
  - **Folder ID**: **Tùy chọn** (nếu muốn upload vào thư mục cụ thể).
  - **File Name**: `CGI_${$node["On form submission"].json["prompt"].substring(0,30)}.mp4` (để tránh trùng tên).
  - **Lưu ý**:
    - **Credentials**: Chọn **googleDriveOAuth2Api** đã cấu hình trước.
    - **File sẽ được upload vào Google Drive** và **sẵn sàng chia sẻ**.

##### **I. Node "Set Google Drive Permissions" (googleDrive)**
- **Cấu hình**:
  - **Action**: `share`
  - **Resource**: `file`
  - **File ID**: `$node["Upload File to Google Drive"].json["id"]`
  - **Email Addresses**: `{{$node["On form submission"].json["email"]}}` (địa chỉ email của người nhận).
  - **Permissions**: `reader` (hoặc `commenter` nếu muốn cho phép chỉnh sửa).
  - **Lưu ý**:
    - **Email của người nhận** phải được lấy từ **form submission** (ví dụ: trường `email` trong Google Form).
    - **File sẽ được chia sẻ với quyền đọc** (hoặc tùy chỉnh theo yêu cầu).

##### **J. Node "Send an email: Video Link" (emailSend)**
- **Cấu hình**:
  - **To**: `$node["On form submission"].json["email"]`
  - **Subject**: `🎬 Video CGI của bạn đã sẵn sàng!`
  - **Body (HTML)**:
    ```html
    <p>Xin chào,</p>
    <p>Video CGI của bạn đã được tạo thành công!</p>
    <p><a href="https://drive.google.com/file/d/{{$node["Upload File to Google Drive"].json["webViewLink"]}}/view?usp=sharing">Xem video</a></p>
    <p>Nếu có vấn đề, hãy liên hệ admin.</p>
    ```
  - **Lưu ý**:
    - **Link Google Drive** được lấy từ **webViewLink** của file đã upload.
    - **Email sẽ tự động gửi** khi video hoàn tất.

##### **K. Node "Clean Output" (code)**
- **Cấu hình**:
  - **JavaScript**:
    ```javascript
    // Xóa các trường không cần thiết trong output
    return {
      ...node.input,
      output: {
        videoUrl: `$node["Upload File to Google Drive"].json["webViewLink"]`,
        taskId: `$node["Sora API Processor"].json["prediction_id"]`,
        status: "success"
      }
    };
    ```
  - **Lưu ý**: **Không xóa node này** – nó giúp **định dạng output** cho dễ theo dõi.

##### **L. Node "Send Email: API Error - Task ID Missing" & "Send Email: API Error - Task Failed" (emailSend)**
- **Cấu hình chung**:
  - **To**: `admin@example.com` (hoặc email của các sếp).
  - **Subject**: `⚠️ Lỗi trong quá trình tạo video CGI`
  - **Body**:
    ```html
    <p>Lỗi xảy ra khi tạo video:</p>
    <p><strong>Lỗi: {{$node["Condition: Check Prediction Id"].json["error"]}}</strong></p>
    <p>Prompt: {{$node["On form submission"].json["prompt"]}}</p>
    ```
  - **Lưu ý**:
    - **Email này sẽ tự động gửi** khi có lỗi (thiếu `prediction_id` hoặc task `failed`).
    - **Các sếp cần theo dõi email này** để khắc phục vấn đề.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tích Hợp Slack/Telegram Notifications**:
   - Thay vì chỉ gửi email, các sếp có thể **gửi thông báo qua Slack/Telegram** khi video hoàn tất.
   - **Cách làm**:
     - Thêm **node `slack`** hoặc **`telegram`** sau node `Upload File to Google Drive`.
     - **Body message**:
       ```json
       {
         "text": `Video CGI đã sẵn sàng!\nLink: {{$node["Upload File to Google Drive"].json["webViewLink"]}}`
       }
       ```

2. **Lưu Log Tất Cả Các Task**:
   - Thêm **node `googleSheets`** để **ghi lại tất cả các task** (prompt, task ID, status, thời gian hoàn tất).
   - **Cách làm**:
     - Tạo một **Google Sheet** mới với các cột: `Prompt`, `Task ID`, `Status`, `Created At`, `Completed At`.
     - Thêm **node `googleSheets`** sau node `Clean Output` với **action `addRow`**.

3. **Tự Động Xóa Video Sau Thời Gian**:
   - Nếu video chỉ cần tồn tại **vài ngày**, các sếp có thể **tự động xóa** sau khi người dùng xem.
   - **Cách làm**:
     - Thêm **node `googleDrive`** với **action `deleteFile`** sau khi người dùng **click vào link**.
     - **Sử dụng Webhook** từ Google Drive để kích hoạt node này khi file được mở.

4. **Tăng Cường Prompt với AI**:
   - Nếu