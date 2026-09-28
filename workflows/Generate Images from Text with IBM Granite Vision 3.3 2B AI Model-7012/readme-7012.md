---
title: "🚀 Tự động tạo hình ảnh từ văn bản với mô hình AI IBM Granite Vision 3.3 2B trong n8n"
description: "Hướng dẫn xây dựng workflow n8n tích hợp mô hình IBM Granite Vision 3.3 2B qua Replicate để tự động hóa quy trình tạo ảnh chất lượng cao từ văn bản."
slug: "tao-hinh-anh-tu-van-ban-voi-ibm-granite-vision-3-3-2b-n8n"
tags: [n8n, automation, ai, image-generation, ibm-granite, replicate]
keywords: [n8n workflow, tạo ảnh bằng AI, IBM Granite Vision, Replicate API, tự động hóa nội dung]
---

# 🚀 Tự động tạo hình ảnh từ văn bản với IBM Granite Vision 3.3 2B AI Model

Trong thời đại số, việc sáng tạo nội dung trực quan đòi hỏi tốc độ và sự liên tục. Việc thuê thiết kế riêng hoặc tự tay tạo từng bức ảnh thủ công trên các công cụ AI tốn rất nhiều thời gian chuyển đổi tab và chờ đợi. 

Workflow n8n này sẽ giúp các sếp giải quyết triệt để vấn đề đó! Bằng cách kết hợp sức mạnh của n8n và mô hình **IBM Granite Vision 3.3 2B** (thông qua nền tảng Replicate), các sếp có thể tự động hóa toàn bộ quy trình tạo hình ảnh từ văn bản chỉ với một cú click hoặc kích hoạt từ các hệ thống khác.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Chuyển đổi ý tưởng văn bản thành hình ảnh hoàn chỉnh mà không cần thao tác thủ công trên giao diện web của AI.
- **Tối ưu thời gian:** Xử lý các tác vụ tạo ảnh hàng loạt, tiết kiệm hàng giờ đồng hồ làm việc mỗi tuần.
- **Linh hoạt tích hợp:** Dễ dàng mở rộng kết nối với Google Sheets, Telegram, Slack hoặc CRM để lưu trữ và phân phối hình ảnh tự động.
- **Hoạt động không gián đoạn:** Workflow tích hợp cơ chế chờ (Wait) và kiểm tra trạng thái (Polling) thông minh giúp đảm bảo nhận được kết quả chính xác từ AI.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống **n8n** đang hoạt động (Cloud hoặc Self-hosted).
- Tài khoản trên **Replicate** và **API Key** để gọi mô hình IBM Granite Vision.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ thư viện n8n (Link gốc: [n8n.io/workflows/7012](https://n8n.io/workflows/7012)) và tiến hành Import trực tiếp vào giao diện n8n Editor của mình, hoặc copy/paste trực tiếp JSON vào canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 8 nodes được bố trí logic để xử lý việc tạo và kiểm tra kết quả từ AI:
- **Set API Key (`Set API Key` - Node `set`):** Các sếp cần cấu hình biến chứa Replicate API Key của mình tại đây để các node HTTP Request có quyền gọi API.
- **Tạo tiến trình (`Create Prediction` - Node `httpRequest`):** Gửi câu lệnh (prompt) văn bản đến endpoint của mô hình `ibm-granite/granite-vision-3.3-2b` trên Replicate.
- **Trích xuất ID (`Extract Prediction ID` - Node `code`):** Sử dụng đoạn mã JavaScript nhỏ để lấy `prediction_id` trả về từ bước khởi tạo.
- **Chờ đợi & Kiểm tra trạng thái (`Wait` & `Check Prediction Status` - Nodes `wait` & `httpRequest`):** Do việc tạo ảnh bằng AI mất một khoảng thời gian ngắn, node Wait sẽ tạm dừng workflow trong giây lát trước khi gọi lại API để kiểm tra xem bức ảnh đã render xong chưa.
- **Đánh giá hoàn thành (`Check If Complete` - Node `if`):** Kiểm tra trạng thái trả về (đã xong hay đang xử lý). Nếu xong, chuyển sang bước tiếp theo; nếu chưa, vòng lặp có thể tiếp tục chờ.
- **Xử lý kết quả (`Process Result` - Node `code`):** Lấy link hình ảnh hoàn thiện từ kết quả trả về của AI để phục vụ cho các bước tiếp theo trong hệ thống của các sếp.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** từ node thủ công (`On clicking 'execute'`) để chạy thử nghiệm với dữ liệu mẫu.
- Kiểm tra kết quả đầu ra ở node cuối cùng để đảm bảo link ảnh được trả về chính xác.
- Bật công tắc **Active** ở góc trên bên phải để đưa workflow vào trạng thái vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Google Sheets:** Thay vì dùng Trigger thủ công, các sếp có thể kết nối Google Sheets làm nguồn dữ liệu đầu vào. Mỗi dòng là một đoạn mô tả (prompt), n8n sẽ đọc và tự động tạo ảnh hàng loạt.
- **Nhận ảnh qua Telegram/Slack:** Thêm một node gửi tin nhắn (Telegram/Slack) ngay sau bước `Process Result` để bot tự động gửi bức ảnh vừa tạo thẳng về group chat cho team.
- **Lưu trữ tự động:** Kết nối thêm dịch vụ lưu trữ như Google Drive hoặc AWS S3 để tải ảnh về lưu trữ vĩnh viễn, tránh trường hợp link tạm thời từ Replicate hết hạn.

### 📌 Kết luận
Workflow tích hợp IBM Granite Vision 3.3 2B này là mảnh ghép hoàn hảo giúp tự động hóa quá trình sáng tạo hình ảnh cho các nhà sáng tạo nội dung, marketer và lập trình viên. Hãy import ngay vào n8n của các sếp và bắt đầu "lên đồ" tự động hóa ngay hôm nay!