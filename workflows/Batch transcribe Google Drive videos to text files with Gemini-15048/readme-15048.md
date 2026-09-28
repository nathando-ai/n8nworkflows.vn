---
title: "🎬 Tự Động Chuyển Video Google Drive Sang Văn Bản Bằng Gemini AI - Không Cần Code"
description: "Workflow tự động hóa chuyển tất cả video từ Google Drive thành văn bản chính xác bằng Gemini AI, tiết kiệm thời gian và tối ưu hóa công việc content creation. Kết quả: 100% video được transcribe, dữ liệu được tổ chức logic, và hoạt động liên tục 24/7."
slug: "tich-hop-video-google-drive-sang-van-ban-gemini"
tags: [n8n, automation, google-drive, gemini-ai, content-creation, multimodal-ai, no-code]
keywords: [tự động hóa chuyển video sang văn bản, gemini transcribe video, google drive automation, workflow n8n google drive, tự động hóa content creation]
---

# 🚀 **Tự Động Chuyển Video Google Drive Sang Văn Bản Bằng Gemini AI**

### **Giải pháp hoàn hảo cho các sếp content creator, marketer hoặc nhà phân tích**
Bạn đã bao giờ phải mất hàng giờ để transcribe video từ Google Drive sang văn bản? Hay phải lo lắng về việc mất dữ liệu khi làm thủ công? **Workflow này sẽ tự động hóa toàn bộ quy trình cho bạn**, chỉ với một cú nhấp chuột!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động ổn định 24/7 và không bị gián đoạn, các sếp nên **self-host n8n trên VPS**. Dưới đây là 2 lựa chọn VPS chất lượng với giá cả cạnh tranh:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### **🎯 Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần transcribe thủ công, tiết kiệm từ 5-10 giờ/lần cho 100 video.
- **Chính xác cao**: Gemini AI phân tích ngữ âm, ngữ cảnh và chuyển thành văn bản chính xác.
- **Tổ chức logic**: Video được chuyển từ "Incoming" → "Processed", văn bản được lưu trong "Transcript" folder.
- **Hoạt động liên tục**: N8n tự động tiếp tục từ điểm dừng nếu bị gián đoạn (ví dụ: restart máy chủ).
- **Tối ưu API**: Cấu hình batch size và thời gian chờ để tránh bị Gemini AI chặn request.
:::

---

### **🔧 Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Drive** với quyền truy cập đầy đủ vào các folder:
   - **Incoming folder**: Chứa tất cả video cần transcribe.
   - **Processed folder**: Lưu video đã được xử lý.
   - **Transcript folder**: Lưu văn bản kết quả.
2. **API Key Google Drive OAuth2** (cài đặt trong n8n dưới tên `googleDriveOAuth2Api`).
3. **Prompt tùy chỉnh** (có mẫu sẵn, các sếp có thể chỉnh sửa theo nhu cầu).
4. **Thời gian và băng thông** để xử lý video (Gemini AI có giới hạn request).

---

### **🚀 Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/15048](https://n8n.io/workflows/15048) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ link trên và dán vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow có **14 node** với các bước quan trọng sau. Các sếp **phải** cấu hình chính xác như sau:

##### **A. Cấu hình Credentials Google Drive**
- Trong **Config Node** (node thứ 5), các sếp cần điền **3 ID folder** tương ứng:
  ```json
  {
    "IncomingFolderId": "ID_FOLDER_INCOMING",  // Folder chứa video cần transcribe
    "ProcessedFolderId": "ID_FOLDER_PROCESSED", // Folder lưu video đã xử lý
    "TranscriptFolderId": "ID_FOLDER_TRANSCRIPT" // Folder lưu văn bản kết quả
  }
  ```
- **Lấy ID folder**:
  1. Mở Google Drive → Chọn folder cần lấy ID.
  2. Trong URL, phần sau `folders/` là ID folder (ví dụ: `https://drive.google.com/drive/folders/1AbCdEfGhIjKlMnOp` → ID là `1AbCdEfGhIjKlMnOp`).

##### **B. Cấu hình Prompt cho Gemini AI**
- Trong **Config Node**, tìm phần `prompt` và chỉnh sửa theo nhu cầu. Mẫu mặc định:
  ```json
  "prompt": "Transcribe the video content in Vietnamese. Include timestamps and speaker identification if possible. Keep the transcript concise but complete."
  ```
- **Gợi ý prompt nâng cao**:
  ```json
  "prompt": "Chuyển video thành văn bản tiếng Việt với cấu trúc sau:
  1. Tiêu đề: [Tên video]
  2. Nội dung chính: [Nội dung chi tiết, phân đoạn theo thời gian]
  3. Khái quát: [Tóm tắt 3 điểm chính]
  Đảm bảo giữ nguyên ngữ điệu và ngữ cảnh của người nói."
  ```

