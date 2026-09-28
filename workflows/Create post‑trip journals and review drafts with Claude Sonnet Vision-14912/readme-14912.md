---
title: "🌍 Tự Động Hoá Sách Nhật Ký Du Lịch & Bài Đánh Giá Sau Chuyến với Claude Sonnet Vision (AI 4.0)"
description: "Workflow này tự động chuyển đổi hình ảnh du lịch và ghi chú thành sách nhật ký đẹp mắt, gói nhấn mạnh điểm nổi bật và bản nháp đánh giá cho các nền tảng như TripAdvisor, Google Reviews. Giúp các sếp tiết kiệm 10+ giờ/tháng và tạo trải nghiệm du lịch cá nhân hóa hoàn toàn tự động."
slug: "tieu-dong-hoa-sach-nhat-ky-du-lich-va-bai-danh-gia"
tags: [n8n, automation, multimodal-ai, content-creation, claude-ai]
keywords: [n8n workflow du lịch, tự động hóa sách nhật ký, Claude Sonnet Vision, AI tạo nội dung du lịch, tự động hóa đánh giá sau chuyến]
---

# 🚀 **Tự Động Hoá Sách Nhật Ký Du Lịch & Bài Đánh Giá Sau Chuyến với Claude Sonnet Vision**

### **Giải Phóng Tay Các Sếp Từ Công Việc "Làm Tay" Sau Mỗi Chuyến Du Lịch**
Du lịch là trải nghiệm tuyệt vời, nhưng việc tổng kết lại những khoảnh khắc đẹp nhất, viết sách nhật ký chi tiết, hoặc soạn bài đánh giá cho các nền tảng như TripAdvisor hay Google Reviews thường là một **công việc mệt mỏi và tốn thời gian**. Thậm chí, nhiều hình ảnh và ghi chú quý giá còn bị "quên" trong thiết bị hoặc Google Photos.

**Workflow này tự động hóa toàn bộ quy trình đó chỉ trong vài giây!** Dựa trên **Claude Sonnet Vision** (AI multimodal hàng đầu của Anthropic), nó sẽ:
✅ **Tự động phân tích hình ảnh** để tìm ra những khoảnh khắc đáng nhớ nhất.
✅ **Tạo sách nhật ký tự động** với cấu trúc logic, kết hợp hình ảnh và câu chuyện.
✅ **Soạn bài đánh giá chi tiết** cho các nền tảng du lịch.
✅ **Tạo gói nhấn mạnh điểm nổi bật** (highlight reel) cho video hoặc slideshow.
✅ **Gửi kết quả qua email** hoặc lưu vào Google Drive một cách tự động.

---
## 🎯 **Kết Quả Các Sếp Nhận Được**

:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm 10+ giờ/tháng**: Không cần viết tay sách nhật ký hoặc soạn bài đánh giá.
- **Nội dung cá nhân hóa cao**: AI phân tích hình ảnh và ghi chú để tạo câu chuyện độc đáo cho mỗi chuyến du lịch.
- **Hoạt động 24/7**: Dùng cả **webhook** (khi hoàn thành chuyến) và **scheduling** (xử lý batch hàng ngày).
- **Tích hợp hoàn hảo**: Kết nối với **Google Photos, Google Drive, Google Sheets** và **email**.
- **Dữ liệu phân tích**: Theo dõi chất lượng hình ảnh, điểm nhấn đáng nhớ nhất của mỗi chuyến.
:::

---
## 🔧 **Yêu Cầu Cần Thiết**

