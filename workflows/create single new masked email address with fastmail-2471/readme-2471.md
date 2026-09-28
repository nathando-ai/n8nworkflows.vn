---
title: "🚀 Tự Động Tạo Email Masked Fastmail Với n8n (Bảo Vệ Quyền Riêng Tư)"
description: "Hướng dẫn chi tiết cách xây dựng workflow n8n để tạo email ẩn danh (masked email) trên Fastmail qua Webhook. Giải pháp bảo mật tuyệt đối cho các sếp cần email dùng một lần."
slug: "tao-email-masked-fastmail-n8n"
tags: [n8n, fastmail, email-automation, privacy, api]
keywords: [n8n workflow, fastmail api, masked email, tự động hóa email, bảo mật email]
---

# 🚀 Tự Động Tạo Email Masked Fastmail Với n8n (Bảo Vệ Quyền Riêng Tư)

Trong thời đại số, việc bảo vệ quyền riêng tư email là một thách thức lớn. Các sếp thường xuyên phải đăng ký dịch vụ, nhận tin nhắn quảng cáo hay làm việc với các đối tác không đáng tin cậy. Việc dùng email chính cho mọi thứ dẫn đến spam, rủi ro lộ thông tin và mất kiểm soát hộp thư.

Workflow này là giải pháp "cứu tinh" giúp các sếp tạo ra các **email masked (email ẩn danh)** trên Fastmail một cách tự động hóa 100% thông qua Webhook. Chỉ với một cú click hoặc lệnh API đơn giản, các sếp có thể tạo ra một địa chỉ email mới, gắn nhãn mô tả và trạng thái cụ thể, sau đó nhận lại kết quả ngay lập tức. Không cần code, không cần mở trình duyệt, mọi thứ diễn ra trong tích tắc.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và đảm bảo tính sẵn sàng cao cho các request API, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Bảo mật tuyệt đối:** Tách biệt email chính khỏi các dịch vụ bên thứ ba, giảm thiểu rủi ro bị lộ email thật.
- **Quản lý tập trung:** Mỗi email masked đều có thể gắn kèm `description` (mô tả) và `state` (trạng thái), giúp các sếp dễ dàng phân loại nguồn gốc email.
- **Tốc độ tức thời:** Tạo email mới trong vài giây thông qua API, không cần thao tác thủ công trên giao diện Fastmail.
- **Tích hợp linh hoạt:** Webhook có thể được gọi từ bất kỳ ứng dụng, script hay workflow n8n khác, mở ra khả năng tự động hóa vô hạn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Fastmail:** Các sếp cần có tài khoản Fastmail (bản trả phí) để sử dụng API.
- **API Credentials:** Cần tạo HTTP Header Authentication trong n8n chứa thông tin xác thực của Fastmail (thường là API Key hoặc Token).
- **n8n Instance:** Một instance n8n đang chạy (cloud hoặc self-hosted).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể import workflow này vào n8n của mình bằng cách:
1. Tải xuống file JSON của workflow từ link gốc hoặc copy toàn bộ code JSON.
2. Mở n8n, chọn **Import from File** hoặc **Import from URL**.
3. Dán JSON vào và nhấn **Import**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình lại các node sau để workflow hoạt động đúng với tài khoản của mình:

- **Node `Session` (HTTP Request):**
  - Đây là node đầu tiên gọi API Fastmail để lấy thông tin session.
  - Các sếp cần chọn **Credentials** đã tạo sẵn (HTTP Header Auth) chứa API Key của Fastmail.
  - Kiểm tra URL API có đúng không (thường là endpoint JMAP của Fastmail).

- **Node `create random masked email` (HTTP Request):**
  - Node này thực hiện việc tạo email masked thực sự.
  - Đảm bảo credentials được chọn giống node `Session`.
  - Body request sẽ được tự động xây dựng dựa trên dữ liệu từ webhook, nhưng các sếp nên kiểm tra cấu trúc JSON gửi đi để đảm bảo khớp với API Fastmail.

- **Node `Webhook`:**
  - Mặc định path là `createMaskedEmail` và method là `POST`.
  - Các sếp có thể đổi path này thành tên dễ nhớ hơn, ví dụ: `new-masked-email`.
  - **Quan trọng:** Nếu các sếp muốn bảo vệ webhook khỏi người lạ, hãy bật tính năng **Authorization** trong node Webhook (sử dụng API Key hoặc Basic Auth).

- **Node `get fields for creation` (Set):**
  - Node này chuẩn bị dữ liệu từ payload webhook.
  - Các sếp có thể chỉnh sửa các trường `state` và `description` nếu muốn đặt giá trị mặc định khác.

- **Node `prepare output` (Set):**
  - Node này định dạng lại dữ liệu trả về.
  - Các sếp có thể thêm các trường thông tin khác vào response nếu cần (ví dụ: ID của email, thời gian tạo...).

#### 3. Kích hoạt ⚡️
1. **Test Run:**
   - Sử dụng `curl` hoặc Postman để gửi một request POST đến webhook.
   - Ví dụ payload:
     ```bash
     curl -X POST -H 'Content-Type: application/json' https://your-n8n-instance/webhook/createMaskedEmail -d '{"state": "active", "description": "Đăng ký newsletter công nghệ"}'
     ```
   - Kiểm tra xem n8n có trả về địa chỉ email masked mới không.
2. **Bật Active:**
   - Sau khi test thành công, các sếp nhấn nút **Active** ở góc trên bên phải để workflow hoạt động liên tục.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp với Telegram/Slack:** Sau khi tạo email masked, các sếp có thể thêm node gửi thông báo vào Telegram hoặc Slack để nhắc nhở mình đã tạo email cho mục đích gì.
- **Lưu vào Google Sheets:** Thêm node Google Sheets để log lại tất cả các email masked đã tạo, kèm theo mô tả và thời gian, giúp quản lý lịch sử dễ dàng.
- **Tự động hủy email:** Tạo một workflow khác để định kỳ kiểm tra và xóa các email masked không còn hoạt động sau một khoảng thời gian nhất định, giữ cho tài khoản Fastmail gọn gàng.
- **Gán nhãn tự động:** Sử dụng AI (LLM) để tự động phân loại `description` dựa trên nội dung email nhận được, giúp các sếp quản lý hộp thư thông minh hơn.

### 📌 Kết luận
Việc bảo vệ quyền riêng tư email không còn là điều xa xỉ khi có n8n và Fastmail. Với workflow này, các sếp có thể tạo ra các email masked một cách nhanh chóng, an toàn và tự động hóa hoàn toàn. Hãy áp dụng ngay để giữ hộp thư chính của mình sạch sẽ và bảo mật hơn. Chúc các sếp thành công!