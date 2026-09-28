---
title: "🚀 Tự Động Hóa Chuyển Đổi YouTube Shorts Sang TikTok & Instagram Với Blotato – Không Cần Code!"
description: "Workflow tự động hóa 100% miễn phí giúp các sếp tự động chuyển đổi YouTube Shorts sang TikTok và Instagram, tiết kiệm thời gian và tăng cường sự hiện diện trên mạng xã hội. Kết quả: nội dung đồng bộ, không trùng lặp, và được quản lý tự động."
slug: "tieu-dong-youtube-shorts-sang-tiktok-instagram"
tags: [n8n, automation, social-media, youtube, tiktok, instagram, blotato, no-code]
keywords: [tự động hóa youtube shorts, chuyển đổi nội dung tiktok instagram, n8n workflow youtube, tự động hóa mạng xã hội, blotato api, yt-dlp tự động]
---

# 🚀 **Tự Động Hóa Chuyển Đổi YouTube Shorts Sang TikTok & Instagram – Không Cần Code!**

### **Giải Pháp Cho Các Sếp Muốn Tiết Kiệm Thời Gian & Tăng Cường Hiện Diện Trên Mạng Xã Hội**
Hiện nay, các sếp và content creator phải mất nhiều thời gian để **tải xuống YouTube Shorts, chỉnh sửa và tái đăng lại lên TikTok và Instagram**. Điều này không chỉ tốn thời gian mà còn dễ gây **trùng lặp nội dung** và mất hiệu quả. **Workflow này tự động hóa toàn bộ quy trình**, giúp bạn đồng bộ nội dung trên 3 nền tảng chính trong **vài giây**, chỉ với một lần upload!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian** – Không cần tải xuống và tái đăng thủ công.
✅ **Tránh trùng lặp nội dung** – Kiểm tra và cập nhật trạng thái trên Google Sheets.
✅ **Đồng bộ hóa tự động** – YouTube Shorts → TikTok & Instagram chỉ trong **vài giây**.
✅ **Quản lý log chuyên nghiệp** – Theo dõi thành công/thất bại trên Google Sheets.
✅ **Tiết kiệm dung lượng** – Xóa tự động file video sau khi upload.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **YouTube Data API Key** (để lấy danh sách Shorts mới).
✔ **Google Sheets** (để lưu trạng thái video và log kết quả).
✔ **Blotato API Credentials** (để upload lên TikTok & Instagram).
✔ **n8n Self-hosted** (để chạy `yt-dlp` và các lệnh hệ thống).
✔ **yt-dlp cài đặt trên VPS** (để tải video từ YouTube).
✔ **Thư mục `youtube`** (để lưu tạm video trước khi upload).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/13954](https://n8n.io/workflows/13954) hoặc **copy/paste JSON** vào **n8n Editor**.
- **Nhấn "Import"** để thêm workflow vào hệ thống.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **22 node**, nhưng các sếp chỉ cần chú ý đến các phần sau:

##### **🔹 Cấu Hình Blotato (Upload TikTok & Instagram)**
- **Node: `Upload Media to Blotato`**
  - Điền **API Key Blotato** vào `credentials`.
  - Chọn **resource = "media"** (để upload video).

- **Node: `Blotato Post to TikTok` & `Blotato Post to Instagram`**
  - Cấu hình **URL TikTok/Instagram** và **tham số đăng bài** (nếu cần).
  - **Lưu ý:** Blotato hỗ trợ **scheduling**, các sếp có thể lên lịch upload vào thời gian tối ưu.

##### **🔹 Cấu Hình YouTube (Lấy Danh Sách Shorts)**
- **Node: `Get Youtube Video List` (HTTP Request)**
  - **URL:** `https://www.googleapis.com/youtube/v3/search?part=snippet&channelId=CHANNEL_ID&maxResults=50&type=video&videoCategoryId=22`
  - **Thay `CHANNEL_ID` bằng ID kênh YouTube của bạn** (tìm trên [YouTube Studio](https://studio.youtube.com/)).
  - **Headers:**
    ```json
    {
      "Authorization": "Bearer YOUR_YOUTUBE_API_KEY"
    }
    ```
  - **Response Format:** Chọn `JSON`.

- **Node: `Download YouTube Shorts via yt-dlp` (Execute Command)**
  - **Command:**
    ```bash
    yt-dlp -f "bestvideo[ext=mp4]+bestaudio[ext=m4a]/best[ext=mp4]" --merge-output-format mp4 --no-warnings "URL_VIDEO"
    ```
  - **Lưu ý:**
    - **URL_VIDEO** phải được truyền từ node trước (từ `Get Youtube Video List`).
    - **Thư mục lưu:** `/youtube/` (đã tạo trước).

##### **🔹 Cấu Hình Google Sheets (Lưu Trạng Thái)**
- **Node: `Insert List to Sheets` & `Update Sheets Success/Error`**
  - **Google Sheets Credentials:** Đăng nhập tài khoản Google và chọn **Sheet phù hợp**.
  - **Sheet Name:** Tạo một sheet mới với **cột: Video ID, Status, Error (nếu có)**.
  - **Operation:** Chọn `appendOrUpdate` để cập nhật trạng thái.

- **Node: `Filter by Status Not Processed` (If Condition)**
  - **Điều kiện:** `{{ $node["Read from Sheets"].json["status"] }} !== "Processed"`

##### **🔹 Cấu Hình Schedule (Chạy Định Kỳ)**
- **Node: `Schedule Trigger Upload` & `Schedule Trigger Get Youtube Video List`**
  - **Thời gian chạy:** Ví dụ **8 giờ/lần** (để kịp thời cập nhật Shorts mới).
  - **Lưu ý:** Nếu muốn chạy thường xuyên hơn, giảm thời gian xuống **4-6 giờ**.

##### **🔹 Xóa File Tạm (Cleanup)**
- **Node: `Remove Local File` (Execute Command)**
  - **Command:**
    ```bash
    rm -rf /youtube/*.mp4
    ```
  - **Lưu ý:** Chạy sau khi upload thành công để **giảm dung lượng lưu trữ**.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với **1-2 video mẫu** để kiểm tra:
   - Video có tải xuống thành công không?
   - Blotato có upload lên TikTok/Instagram không?
   - Google Sheets có cập nhật trạng thái không?
2. **Bật Active** workflow sau khi kiểm tra xong.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tích Hợp Slack/Telegram**
   - Thêm **node `webhook`** để nhận thông báo khi upload thành công/thất bại.
   - Ví dụ: Gửi tin nhắn **"Shorts đã upload lên TikTok & Instagram thành công!"**.

2. **Lưu Log Chi Tiết**
   - Thêm **node `set`** để lưu **thời gian upload, URL TikTok/Instagram** vào Google Sheets.

3. **Scheduling Smart**
   - Sử dụng **Blotato Scheduling** để upload vào **giờ cao điểm** (ví dụ: 8h-10h sáng).

4. **Tự Động Chỉnh Sải Video**
   - Nếu video dài hơn 60s, **cắt tự động** bằng `ffmpeg` (thêm node `executeCommand`).

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **tạo nội dung chất lượng** thay vì **tái đăng thủ công**. Với **n8n + Blotato + yt-dlp**, bạn có thể:
✔ **Tự động hóa 100% quy trình**.
✔ **Tránh trùng lặp nội dung**.
✔ **Tăng cường sự hiện diện trên 3 nền tảng chính**.
✔ **Quản lý log chuyên nghiệp**.

**Hãy áp dụng ngay và bắt đầu tự động hóa nội dung của mình!** 🚀

---
**🔗 [Tải workflow nguyên bản](https://n8n.io/workflows/13954) | 📌 [Cài đặt n8n Self-hosted](https://docs.n8n.io/)**