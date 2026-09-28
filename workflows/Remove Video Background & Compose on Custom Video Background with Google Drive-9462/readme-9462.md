---
title: "🎬 Tự Động Xóa Nền Video + Ghép Video Với Nền Tùy Chỉnh Sử Dụng Google Drive (N8N)"
description: "Workflow tự động hóa hoàn toàn không cần code để xóa nền video AI, ghép video với nền tùy chỉnh, và lưu kết quả lên Google Drive. Giúp các sếp tiết kiệm thời gian và nâng cao chất lượng nội dung video cho marketing, e-commerce, và sản xuất nội dung AI."
slug: "tieu-nen-video-va-ghep-video-voi-nen-tu-chinh-google-drive"
tags: [n8n, tự động hóa video, xóa nền video, ghép video, Google Drive, AI video, no-code]
keywords: [n8n workflow video, tự động hóa video marketing, xóa nền video AI, ghép video với nền tùy chỉnh, lưu video lên Google Drive, tự động hóa nội dung AI]
---

# 🚀 **Tự Động Xóa Nền Video + Ghép Video Với Nền Tùy Chỉnh Sử Dụng Google Drive**

### **Giải pháp hoàn toàn không code cho các sếp muốn tạo video chuyên nghiệp, tiết kiệm thời gian và chi phí**

---

### **🎯 Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Xóa nền video và ghép video chỉ trong **3-5 phút/phút video** (thay vì mất hàng giờ thủ công).
- **Chất lượng chuyên nghiệp**: Kết quả tương tự như sử dụng phần mềm như CapCut hoặc Adobe Premiere, nhưng tự động hóa hoàn toàn.
- **Tích hợp Google Drive**: Kết quả video được lưu tự động lên Google Drive với liên kết chia sẻ và metadata chi tiết.
- **Hoạt động 24/7**: Sử dụng webhook để tự động xử lý video khi có yêu cầu (không cần can thiệp thủ công).
- **Áp dụng đa dạng**: Phù hợp cho **video AI (HeyGen, Synthesia), quảng cáo e-commerce, nội dung social media, hoặc video đào tạo chuyên nghiệp**.
:::

---

