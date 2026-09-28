---
title: "🚀 Tự Động Hóa Tạo Video AI Avatar Hàng Loạt Với HeyGen Và Google Sheets Trong n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình tạo video AI Avatar từ kịch bản Google Sheets bằng HeyGen API, giúp tiết kiệm hàng giờ sản xuất nội dung."
slug: "tu-dong-hoa-tao-video-ai-avatar-heygen-google-sheets-n8n"
tags: [n8n, automation, heygen, google-sheets, ai-video, marketing]
keywords: [n8n workflow, tạo video ai, heygen api, google sheets automation, tự động hóa marketing, ai avatar]
---

# 🚀 Tự Động Hóa Tạo Video AI Avatar Hàng Loạt Với HeyGen Và Google Sheets

Các sếp có đang gặp khó khăn khi phải sản xuất hàng loạt video AI Avatar cho các chiến dịch marketing, chăm sóc khách hàng hay phễu bán hàng không? Việc copy-paste từng đoạn kịch bản vào nền tảng HeyGen, chờ đợi render rồi tải về thủ công chắc chắn ngốn rất nhiều thời gian và công sức. 

Đừng lo, bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n tự động hóa 100% quy trình này: Lấy kịch bản từ **Google Sheets**, gọi **HeyGen API** để khởi tạo và kiểm tra trạng thái video, sau đó tự động trả link video hoàn chỉnh ngược lại vào bảng tính. Tất cả đều không cần một dòng code phức tạp nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa sản xuất nội dung:** Biến hàng trăm dòng kịch bản thành video AI Avatar chỉ trong vài cú click.
- **Đồng bộ dữ liệu mượt mà:** Link video hoàn chỉnh được tự động cập nhật thẳng vào Google Sheets, giúp dễ dàng quản lý và tải về.
- **Tiết kiệm thời gian tuyệt đối:** Loại bỏ hoàn toàn thao tác thủ công lặp đi lặp lại trên giao diện HeyGen.
- **Khả năng mở rộng cao:** Dễ dàng tích hợp thêm các trigger khác (như Webhook từ CRM hoặc Telegram bot) để tạo video theo thời gian thực.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt đầu "lên đồ", các sếp cần chuẩn bị sẵn:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản HeyGen** kèm theo **API Key** (để cấu hình HTTP Request Header Auth).
- **Google Account** đã tạo sẵn một Google Sheet với các cột cơ bản (ví dụ: `Script/voice text`, `Final Video Link`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trên n8n, sau đó copy toàn bộ JSON của workflow này hoặc import file JSON trực tiếp vào giao diện n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru, các sếp cần cấu hình chính xác các node sau:

- **Node `Google Sheets` (Đọc dữ liệu):** 
  - Kết nối tài khoản Google Sheets OAuth2 API của các sếp.
  - Trỏ tới file Google Sheet vừa chuẩn bị (ví dụ: bảng *AI Avatar Script*).
  - Cấu hình lấy dữ liệu từ cột chứa kịch bản (`Script/voice text`).

- **Node `creating Video` (HTTP Request - Tạo Video):**
  - **Method:** `POST`
  - **URL:** `https://api.heygen.com/v2/video/generate`
  - **Authentication:** Cấu hình `HTTP Header Auth` với API Key lấy từ tài khoản HeyGen của các sếp.
  - Sử dụng JSON payload chứa thông tin `video_id`, `voice_id` và văn bản kịch bản lấy từ Google Sheets.

- **Node `Get Video` (HTTP Request - Kiểm tra trạng thái video):**
  - **Method:** `GET`
  - **URL:** `https://api.heygen.com/v2/avatar/avatar_id/details` (hoặc endpoint kiểm tra trạng thái video tương ứng của HeyGen API).
  - Truyền tham số `video-id` lấy ra từ kết quả của node `creating Video` phía trước để nhận về link video hoàn chỉnh.

- **Node `Google Sheets1` (Ghi dữ liệu):**
  - **Operation:** `append` (Thêm dòng mới hoặc cập nhật dòng hiện tại).
  - Ghép nối tham số trả về từ HTTP Request (Link video hoàn chỉnh) vào cột `Final Video Link` trong Google Sheets.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Test workflow** để chạy thử nghiệm với một dòng kịch bản mẫu và kiểm tra kết quả trả về trong Google Sheets.
- Sau khi test thành công, bật công tắc **Active** để đưa workflow vào trạng thái vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo qua Telegram/Slack:** Thêm một node Telegram hoặc Slack ở cuối workflow để bắn thông báo ngay cho sếp hoặc team khi video đã render xong xuôi.
- **Lưu trữ tự động:** Kết hợp thêm node tải file để tự động lưu video từ link HeyGen về Google Drive hoặc OneDrive cá nhân.
- **Chạy tự động định kỳ:** Thay vì dùng `Manual Trigger`, các sếp có thể đổi thành `Schedule Trigger` để hệ thống tự quét bảng Google Sheets và tạo video vào mỗi khung giờ cố định trong ngày.

### 📌 Kết luận
Việc tự động hóa sản xuất video AI chưa bao giờ dễ dàng đến thế với sự kết hợp giữa n8n, Google Sheets và HeyGen. Hãy áp dụng ngay workflow này để tối ưu hóa hiệu suất làm nội dung số của các sếp ngay hôm nay!