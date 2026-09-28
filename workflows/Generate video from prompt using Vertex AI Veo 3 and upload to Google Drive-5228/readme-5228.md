---
title: "🚀 Tự động tạo video từ văn bản với Vertex AI Veo 3 và Google Drive trên n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình tạo video bằng AI từ text prompt sử dụng Vertex AI Veo 3 và lưu trữ trực tiếp lên Google Drive."
slug: "tao-video-tu-van-ban-vertex-ai-veo-google-drive-n8n"
tags: [n8n, automation, ai, vertex-ai, google-drive, video-generation]
keywords: [n8n workflow, vertex ai veo 3, tao video tu text, google drive automation, ai video generator]
---

# 🚀 Tự động tạo video từ văn bản với Vertex AI Veo 3 và Google Drive

Các sếp có bao giờ cảm thấy mệt mỏi khi phải tốn hàng giờ liền để tạo và quản lý video thủ công cho các chiến dịch marketing? Việc lên ý tưởng, render video và tải lên lưu trữ trên cloud tốn rất nhiều thời gian và thao tác lặp đi lặp lại. 

Đừng lo, bài toán này sẽ được giải quyết triệt để với workflow n8n tích hợp **Vertex AI Veo 3** và **Google Drive**. Chỉ với một form nhập liệu đơn giản, hệ thống sẽ tự động hóa 100% quy trình từ việc nhận prompt, gọi AI render video cho đến khi lưu file hoàn chỉnh lên Google Drive mà không cần động tay chân!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Chuyển đổi ý tưởng thành video chỉ qua một form nhập liệu trực tuyến.
- **Tiết kiệm thời gian:** Không cần thao tác thủ công trên các công cụ tạo video phức tạp và tải lên Drive thủ công.
- **Đồng bộ thông minh:** Video sau khi render xong sẽ tự động được lưu trữ gọn gàng trên Google Drive để sẵn sàng sử dụng.
- **Hoạt động 24/7:** Chạy ngầm liên tục trên server, sẵn sàng xử lý yêu cầu bất cứ lúc nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Khuyên dùng Self-hosted trên VPS).
- **Google Cloud Platform (GCP) Account:** Đã kích hoạt Vertex AI và chuẩn bị sẵn `Project ID`, `Location`.
- **GCP Access Token:** Dùng để xác thực API gọi đến Vertex AI.
- **Google Drive Account:** Cấp quyền kết nối (OAuth2) với n8n để tải file video lên.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ nguồn gốc (`https://n8n.io/workflows/5228`) và import trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình kỹ các node quan trọng sau:

- **Node `On form submission` (Form Trigger):** Thiết lập giao diện form để người dùng nhập text prompt và cung cấp GCP Access Token.
- **Node `Setting` (Set):** Cấu hình các biến môi trường cho GCP như:
  - `PROJECT_ID`: ID dự án Google Cloud của các sếp.
  - `MODEL_VERSION`: Phiên bản model Veo 3.
  - `LOCATION`: Khu vực đặt server GCP (ví dụ: `us-central1`).
  - `API_ENDPOINT`: Endpoint gọi API của Vertex AI.
- **Node `Vertex AI-VEO3` (HTTP Request):** Gửi yêu cầu (prompt) tới Veo3 sử dụng endpoint `predictLongRunning`.
- **Node `Wait`:** Đợi quá trình render video hoàn tất từ phía Vertex AI.
- **Node `Vertex AI-fetch` (HTTP Request):** Lấy kết quả video trả về sau khi render xong.
- **Node `Convert to File` (Convert to File):** Chuyển đổi dữ liệu Base64 nhận được từ API thành file nhị phân (Binary).
  - *Base64 Input Field:* `response.videos[0].bytesBase64Encoded`
- **Node `Google Drive` (Google Drive):** Cấu hình tài khoản Google Drive OAuth2 để tự động tải file video vừa convert lên thư mục chỉ định trên Drive.

> **💡 Mẹo lấy GCP Access Token:** 
> Các sếp có thể chạy câu lệnh sau trong VM hoặc Google Cloud Shell để lấy token nhanh chóng:
> ```bash
> gcloud auth print-access-token
> ```

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng cách điền form mẫu để kiểm tra toàn bộ luồng chạy.
- Sau khi test thành công, bật công tắc **Active** để đưa workflow vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node Telegram hoặc Slack vào cuối workflow để nhận thông báo ngay khi video được tạo và tải lên Google Drive thành công.
- **Lưu lịch sử:** Thêm node Google Sheets để ghi lại nội dung prompt, thời gian tạo và link Google Drive của video để dễ dàng quản lý.
- **Tự động hóa nâng cao:** Kết hợp nhận prompt tự động từ một bảng Google Sheets hoặc hệ thống CRM thay vì phải điền form thủ công.

### 📌 Kết luận
Workflow tự động hóa tạo video với Vertex AI Veo 3 và Google Drive là một "vũ khí" cực kỳ lợi hại giúp tối ưu hóa quy trình sáng tạo nội dung cho các nhà quản lý và nhà sáng tạo. Hãy cài đặt ngay lên hệ thống n8n của các sếp để trải nghiệm sức mạnh của AI trong tự động hóa doanh nghiệp!