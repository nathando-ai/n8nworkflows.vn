---
title: "🚀 Tự động tạo ảnh đồng nhất phong cách với Google Gemini và Google Sheets trên n8n"
description: "Xây dựng pipeline tự động hóa tạo ảnh bằng AI với Google Gemini, duy trì phong cách từ ảnh mẫu, quản lý qua Google Sheets và giám sát real-time."
slug: "tao-anh-dong-nhat-phong-cach-gemini-google-sheets"
tags: [n8n, automation, google-gemini, google-sheets, ai-image-generation, content-creation]
keywords: [n8n workflow, tạo ảnh AI, google gemini api, tự động hóa google sheets, ai multimodal]
---

# 🚀 Tự động tạo ảnh đồng nhất phong cách với Google Gemini và Google Sheets

Các sếp làm sáng tạo nội dung, marketing hay thiết kế chắc chắn hiểu cảm giác đau đầu khi phải giữ sự đồng nhất về phong cách (visual style) cho hàng loạt bức ảnh. Việc copy prompt thủ công hay tinh chỉnh từng chút một vừa tốn thời gian lại dễ sai sót. 

Được xây dựng bởi chuyên gia tự động hóa **Adem Tasin**, workflow n8n này sẽ giải quyết trọn vẹn bài toán trên. Hệ thống tự động đọc danh sách prompt từ Google Sheets, phân tích ảnh mẫu bằng Google Gemini để trích xuất phong cách, sau đó tạo ra bức ảnh mới hoàn toàn đồng nhất, lưu trữ trên Google Drive và gửi thông báo trạng thái real-time qua ntfy.sh. Tất cả tự động 100% không cần can thiệp thủ công!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Đồng nhất phong cách 100%:** AI phân tích sâu màu sắc, bố cục và trường phái của ảnh mẫu (`referans_url`) để áp dụng vào ảnh mới.
- **Vận hành hàng loạt (Batch Processing):** Đọc dữ liệu từ Google Sheets, xử lý từng dòng tuần tự tránh nghẽn API.
- **Giám sát thời gian thực:** Tích hợp ntfy.sh gửi thông báo tiến độ, lỗi hoặc hoàn thành ngay lập tức về điện thoại/dashboard.
- **Lưu trữ khoa học:** Tự động convert binary, lưu ảnh vào Google Drive và cập nhật link kèm trạng thái vào Google Sheet.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Google Sheets:** Tài khoản và file Google Sheets quản lý prompt.
- **Google Drive:** Thư mục lưu trữ ảnh xuất ra.
- **Google Gemini API Key:** Tài khoản Google AI Studio để gọi Gemini phân tích và tạo ảnh.
- **ntfy.sh (Tùy chọn):** Kênh thông báo để theo dõi tiến trình chạy.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này hoặc copy toàn bộ JSON, sau đó paste trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các thành phần sau để workflow không báo lỗi:

- **Chuẩn bị Google Sheets:** Tạo một sheet gồm các cột: `gorsel_id`, `ana_prompt`, `stil_prompt`, `referans_url`, `durum` (Trạng thái, ví dụ: "Pending").
- **Nodes Google Sheets & Google Drive:** 
  - Tại các node `Read – Google Sheets – Pending Prompts`, `Update – Google Sheets – Success Status`, và `Update – Google Sheets – Error Status`: Thay thế **Document ID** bằng ID file Google Sheets của các sếp.
  - Tại node `Upload – Google Drive – Store Generated Image`: Thay thế **Folder ID** bằng thư mục chứa ảnh trên Google Drive.
- **Nodes Thông báo (ntfy):** 
  - Các HTTP Request nodes (`ntfy - Start Alert`, `ntfy - Task Error Alert`, v.v.): Thay thế tên topic mặc định `ai-gorsel-uretimi100` thành một chuỗi định danh độc lập của riêng các sếp.
- **Google Gemini Node:** 
  - Kết nối Credentials với `Google Palm/Gemini API`.
  - Node `Analyze – Gemini – Visual Style` sẽ lo việc bóc tách phong cách, còn node `Create – Gemini – New Image From Style` nhận prompt (`ana_prompt`) để tạo ảnh dựa trên khung phong cách đó.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (Test workflow) với 1 dòng dữ liệu mẫu trong Google Sheet thông qua Webhook URL được cung cấp ở node `Webhook`.
- Kiểm tra kết quả trả về trên Google Drive và Google Sheets.
- Bật công tắc **Active** để đưa workflow vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Kiểm soát Rate Limit:** Các node `Wait #1` đến `Wait #4` được đặt khéo léo để tránh việc gọi API quá giới hạn (Rate limit) khi xử lý hàng loạt. Các sếp có thể điều chỉnh thời gian chờ nếu dùng gói API trả phí cao hơn.
- **Mở rộng kênh thông báo:** Thay vì ntfy.sh, các sếp có thể thay thế bằng node Telegram hoặc Slack để nhận thông báo kết quả tạo ảnh trực tiếp vào nhóm chat công việc.
- **Lưu log chi tiết:** Kết hợp thêm một bảng Google Sheet phụ để ghi nhận lịch sử lỗi (Error Log) phục vụ việc tối ưu prompt về sau.

### 📌 Kết luận
Workflow này là cỗ máy tự động hóa hoàn hảo cho những ai cần sản xuất hình ảnh hàng loạt mà vẫn đảm bảo tính nhất quán về mặt nhận diện thương hiệu. Hãy cài đặt ngay hôm nay để giải phóng hàng giờ làm việc thủ công và để AI thay bạn làm phần việc nặng nhọc!