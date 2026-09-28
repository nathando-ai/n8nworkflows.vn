---
title: "🚀 Tự động giải reCAPTCHA v2 bằng CapSolver trong n8n"
description: "Workflow n8n cho phép nhận yêu cầu qua webhook, tự động giải reCAPTCHA v2 bằng CapSolver và trả kết quả, chạy định kỳ mỗi giờ."
slug: "tu-dong-giai-recaptcha-v2-bang-capsolver"
tags: [n8n, automation, no-code, captcha, capsolver]
keywords: [n8n workflow, tự động hóa, giải captcha, CapSolver, reCAPTCHA v2]
---

# 🚀 Tự động giải reCAPTCHA v2 bằng CapSolver trong n8n

Khi các dự án **scraping**, **automation** hay **AI agent** gặp phải reCAPTCHA v2, việc giải thủ công hoặc mua phần mềm trả phí thường tốn thời gian, chi phí và không ổn định. Các sếp thường phải dừng quy trình, mất dữ liệu và giảm năng suất.  

**Workflow này** sẽ nhận yêu cầu giải captcha qua webhook, giao cho dịch vụ CapSolver (một nhà cung cấp giải captcha nhanh, đáng tin cậy) và trả lại token đã giải ngay trong vòng vài giây. Ngoài ra, workflow còn có chế độ **định kỳ mỗi giờ** để kiểm tra trạng thái các task đang chờ, đồng thời cung cấp **công cụ test thủ công** để các sếp có thể kiểm tra nhanh trước khi đưa vào sản xuất.

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm thời gian**: Giải captcha tự động trong < 5 giây, không cần can thiệp thủ công.  
- **Độ chính xác cao**: CapSolver có tỷ lệ giải thành công > 95 % cho reCAPTCHA v2.  
- **Hoạt động liên tục**: Workflow chạy 24/7, tự động xử lý mọi yêu cầu đến.  
- **Dễ mở rộng**: Có thể tích hợp ngay vào các pipeline scraping, bot, hoặc AI workflow.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **Tài khoản CapSolver** và **API Key** (được cấp trong dashboard của CapSolver).  
- **n8n** đã được cài đặt (Self‑hosted hoặc Cloud).  
- Quyền **HTTP Request** để gọi endpoint reCAPTCHA của Google (`https://www.google.com/recaptcha/api/siteverify`).  
- (Tùy chọn) **Domain** đã đăng ký với reCAPTCHA v2 để lấy `sitekey` và `secret`.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. **Tải file JSON** của workflow (từ trang gốc https://n8n.io/workflows/13996).  
2. Vào **n8n Editor → Import** → Chọn **Upload JSON** hoặc **Paste JSON**.  
3. Nhấn **Import** → Workflow sẽ xuất hiện với 13 node như mô tả.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Mô tả | Cấu hình cần chỉnh |
|------|------|--------------------|
| **Receive Solver Request** (Webhook) | Nhận POST request chứa `sitekey`, `url` và các tham số tùy chỉnh. | - **Path**: `solve-recaptcha-v2` (đã có). <br> - **Method**: `POST`. <br> - **Authentication**: nếu muốn bảo mật, bật **Basic Auth** hoặc **Header Auth**. |
| **CapSolver [Webhook]** | Gửi yêu cầu giải captcha tới CapSolver. | - **Credentials**: chọn **CapSolver API** (cần tạo credential với API Key). <br> - **Task Type**: `RecaptchaV2`. <br> - **SiteKey**: lấy từ payload (`{{$json["sitekey"]}}`). <br> - **PageURL**: lấy từ payload (`{{$json["url"]}}`). |
| **Return Solver Result** (Respond to Webhook) | Trả token đã giải về client. | - **Response Body**: `{{$node["CapSolver [Webhook]"].json["solution"]["gRecaptchaResponse"]}}`. |
| **Schedule Trigger (Every 1h)** | Kích hoạt quy trình kiểm tra trạng thái các task đang chờ. | - **Cron**: `0 * * * *` (mỗi đầu giờ) – có thể tùy chỉnh. |
| **Set Target Params** (Set) | Định dạng dữ liệu gửi tới CapSolver khi chạy theo lịch. | - Thêm các trường: `sitekey`, `url`, `type: "RecaptchaV2"` (hoặc lấy từ biến môi trường). |
| **CapSolver [Schedule]** | Giải captcha cho các task được lên lịch. | - **Credentials**: **CapSolver API** (cùng như trên). <br> - **Task Type**: `RecaptchaV2`. <br> - **SiteKey** & **PageURL**: lấy từ node **Set Target Params** (`{{$json["sitekey"]}}`, `{{$json["url"]}}`). |
| **Submit Token** (HTTP Request) | Gửi token đã giải tới endpoint xác thực của Google. | - **Method**: `POST`. <br> - **URL**: `https://www.google.com/recaptcha/api/siteverify`. <br> - **Body (Form‑URL‑Encoded)**: `secret={{$json["secret"]}}&response={{$node["CapSolver [Schedule]"].json["solution"]["gRecaptchaResponse"]}}&remoteip={{$json["remoteIp"]}}`. |
| **Check Result** (If) | Kiểm tra phản hồi `success` từ Google. | - **Condition**: `{{$json["success"]}} === true`. |
| **Monitor Passed** (Set) | Ghi log/đánh dấu task thành công. | - Thêm trường `status: "passed"` và thời gian. |
| **Monitor Failed** (Set) | Ghi log/đánh dấu task thất bại. | - Thêm trường `status: "failed"` và lý do (`error-codes`). |
| **Manual Trigger (Test)** | Dùng để test nhanh workflow mà không cần webhook. | - Không cần cấu hình đặc biệt. |
| **CapSolver [Manual]** | Giải captcha trong chế độ test. | - **Credentials**: **CapSolver API**. <br> - **Task Type**: `RecaptchaV2`. <br> - **SiteKey** & **PageURL**: nhập tĩnh hoặc lấy từ **Manual Trigger** payload. |
| **Format Result** (Set) | Định dạng lại kết quả trả về cho test. | - Trả về `{ token: {{$node["CapSolver [Manual]"].json["solution"]["gRecaptchaResponse"]}} }`. |

> **Lưu ý:** Mọi node có trường `Credentials` đều phải **tạo credential** trong n8n → **Credentials → New Credential → CapSolver API** và dán **API Key** của bạn.

#### 3. Kích hoạt ⚡️
1. **Test chạy**: Dùng **Manual Trigger** → nhập `sitekey` & `url` → chạy workflow → kiểm tra `Format Result`.  
2. **Kiểm tra webhook**: Gửi POST tới `https://<your-n8n-domain>/webhook/solve-recaptcha-v2` với JSON `{ "sitekey": "...", "url": "https://example.com" }`. Đảm bảo nhận được `gRecaptchaResponse`.  
3. Khi mọi thứ ổn, **bật** nút **Active** trên workflow để cho phép webhook và schedule hoạt động liên tục.

### ✍️ Mẹo & gợi ý nâng cao
- **Gửi log vào Slack/Telegram**: Thêm node **Slack** hoặc **Telegram** vào `Monitor Passed` / `Monitor Failed` để nhận thông báo ngay khi có lỗi.  
- **Lưu lịch sử**: Kết nối **MongoDB** hoặc **Google Sheets** để lưu lịch sử token, thời gian, trạng thái – hữu ích cho audit.  
- **Retry tự động**: Thêm node **Function** sau `Check Result` để tự động retry tối đa 3 lần nếu `success` = false.  
- **Giới hạn tốc độ**: Dùng node **Delay** hoặc **Rate Limit** nếu bạn có quota API CapSolver hạn chế.  

### 📌 Kết luận
Với workflow này, các sếp có thể **tự động giải reCAPTCHA v2** trong mọi quy trình mà không cần viết code, giảm chi phí và tăng độ tin cậy. Hãy **import**, **cấu hình API Key**, **test** và **đưa vào production** ngay hôm nay – để các bot, scraper và AI agent của bạn luôn “đi qua” mọi rào cản captcha một cách mượt mà! 🚀