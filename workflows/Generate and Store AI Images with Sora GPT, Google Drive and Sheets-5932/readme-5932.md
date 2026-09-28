---
title: "🚀 Tự Động Tạo và Lưu Trữ Ảnh AI Bằng Sora GPT, Google Drive và Google Sheets trong n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình tạo ảnh AI từ prompt và ảnh gốc qua Sora GPT API, sau đó lưu trữ trực tiếp lên Google Drive và ghi log vào Google Sheets."
slug: "tu-dong-tao-va-luu-tru-anh-ai-sora-gpt-google-drive-sheets"
tags: [n8n, automation, no-code, ai-images, google-drive, google-sheets, sora-gpt]
keywords: [n8n workflow, tạo ảnh ai tự động, sora gpt api, google drive automation, google sheets logging, no-code automation]
---

# 🚀 Tự Động Tạo và Lưu Trữ Ảnh AI Bằng Sora GPT, Google Drive và Google Sheets

Các sếp có đang tốn quá nhiều thời gian để nghĩ ý tưởng, tạo ảnh thủ công bằng các công cụ AI, rồi lại phải tải về máy và upload lên Google Drive để lưu trữ? Chưa kể việc quản lý prompt và ngày tháng tạo ảnh rải rác khiến việc tìm kiếm lại vô cùng cực khổ. 

Giải pháp cho các sếp đây! Bài viết này sẽ hướng dẫn chi tiết cách thiết lập một workflow n8n hoàn toàn tự động: **Nhận yêu cầu qua Form 👉 Tạo ảnh bằng Sora GPT AI 👉 Chuyển đổi định dạng 👉 Lưu vào Google Drive 👉 Ghi log chi tiết vào Google Sheets**. Không cần viết code phức tạp, chỉ cần vài cú click là hệ thống AI sáng tạo nội dung của các sếp đã sẵn sàng hoạt động 24/7!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Từ khâu nhận input của người dùng đến khi trả ra ảnh hoàn chỉnh trên Cloud.
- **Lưu trữ khoa học:** Ảnh tự động đồng bộ vào Google Drive, thông tin prompt và thời gian được ghi chép gọn gàng trong Google Sheets.
- **Mở rộng dễ dàng:** Phục vụ tuyệt vời cho Content Creator, Marketer, Designer hoặc các ứng dụng cần scale số lượng lớn hình ảnh.
- **Tiết kiệm hàng chục giờ:** Không còn thao tác thủ công lặp đi lặp lại mỗi ngày.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị sẵn:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **RapidAPI Key** để kết nối với *Sora GPT Image API*.
- **Google Account** (để cấu hình Google Drive và Google Sheets thông qua Google OAuth2 hoặc Service Account).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng dữ liệu JSON của workflow này, copy và paste trực tiếp vào n8n Editor của mình. Workflow bao gồm 5 nodes chính:
1. `On form submission` (Form Trigger)
2. `HTTP Request` (Sora GPT API)
3. `Code` (Xử lý chuỗi Base64 thành file ảnh nhị phân)
4. `Google Drive` (Upload ảnh)
5. `Google Sheets` (Ghi log dữ liệu)

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node `On form submission` (Form Trigger):** Node này tạo sẵn một giao diện form đơn giản cho người dùng nhập `Prompt` (Mô tả ảnh) và `Image URL` (Ảnh gốc tham chiếu). Các sếp có thể lấy link Webhook công khai để gửi cho team sử dụng.
- **Node `HTTP Request`:** 
  - Method: `POST`
  - URL: `https://sora-gpt-image.p.rapidapi.com/ai-img/img-to-img.php`
  - Cần thêm Header chứa **RapidAPI Key** của các sếp để xác thực.
  - Body parameters bao gồm `Prompt`, `Image URL`, `Width` và `Height` (mặc định để 1024x1024).
- **Node `Code`:** Node này nhận chuỗi Base64 từ API trả về và chuyển đổi thành định dạng file ảnh (JPEG) để các node phía sau có thể đọc được file nhị phân (binary). Không cần sửa code ở đây trừ khi các sếp muốn đổi tên hoặc định dạng file.
- **Node `Google Drive`:** 
  - Kết nối Credentials Google của các sếp.
  - Chọn **Folder ID** cụ thể trên Drive để lưu trữ các bức ảnh được tạo ra tự động.
- **Node `Google Sheets`:**
  - Kết nối Credentials Google Sheets.
  - Điền **Spreadsheet ID** và chọn đúng **Sheet Name**.
  - Map các cột dữ liệu tương ứng: Cột Prompt lấy từ form, Cột Image lấy tên file từ Google Drive, và Cột Generated Date lấy thời điểm thực thi.

#### 3. Kích hoạt ⚡️
- Nhấn **Test step** hoặc **Execute Workflow** chạy thử với một prompt mẫu để kiểm tra toàn bộ luồng dữ liệu.
- Sau khi test thành công, gạt công tắc sang **Active** để workflow chính thức chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo qua Telegram/Slack:** Thêm một node Telegram hoặc Slack ngay sau Google Sheets để bắn thông báo kèm hình ảnh trực tiếp về nhóm chat khi có ảnh mới vừa được tạo xong.
- **Tạo bảng Dashboard:** Sử dụng Google Looker Studio kết nối với Google Sheets log để trực quan hóa số lượng hình ảnh đã tạo theo ngày/tuần/tháng.

### 📌 Kết luận
Workflow tích hợp Sora GPT, Google Drive và Google Sheets là một cỗ máy tự động hóa hoàn hảo giúp tối ưu hóa quy trình sáng tạo hình ảnh cho cá nhân và doanh nghiệp. Hãy thiết lập ngay hôm nay để giải phóng sức lao động và để AI thay bạn làm những công việc lặp đi lặp lại!