---
title: "🚀 Tự Động Hóa Telegram → Notion → Google Drive & Sheets: Lưu Trữ & Quản Lý Tất Cả Nội Dung Một Cách Tiện Lợi"
description: "Workflow tự động hóa 100% không code giúp các sếp đồng bộ hóa tin nhắn, ảnh, và tệp từ Telegram sang Notion (lưu ảnh), Google Drive (lưu file), và Google Sheets (đăng ký chi tiết), đồng thời gửi thông báo hoàn thành. Giúp tiết kiệm thời gian lên đến 80% trong quản lý nội dung và tăng cường tính chuyên nghiệp cho công việc."
slug: "tieu-dong-hoa-telegram-notion-google-drive-sheets"
tags: [n8n, automation, no-code, telegram-bot, notion-api, google-drive, google-sheets, it-ops]
keywords: [tự động hóa telegram, đồng bộ hóa nội dung, lưu ảnh vào notion, lưu file google drive, google sheets tự động, workflow n8n, quản lý công việc hiệu quả]
---

# 🚀 **Tự Động Hóa Telegram → Notion → Google Drive & Sheets: Lưu Trữ & Quản Lý Tất Cả Nội Dung Một Cách Tiện Lợi**

## **🔥 Nỗi Đau Của Các Sếp Khi Quản Lý Nội Dung Bằng Tay**
Hàng ngày, các sếp phải:
- **Lặp đi lặp lại** việc tải ảnh, văn bản, và tệp từ Telegram vào Notion, Google Drive, và Google Sheets.
- **Mất thời gian** để tổ chức lại nội dung, dẫn đến rối loạn và mất mát thông tin.
- **Không theo dõi được** ai đã tải lên tệp nào, kích thước, hoặc thời gian tạo, khiến quản lý trở nên khó khăn.
- **Không có thông báo tự động**, phải nhớ nhắc lại với team hoặc khách hàng về kết quả xử lý.

**Workflow này giải quyết tất cả!** Nó tự động đồng bộ hóa **tin nhắn, ảnh, và tệp** từ Telegram sang các nền tảng khác nhau, đồng thời **ghi lại chi tiết** và **gửi thông báo hoàn thành** một cách tự động.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian lên đến 80%** trong việc quản lý nội dung từ Telegram.
- **Tự động lưu ảnh vào Notion** với caption tự động, giúp tổ chức nội dung một cách chuyên nghiệp.
- **Tự động upload tệp vào Google Drive** và ghi lại chi tiết (tên, kích thước, loại, người tải) vào **Google Sheets**.
- **Gửi thông báo hoàn thành** ngay lập tức qua Telegram, đảm bảo sự minh bạch và giảm thiểu lỗi.
- **Hoạt động liên tục 24/7**, không cần can thiệp thủ công.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Telegram** và **API Key Telegram Bot** (để nhận tin nhắn và tải ảnh/tệp).
2. **Tài khoản Notion** và **API Key Notion** (để lưu ảnh và văn bản).
3. **Tài khoản Google** với quyền truy cập vào:
   - **Google Drive** (để lưu tệp).
   - **Google Sheets** (để ghi lại chi tiết tệp).
