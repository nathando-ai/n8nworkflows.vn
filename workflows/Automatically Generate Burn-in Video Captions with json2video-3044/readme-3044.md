---
title: "🎬 Tự Động Chèn Chú Thích Video Cho Video Bạn Với json2video + n8n (Không Cần Code)"
description: "Workflow tự động hóa hoàn toàn miễn phí giúp các sếp thêm caption cho video YouTube, TikTok, Reels chỉ với 1 cú nhấp chuột - tiết kiệm thời gian lên đến 80% so với cách làm thủ công."
slug: "tu-dong-chen-chu-thich-video-voi-json2video-n8n"
tags: [n8n, automation, ai, video-marketing, json2video]
keywords: [tự động hóa video caption, n8n workflow video, thêm caption tự động, json2video n8n, tự động hóa marketing video]
---

# 🚀 Tự Động Chèn Chú Thích Video Cho Video Bạn Với json2video + n8n (Không Cần Code)

## 🔥 Nỗi Đau Của Các Sếp Khi Làm Thủ Công
Các sếp đã từng phải:
- **Chỉnh sửa caption thủ công** cho hàng chục video mỗi tháng, mất từ 2-5 giờ/lần?
- **Lo lắng về độ chính xác** khi dịch tự động không phù hợp với nội dung?
- **Không biết cách tự động hóa** vì nghĩ cần biết code hoặc chi phí cao?

Workflow này **giải quyết tất cả** bằng cách kết hợp sức mạnh của **n8n (tự động hóa không code)** và **json2video (API caption tự động)** để **chèn caption chính xác, cá nhân hóa** cho video chỉ trong vài giây!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động 24/7 mà không gián đoạn, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ cao)
:::

---

### 🎯 Kết Quả Các Sếp Nhận Được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Chèn caption cho 100 video chỉ trong **5 phút** thay vì 5 giờ.
- **Chất lượng cao**: Caption chính xác, đồng bộ với âm thanh (không sai lệch như dịch tự động thông thường).
- **Cá nhân hóa**: Thêm logo, font chữ, màu sắc theo brand của doanh nghiệp.
- **Hoạt động liên tục**: Workflow chạy tự động mỗi khi có video mới (không cần can thiệp).
- **Tiết kiệm chi phí**: So với dịch vụ chuyên nghiệp (từ 50k-200k/video).
:::

---

### 🔧 Yêu Cầu Cần Thiết
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản json2video**:
   - Đăng ký tại [json2video.com](https://json2video.com/?afco=manu) (sử dụng mã giới thiệu **manu** để được hỗ trợ).
   - Nhận **API Key** qua email sau khi đăng ký.
2. **VPS hoặc n8n Cloud** (nếu không self-host).
3. **Video cần xử lý**:
   - Link video (YouTube, TikTok, Reels, MP4).
   - Kích thước video (Width & Height, ví dụ: 1920x1080).

---

### 🚀 Cách Import & Lưu Ý Khi "Lên Đồ"

#### 1. Import Workflow 📥
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/3044) hoặc copy toàn bộ JSON từ đây.
- Mở **n8n Editor** → Nhấn **"Import"** → Dán JSON → Chọn **"Import"**.

#### 2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌
Workflows này gồm **9 node** quan trọng, các sếp cần cấu hình như sau:

##### **A. Cấu Hình Credentials (Bước Quán Trọng)**
1. **Tạo Credentials Custom Auth**:
   - Trong n8n, đi đến **"Credentials"** → **"Add"** → Chọn **"Custom Auth"**.
   - Dán JSON sau vào **Configuration**, thay thế `your-json2video-api-key` bằng API Key của bạn:
     ```json
     {
       "headers": {
         "x-api-key": "your-json2video-api-key"
       }
     }
     ```
   - **Lưu** credentials này (sẽ dùng cho 2 node HTTP sau).

2. **Gán Credentials cho Node HTTP**:
   - Mở node **"json2video - Add Captions"** và **"json2video - Get Status"**.
   - Trong phần **"Credentials"**, chọn **Custom Auth** vừa tạo.

##### **B. Cấu Hình Input (Video & Kích Thước)**
- Node **"Config"** (type: `set`) là nơi các sếp **điền thông tin video**:
  - **URL**: Link video (ví dụ: `https://youtu.be/dQw4w9WgXcQ`).
  - **Width & Height**: Kích thước video (ví dụ: `1920` và `1080`).
  - **Font & Style** (tùy chọn): Chọn font, màu chữ, vị trí caption theo yêu cầu.

##### **C. Kiểm Tra & Bật Workflow**
1. **Test Run**:
   - Nhấn **"Execute"** trên node **"Manual Trigger"** để thử với dữ liệu mẫu.
   - Kiểm tra node **"Is Error"** và **"is Completed"** để đảm bảo không lỗi.
2. **Bật Workflow**:
   - Đánh dấu **"Active"** để workflow chạy tự động khi kích hoạt.

---

### ✍️ Mẹo & Gợi Ý Nâng Cao
1. **Kết Nối Với Slack/Telegram**:
   - Thêm node **Slack/Telegram** sau node **"Output"** để nhận thông báo khi caption hoàn tất.
   - Ví dụ: `Gửi tin nhắn: "Caption video [URL] đã hoàn tất!"`.

2. **Lưu Log Tự Động**:
   - Thêm node **Google Sheets** hoặc **Airtable** để lưu lịch sử video đã xử lý (URL, thời gian, trạng thái).

3. **Chạy Định Kỳ**:
   - Sử dụng **n8n Cron Trigger** để chạy workflow hàng ngày/tuần để cập nhật caption cho video mới.

4. **Tối Ưu Hiệu Suất**:
   - Nếu video dài, thêm node **Wait** giữa các bước để tránh overloading API.

---

### 📌 Kết Luận
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào nội dung chất lượng cao hơn, trong khi **json2video + n8n** làm việc 24/7 để tự động hóa công việc mòn mỏi. **Bắt đầu ngay** với chỉ **3 bước đơn giản**:
1. Đăng ký json2video và lấy API Key.
2. Import workflow và cấu hình credentials.
3. Nhấn **"Active"** và để n8n làm việc!

👉 [**Tải workflow ngay**](https://n8n.io/workflows/3044) và **tự động hóa video của bạn trong 5 phút!**

---
**Chia sẻ workflow này với đồng nghiệp để cùng tiết kiệm thời gian!** 🚀