---
title: "🚀 Tự động tạo hàng loạt hình ảnh AI với Freepik, Google Sheets và Google Drive trong n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình tạo ảnh AI hàng loạt từ Google Sheets bằng Freepik API và lưu trữ trực tiếp lên Google Drive."
slug: "tao-anh-ai-hang-loat-freepik-google-sheets-drive-n8n"
tags: [n8n, automation, no-code, freepik, google-sheets, google-drive, ai-image-generation]
keywords: [n8n workflow, tạo ảnh ai hàng loạt, freepik api, google sheets automation, tự động hóa n8n]
---

# 🚀 Tự động tạo hàng loạt hình ảnh AI với Freepik, Google Sheets & Google Drive

Các sếp có bao giờ cảm thấy đuối sức khi phải ngồi copy từng câu lệnh (prompt), dán vào công cụ tạo ảnh AI, rồi lại tải về máy và upload lên Google Drive cho hàng chục hoặc hàng trăm ý tưởng thiết kế? Công việc thủ công này ngốn rất nhiều thời gian, làm gián đoạn sự sáng tạo và cực kỳ dễ nhầm lẫn.

Đừng lo, bài toán đó sẽ được giải quyết triệt để với **Workflow n8n tự động hóa 100%**. Workflow này được thiết kế bởi chuyên gia Robert Breen, giúp đọc danh sách prompt từ Google Sheets, gọi Freepik API để tạo ảnh hàng loạt (có hỗ trợ nhân bản biến thể), chuyển đổi dữ liệu và tự động lưu trữ gọn gàng vào thư mục Google Drive của các sếp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Không cần thao tác thủ công, chỉ cần điền prompt vào Google Sheets và bấm chạy.
- **Nhân đôi sáng tạo:** Node code thông minh giúp tự động tạo nhiều biến thể hình ảnh cho cùng một prompt.
- **Lưu trữ khoa học:** Hình ảnh được tự động đổi tên và lưu vào đúng thư mục Google Drive đã chọn.
- **Tiết kiệm thời gian:** Xử lý hàng loạt hình ảnh AI chỉ trong vài phút, tối ưu hóa năng suất làm việc cho đội ngũ marketing và thiết kế.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Freepik API Key:** Tài khoản Freepik Developer để gọi API tạo ảnh (`/v1/ai/text-to-image`).
- **Google Account:** Kết nối Google Sheets và Google Drive qua OAuth2.
- **Template Google Sheet:** Bản sao của [Google Sheet mẫu này](https://docs.google.com/spreadsheets/d/1_u9IxEZINcwKQB15Rfx7C1hM71zeDST58Fz3nRHTCUY/edit?usp=sharing).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trong n8n, sau đó copy toàn bộ JSON của workflow hoặc import file JSON trực tiếp vào giao diện n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động mượt mà, các sếp cần cấu hình chính xác các node sau:

- **Get Prompt from Google Sheet (Google Sheets):**
  - Chọn Credentials: Google Sheets OAuth2.
  - **Document ID**: Dán ID của Google Sheet (lấy từ URL của bảng tính mẫu).
  - **Sheet Name**: `Sheet1` (hoặc tên tab tương ứng).
  - **Operation**: `Read`.

- **Double Output (Code Node):**
  - Node này dùng để nhân bản mỗi prompt thành 2 biến thể (`run: 1` và `run: 2`). Các sếp có thể giữ nguyên đoạn mã JavaScript có sẵn trên canvas để tạo nhiều phiên bản hình ảnh.

- **Create Image (HTTP Request):**
  - **Method**: `POST`
  - **URL**: `https://api.freepik.com/v1/ai/text-to-image`
  - **Authentication**: Generic → HTTP Header Auth (Điền API Key Freepik của các sếp).
  - **Send Body**: `true`
  - **Body Parameters**: Thêm tham số `prompt` với giá trị là `={{ $json.Prompt }}`.

- **Split Responses (Split Out):**
  - **Field to Split Out**: `data` (giúp tách các hình ảnh trả về từ API).

- **Convert to File (Convert to File):**
  - **Operation**: `toBinary`
  - **Source Property**: `base64` (chuyển đổi dữ liệu ảnh base64 sang dạng file nhị phân).

- **Upload Image to Google Drive (Google Drive):**
  - Chọn Credentials: Google Drive OAuth2.
  - **Operation**: `Upload`
  - **Name**: `=Image - {{ $('Get Prompt from Google Sheet').item.json.Name }} - {{ $('Double Output').item.json.run }}`
  - **Drive ID**: `My Drive`
  - **Folder ID**: Dán ID thư mục Google Drive nơi các sếp muốn lưu ảnh.

#### 3. Kích hoạt ⚡️
- Bấm nút **Execute Workflow** ở node `Start Workflow` để test thử với dữ liệu mẫu.
- Kiểm tra kết quả trong Google Drive xem ảnh đã được tạo và lưu đúng tên chưa.
- Sau khi test OK, gạt công tắc **Active** góc trên cùng bên phải để bật workflow chạy chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Thêm node Slack hoặc Telegram ở cuối workflow để nhận thông báo ngay khi hệ thống tạo xong loạt ảnh mới.
- **Mở rộng nguồn dữ liệu:** Thay vì đọc từ Google Sheets, các sếp có thể nhận prompt từ Airtable hoặc Notion.
- **Ghi log kết quả:** Thêm một bước cập nhật ngược lại Google Sheets (ghi trạng thái "Đã xong" hoặc link ảnh Google Drive) để dễ dàng theo dõi tiến độ.

### 📌 Kết luận
Workflow tạo ảnh AI hàng loạt với Freepik, Google Sheets và Google Drive là một "vũ khí" cực mạnh giúp tiết kiệm hàng giờ đồng hồ mỗi ngày cho việc sản xuất content trực quan. Hãy áp dụng ngay vào hệ thống của các sếp để tối ưu hóa quy trình làm việc ngay hôm nay!