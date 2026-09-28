---
title: "🚀 Tự động hóa thông báo Discord tùy chỉnh cho Radarr, Sonarr và Bazarr qua n8n"
description: "Tối ưu hóa thông báo tự động từ hệ thống Media Server (Radarr, Sonarr, Bazarr) lên Discord với giao diện đẹp mắt, tinh gọn và đầy đủ thông tin bằng n8n."
slug: "custom-discord-notifications-radarr-sonarr-bazarr-n8n"
tags: [n8n, automation, no-code, discord, radarr, sonarr, bazarr, media-server]
keywords: [n8n workflow, discord notifications, radarr sonarr bazarr n8n, tự động hóa media server, webhook discord]
---

# 🚀 Tự động hóa thông báo Discord tùy chỉnh cho Radarr, Sonarr và Bazarr

Các sếp đang tự host (self-host) hệ thống giải trí gia đình với **Radarr**, **Sonarr**, **Bazarr** chắc chắn đã quen thuộc với các thông báo mặc định. Tuy nhiên, thông báo mặc định thường quá dài dòng, thiếu thẩm mỹ hoặc không theo đúng ý muốn của mình. Việc cấu hình trực tiếp đôi khi bị giới hạn về giao diện và nội dung.

Workflow n8n này sinh ra để giải quyết triệt để vấn đề đó! Nó đóng vai trò là một "trạm trung chuyển" nhận webhook từ các ứng dụng *arr, xử lý dữ liệu thông qua các node Code thông minh, dịch thuật hoặc định dạng lại, rồi bắn thẳng lên **Discord** với định dạng cực kỳ gọn gàng, trực quan (có ảnh thumbnail, chất lượng, dung lượng, tên bản phát hành...).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và nhận webhook real-time từ các ứng dụng media server, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tùy biến giao diện tuyệt đẹp:** Thông báo trên Discord được thiết kế lại gọn gàng, bao gồm tiêu đề, năm, tập phim, trạng thái, thumbnail, chất lượng file, kích thước và tên release.
- **Tập trung hóa:** Gom toàn bộ thông báo từ Radarr (phim), Sonarr (phim truyền hình) và Bazarr (phụ đề) về chung một mối xử lý.
- **Xử lý dữ liệu thông minh:** Sử dụng các đoạn code JavaScript nhẹ nhàng để lọc và định dạng lại thuộc tính của phim, series và phụ đề trước khi gửi đi.
- **Hoạt động 24/7 tự động 100%:** Không cần can thiệp thủ công, cứ có sự kiện tải xuống, xóa file hay lỗi là Discord reo lên ngay lập tức.
:::

### 📦 Các loại Nodes chính trong Workflow
- **Webhook:** Nhận tín hiệu (POST request) từ Radarr, Sonarr, Bazarr.
- **Switch / If / Filter:** Phân loại sự kiện đến từ ứng dụng nào để điều hướng logic xử lý phù hợp.
- **Code Nodes:** Xử lý, trích xuất và dịch các trường dữ liệu (properties) của movie, series, subtitle.
- **HTTP Request (Notify Discord):** Gửi payload JSON hoàn thiện lên kênh Discord qua Webhook URL.

---

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance **n8n** đang hoạt động (có thể public URL để các *arr gọi webhook tới).
- Hệ thống **Radarr**, **Sonarr**, và **Bazarr** đang chạy.
- Một **Discord Webhook URL** tại kênh mà các sếp muốn nhận thông báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy đoạn JSON của workflow từ nguồn (hoặc file JSON được cung cấp), sau đó paste trực tiếp vào n8n Editor của mình thông qua phím tắt `Ctrl + V` (hoặc `Cmd + V`).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần chú ý cấu hình các điểm sau:
- **Node `Webhook`:** Cấu hình lại đường dẫn (path) nếu cần (mặc định trong hướng dẫn gốc là `/radarr`). Hãy đảm bảo URL public của n8n trỏ đến đây.
- **Node `Notify Discord` (HTTP Request):** Thay thế URL Discord Webhook mặc định bằng Webhook URL kênh Discord của chính các sếp.
- **Cấu hình phía Radarr / Sonarr:**
  1. Vào `Settings` > `Connect`.
  2. Thêm kết nối dạng `Webhook` và trỏ tới URL Webhook của n8n ở trên.
  3. Chọn các sự kiện cần thiết: *File Import, Movie File Delete, Movie File Delete for Upgrade, Manual Interaction Required*.
- **Cấu hình phía Bazarr:**
  Bazarr sử dụng cấu hình đơn giản hơn và không có mục Webhook chuyên dụng. Các sếp cần dùng dạng **JSON** và trong phần URL, hãy thay thế tiền tố `https://` bằng `jsons://` (Ví dụ: `jsons://your-n8n-domain.com/webhook/radarr`).

#### 3. Kích hoạt ⚡️
- Thực hiện bắn thử một sự kiện từ Radarr/Sonarr để kiểm tra data đổ về node Webhook.
- Kiểm tra kết quả hiển thị trên Discord.
- Khi mọi thứ đã mượt mà, gạt công tắc **Active** góc trên bên phải để workflow chạy tự động.

---

### ✍️ Mẹo & gợi ý nâng cao
- **Đa kênh thông báo:** Các sếp có thể nhân bản node HTTP Request cuối cùng để bắn đồng thời thông báo sang **Telegram Bot** hoặc **Slack** nếu team hoặc gia đình dùng nhiều nền tảng khác nhau.
- **Lưu log sự kiện:** Thêm một node Google Sheets hoặc Airtable vào sau bước xử lý JSON để lưu lại lịch sử tải phim/phụ đề phục vụ việc thống kê.
- **Lọc sự kiện rác:** Tận dụng các node `Filter` sẵn có trong workflow để loại bỏ các thông báo không quan trọng (ví dụ: chỉ nhận thông báo khi tải thành công, bỏ qua các thông báo xóa file nhỏ lẻ).

### 📌 Kết luận
Với workflow này, hệ thống thông báo media server tự host của các sếp sẽ trở nên chuyên nghiệp, gọn gàng và sinh động hơn rất nhiều trên Discord. Chúc các sếp cài đặt thành công và có những phút giây giải trí tuyệt vời!