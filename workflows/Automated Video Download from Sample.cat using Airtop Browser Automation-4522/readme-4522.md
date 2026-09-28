---
title: "🎬 Tự Động Hạ Tải Video từ Sample.cat bằng Airtop.ai – Không Cần Code!"
description: "Giải pháp tự động hóa 100% không code để tải video từ bất kỳ trang web nào, đặc biệt là Sample.cat, tiết kiệm thời gian và tránh thủ công sai sót. Dùng Airtop Browser Automation kết hợp n8n để tự động hóa quá trình tải video, phù hợp cho content creator, marketer hoặc IT ops."
slug: "tự-dộng-hạ-tải-video-samplecat-airtop-n8n"
tags: [n8n, automation, no-code, airtop, browser-automation, it-ops]
keywords: [tự động hóa tải video, airtop n8n, tự động hóa web scraping, tải video tự động, sample.cat, không cần code]
---

# 🚀 **Tự Động Hạ Tải Video từ Sample.cat bằng Airtop.ai trên n8n – Không Cần Code!**

## 🔥 **Nỗi Đau Của Các Sếp**
Bạn có bao giờ phải **tải video từ Sample.cat** (hoặc bất kỳ trang web nào khác) **một cách thủ công**? Thời gian mất đi, dễ bị sai sót, và nếu phải làm hàng loạt video, công việc trở nên **mệt mỏi và tốn kém**. Đặc biệt với những người làm **content creator, marketer, hoặc IT ops**, việc tự động hóa quá trình này là **cần thiết** để tiết kiệm thời gian và nâng cao hiệu suất.