4. **Tài khoản ImgBB** (để hosting ảnh trước khi upload vào Notion).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Bước 1:** Tải file JSON của workflow từ [n8n.io/workflows/4404](https://n8n.io/workflows/4404).
- **Bước 2:** Mở **n8n Editor** và chọn **"Import"** → Chọn file JSON vừa tải.
- **Bước 3:** Chọn **"Import"** để workflow xuất hiện trên canvas.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **3 đường dẫn chính** để xử lý nội dung từ Telegram:
- **📸 Ảnh** → Download → Upload lên ImgBB → Lưu vào Notion.
- **📝 Văn bản** → Lưu vào Notion dưới dạng heading.
- **📁 Tệp** → Download → Upload vào Google Drive → Ghi chi tiết vào Google Sheets.

##### **🔹 Cấu Hình Telegram Trigger**
- **Node:** `📱 Telegram Message Trigger`
  - **Credentials:** Chọn `telegramApi` (đã cấu hình trước khi import).
  - **Chat ID:** Điền ID của chat Telegram muốn đồng bộ (có thể lấy từ URL chat hoặc sử dụng `@username`).
  - **Filter:** Để trống hoặc chỉ định các từ khóa cụ thể (nếu muốn chỉ xử lý tin nhắn có chứa từ khóa).

##### **🔹 Cấu Hình Notion (Lưu Ảnh & Văn Bản)**
- **Node:** `📝 Add Image to Notion` và `📝 Add Text to Notion`
  - **Credentials:** Chọn `notionApi` (đã cấu hình trước).
  - **Database/Page:** Chọn Notion Database hoặc Page muốn lưu nội dung.
  - **Properties:**
    - **Caption:** Điền tên caption cho ảnh (có thể lấy từ tin nhắn Telegram).
    - **Heading:** Điền tiêu đề cho văn bản (có thể lấy từ nội dung tin nhắn).

##### **🔹 Cấu Hình Google Drive (Lưu Tệp)**
- **Node:** `☁️ Upload to Google Drive`
  - **Credentials:** Chọn `googleDriveOAuth2Api`.
  - **Folder:** Chọn thư mục trong Google Drive muốn lưu tệp.
  - **File Name:** Có thể lấy từ tên tệp gốc hoặc tự định nghĩa (ví dụ: `Tên_Tệp_${currentDate}`).

##### **🔹 Cấu Hình Google Sheets (Ghi Chi Tiết)**
- **Node:** `📊 Record in Google Sheets`
  - **Credentials:** Chọn `googleSheetsOAuth2Api`.
  - **Sheet Name:** Chọn bảng Google Sheets muốn ghi dữ liệu.
  - **Headers:** Đảm bảo các cột trong Sheets phù hợp với dữ liệu được gửi (tên tệp, người tải, kích thước, loại, ngày tạo).
  - **Operation:** Đặt là `append` để thêm dữ liệu mới vào cuối bảng.

##### **🔹 Cấu Hình ImgBB (Hosting Ảnh)**
- **Node:** `🌐 Upload to ImgBB`
  - **URL:** `https://api.imgbb.com/1/upload`
  - **Headers:**
    - `Authorization: Bearer ${IMG_BB_API_KEY}` (điền API Key của ImgBB).
  - **Body:**
    ```json
    {
      "key": "${IMG_BB_API_KEY}",
      "image": "${base64Image}"
    }
    ```
  - **Response:** Lấy URL ảnh từ phản hồi và gửi vào Notion.

##### **🔹 Cấu Hình Telegram Completion Message**
- **Node:** `✅ Send Completion Message`
  - **Credentials:** Chọn `telegramApi`.
  - **Chat ID:** Điền lại ID chat Telegram (cùng với trigger).
  - **Message:** Có thể tự định nghĩa (ví dụ: `📤 File đã được lưu vào Google Drive và ghi vào Google Sheets!`).

---

#### **3. Kích Hoạt ⚡️**
- **Bước 1:** Chạy **Test Run** với một tin nhắn mẫu (ảnh, văn bản, hoặc tệp) để kiểm tra workflow.
- **Bước 2:** Nếu tất cả các node hoạt động bình thường, chuyển workflow sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tự động tạo Notion Page mới cho mỗi tin nhắn:**
   - Sử dụng node **Notion** để tạo một page mới mỗi khi nhận tin nhắn, thay vì ghi vào database.
2. **Gửi báo cáo định kỳ:**
   - Sử dụng node **Google Sheets** kết hợp với **n8n Scheduler** để gửi báo cáo tổng hợp về tệp đã upload hàng tuần.
3. **Kết hợp với Slack/Telegram:**
   - Thêm node **Slack** hoặc **Telegram** để gửi thông báo khi có tệp mới được upload.
4. **Lưu log hoạt động:**
   - Sử dụng node **StickyNote** (đã có trong workflow) để ghi lại log hoạt động của workflow, giúp theo dõi và debug dễ dàng.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** để các sếp tự động hóa việc quản lý nội dung từ Telegram, đồng thời lưu trữ và theo dõi một cách chuyên nghiệp. **Không cần code, không cần kỹ thuật cao**, chỉ cần cấu hình vài bước đơn giản là có thể tiết kiệm thời gian và tăng hiệu suất công việc lên nhiều lần.

**Hãy áp dụng ngay và trải nghiệm sự tiện lợi của tự động hóa!** 🚀

---
**🔗 [Tải workflow nguyên bản tại đây](https://n8n.io/workflows/4404)** | **📌 [Cài đặt n8n Self-hosted](https://docs.n8n.io/)**