---
title: "📧 Tự Động Hoàn Thành Tạp Chí Tuần Kỉ Plex Media qua Email (Thay Thế Tautulli)"
description: "Workflow tự động hóa gửi newsletter tuần về phim mới và chương trình truyền hình từ Plex Media qua email, tiết kiệm thời gian và tối ưu trải nghiệm người dùng. Chỉ cần cấu hình 1 lần, hoạt động tự động hàng tuần."
slug: "tu-dong-hoan-thanh-tap-chi-tuan-ki-plex-media-qua-email"
tags: [n8n, automation, no-code, plex-media, email-marketing, self-hosted]
keywords: [n8n workflow plex, tự động hóa email newsletter, tự động hóa media, newsletter tuần, tự động hóa plex, tự động hóa media streaming]
---

# 🚀 Tự Động Hoàn Thành Tạp Chí Tuần Kỉ Plex Media qua Email (Thay Thế Tautulli)

### 🎯 **Giải Pháp Cho Nỗi Đau Của Các Sếp**
Bạn có bao giờ phải mất nhiều thời gian để theo dõi và tổng hợp danh sách phim mới, chương trình truyền hình mới từ Plex Media để gửi cho khách hàng hoặc thành viên trong nhóm? Hoặc bạn đã từng sử dụng Tautulli nhưng muốn một giải pháp tự động hóa hoàn toàn không cần code? **Workflow này sẽ giúp bạn tự động hóa toàn bộ quy trình!**

Với **Workflow tự động hóa gửi newsletter tuần về phim mới và chương trình truyền hình từ Plex Media**, các sếp sẽ không phải mất thời gian thủ công để cập nhật danh sách phim mới, tạo email và gửi cho người dùng. Thay vào đó, chỉ cần cấu hình 1 lần, hệ thống sẽ tự động lấy dữ liệu từ Plex Media, tổng hợp và gửi email hàng tuần vào thời gian đã chỉ định.

---

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải thủ công cập nhật danh sách phim mới hàng tuần.
- **Tính chính xác cao**: Dữ liệu được lấy trực tiếp từ Plex Media, không có sai sót.
- **Cá nhân hóa**: Có thể tùy chỉnh danh sách người nhận và nội dung email.
- **Hoạt động liên tục**: Hoạt động tự động hàng tuần mà không cần can thiệp của con người.
- **Tối ưu trải nghiệm người dùng**: Người dùng nhận được thông tin mới nhất về phim và chương trình truyền hình một cách nhanh chóng và dễ dàng.
:::

---

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
- **Tautulli API Key**: Để lấy dữ liệu về phim mới và chương trình truyền hình từ Plex Media.
- **Plex Token**: Để xác thực với Plex Media.
- **Plex Server ID**: ID của máy chủ Plex Media.
- **SMTP Credentials**: Để gửi email qua SMTP (gồm `fromEmail`, tên miền SMTP, port, username, password).
- **Danh sách email người nhận**: Danh sách email của những người bạn muốn gửi newsletter.
:::

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể import workflow này bằng cách:
- **Tải file JSON** từ [n8n.io/workflows/7556](https://n8n.io/workflows/7556) và import vào n8n Editor.
- **Copy/Paste JSON** từ trang trên vào n8n Editor và nhấn "Import".

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

##### ⏰ Schedule Trigger
- Workflow được cấu hình chạy **mỗi tuần vào thứ Sáu lúc 8h00**. Các sếp có thể điều chỉnh ngày và giờ theo nhu cầu bằng cách chỉnh sửa trong node này.

##### 🎬 Fetch Recent Movies (Tautulli)
- **Thay thế placeholder trong URL**:
  - `YOUR_TAUTULLI_URL`: URL của máy chủ Tautulli (ví dụ: `http://your-tautulli-server:8081`).
  - `YOUR_API_KEY`: API Key của Tautulli (tìm trong cài đặt của Tautulli).

##### 📺 Fetch Recent TV Shows (Tautulli)
- **Thay thế placeholder trong URL**:
  - `YOUR_TAUTULLI_URL`: URL của máy chủ Tautulli (giống như trên).
  - `YOUR_API_KEY`: API Key của Tautulli (giống như trên).

##### 🔗 Combine Movie & TV Data
- Node này chỉ kết hợp dữ liệu phim và chương trình truyền hình trước khi xây dựng email. **Không cần chỉnh sửa**.

##### 📰 Generate HTML Newsletter
- **Chỉnh sửa code trong node này** để điền các thông tin sau:
  - `YOUR_TAUTULLI_URL`: URL của máy chủ Tautulli.
  - `YOUR_PLEX_TOKEN`: Token xác thực của Plex Media.
  - `YOUR_PLEX_SERVER_ID`: ID của máy chủ Plex Media.
- **Cấu trúc code** đã được thiết kế sẵn, các sếp chỉ cần thay thế các placeholder và chỉnh sửa template HTML nếu cần.

##### 📧 Prepare Emails for Recipients
- **Thay thế danh sách email mẫu** trong node này bằng danh sách email của người nhận thực tế. Ví dụ:
  ```json
  [
    "email1@example.com",
    "email2@example.com"
  ]
  ```

##### 📤 Send via SMTP
- **Cấu hình SMTP**:
  - `fromEmail`: Email gửi (ví dụ: `no-reply@yourdomain.com`).
  - **Thêm credentials SMTP**:
    - Tên miền SMTP (ví dụ: `smtp.gmail.com`).
    - Port (ví dụ: 587).
    - Username và password của tài khoản SMTP.

##### ✅ Finish
- Node này chỉ hiển thị thông tin tóm tắt về số lượng email đã gửi. **Không cần chỉnh sửa**.

---

### ✍️ Mẹo & gợi ý nâng cao
:::info[MỘT SỐ Ý TƯỞNG MỞ RỘNG]
- **Kết hợp với Slack/Telegram**: Sau khi gửi email thành công, các sếp có thể thêm node Slack hoặc Telegram để thông báo kết quả.
- **Lưu log hoạt động**: Thêm node `stickyNote` hoặc `file` để lưu log hoạt động của workflow, giúp theo dõi và debug dễ dàng.
- **Gửi báo cáo định kỳ**: Nếu cần, các sếp có thể thêm node `emailSend` để gửi báo cáo tổng hợp về số lượng phim/tv được gửi hàng tháng.
- **Tùy chỉnh nội dung email**: Sử dụng node `code` để thêm hoặc chỉnh sửa nội dung email theo phong cách riêng của doanh nghiệp.
- **Dùng Plex API trực tiếp**: Nếu không muốn sử dụng Tautulli, các sếp có thể thay thế node `httpRequest` để lấy dữ liệu trực tiếp từ Plex API.
:::

---

### 📌 Kết luận
Workflow này là giải pháp hoàn hảo cho các sếp muốn tự động hóa việc gửi newsletter về phim mới và chương trình truyền hình từ Plex Media. **Chỉ cần cấu hình 1 lần, hệ thống sẽ tự động hoạt động hàng tuần**, tiết kiệm thời gian và nâng cao trải nghiệm người dùng.

**Hãy áp dụng ngay và trải nghiệm sự tiện lợi mà tự động hóa mang lại!** 🚀

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::