---
title: "🎥 Tự Động Chia Video Influencer Thành Clip Ngắn Với WayinVideo AI + Google Drive (N8N)"
description: "Workflow tự động hóa chia video dài của influencer thành clip ngắn viral với AI WayinVideo, sau đó lưu trực tiếp vào Google Drive - tiết kiệm thời gian lên đến 80% cho việc repurpose content."
slug: "tieu-dong-hoa-chia-video-influencer-thanh-clip-ngan"
tags: [n8n, automation, content-creation, ai-multimodal, google-drive, wayinvideo]
keywords: [tự động hóa chia video, wayinvideo ai, repurpose content, n8n workflow, google drive tự động, chia video thành clip ngắn]
---

# 🚀 **Tự Động Chia Video Influencer Thành Clip Ngắn Viral Với AI + Google Drive (N8N)**

### **Nỗi Đau Của Các Sếp**
Các sếp trong ngành marketing, content creation hay quản lý cộng đồng xã hội thường phải mất **giờ đồng hồ** để:
- Chia video dài của influencer thành các clip ngắn (TikTok, Reels, Shorts).
- Chỉnh sửa, cắt ghép thủ công để tối ưu hóa engagement.
- Lưu trữ và quản lý hàng trăm clip trên nhiều nền tảng khác nhau.

**Kết quả?** Thời gian và năng suất bị "cướp" bởi công việc lặp đi lặp lại, trong khi AI và tự động hóa có thể giải quyết vấn đề này **một cách hoàn toàn tự động**.

### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian lên đến 80%** so với cách làm thủ công.
- **Tối ưu hóa nội dung** với các clip ngắn viral tự động từ video dài.
- **Lưu trữ trung tâm** tất cả clip vào Google Drive, dễ dàng chia sẻ và quản lý.
- **Hoạt động 24/7** mà không cần can thiệp của con người.
:::

---

