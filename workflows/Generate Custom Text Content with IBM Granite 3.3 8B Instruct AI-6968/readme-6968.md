---
title: "🚀 Tự động tạo nội dung văn bản tùy chỉnh với IBM Granite 3.3 8B Instruct AI trên n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa việc tạo nội dung văn bản chất lượng cao sử dụng mô hình IBM Granite 3.3 8B Instruct thông qua Replicate API, giúp tiết kiệm thời gian tối đa."
slug: "tao-noi-dung-tu-dong-voi-ibm-granite-3-3-8b-instruct-n8n"
tags: [n8n, automation, no-code, ai, content-creation, ibm-granite, replicate]
keywords: [n8n workflow, ibm granite 3.3 8b, tạo nội dung tự động, replicate api, ai automation, no-code ai]
---

# 🚀 Tự động tạo nội dung văn bản tùy chỉnh với IBM Granite 3.3 8B Instruct AI

Việc sáng tạo nội dung, viết bài marketing hay tổng hợp thông tin thủ công ngốn rất nhiều thời gian và năng lượng của các doanh nghiệp. Nếu các sếp đang tìm kiếm một giải pháp tích hợp trí tuệ nhân tạo (AI) mạnh mẽ để tự động hóa toàn bộ quy trình sinh văn bản mà không muốn phụ thuộc vào các giải pháp tốn kém, thì đây chính là câu trả lời.

Workflow n8n này sẽ giúp các sếp kết nối trực tiếp với mô hình **IBM Granite 3.3 8B Instruct** (thông qua nền tảng Replicate) để tự động tạo ra các đoạn văn bản, bài viết, hoặc nội dung tùy chỉnh theo yêu cầu chỉ trong chớp mắt. Toàn bộ quy trình chạy hoàn toàn tự động, mượt mà và không cần can thiệp thủ công.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Sinh nội dung văn bản chất lượng cao theo yêu cầu định sẵn mà không cần gõ phím thủ công.
- **Sử dụng mô hình AI tiên tiến:** Tận dụng sức mạnh của IBM Granite 3.3 8B Instruct thông qua Replicate API với tốc độ xử lý nhanh chóng.
- **Quy trình chuẩn hóa thông minh:** Xử lý bất đồng bộ (Asynchronous prediction) chuyên nghiệp với các bước chờ (Wait) và kiểm tra trạng thái tự động.
- **Dễ dàng mở rộng:** Dễ dàng kết nối đầu ra với Google Sheets, Slack, Email hoặc CRM tùy theo nhu cầu của doanh nghiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Replicate Account:** Tài khoản trên [Replicate](https://replicate.com/) để lấy API Key (vì workflow sử dụng mô hình AI từ nền tảng này).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ thư viện n8n (Link gốc: [n8n Workflow #6968](https://n8n.io/workflows/6968)) hoặc copy toàn bộ mã nguồn JSON dán thẳng vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm **8 nodes** chính được thiết kế để gọi API, chờ kết quả và xử lý dữ liệu trả về. Các sếp cần chú ý cấu hình các node sau:

- **Set API Key (Node loại `set`):**
  - Tại đây, các sếp cần cấu hình biến chứa **Replicate API Key** của mình để các node gọi HTTP phía sau có quyền truy cập hệ thống.
- **Create Prediction (Node loại `httpRequest`):**
  - Node này gửi request đến Replicate để khởi tạo tiến trình tạo văn bản với mô hình `ibm-granite/granite-3.3-8b-instruct`. Kiểm tra lại phần Body/Payload để chắc chắn prompt truyền vào đúng với mong muốn.
- **Extract Prediction ID & Check Prediction Status / Check If Complete:**
  - Các node `code`, `wait`, `httpRequest`, và `if` phối hợp nhịp nhàng để lấy ID của tiến trình, tạm dừng chờ AI xử lý, kiểm tra trạng thái và rẽ nhánh khi hoàn thành. Các sếp hầu như không cần sửa logic ở các node này trừ khi muốn thay đổi thời gian `Wait`.
- **Process Result (Node loại `code`):**
  - Nhận dữ liệu text đã được AI tạo ra và định dạng lại cấu trúc JSON sạch sẽ để các sếp dễ dàng sử dụng cho các bước tiếp theo trong n8n.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử nghiệm thủ công với node **On clicking 'execute' (`manualTrigger`)**.
- Kiểm tra kết quả trả về ở node cuối cùng để đảm bảo AI đã sinh nội dung chính xác.
- Bật công tắc **Active** để workflow sẵn sàng hoạt động ở chế độ tự động.

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa workflow này cho công việc thực tế, các sếp có thể:
1. **Thay đổi Trigger:** Thay thế `manualTrigger` bằng `Webhook` hoặc `Schedule Trigger` để tự động tạo nội dung theo lịch trình hoặc nhận yêu cầu từ ứng dụng khác.
2. **Lưu trữ tự động:** Nối thêm node **Google Sheets** hoặc **Notion** ở cuối workflow để tự động lưu lại toàn bộ các đoạn văn bản AI vừa tạo.
3. **Giao tiếp qua Chat:** Tích hợp thêm node **Telegram** hoặc **Slack** để bot tự động gửi kết quả nội dung vừa tạo về group chat ngay khi hoàn thành.

### 📌 Kết luận
Workflow tích hợp IBM Granite 3.3 8B Instruct AI này là một "vũ khí" đắc lực giúp các marketer, nhà sáng tạo nội dung và doanh nghiệp tối ưu hóa thời gian sản xuất content. Hãy cài đặt ngay lên hệ thống n8n của các sếp để trải nghiệm sức mạnh tự động hóa thời đại AI!