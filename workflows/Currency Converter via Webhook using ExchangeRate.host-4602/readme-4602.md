---
title: "💱 Tự động quy đổi ngoại tệ qua Webhook trong n8n với ExchangeRate.host"
description: "Hướng dẫn xây dựng API chuyển đổi tiền tệ tự động 100% bằng n8n, tích hợp dịch vụ ExchangeRate.host qua Webhook cực nhanh chóng và bảo mật."
slug: "tu-dong-quy-doi-ngoai-te-n8n-exchangerate-host"
tags: [n8n, automation, no-code, api-integration, webhook, finance]
keywords: [n8n workflow, đổi tiền tệ n8n, exchangerate host, api conversion, tự động hóa tài chính]
---

# 💱 Tự động quy đổi ngoại tệ qua Webhook trong n8n với ExchangeRate.host

Các sếp có đang gặp khó khăn khi cần tích hợp tính năng quy đổi tỷ giá ngoại tệ vào các ứng dụng nội bộ, website hay hệ thống CRM của công ty? Việc viết code thủ công gọi API liên tục vừa tốn thời gian, vừa khó bảo trì và dễ phát sinh lỗi khi nhà cung cấp dịch vụ thay đổi cấu trúc dữ liệu.

Đừng lo! Bài viết này sẽ hướng dẫn các sếp triển khai ngay một API quy đổi tiền tệ thu nhỏ hoàn toàn tự động chỉ với 3 nodes trong n8n, kết nối trực tiếp với dịch vụ **ExchangeRate.host** thông qua Webhook. Giải pháp này giúp hệ thống của các sếp lấy tỷ giá chuẩn xác theo thời gian thực mà không cần viết một dòng code phức tạp nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và phản hồi API tức thì, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Nhận request qua Webhook, gọi API quy đổi và trả về kết quả ngay lập tức dưới dạng JSON.
- **Bảo mật tuyệt đối:** API Key của ExchangeRate.host được lưu trữ an toàn trong hệ thống credentials của n8n, tuyệt đối không bị lộ ra ngoài qua Webhook request.
- **Dễ dàng tích hợp:** Có thể kết nối mượt mà với bất kỳ hệ thống nào (CRM, Website, Bot Telegram, Mobile App) hỗ trợ gửi HTTP POST.
- **Hoạt động bền bỉ 24/7:** Vận hành ổn định trên nền tảng n8n self-hosted không giới hạn số lượng request nội bộ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống **n8n** đang hoạt động (Cloud hoặc Self-hosted).
- Tài khoản tại [ExchangeRate.host](https://exchangerate.host/) để lấy **API Key**.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng file JSON của workflow này, sao chép (copy) đoạn mã JSON từ nguồn gốc và dán (paste) trực tiếp vào giao diện n8n Editor của mình. Workflow gồm 3 nodes cơ bản:
1. `Receive Conversion Request Webhook` (Webhook)
2. `Convert Currency` (HTTP Request)
3. `Respond with Converted Amount` (Respond to Webhook)

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống hoạt động trơn tru, các sếp cần cấu hình chính xác các điểm sau:

* **Node `Receive Conversion Request Webhook`:**
  - Node này lắng nghe các yêu cầu dạng `POST` tại đường dẫn `/convert-currency`.
  - Body của request gửi lên cần truyền vào định dạng JSON với 3 thuộc tính bắt buộc:
    - `from`: Mã tiền tệ gốc (chuẩn ISO 4217 gồm 3 chữ cái, ví dụ: `USD`).
    - `to`: Mã tiền tệ đích (ví dụ: `EUR` hoặc `VND`).
    - `amount`: Số tiền cần quy đổi (kiểu số).

* **Node `Convert Currency` (HTTP Request):**
  - Node này thực hiện gọi API GET đến ExchangeRate.host.
  - Các sếp cần tạo một **Credential** mới loại `HTTP Query Auth` để lưu **API Key** của ExchangeRate.host. Việc này giúp key tự động được gắn vào tham số truy vấn (`access_key`) một cách bảo mật, không bị lộ trong Body hay URL của Webhook.

* **Node `Respond with Converted Amount`:**
  - Nhận kết quả trả về từ ExchangeRate.host và gửi ngược lại kết quả cho bên gọi Webhook. 

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** và thử gửi một request POST mẫu qua Postman hoặc cURL để kiểm tra dữ liệu trả về.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để đưa workflow vào trạng thái vận hành tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu lịch sử giao dịch:** Thêm một node Google Sheets hoặc Database (PostgreSQL/MySQL) ngay trước node trả phản hồi để ghi lại lịch sử mỗi lần quy đổi tiền tệ.
- **Thông báo qua Telegram/Slack:** Tích hợp thêm nhánh gửi thông báo về kênh chat nội bộ khi có lượng request quy đổi ngoại tệ lớn hoặc khi API gặp sự cố.
- **Xử lý ngoại lệ (Error Handling):** Bổ sung Error Trigger để bắt lỗi trong trường hợp mã tiền tệ người dùng nhập không hợp lệ hoặc hết hạn mức API.

### 📌 Kết luận
Workflow quy đổi ngoại tệ qua Webhook này là một "building block" cực kỳ nhỏ gọn nhưng mang lại giá trị cao, giúp các sếp nhanh chóng bổ sung tính năng tài chính vào hệ sinh thái phần mềm của mình mà không tốn công sức lập trình phức tạp. Hãy triển khai ngay hôm nay để tối ưu hóa quy trình làm việc!