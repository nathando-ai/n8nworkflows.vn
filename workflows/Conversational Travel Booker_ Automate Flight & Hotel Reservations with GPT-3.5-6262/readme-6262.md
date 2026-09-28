---
title: "🌍 **Tự Động Hóa Đặt Chuyến Bay & Khách Sạn Với AI GPT-3.5 – Không Cần Code!**"
description: "Workflow tự động hóa đặt chuyến bay và khách sạn thông minh dựa trên yêu cầu tự nhiên bằng GPT-3.5, gửi xác nhận email tự động và tối ưu hóa quy trình du lịch cho doanh nghiệp. Giảm thời gian xử lý từ 30 phút xuống chỉ 5 giây!"
slug: "tự-dộng-hoa-dat-chuyen-bay-khach-san-voi-gpt-3-5"
tags: [n8n, automation, ai-chatbot, du-lịch, openai, email-automation]
keywords: [n8n workflow đặt chuyến bay, tự động hóa đặt khách sạn với AI, GPT-3.5 tự động hóa du lịch, n8n chatbot đặt vé máy bay, tự động hóa email xác nhận đặt phòng]
---

# 🚀 **Tự Động Hóa Đặt Chuyến Bay & Khách Sạn Với AI GPT-3.5 – Không Cần Code!**

### **Giải pháp AI hoàn toàn tự động hóa đặt vé du lịch – từ yêu cầu tiếng Việt đến xác nhận email chỉ trong 5 giây!**

