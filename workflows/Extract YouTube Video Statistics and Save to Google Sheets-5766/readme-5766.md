---
title: "🚀 Tự động trích xuất thống kê video YouTube và lưu vào Google Sheets với n8n"
description: "Hướng dẫn xây dựng workflow n8n giúp tự động cào dữ liệu view, like, comment từ YouTube API và cập nhật thẳng vào Google Sheets một cách chuyên nghiệp."
slug: "tu-dong-trich-xuat-thong-ke-video-youtube-google-sheets-n8n"
tags: [n8n, automation, youtube, google-sheets, market-research, no-code]
keywords: [n8n workflow, trích xuất youtube, youtube api google sheets, tự động hóa marketing, agent circle]
---

# 🚀 Tự động trích xuất thống kê video YouTube và lưu vào Google Sheets

Các sếp làm nội dung, YouTube Creator hay Growth Marketer có bao giờ cảm thấy mệt mỏi khi phải ngồi copy từng đường link video, mở YouTube Studio lên để xem số liệu view, like, comment rồi thủ công paste vào Google Sheets chưa? Việc này vừa tốn hàng giờ đồng hồ, vừa dễ xảy ra sai sót khi số lượng video lên tới hàng trăm, hàng nghìn.

Giải pháp ở đây là gì? Hãy để chiếc workflow n8n siêu việt này từ **Agent Circle** thay các sếp làm tất cả! Workflow này sẽ tự động đọc danh sách link video, gọi YouTube API để lấy toàn bộ thông số chi tiết và ghi ngược lại vào Google Sheets 100% tự động không cần chạm tay.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 99% thời gian:** Không còn cảnh copy-paste thủ công số liệu từng video.
- **Dữ liệu thời gian thực, chính xác:** Lấy trực tiếp từ YouTube Data API, bao gồm tiêu đề, lượt xem, lượt thích, bình luận...
- **Quản lý trạng thái thông minh:** Tự đánh dấu trạng thái **Finished** khi thành công hoặc **Error** nếu có lỗi để dễ dàng rà soát.
- **Hoạt động linh hoạt:** Dễ dàng mở rộng, tích hợp thêm các trigger tự động theo lịch trình hoặc sự kiện.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google Cloud Console Project** đã bật quyền truy cập YouTube Data API v3 và Google Sheets API.
- **Tài khoản Google** chứa Google Sheet quản lý danh sách video.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy toàn bộ mã nguồn JSON.
- Trong giao diện n8n Editor, chọn **Add workflow** -> Nhấn vào dấu `...` ở góc trên bên phải -> Chọn **Import from File** hoặc **Import from Clipboard** và dán mã JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các thành phần sau:

- **Chuẩn bị Google Sheet:** Copy mẫu [YouTube - Get Video Statistics Google Sheet template](https://docs.google.com/spreadsheets/d/1I9gyb27WiRHz--g-xi-QH1W3WppZJdSfY6L32-DyUw0/edit?gid=426418282#gid=426418282) về tài khoản của các sếp.
- **Node `Google Sheets - Get Video URLs`**: 
  - Chọn Credentials Google Sheets OAuth2.
  - Trỏ đến đúng file Google Sheet vừa tạo và chọn Tab **Video URLs**.
- **Node `Google Sheets - Update Data`** & **`Google Sheets - Update Data - Error`**:
  - Kết nối chung credentials Google Sheets OAuth2.
  - Cấu hình trỏ đúng về Tab **Video URLs** để cập nhật trạng thái (`Finished` / `Error`) và các chỉ số thống kê.
- **Node `HTTP - Find Video Data`**:
  - Cấu hình Credentials **YouTube OAuth2 API** (hoặc API Key tùy theo cách thiết lập trên Google Cloud Console).
  - Đảm bảo phương thức gọi là `GET` tới endpoint lấy thông tin video của YouTube API.

#### 3. Kích hoạt ⚡️
- Nhập một vài đường link video YouTube vào Google Sheet và đổi trạng thái cột A thành **Ready**.
- Nhấn **Test workflow** trên n8n để kiểm tra xem dữ liệu có được kéo về và cập nhật vào Google Sheet thành công hay không.
- Nếu mọi thứ chạy mượt, hãy bật công tắc **Active** để workflow sẵn sàng vận hành.

### ✍️ Mẹo & gợi ý nâng cao
- **Tự động hóa theo lịch:** Thay thế node `When clicking ‘Test workflow’` bằng node **Schedule Trigger** để workflow tự chạy cào dữ liệu mỗi ngày/mỗi tuần một lần.
- **Cảnh báo lỗi qua Slack/Telegram:** Thêm một nhánh phụ từ node lỗi (`Google Sheets - Update Data - Error`) để bắn tin nhắn thông báo về kênh Telegram hoặc Slack của team khi có video lỗi.
- **Mở rộng chỉ số:** Chỉnh sửa node `HTTP - Find Video Data` để lấy thêm các trường dữ liệu nâng cao như danh mục (category ID), thẻ tags, hoặc thời lượng video nếu cần phân tích sâu hơn.

### 📌 Kết luận
Workflow này là trợ thủ đắc lực giúp các nhà sáng tạo nội dung và marketer tự động hóa toàn bộ quy trình thu thập số liệu YouTube chỉ với vài cú click. Hãy cài đặt ngay hôm nay để tối ưu hóa hiệu suất làm việc cho team của các sếp!