### **🔧 Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **API Key của Video Background Remover**:
   - Đăng ký tại [trang API của Video Background Remover](https://videobgremover.com/api-management) (miễn phí có giới hạn).
   - Copy API key và thêm vào **Environment Variables** của n8n với tên `VIDEOBGREMOVER_KEY`.
     *Cách thêm biến môi trường:*
     ```
     Settings → Variables → Add new variable
     - Name: `VIDEOBGREMOVER_KEY`
     - Value: [API key của bạn]
     ```

2. **Tài khoản Google Drive**:
   - Đăng nhập và cấp quyền cho n8n trong node **"Upload to Google Drive"**.

3. **Video nguồn**:
   - **Video foreground** (chủ thể cần xóa nền): AI actor, sản phẩm, hoặc footage webcam.
   - **Video background** (nền tùy chỉnh): Video branded, stock footage, hoặc nền động.
   - *Yêu cầu*: Cả hai video phải là **URL công khai (publicly accessible)**.

4. **Hệ thống n8n**:
   - **Self-hosted** (khuyến nghị) để workflow hoạt động 24/7.
   - **N8N Cloud** cũng có thể sử dụng, nhưng không hỗ trợ webhook tự động hóa liên tục.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### **🚀 Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/9462) hoặc copy/paste JSON từ trang này vào **n8n Editor**.
- **Cách import**:
  1. Mở n8n Editor → Nhấn **"Import"** → Chọn file JSON hoặc dán JSON vào ô **"Import Workflow"**.
  2. Nhấn **"Import"** để hoàn tất.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **18 node** với logic phức tạp. Dưới đây là hướng dẫn chi tiết để cấu hình:

##### **A. Cấu hình API Key**
- **Node quan trọng**: Tất cả các node `httpRequest` liên quan đến API của Video Background Remover **sử dụng biến môi trường `VIDEOBGREMOVER_KEY`**.
- **Kiểm tra**:
  - Đảm bảo biến `VIDEOBGREMOVER_KEY` đã được thêm vào **Settings → Variables**.
  - Trong các node `httpRequest`, tham số `headers` phải có:
    ```json
    {
      "Authorization": "Bearer $vars.VIDEOBGREMOVER_KEY"
    }
    ```

##### **B. Cấu hình Google Drive**
- **Node**: **"Upload to Google Drive"**
  1. Nhấn **"Connect"** để đăng nhập tài khoản Google Drive.
  2. Chọn **folder lưu trữ** (nếu muốn lưu vào thư mục cụ thể).
  3. **Lưu ý**:
     - Nếu không chọn folder, video sẽ được lưu vào **My Drive**.
     - Kiểm tra quyền **Read & Write** để workflow có thể upload file.

##### **C. Cấu hình Webhook (nếu sử dụng tự động hóa)**
- **Node**: **"Webhook Trigger"**
  - **Path**: `compose-video` (không thay đổi).
  - **HTTP Method**: `POST`.
  - **Lưu ý**:
    - Sau khi import, nhấn **"Execute"** trên node này để lấy **URL webhook**.
    - URL này sẽ được sử dụng để gửi yêu cầu tự động hóa từ bên ngoài (ví dụ: từ Google Sheets, API, hoặc ứng dụng khác).

##### **D. Cấu hình Video Input**
- **Node**: **"Sample Video URLs (Edit Here)"**
  - Đây là nơi các sếp **điền URL video foreground và background**.
  - **Cấu trúc JSON**:
    ```json
    {
      "foreground_video_url": "https://example.com/foreground.mp4",
      "background_video_url": "https://example.com/background.mp4"
    }
    ```
  - **Lưu ý**:
    - URL phải là **public** (không yêu cầu đăng nhập).
    - Đối với **webhook automation**, các sếp sẽ gửi dữ liệu này dưới dạng JSON qua webhook.

##### **E. Cấu hình Template Composition**
- **Node**: **"2. Start Composition"**
  - **Template**: `ai_ugc_ad` (mặc định).
  - **Cấu hình chi tiết**:
    - Vị trí chủ thể: **góc phải dưới**, chiếm **35% kích thước màn hình**.
    - Độ trong suốt: **95%** (để hiệu ứng mờ nhẹ).
    - **Audio mixing**:
      - Nền: **30%** âm lượng.
      - Chủ thể: **100%** âm lượng.
    - **Export format**: H.264 (MP4), **preset: Medium** (cân bằng chất lượng và tốc độ).

##### **F. Cấu hình Polling Status**
- **Node**: **"3. Check Job Status"**
  - Workflow sẽ **kiểm tra trạng thái** của job mỗi **20 giây** (do node `Wait 20s`).
  - **Trạng thái xử lý**:
    - `processing` → Chờ 20s → Kiểm tra lại.
    - `completed` → Tải video xuống và upload lên Google Drive.
    - `failed` → Trả về lỗi và thông báo cho người dùng.

##### **G. Cấu hình Response**
- **Node**: **"Respond to Webhook"**
  - Sau khi xử lý xong, workflow sẽ trả về **JSON response** cho webhook, bao gồm:
    ```json
    {
      "status": "success/failure",
      "video_url": "https://drive.google.com/...",
      "message": "Video processed successfully!"
    }
    ```

#### **3. Kích hoạt ⚡️**
1. **Test run dữ liệu mẫu**:
   - Sử dụng node **"Manual Trigger"** để chạy thử với video mẫu.
   - Kiểm tra **Google Drive** để xác nhận video đã được upload.
2. **Bật Active workflow**:
   - Nhấn **"Active"** trên tab workflow để bật chế độ tự động hóa.

---

### **✍️ Mẹo & gợi ý nâng cao**
:::tip[CÁCH ÁP DỤNG THỰC TẾ]
1. **Tự động hóa từ Google Sheets/Airtable**:
   - Sử dụng node **Google Sheets** để lấy danh sách video từ sheet, sau đó gửi qua webhook này để tự động xử lý batch.

2. **Gửi thông báo kết quả qua Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** sau node **"Respond to Webhook"** để thông báo kết quả xử lý.

3. **Lưu log xử lý**:
   - Thêm node **Google Sheets** hoặc **Database** để ghi lại lịch sử xử lý (video input, thời gian xử lý, trạng thái).

4. **Tối ưu hóa chi phí**:
   - Video Background Remover tính phí theo **phút video** ($0.50-$2.00/min).
   - **Mẹo**: Chỉ xử lý video ngắn (dưới 1 phút) hoặc chia video dài thành nhiều đoạn.

5. **Sử dụng template tùy chỉnh**:
   - Nếu muốn thay đổi vị trí hoặc độ trong suốt của chủ thể, chỉnh sửa **template composition** trong node **"2. Start Composition"**.
:::

---

### **📌 Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa việc **xóa nền video và ghép video với nền tùy chỉnh**, tiết kiệm thời gian và nâng cao chất lượng nội dung. Đặc biệt phù hợp cho:
- **Tạo video AI UGC** (HeyGen, Synthesia).
- **Quảng cáo e-commerce** với nền branded.
- **Nội dung social media** chuyên nghiệp.
- **Video đào tạo** với nền chuyên nghiệp.

**Hành động ngay**:
1. **Import workflow** và cấu hình theo hướng dẫn trên.
2. **Test với video mẫu** để đảm bảo hoạt động ổn định.
3. **Áp dụng tự động hóa** qua webhook hoặc kết nối với Google Sheets.

👉 **Bắt đầu tự động hóa video của bạn ngay hôm nay!** 🚀