---
title: "🚀 Tự động tải Slideshare Presentations lên Google Drive với RapidAPI qua n8n"
description: "Hướng dẫn xây dựng workflow tự động tải tài liệu từ Slideshare thông qua RapidAPI, lưu trữ an toàn trên Google Drive, phân quyền chia sẻ công khai và ghi log lỗi vào Google Sheets."
slug: "tu-dong-tai-slideshare-len-google-drive-n8n"
tags: [n8n, automation, no-code, google-drive, google-sheets, rapidapi]
keywords: [n8n workflow, tải slideshare tự động, google drive automation, rapidapi slideshare, tự động hóa n8n]
keywords: [n8n workflow, tải slideshare tự động, google drive automation, rapidapi slideshare, tự động hóa n8n]
---

# 🚀 Tự động tải Slideshare Presentations lên Google Drive với RapidAPI

Các sếp có bao giờ cảm thấy phiền toái khi tìm được một tài liệu hay trên Slideshare nhưng lại không thể tải về trực tiếp, hoặc phải dùng những trang web bên thứ ba đầy quảng cáo và kém an toàn? Việc lưu trữ và quản lý tài liệu thủ công này ngốn rất nhiều thời gian, đặc biệt khi cần xử lý số lượng lớn.

Giải pháp là đây! Bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n tự động hóa 100%: Nhận link Slideshare qua Form giao diện, gọi API lấy link tải, tự động lưu file PDF vào Google Drive, cấp quyền chia sẻ công khai và tự động ghi log vào Google Sheets nếu có lỗi xảy ra. Không cần một dòng code phức tạp nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Chỉ cần dán link Slideshare vào form, hệ thống sẽ tự lo phần còn lại từ tải về đến lưu trữ.
- **Lưu trữ đám mây an toàn:** Tài liệu được đẩy thẳng lên thư mục Google Drive định sẵn và tự động bật link chia sẻ (Anyone with the link can view).
- **Kiểm soát lỗi thông minh:** Tự động ghi nhận các link lỗi vào Google Sheets để kiểm tra lại sau mà không làm gián đoạn hệ thống.
- **Tiết kiệm thời gian:** Thay vì thao tác thủ công mất hàng phút cho mỗi tài liệu, giờ đây chỉ mất vỏn vẹn vài giây.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị sẵn:
- **Tài khoản n8n** (Self-hosted hoặc n8n Cloud).
- **Tài khoản RapidAPI** và đăng ký một gói Slideshare Downloader Pro API để lấy API Key.
- **Tài khoản Google** để kết nối Google Drive (OAuth2) và Google Sheets (Google API).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và dán trực tiếp vào giao diện n8n Editor (hoặc sử dụng tính năng Import từ file JSON).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 8 nodes chính, các sếp cần chú ý cấu hình kỹ các điểm sau:
- **On form submission (`formTrigger`):** Tạo sẵn giao diện form đơn giản có 1 trường nhập URL Slideshare. Các sếp có thể tuỳ chỉnh giao diện hoặc title theo ý muốn.
- **Slideshare downloader (`httpRequest`):** Node gọi API tới RapidAPI. Các sếp cần điền Endpoint của RapidAPI Slideshare, kèm theo Header chứa `X-RapidAPI-Key` và `X-RapidAPI-Host` của tài khoản RapidAPI cá nhân.
- **If (`if`):** Kiểm tra xem API trả về status thành công hay không.
  - 🟢 **True Path:** Đi tiếp đến node tải file PDF.
  - 🔴 **False Path:** Chuyển qua node Wait và Google Sheets để ghi log lỗi.
- **Upload To Google Drive (`googleDrive`):** Kết nối tài khoản Google Drive và chọn thư mục (`Folder ID`) đích mà các sếp muốn lưu trữ file PDF tải về.
- **Google Drive Set Permission (`googleDrive`):** Cấu hình phân quyền file thành `Anyone with the link can view` để dễ dàng chia sẻ.
- **Google Sheets Append Row (`googleSheets`):** Chọn file Google Sheets và sheet dùng để ghi log lỗi. Cấu hình map 2 cột: `URL` (link gốc Slideshare) và `Drive_URL` (gán giá trị `N/A` để báo hiệu lỗi tải).

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng một link Slideshare thực tế qua Form trigger để kiểm tra dữ liệu chạy qua các nhánh.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để workflow hoạt động tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Thêm node Telegram hoặc Slack ở nhánh True để gửi thông báo kèm link Google Drive ngay khi tải xong tài liệu.
- **Mở rộng nguồn tài liệu:** Có thể bổ sung thêm các node xử lý để hỗ trợ các nền tảng chia sẻ tài liệu khác ngoài Slideshare.
- **Tự động làm sạch log:** Thiết lập lịch chạy định kỳ hàng tuần để dọn dẹp các dòng log lỗi cũ trong Google Sheets.

### 📌 Kết luận
Với workflow n8n này, việc quản lý và lưu trữ tài liệu từ Slideshare đã trở nên mượt mà và tự động hoàn toàn. Hãy áp dụng ngay vào hệ thống của các sếp để tối ưu hóa năng suất làm việc nhé!