Hiện nay, việc đặt chuyến bay hoặc khách sạn thủ công không chỉ tốn thời gian mà còn dễ mắc lỗi, đặc biệt khi phải xử lý hàng loạt yêu cầu từ khách hàng. **Workflow này giúp các sếp tự động hóa toàn bộ quy trình đặt vé du lịch bằng AI GPT-3.5**, từ nhận yêu cầu đến gửi xác nhận email hoàn chỉnh – **không cần viết một dòng code nào!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động 24/7 với hiệu suất tối ưu, các sếp nên **self-host n8n trên VPS** để tránh giới hạn của phiên bản cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ nhanh cho API OpenAI)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Xử lý hàng loạt yêu cầu đặt vé trong giây lát thay vì mất giờ.
- **Tính chính xác cao**: AI hiểu yêu cầu tự nhiên (ví dụ: *"Đặt vé từ Hà Nội đến Đà Nẵng ngày 15/12"*) và trả kết quả chính xác.
- **Trải nghiệm cá nhân hóa**: Xác nhận email tự động với thông tin chi tiết, lịch trình và liên kết thanh toán.
- **Hoạt động 24/7**: Không cần can thiệp thủ công, hệ thống tự động xử lý yêu cầu bất kỳ lúc nào.
- **Tích hợp API thực tế**: Kết nối với các API đặt vé (mock hoặc thực tế) và gửi email thông qua SMTP.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **API Key OpenAI**:
   - Đăng ký tài khoản tại [OpenAI](https://platform.openai.com/) và lấy `API Key`.
   - Trong n8n, thêm **credentials** mới với tên `openAiApi` và dán `API Key` vào.

2. **Tài khoản SMTP cho gửi email**:
   - Các sếp cần một tài khoản email (ví dụ: Gmail, Outlook) và **thiết lập SMTP** trong n8n.
   - Thêm **credentials** mới với tên `smtp` và cấu hình:
     - Host: `smtp.gmail.com` (hoặc SMTP của nhà cung cấp email).
     - Port: `587` (hoặc `465` nếu sử dụng SSL).
     - Username/Password: Tài khoản email và mật khẩu (hoặc App Password nếu sử dụng Gmail).
     - Security: `STARTTLS`.

3. **(Tùy chọn) API đặt vé thực tế**:
   - Workflow sử dụng **mock API** để demo, nhưng các sếp có thể thay thế bằng API thực tế như:
     - Skyscanner, Kayak (chuyến bay).
     - Booking.com, Agoda (khách sạn).
   - Cần **API Key** của dịch vụ đó và cấu hình trong node `Flight Search API`/`Hotel Search API`.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/6262](https://n8n.io/workflows/6262) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/6262) và dán vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này bao gồm **12 node** quan trọng, các sếp cần chú ý cấu hình sau:

##### **A. Webhook Trigger**
- **Địa chỉ Webhook**: `booking-request` (được sử dụng trong yêu cầu HTTP POST).
- **Lưu ý**:
  - Các sếp cần **bật Webhook** và lưu địa chỉ URL để gửi yêu cầu đặt vé.
  - Ví dụ: Gửi yêu cầu từ Slack, Telegram, hoặc ứng dụng web bằng `POST` đến URL này.

##### **B. AI Request Parser (GPT-3.5)**
- **Model**: Đã cấu hình sẵn `gpt-3.5-turbo`.
- **Prompt**: Bắt đầu với `{{json.data}}` (lấy dữ liệu từ yêu cầu Webhook).
- **Lưu ý**:
  - AI sẽ phân tích yêu cầu tự nhiên (ví dụ: *"Đặt vé Hà Nội -> Đà Nẵng ngày 15/12"*) và trả về thông tin cấu trúc (ngày, địa điểm, loại vé).
  - Nếu muốn cải thiện, các sếp có thể **tùy chỉnh prompt** trong node này.

##### **C. Booking Type Router (Switch)**
- **Công dụng**: Xác định yêu cầu là **chuyến bay** hay **khách sạn**.
- **Lưu ý**:
  - Node này sử dụng logic từ kết quả của AI để phân luồng sang `Flight Data Processor` hoặc `Hotel Data Processor`.

##### **D. Flight/Hotel Data Processor (Code)**
- **Công dụng**: Xử lý và chuẩn hóa dữ liệu trước khi gọi API.
- **Lưu ý**:
  - Các sếp có thể **mở node này** và xem mã JavaScript để hiểu cách xử lý dữ liệu.
  - Nếu cần thay đổi logic, các sếp có thể chỉnh sửa tại đây.

##### **E. Flight/Hotel Search API (HTTP Request)**
- **Công dụng**: Gọi API để tìm kiếm vé/chỗ ở.
- **Lưu ý**:
  - **Mock API**: Workflow đã cấu hình mock API để demo. Nếu muốn sử dụng API thực tế:
    - Thay đổi `url` trong node này (ví dụ: `https://api.skyscanner.com`).
    - Thêm `headers` và `body` theo yêu cầu của API.
    - Cần **API Key** và cấu hình trong `Authorization`.

##### **F. Flight/Hotel Booking Processor (Code)**
- **Công dụng**: Xử lý xác nhận đặt vé/chỗ.
- **Lưu ý**:
  - Tương tự như `Data Processor`, các sếp có thể chỉnh sửa logic đặt vé.

##### **G. Confirmation Message Generator (GPT-3.5)**
- **Công dụng**: Tạo thông điệp xác nhận email cá nhân hóa.
- **Prompt**: `{{json.data}}` (dữ liệu từ quá trình đặt vé).
- **Lưu ý**:
  - AI sẽ tự động tạo email xác nhận với thông tin chi tiết (mã vé, ngày giờ, liên kết thanh toán).
  - Các sếp có thể **tùy chỉnh prompt** để phù hợp với brand.

##### **H. Send Confirmation Email (EmailSend)**
- **Công dụng**: Gửi email xác nhận đến khách hàng.
- **Lưu ý**:
  - Chọn **credentials SMTP** đã cấu hình trước đó.
  - Thiết lập **người nhận** (`{{$json["email"]}}`) và **tiêu đề email** (ví dụ: *"Xác nhận đặt vé du lịch của bạn"*).

##### **I. Send Response (RespondToWebhook)**
- **Công dụng**: Trả về kết quả cho yêu cầu Webhook (ví dụ: phản hồi từ Slack/Telegram).
- **Lưu ý**:
  - Node này trả về dữ liệu JSON cho yêu cầu gốc (có thể hiển thị trên UI).

---

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Gửi một yêu cầu mẫu đến Webhook (ví dụ: `POST /booking-request` với body JSON:
     ```json
     {
       "message": "Đặt vé từ Hà Nội đến Đà Nẵng ngày 15/12/2024, 2 người, economy",
       "email": "khachhang@example.com"
     }
     ```
   - Kiểm tra kết quả trong **Execution Log** của n8n.

2. **Bật Active**:
   - Chuyển trạng thái workflow sang **Active** để chạy liên tục.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tích hợp với Slack/Telegram**:
   - Sử dụng **node `webhook`** để nhận yêu cầu từ Slack (via `/booking` command) hoặc Telegram bot.
   - Cấu hình **Slack App** hoặc **Telegram Bot** để gửi yêu cầu đến Webhook của n8n.

2. **Lưu log và báo cáo**:
   - Thêm node **`stickyNote`** để ghi lại lịch sử đặt vé.
   - Sử dụng **node `emailSend`** để gửi báo cáo hàng tuần về số lượng đặt vé thành công.

3. **Cải thiện AI với prompt nâng cao**:
   - Tùy chỉnh **prompt** trong `AI Request Parser` để AI hiểu rõ hơn các yêu cầu phức tạp (ví dụ: yêu cầu đặt vé và khách sạn cùng lúc).

4. **Thay thế mock API bằng API thực tế**:
   - Kết nối với **Skyscanner, Booking.com** để đặt vé/chỗ thực tế.
   - Cần **API Key** và cấu hình trong node `HTTP Request`.

5. **Tự động thanh toán**:
   - Kết hợp với **Stripe/PayPal** để xử lý thanh toán tự động sau khi đặt vé.

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn chỉnh** để tự động hóa đặt chuyến bay và khách sạn với AI GPT-3.5, **giảm thời gian xử lý từ 30 phút xuống chỉ 5 giây**! Các sếp không cần viết code, chỉ cần **cấu hình API và SMTP** là có thể chạy workflow 24/7.

👉 **Hãy áp dụng ngay** và tự động hóa quy trình du lịch của doanh nghiệp để **tăng hiệu suất và giảm chi phí**!

---
**Ghi chú cuối**:
- Workflow này **không yêu cầu kiến thức code** nhưng các sếp có thể mở node `code` để học cách xử lý dữ liệu.
- Nếu gặp vấn đề, hãy **check Execution Log** trong n8n để debug.