## 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **API Key của WayinVideo**:
   - Đăng ký tại [WayinVideo](https://wayinvideo.com/) để lấy API Key.
   - **Không** để API Key trong node trực tiếp (mang lại rủi ro an toàn). Thay vào đó, sử dụng **n8n Credentials** (Header Auth) để bảo mật.
2. **Tài khoản Google Drive**:
   - Cần kết nối với n8n thông qua **OAuth2** (quyền chỉnh sửa file).
   - Chuẩn bị **ID của thư mục Google Drive** để lưu clip (có thể tạo thư mục mới và copy ID từ liên kết chia sẻ).
3. **VPS cho n8n (khuyến nghị)**:
   - Để workflow hoạt động liên tục 24/7, các sếp nên **self-host n8n** trên VPS.
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải workflow từ [n8n.io/workflows/14540](https://n8n.io/workflows/14540).
2. Trong n8n Editor, nhấn **Import** và chọn file JSON.
   **Hoặc**:
   - Copy toàn bộ JSON từ trang workflow trên n8n.io.
   - Trong n8n Editor, nhấn **Import** → **Paste JSON**.

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này bao gồm **8 node** quan trọng, các sếp cần chú ý cấu hình như sau:

#### **Node 1: Form — Video URL + Brand + Clip Count**
- **Mục đích**: Nhận dữ liệu đầu vào từ người dùng (URL video, tên brand, số lượng clip cần tạo).
- **Lưu ý**:
  - Đảm bảo form hiển thị rõ ràng trên trang web hoặc ứng dụng bạn sử dụng.
  - Các trường bắt buộc: `videoUrl`, `brand`, `clipCount`.

#### **Node 2 & 4: WayinVideo — Submit Clipping Task & Poll Clips Result**
- **Mục đích**: Gửi video đến API WayinVideo để AI chia thành clip và kiểm tra kết quả.
- **Cấu hình quan trọng**:
  - **API Key**: **Không** điền trực tiếp vào node. Thay vào đó:
    1. Trong n8n, đi đến **Credentials** → **Add Credential** → **Header Auth**.
    2. Đặt tên credential (ví dụ: `wayinvideo-api-key`).
    3. Nhập `Authorization` với giá trị `Bearer YOUR_WAYINVIDEO_API_KEY`.
    4. Trong node **WayinVideo**, chọn credential này thay vì nhập API Key trực tiếp.
  - **URL API**:
    - Submit: `https://api.wayinvideo.com/v1/tasks`
    - Poll: `https://api.wayinvideo.com/v1/tasks/{taskId}`
  - **Tham số gợi ý**:
    ```json
    {
      "method": "POST",
      "headers": {
        "Content-Type": "application/json"
      },
      "body": {
        "video_url": "${{ $json.videoUrl }}",
        "brand": "${{ $json.brand }}",
        "target_duration": "DURATION_30_60" // Thay đổi theo nhu cầu (ví dụ: DURATION_15_30 cho TikTok)
      }
    }
    ```

#### **Node 3: Wait — 45 Seconds**
- **Mục đích**: Đợi 45 giây trước khi kiểm tra kết quả từ WayinVideo.
- **Lưu ý**: Thời gian này có thể điều chỉnh tùy thuộc vào tốc độ xử lý của API.

#### **Node 5: If — Clips Ready?**
- **Mục đích**: Kiểm tra nếu clip đã sẵn sàng.
- **Cấu hình quan trọng**:
  - **Condition**: Kiểm tra `status` trong response từ WayinVideo có bằng `"ready"` không.
  - **Lưu ý an toàn**: Để tránh **lặp vô hạn**, các sếp nên thêm **số lần retry tối đa** (ví dụ: 5 lần) trong node này. Nếu sau 5 lần vẫn chưa ready, workflow sẽ dừng và báo lỗi.

#### **Node 6: Code — Extract Clips Array**
- **Mục đích**: Trích xuất danh sách clip từ response của WayinVideo.
- **Lưu ý**:
  - Code mẫu trong node có thể là:
    ```javascript
    // Trích xuất mảng clip từ response
    return {
      json: {
        clips: $input.all().clips,
      },
    };
    ```

#### **Node 7: HTTP Request — Download Clip File**
- **Mục đích**: Tải xuống từng clip từ URL được cung cấp bởi WayinVideo.
- **Cấu hình quan trọng**:
  - **URL**: `${{ $json.clips[0].url }}` (đối với mỗi clip trong mảng).
  - **Method**: `GET`.
  - **Headers**: `Accept: application/octet-stream`.

#### **Node 8: Google Drive — Upload Clip**
- **Mục đích**: Lưu clip đã tải xuống vào Google Drive.
- **Cấu hình quan trọng**:
  1. **Kết nối Google Drive**:
     - Trong n8n, đi đến **Credentials** → **Add Credential** → **Google Drive**.
     - Chọn **OAuth2** và kết nối với tài khoản Google.
  2. **Tham số node**:
     - **Folder ID**: Nhập ID thư mục bạn muốn lưu clip (có thể lấy từ liên kết chia sẻ thư mục).
     - **File Name**: `${{ $json.clips[0].title }}.mp4` (hoặc tự định nghĩa).
     - **File Content**: `${{ $json.body }}` (dữ liệu binary từ node tải xuống).

---

### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhập một URL video và số lượng clip vào form.
   - Chạy workflow và kiểm tra kết quả:
     - Clip có được tạo không?
     - Clip có được tải xuống và lưu vào Google Drive không?
2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active**.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Thêm Slack/Telegram Notifications**:
   - Sau khi upload thành công, thêm node **Slack** hoặc **Telegram** để thông báo kết quả cho team.
   - Ví dụ: `Clip đã được tạo thành công! Link: [LINK_GOOGLE_DRIVE]`.
2. **Lưu Log Vào Google Sheets**:
   - Thêm node **Google Sheets** để ghi log chi tiết:
     - Tên clip, URL video gốc, thời gian tạo, độ dài clip.
   - Cách làm:
     - Tạo một sheet mới với các cột: `Tên Clip`, `URL Video`, `Thời Gian Tạo`, `Độ Dài`.
     - Sử dụng node **Google Sheets** với action `Create Row`.
3. **Tự Động Chia Sẻ Vào Mạng Xã Hội**:
   - Sau khi upload, thêm node **Facebook**, **Instagram**, hoặc **Twitter** để chia sẻ clip tự động.
4. **Tối Ưu Hóa Thời Gian Chờ**:
   - Thay đổi thời gian chờ trong node **Wait** (ví dụ: 30s hoặc 60s) nếu API phản hồi nhanh hơn.
5. **Xử Lý Lỗi Hiệu Quả**:
   - Thêm node **Set** trước node **If** để đếm số lần retry và dừng workflow nếu quá nhiều lần thất bại.
:::

---

## 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp cần tự động hóa việc chia video dài thành clip ngắn viral, tiết kiệm thời gian và nâng cao hiệu suất content creation. Với **AI WayinVideo** và **Google Drive**, các sếp có thể:
✅ **Tạo clip trong giây lát** mà không cần cắt ghép thủ công.
✅ **Lưu trữ và quản lý** tất cả clip tại một nơi trung tâm.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

**Hành động ngay hôm nay!**
1. **Chuẩn bị API Key và Google Drive**.
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Test và kích hoạt** để bắt đầu tự động hóa!

Nếu có bất kỳ vấn đề nào, hãy để lại bình luận hoặc liên hệ với cộng đồng n8n để được hỗ trợ. **Tự động hóa là tương lai - bắt đầu từ hôm nay!** 🚀