**Giải pháp này giúp:**
✅ **Tải video tự động** từ Sample.cat (hoặc bất kỳ trang web nào) **không cần code**.
✅ **Không bị chặn CAPTCHA** nhờ Airtop Browser Automation – công nghệ **tương tự như con người** khi tương tác với trang web.
✅ **Hoạt động 24/7** trên VPS riêng, không phụ thuộc vào máy tính cá nhân.
✅ **Dễ dàng mở rộng** để tải nhiều video từ nhiều trang web khác nhau.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không phải làm thủ công mỗi lần tải video.
- **Chính xác 100%**: Không bị lỗi do người dùng nhấn sai hoặc quên tải.
- **Hoạt động liên tục**: Chạy tự động trên VPS, không cần phải mở máy tính.
- **Dễ dàng mở rộng**: Có thể tự động hóa tải video từ nhiều trang web khác nhau.
- **Không bị chặn**: Airtop mô phỏng hành vi người dùng, tránh bị chặn CAPTCHA.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow này, các sếp cần chuẩn bị:
1. **Tài khoản Airtop** và **API Key**:
   - Đăng ký tại [Airtop Portal](https://portal.airtop.ai/) để lấy **API Key**.
   - Cài đặt **credentials** trong n8n với tên `airtopApi` và gán API Key tương ứng.
2. **n8n Self-hosted** (khuyến nghị):
   - Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng**.
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể **import workflow** từ file JSON hoặc **copy/paste JSON** vào n8n Editor:
1. **Tải file JSON** từ [link gốc](https://n8n.io/workflows/4522).
2. Trong n8n Dashboard, chọn **Import Workflow** và chọn file JSON.
3. **Hoặc** copy toàn bộ JSON và paste vào **Create Workflow** → **Import JSON**.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này sử dụng **Airtop Browser Automation**, vì vậy các sếp cần **cấu hình chính xác** các node sau:

##### **🔹 Node "Session" (Khởi tạo phiên browser)**
- **Credentials**: Chọn `airtopApi` (đã cài đặt API Key trước đó).
- **Không cần chỉnh sửa thêm** (Airtop sẽ tự động tạo phiên mới).

##### **🔹 Node "Window" (Mở trang web)**
- **Credentials**: Chọn `airtopApi`.
- **Key Parameters**:
  - `resource: window`
  - **URL cần mở**: `https://sample.cat/en/webm` (để tải video mẫu).
  - *Lưu ý*: Nếu muốn tải từ trang khác, **cập nhật URL** tại đây.

##### **🔹 Node "Click on download button" (Nhấn nút tải)**
- **Credentials**: Chọn `airtopApi`.
- **Key Parameters**:
  - `resource: interaction`
  - **Lệnh nhấn nút**: Airtop sẽ tự động **tìm và nhấn nút tải video** có tiêu đề:
    > *"SD 640x360 (Seawater, drone view video, 30 FPS)"*
  - *Lưu ý*: Nếu trang web thay đổi, **cần cập nhật tiêu đề** hoặc **sử dụng selector CSS** (nếu có).

##### **🔹 Node "Wait" (Đợi file sẵn sàng)**
- Thời gian mặc định: **10 giây** (đủ để file tải xong).
- *Lưu ý*: Nếu file tải chậm, có thể **tăng thời gian** hoặc **thêm logic lặp lại** (xem phần **Mẹo & Gợi Ý Nâng Cao**).

##### **🔹 Node "Get file data" (Kiểm tra file có sẵn)**
- **Credentials**: Chọn `airtopApi`.
- **Key Parameters**:
  - `resource: file`
- **Lưu ý**: Node này **kiểm tra trạng thái file** trước khi tải. Nếu file chưa sẵn sàng, workflow sẽ **dừng lại**.

##### **🔹 Node "Download file" (Tải file)**
- **Credentials**: Chọn `airtopApi`.
- **Key Parameters**:
  - `operation: get`
  - `resource: file`
- **Lưu ý**: File sẽ được tải về **tạm thời** trong phiên Airtop. Các sếp cần **cấu hình lưu trữ** (xem phần **Mẹo & Gợi Ý Nâng Cao**).

##### **🔹 Node "Terminate" (Kết thúc phiên)**
- **Credentials**: Chọn `airtopApi`.
- **Key Parameters**:
  - `operation: terminate`
- **Lưu ý**: **Bắt buộc** để **giải phóng tài nguyên** và tránh phí không cần thiết.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chọn **Run Workflow** và kiểm tra **log** để đảm bảo không có lỗi.
   - Nếu file tải thành công, sẽ xuất hiện **link download** trong node "Download file".
2. **Bật Active**:
   - Sau khi test thành công, **bật Active** để workflow chạy tự động khi kích hoạt.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Thêm Logic Lặp Lại (Retry) cho File Chậm**:
   - Sử dụng **node `Wait` + `Set`** để **lặp lại kiểm tra file** cho đến khi trạng thái là `available`.
   - Ví dụ:
     ```json
     {
       "operation": "set",
       "property": "fileStatus",
       "value": "$json[\"status\"]"
     }
     ```
     Sau đó, **sử dụng node `if`** để lặp lại nếu `fileStatus !== "available"`.

2. **Lưu File Vào Cloud Storage (Google Drive, Dropbox, S3)**:
   - Sau khi tải xong, **sử dụng node `HTTP Request`** để gửi file lên cloud.
   - Ví dụ với **Google Drive**:
     ```json
     {
       "operation": "request",
       "method": "POST",
       "url": "https://www.googleapis.com/upload/drive/v3/files?uploadType=media",
       "headers": {
         "Authorization": "Bearer $googleDriveToken"
       },
       "body": "$fileData"
     }
     ```

3. **Tự Động Tải Nhiều Video Từ Nhiều Trang Web**:
   - Sử dụng **node `Set`** để **động态 thay đổi URL** và **tiêu đề button**.
   - Ví dụ:
     ```json
     {
       "operation": "set",
       "property": "url",
       "value": "https://example.com/video2"
     }
     ```

4. **Gửi Thông Báo Khi Tải Xong (Slack/Email/Telegram)**:
   - Sau khi tải xong, **sử dụng node `Slack` hoặc `Email`** để thông báo.
   - Ví dụ với **Slack**:
     ```json
     {
       "operation": "slack",
       "webhookUrl": "$slackWebhook",
       "text": "Video đã tải thành công: $fileName"
     }
     ```

5. **Lưu Log Tải File (Google Sheets/Notion)**:
   - Sử dụng **node `Google Sheets`** để ghi lại **thời gian tải, tên file, trạng thái**.
   - Ví dụ:
     ```json
     {
       "operation": "addRow",
       "sheetName": "VideoDownloads",
       "values": {
         "Time": "$currentDateTime",
         "FileName": "$fileName",
         "Status": "Success"
       }
     }
     ```

---

### 📌 **Kết Luận**
Workflow này **giải quyết hoàn toàn** vấn đề **tải video từ Sample.cat (hoặc bất kỳ trang web nào) một cách tự động, không cần code**. Với **Airtop Browser Automation**, các sếp không phải lo **bị chặn CAPTCHA** như khi dùng các công cụ truyền thống.

**Hành động ngay hôm nay:**
1. **Cài đặt n8n trên VPS** (để workflow chạy 24/7).
2. **Import workflow** và **cấu hình Airtop API Key**.
3. **Test và bật Active** để tự động hóa quá trình tải video!

**Nếu có bất kỳ câu hỏi nào**, các sếp có thể **đăng ký hỗ trợ** từ [Airtop](https://portal.airtop.ai/) hoặc liên hệ với cộng đồng n8n tại [Discord](https://n8n.io/community). **Chúc các sếp thành công!** 🚀