##### **C. Cấu hình Batch Size và Thời gian Chờ**
- **Node "Loop Over Videos" (node thứ 2)**:
  - **Batch Size**: Đặt từ **1-5 video/lần** (khuyến nghị bắt đầu từ **1** để test).
  - **Loop Size**: Số video được gửi đến Gemini cùng một lúc (khuyến nghị **1** để tránh overloading).
- **Node "Pause Between Videos" (node thứ 9)**:
  - Thời gian chờ mặc định **10 giây** (đảm bảo Gemini không bị quá tải).
- **Node "Pause Between Loops" (node thứ 14)**:
  - Thời gian chờ **10 giây** giữa các batch (tránh xử lý trùng lặp).

##### **D. Cấu hình Node "Find Incoming Videos"**
- Trong **Query** của node này, thay thế `XXXXX` bằng **ID folder Incoming**:
  ```json
  {
    "query": {
      "q": "mimeType='video/*' and trashed=false and parents='ID_FOLDER_INCOMING'",
      "fields": "id, name, mimeType, modifiedTime"
    }
  }
  ```

##### **E. Node "Format Transcript" (Code Node)**
- Node này tự động định dạng văn bản kết quả. **Không cần chỉnh sửa** trừ khi các sếp muốn thay đổi cấu trúc output.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Chọn **1 video mẫu** trong folder Incoming và chạy **Test Execution**.
   - Kiểm tra:
     - Video có được transcribe thành văn bản không?
     - Văn bản có được lưu vào folder Transcript không?
     - Video có được chuyển sang folder Processed không?
2. **Bật Active**:
   - Sau khi test thành công, **bật Active workflow** và chọn **Manual Trigger** để chạy toàn bộ.

---

### **✍️ Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** sau node "Transcript Succeeded?" để thông báo kết quả.
   - Ví dụ:
     ```json
     {
       "type": "n8n-nodes-base.slack",
       "operation": "sendMessage",
       "resource": "message",
       "parameters": {
         "text": "🎬 Video {{ $node["Loop Over Videos"].jsonpath("$.name") }} đã được transcribe thành văn bản!"
       }
     }
     ```

2. **Lưu log hoạt động**:
   - Thêm node **Google Sheets** sau node "Create Transcript File" để ghi lại:
     - Tên video.
     - Thời gian transcribe.
     - Trạng thái (thành công/thất bại).
   - Cấu hình như sau:
     ```json
     {
       "operation": "createRow",
       "resource": "table",
       "parameters": {
         "table": "Sheet1",
         "values": [
           { "Tên video": "{{ $node["Loop Over Videos"].jsonpath("$.name") }}", "Trạng thái": "{{ $node["Transcript Succeeded?"].jsonpath("$.jsonpath") }}" }
         ]
       }
     }
     ```

3. **Gửi báo cáo định kỳ**:
   - Sử dụng **n8n Cron Trigger** để chạy workflow hàng ngày/lần tuần và gửi báo cáo qua email.
   - Ví dụ:
     ```json
     {
       "type": "n8n-nodes-base.cron",
       "parameters": {
         "cronExpression": "0 0 * * *" // Chạy hàng ngày lúc 00:00
       }
     }
     ```

4. **Optimize Prompt cho chất lượng cao**:
   - Nếu video có **nhiều tiếng lạ/âm thanh nền**, thử prompt:
     ```json
     "prompt": "Transcribe video với độ chính xác cao, loại bỏ tiếng lạ và âm thanh không liên quan. Nếu có đoạn thoại không rõ, ghi chú 'Không rõ: [thời gian]'."
     ```

---

### **📌 Kết luận**
Workflow này **giải phóng thời gian** cho các sếp từ việc làm thủ công, đồng thời **tăng cường hiệu quả** trong việc xử lý video lớn. Với **Gemini AI** và **n8n**, bạn có thể:
✅ **Tự động hóa 100% quy trình**.
✅ **Tối ưu hóa chi phí** (không cần thuê người transcribe).
✅ **Hoạt động 24/7** mà không cần can thiệp.

**Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với 1-2 video** trước khi chạy toàn bộ.
3. **Tích hợp với Slack/Email** để theo dõi tiến độ.

**🚀 Cài đặt VPS n8n ngay hôm nay** để workflow chạy không ngừng nghỉ! [TinoHost](https://tino.vn/vps-n8n?affid=388) hoặc [BNIX](https://my.bnix.one/aff.php?aff=172) với mã giảm giá **VPSN8N**.

---
**Chia sẻ ý kiến** của các sếp về workflow này trong phần comment dưới đây! 👇