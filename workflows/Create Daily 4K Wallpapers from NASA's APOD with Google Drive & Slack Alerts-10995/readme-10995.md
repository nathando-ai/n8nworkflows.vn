---
title: "🚀 Tự động tạo Wallpaper 4K hàng ngày từ NASA APOD, lưu Google Drive & thông báo Slack"
description: "Workflow n8n tải ảnh NASA APOD mỗi ngày, resize lên 4K, lưu vào Google Drive và gửi thông báo Slack nếu là video."
slug: "tu-dong-tao-wallpaper-4k-nasa-apod"
tags: [n8n, automation, no-code, file-management, google-drive, slack, nasa]
keywords: [n8n workflow, tự động hóa, NASA APOD, Google Drive, Slack alerts, wallpaper 4K]
---

# 🚀 Tự động tạo Wallpaper 4K hàng ngày từ NASA APOD, lưu Google Drive & thông báo Slack

Bạn có bao giờ muốn mỗi sáng mở máy tính là đã có một bức ảnh nền 4K tuyệt đẹp, nhưng lại phải **tải thủ công** từ trang NASA, **cắt tỉa** kích thước, rồi **đưa lên Drive**?  
Việc này không chỉ tốn thời gian mà còn dễ gây lỗi, đặc biệt khi ngày nào APOD là video thì bạn lại phải **đánh giá** và **bỏ qua** thủ công.

**Workflow này** sẽ giải quyết toàn bộ quy trình **100% không cần code**:
- Tự động gọi API NASA mỗi ngày, lấy metadata của APOD.  
- Nếu APOD là ảnh, tải về, resize lên độ phân giải 4K, lưu vào Google Drive (kiểm tra trùng lặp).  
- Nếu APOD là video, bỏ qua download và **đẩy thông báo** ngay lên Slack để bạn biết.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không còn phải mở trình duyệt, tải, chỉnh kích thước mỗi ngày.  
- **Độ chính xác 100%**: Kiểm tra loại media, tránh lưu video nhầm ảnh.  
- **Cá nhân hoá**: Ảnh nền luôn luôn ở độ phân giải 4K, phù hợp màn hình hiện đại.  
- **Hoạt động liên tục**: Workflow chạy tự động 24/7, thông báo ngay khi có video.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản NASA API** (đăng ký tại https://api.nasa.gov) → API Key.  
- **Tài khoản Google** với **Google Drive API** đã bật, tạo **OAuth2 credentials** và cấp quyền `drive.file`.  
- **Tài khoản Slack** → tạo **Bot Token** và **Channel ID** nơi muốn nhận thông báo.  
- **n8n** đã cài đặt (self‑hosted hoặc cloud) và **các credentials** trên các node tương ứng.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON của workflow (từ trang gốc hoặc export từ n8n).  
2. Vào **n8n Editor → Import → From File** và chọn file JSON.  
3. Hoặc **Copy/Paste** toàn bộ JSON vào ô **Import from Clipboard**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Vai trò | Cấu hình cần chỉnh |
|------|----------|--------------------|
| **Daily Schedule** (`scheduleTrigger`) | Kích hoạt workflow mỗi ngày | Đặt thời gian chạy (UTC hoặc local) phù hợp với múi giờ doanh nghiệp. |
| **Fetch Metadata** (`nasa`) | Lấy metadata APOD | **Credentials** → NASA API Key. |
| **Download Image** (`httpRequest`) | Tải file ảnh từ URL | **URL** được lấy từ `{{$json["url"]}}` của node trước. |
| **Resize Image** (`editImage`) | Resize lên 3840×2160 (4K) | **Operation**: `resize` → **Width**: `3840` → **Height**: `2160`. |
| **Generate Filename** (`set`) | Tạo tên file duy nhất | Thiết lập `filename` = `APOD_{{ $json["date"] }}.jpg`. |
| **Check Storage Provider** (`if`) | Kiểm tra trùng tên trên Drive | **Condition**: `{{$node["Upload to Google Drive"].json["exists"]}}` → `false` để tiếp tục upload. |
| **Upload to Google Drive** (`googleDrive`) | Lưu ảnh vào Drive | **Credentials** → Google Drive OAuth2.<br>**Folder ID**: nhập ID thư mục (được cấu hình trong node `Workflow Configuration`). |
| **If** (node thứ 8) | Kiểm tra loại media | **Condition**: `{{$json["media_type"]}} === "image"` → nếu **false** (video) sẽ đi tới node Slack. |
| **Send a message** (`slack`) | Thông báo video không lưu được | **Credentials** → Slack Bot Token.<br>**Channel**: nhập Channel ID.<br>**Message**: `APOD hôm nay là video, không có ảnh để lưu. Link: {{$json["url"]}}`. |
| **Workflow Configuration** (`set`) | Cấu hình chung | Điền **Google Drive Folder ID** và **Slack Channel ID** vào các trường tương ứng. |

> **Lưu ý:** Các node `if` phải được **đánh dấu** đúng hướng (true/false) để luồng logic hoạt động như mô tả.

#### 3. Kích hoạt ⚡️
1. **Test run**: Nhấn **Execute Workflow** lần đầu với dữ liệu mẫu để kiểm tra download, resize và upload.  
2. Kiểm tra **Google Drive** có file mới, và **Slack** nhận thông báo (nếu APOD là video).  
3. Khi mọi thứ ổn, bật **Active workflow** bằng công tắc góc trên‑phải.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm bước lưu log**: Dùng node `Google Sheets` hoặc `Airtable` để ghi lại ngày, URL, và trạng thái (saved / video).  
- **Gửi báo cáo tuần**: Dùng `Cron` + `Slack` để tổng hợp các ảnh đã lưu và gửi danh sách vào kênh Slack mỗi thứ Bảy.  
- **Kết hợp Telegram**: Thêm node `Telegram` để nhận thông báo đồng thời trên nhiều kênh.  
- **Tự động đặt làm wallpaper** trên máy cá nhân (Windows/macOS) bằng script PowerShell hoặc AppleScript được kích hoạt qua webhook.

### 📌 Kết luận
Với workflow này, các sếp sẽ **không còn mất công tải ảnh nền mỗi ngày**, đồng thời luôn nhận được **cảnh báo kịp thời** khi APOD là video. Hãy **import**, **cấu hình credentials**, **kiểm tra** và **bật chạy** ngay hôm nay để biến mỗi buổi sáng thành một trải nghiệm hình ảnh tuyệt đẹp! 🚀