:::info[**CHUẨN BỊ TRƯỚC KHI BẮT ĐẦU**]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản và API Keys**:
   - **Anthropic API** (Claude Sonnet Vision) → [Đăng ký miễn phí](https://console.anthropic.com/)
   - **Google Photos API** → [Cài đặt OAuth 2.0](https://developers.google.com/photos/api/guides/overview)
   - **Google Drive API** → [Cài đặt OAuth 2.0](https://developers.google.com/drive/api/v3/quickstart/python)
   - **Google Sheets API** → [Cài đặt OAuth 2.0](https://developers.google.com/sheets/api/quickstart/python)
   - **SMTP/Gmail** (để gửi email kết quả) → [Cài đặt SMTP](https://support.google.com/mail/answer/7126229)
   *(Lưu ý: Nếu dùng Gmail, cần bật "Less Secure Apps" hoặc tạo mật khẩu ứng dụng.)*

2. **Cấu trúc Google Sheets**:
   - **Bảng `trips`**: Danh sách chuyến du lịch với cột `start_date`, `end_date`, `destination`.
   - **Bảng `trip_notes`**: Ghi chú hàng ngày của chuyến du lịch.
   - **Bảng `generated_content`**: Lưu kết quả AI (sách nhật ký, bài đánh giá).
   - **Bảng `analytics`**: Theo dõi điểm nhấn, chất lượng hình ảnh.

3. **Cấu trúc Google Drive**:
   ```
   /Travel Memories/
     ├── {Năm}/
     │   ├── {Tên Chuyến Du Lịch}/
     │   │   ├── Photos/ (tất cả hình ảnh chuyến)
     │   │   ├── Journal/ (sách nhật ký PDF)
     │   │   └── Reviews/ (bài đánh giá)
   ```

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/14912](https://n8n.io/workflows/14912) hoặc copy/paste JSON vào **n8n Editor**.
- **Cách import nhanh**:
  ```bash
  curl -o workflow.json https://raw.githubusercontent.com/n8n-io/workflows/master/workflows/14912.json
  ```
  Sau đó nhấn **Import** trong n8n Dashboard.

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**

#### **A. Cấu Hình Credentials (Tất Cả Các Node Quan Trọng)**
| **Node**                     | **Yêu Cầu Cấu Hình**                                                                 | **Lưu Ý**                                                                 |
|------------------------------|------------------------------------------------------------------------------------|----------------------------------------------------------------------------|
| **Trip Completion Webhook**  | Cấu hình `path: "trip-completed"` và `httpMethod: POST`.                          | Sử dụng **ngrok** nếu test trên máy local: `ngrok http 5678` (cổng mặc định n8n). |
| **Fetch Google Photos**      | Thêm **Google Photos API** vào credentials.                                        | Chọn **OAuth 2.0** và cấp quyền `https://www.googleapis.com/auth/photoslibrary.readonly`. |
| **Fetch Trip Notes**         | Chọn **Google Sheets OAuth2Api** và chỉ định **Sheet Name = "trip_notes"**.         | Đảm bảo cột `trip_id` trong Sheets trùng với `trip_id` trong webhook.       |
| **Claude Sonnet Vision**     | Thêm **Anthropic API** với `model: claude-sonnet-4-20250514`.                     | API Key phải có quyền `read:images`, `read:messages`.                     |
| **Generate Travel Journal**  | Node **Agent** sẽ tự động gọi Claude. Cần cấu hình **prompt** trong code node.      | Mở node `Process Trip Notes` và `Merge Photos & Notes` để chỉnh sửa logic. |
| **Save to Google Drive**     | Chọn **Google Drive OAuth2Api** và cấu hình folder: `/Travel Memories/{Năm}/{Tên Chuyến}/`. | Sử dụng **`{{ $node["Fetch Trip Notes"].json["trip_name"] }}`** trong path. |
| **Send Email**               | Thêm **SMTP** (Gmail) với cấu hình: `host: smtp.gmail.com`, `port: 465`.            | Bật **MFA** và tạo mật khẩu ứng dụng trong Google Account.                 |

#### **B. Cấu Hình Cụ Thể Trong Code Nodes**
1. **Node `Validate Trip Data`**:
   - Kiểm tra `start_date` và `end_date` trong payload webhook.
   - Thêm logic kiểm tra:
     ```javascript
     if (!jsonNode.trip_id || !jsonNode.destination) {
       return { error: "Thiếu thông tin chuyến du lịch!" };
     }
     ```

2. **Node `Extract Photo Metadata`**:
   - Sử dụng API Google Photos để lấy metadata (vị trí, thời gian chụp).
   - Ví dụ:
     ```javascript
     const photos = await $node["Fetch Google Photos"].execute();
     const metadata = photos.json.items.map(photo => ({
       id: photo.id,
       location: photo.mediaMetadata.location,
       timestamp: photo.mediaMetadata.creationTime
     }));
     ```

3. **Node `Generate Travel Journal`**:
   - Prompt mẫu cho Claude:
     ```
     Tôi là một AI hỗ trợ du lịch. Hãy tạo một sách nhật ký chi tiết cho chuyến du lịch {trip_name} từ {start_date} đến {end_date}.
     Dữ liệu đầu vào:
     - {photos_metadata}
     - {trip_notes}
     Yêu cầu:
     1. Sắp xếp theo thời gian.
     2. Kết hợp hình ảnh và câu chuyện.
     3. Tránh lặp lại.
     ```

4. **Node `Create Highlights Package`**:
   - Lọc ra 5 hình ảnh tốt nhất dựa trên metadata (ví dụ: có vị trí hoặc cảm xúc tích cực).
   - Sử dụng code:
     ```javascript
     const highlights = photos_metadata
       .filter(photo => photo.location && photo.timestamp)
       .sort((a, b) => new Date(b.timestamp) - new Date(a.timestamp))
       .slice(0, 5);
     ```

#### **C. Kích Hoạt Workflow ⚡️**
1. **Test Run**:
   - Gửi một payload mẫu đến webhook:
     ```json
     {
       "trip_id": "CHUYEN-DU-LICH-001",
       "trip_name": "Hà Nội - Sapa 2024",
       "start_date": "2024-05-15",
       "end_date": "2024-05-20",
       "destination": "Hà Nội, Sapa"
     }
     ```
   - Kiểm tra các node `Claude Sonnet Vision` và `Generate Travel Journal` có trả về kết quả không.

2. **Bật Active**:
   - Nhấn **Active** trên workflow.
   - **Kích hoạt cả hai trigger**:
     - **Webhook**: Dùng khi hoàn thành chuyến du lịch.
     - **Schedule Trigger**: Xử lý batch hàng ngày (cấu hình `cron: 0 0 * * *` để chạy mỗi ngày 00:00).

---

### **✍️ Mẹo & Gợi Ý Nâng Cao**

1. **Kết Nối với Slack/Telegram**:
   - Thêm node **Slack Webhook** hoặc **Telegram Bot** để thông báo khi hoàn thành xử lý.
   - Ví dụ:
     ```json
     {
       "text": `✅ Xử lý chuyến du lịch "${trip_name}" thành công! Kết quả đã lưu tại: ${drive_link}`
     }
     ```

2. **Lưu Log & Theo Dõi**:
   - Thêm node **Google Sheets** để ghi log lỗi:
     ```javascript
     if (error) {
       await $node["Log Batch Processing Analytics"].execute({
         json: { trip_id, error, timestamp: new Date().toISOString() }
       });
     }
     ```

3. **Tích Hợp OpenWeatherMap (Tùy Chọn)**:
   - Sử dụng node **HTTP Request** để lấy dữ liệu thời tiết lịch sử:
     ```javascript
     const weather = await $node["OpenWeatherMap"].execute({
       parameters: { lat: location.lat, lon: location.lon, units: "metric" }
     });
     ```
   - Thêm vào sách nhật ký: *"Ngày {date}, thời tiết mát mẻ với {weather.main} độ, phù hợp cho chuyến thám hiểm."*

4. **Tạo Báo Cáo Định Kỳ**:
   - Sử dụng **Schedule Trigger** để gửi báo cáo tổng hợp hàng tháng:
     ```javascript
     const monthlyReport = await $node["Google Sheets"].execute({
       operation: "query",
       query: "SELECT * FROM analytics WHERE MONTH(timestamp) = MONTH(CURRENT_DATE())"
     });
     ```

---

## 📌 **Kết Luận: Hãy Tự Động Hoá Ngay Hôm Nay!**

Workflow này không chỉ **giải phóng thời gian** cho các sếp mà còn **tăng giá trị trải nghiệm du lịch** bằng cách tự động hóa việc tổng kết và chia sẻ. Với **Claude Sonnet Vision**, mỗi chuyến du lịch trở thành một **câu chuyện sống động**, trong khi bạn chỉ cần **nhấn một nút** hoặc chờ **batch hàng ngày** xử lý.

### **Bước Đầu Tiên: Cài Đặt VPS Cho n8n (Nếu Chưa Có)**
:::info[**Gợi Ý Hạ Tầng**]
Để workflow chạy **ổn định 24/7**, các sếp nên **self-host n8n** trên VPS. Dưới đây là các lựa chọn uy tín với **mã giảm giá** dành cho bạn:
- **TinoHost (VPS 4GB RAM chỉ 1.500.000 VND/tháng)** 🎁 [Mã giảm: **VPSN8N**](https://tino.vn/vps-n8n?affid=388)
- **BNIX (VPS Xeon 4GB chỉ 50.000 VND/tháng)** 🎁 [Mã giảm: **BNIXN8N**](https://my.bnix.one/aff.php?aff=172)

**Cài đặt n8n trên VPS chỉ trong 5 phút** với hướng dẫn:
```bash
# Cài Docker (nếu chưa có)
curl -fsSL https://get.docker.com | sh
sudo usermod -aG docker $USER

# Cài n8n
docker run -d \
  --name n8n \
  -e N8N_BASIC_AUTH_ACTIVE=true \
  -e N8N_BASIC_AUTH_USER=admin \
  -e N8N_BASIC_AUTH_PASSWORD=yourpassword \
  -p 5678:5678 \
  --restart unless-stopped \
  n8nio/n8n
```
:::

### **Hành Động Ngay Bây Giờ**
1. **Import workflow** từ [n8n.io/workflows/14912](https://n8n.io/workflows/14912).
2. **Cấu hình credentials** theo hướng dẫn trên.
3. **Test với một chuyến du lịch mẫu**.
4. **Bật Active** và **chờ AI làm việc cho bạn!**

**🚀 Chúc các sếp có những chuyến du lịch tuyệt vời và sách nhật ký hoàn hảo!** Nếu có vấn đề, hãy để lại comment bên dưới hoặc liên hệ **Oneclick AI Squad** qua [GitHub](https://github.com/oneclick-ai).