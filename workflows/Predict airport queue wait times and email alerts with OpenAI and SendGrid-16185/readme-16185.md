---
title: "🚀 Dự đoán Thời Gian Đợi Sân Bay & Gửi Cảnh Báo Email Tự Động với OpenAI và SendGrid"
description: "Workflow tự động hóa dự đoán thời gian chờ hàng loạt tại sân bay (an ninh, nhập cảnh, lên máy bay) và gửi cảnh báo email tự động cho hành khách, giúp tối ưu hóa thời gian đến sân bay và giảm thiểu trễ chuyến bay. Giúp các công ty du lịch, sân bay và ứng dụng di chuyển tiết kiệm thời gian và cải thiện trải nghiệm hành khách."
slug: "dự-doán-thời-gian-đợi-sân-bay-và-cảnh-báo-email"
tags: [n8n, tự động hóa, AI, OpenAI, SendGrid, du lịch, sân bay, dự đoán thời gian chờ]
keywords: [n8n workflow sân bay, tự động hóa cảnh báo hành khách, dự đoán thời gian chờ an ninh, AI cho du lịch, SendGrid email tự động, OpenAI chatbot hành khách]
---

# 🚀 **Dự Đoán Thời Gian Đợi Sân Bay & Gửi Cảnh Báo Email Tự Động với OpenAI và SendGrid**

### **Giải pháp tự động hóa thông minh cho hành khách và sân bay**
Hành khách đã bao giờ phải chờ hàng giờ tại sân bay vì thời gian chờ hàng loạt không chính xác? Hay các công ty du lịch, sân bay hoặc ứng dụng di chuyển muốn tối ưu hóa trải nghiệm hành khách bằng cách dự đoán thời gian chờ hàng loạt (an ninh, nhập cảnh, lên máy bay) và gửi cảnh báo kịp thời? **Workflow này là giải pháp hoàn hảo!**

Dựa trên dữ liệu thời gian thực và mô hình AI, workflow này **dự đoán thời gian chờ hàng loạt tại sân bay**, tính toán thời gian đến sân bay tối ưu, và **gửi cảnh báo email tự động** cho hành khách để họ đến sân bay đúng giờ, tránh trễ chuyến bay. Ngoài ra, dữ liệu dự đoán còn được lưu trữ trên **Google Sheets** để phân tích và cải thiện dịch vụ.

---
### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian hành khách**: Hành khách đến sân bay đúng giờ, tránh chờ đợi dài và trễ chuyến bay.
- **Tăng hiệu quả cho sân bay**: Theo dõi thời gian chờ hàng loạt và điều chỉnh nguồn lực (nhân viên, máy móc) một cách thông minh.
- **Cải thiện trải nghiệm du lịch**: Hành khách được cảnh báo kịp thời với thông tin chi tiết và lời khuyên từ AI.
- **Dữ liệu phân tích**: Lưu trữ tất cả dự đoán và kết quả trên Google Sheets để theo dõi xu hướng và tối ưu hóa dịch vụ.
- **Hoạt động 24/7**: Workflow chạy tự động, không cần can thiệp thủ công.
:::

---
### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị các tài khoản và API keys sau:
1. **API Dữ liệu Sân Bay**:
   - **AviationStack** hoặc **AeroDataBox** (hoặc **FlightAware**) để lấy dữ liệu thời gian thực về hàng loạt tại sân bay.
   - [Đăng ký AviationStack](https://www.aviationstack.com/) (Mã giảm giá: **N8NAVIATION** - giảm 10%).
   - [Đăng ký AeroDataBox](https://aerodatabox.com/) (Mã giảm giá: **N8NAERO** - giảm 15%).

2. **Gửi Email Cảnh Báo**:
   - **SendGrid** (hoặc **Twilio** để gửi SMS) để gửi cảnh báo đến hành khách.
   - [Đăng ký SendGrid](https://sendgrid.com/) (Mã giảm giá: **N8NSENDGRID** - giảm 20%).

3. **Google Sheets**:
   - Tài khoản Google với quyền chỉnh sửa một **Google Sheet** để lưu trữ dữ liệu dự đoán.

4. **OpenAI API Key**:
   - API Key của **OpenAI** để sử dụng mô hình **GPT-4.1-mini** trong việc tạo cảnh báo tự động.
   - [Đăng ký OpenAI](https://platform.openai.com/) (Mã giảm giá: **N8NOPENAI** - giảm 20% cho tài khoản Pro).

5. **n8n Self-hosted**:
   - Workflow này hoạt động tốt nhất khi được cài đặt trên **VPS riêng** để đảm bảo hoạt động 24/7.
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
:::

---
### 🚀 **Cách Import & Lưu ý khi "Lên đồ"**

#### 1. **Import Workflow 📥**
- **Bước 1**: Tải file JSON của workflow từ [đây](https://n8n.io/workflows/16185) (hoặc copy JSON từ trang gốc).
- **Bước 2**: Mở **n8n Editor** và nhấn **"Import"** → Dán JSON hoặc tải file JSON lên.
- **Bước 3**: Chọn **"Import"** để workflow xuất hiện trên canvas.

#### 2. **Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **10 node** chính, mỗi node đều cần cấu hình kỹ lưỡng. Dưới đây là hướng dẫn chi tiết:

##### **A. Cấu hình Credentials**
1. **OpenAI API**:
   - Tạo **credentials** mới trong n8n với tên **"openAiApi"**.
   - Điền **API Key** từ tài khoản OpenAI vào trường `Api Key`.
   - Chọn mô hình: `gpt-4.1-mini`.

2. **Google Sheets OAuth2**:
   - Tạo **credentials** mới với tên **"googleSheetsOAuth2Api"**.
   - Theo hướng dẫn của n8n để kết nối với Google Sheets và cấp quyền chỉnh sửa.

3. **SendGrid (hoặc Twilio)**:
   - Tạo **credentials** mới với tên **"sendGridApi"** (hoặc **"twilioApi"** nếu sử dụng SMS).
   - Điền **API Key** và **Sender Email** (hoặc **Twilio Account SID và Auth Token**).

##### **B. Cấu hình Node Quan Trọng**
1. **Webhook - Traveler Queue Request**:
   - Path: `airport-queue-check` (không cần thay đổi).
   - HTTP Method: `POST` (không cần thay đổi).
   - **Lưu ý**: Nếu muốn kích hoạt webhook, cần tạo một **URL webhook** từ n8n và chia sẻ với ứng dụng hoặc hành khách để gửi yêu cầu.

2. **Poll Airport Data Every 5 Min**:
   - Thiết lập lịch trình để **lấy dữ liệu sân bay mỗi 5 phút** (không cần thay đổi).

3. **Normalise Traveler & Airport Context**:
   - Node này chuẩn hóa dữ liệu đầu vào (từ webhook hoặc lịch trình) thành một đối tượng thống nhất.
   - **Không cần chỉnh sửa** trừ khi cần thêm trường dữ liệu mới.

4. **JS - Wait-Time Prediction Engine**:
   - Node này chứa **mô hình dự đoán thời gian chờ** bằng JavaScript.
   - **Lưu ý**:
     - Đảm bảo dữ liệu đầu vào có các trường như `flightNumber`, `airportCode`, `departureTime`, `passengerCount`, `season`, `dayOfWeek`.
     - Nếu cần thay đổi logic dự đoán, chỉnh sửa mã JavaScript trong node này.

5. **AI - Generate Traveler Alert Message**:
   - Node này sử dụng **OpenAI GPT-4.1-mini** để tạo cảnh báo tự động cho hành khách.
   - **Lưu ý**:
     - Đảm bảo node **OpenAI Chat Model** đã kết nối với credentials `openAiApi`.
     - Tham số `model` đã được thiết lập là `gpt-4.1-mini`.

6. **JS - Format Alert Payload**:
   - Node này định dạng cảnh báo thành định dạng phù hợp để gửi email.
   - **Không cần chỉnh sửa** trừ khi cần thay đổi cấu trúc email.

7. **Send Email Alert via SendGrid**:
   - Node này gửi email cảnh báo đến hành khách.
   - **Lưu ý**:
     - Đảm bảo credentials `sendGridApi` đã được cấu hình.
     - Thay đổi trường `to` (địa chỉ email hành khách) và `subject` (tiêu đề email) nếu cần.

8. **Log Prediction to Google Sheets**:
   - Node này ghi dữ liệu dự đoán vào Google Sheets.
   - **Lưu ý**:
     - Thay đổi `sheetId` trong tham số `url` thành **ID của Google Sheet** của bạn (tìm trong URL của sheet).
     - Thay đổi `range` thành tên **tab** (sheet) muốn ghi dữ liệu (ví dụ: `Dự đoán sân bay`).

##### **C. Kích hoạt Workflow ⚡️**
1. **Test Run**:
   - Nhấn **"Run"** trên node **Webhook** để gửi một yêu cầu mẫu (ví dụ: dữ liệu chuyến bay).
   - Kiểm tra các node tiếp theo để đảm bảo dữ liệu được xử lý đúng.
   - **Lưu ý**: Nếu sử dụng **lịch trình**, chạy test với dữ liệu mẫu trước khi kích hoạt.

2. **Bật Active**:
   - Sau khi kiểm tra xong, nhấn **"Active"** trên workflow để nó hoạt động liên tục.

---
### ✍️ **Mẹo & Gợi ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** để gửi cảnh báo ngay khi có dự đoán mới.
   - Cách làm: Sử dụng node **HTTP Request** để gọi API của Slack/Telegram.

2. **Lưu Log Chi tiết**:
   - Thêm node **Google Sheets** hoặc **Database** để lưu log chi tiết của mỗi cảnh báo (ví dụ: thời gian gửi, hành khách nhận, kết quả).

3. **Báo cáo Định Kỳ**:
   - Sử dụng node **Schedule Trigger** để chạy một workflow khác mỗi ngày/tuần để tổng hợp báo cáo từ Google Sheets và gửi qua email.

4. **Tối Ưu Mô Hình Dự Đoán**:
   - Nếu có dữ liệu lịch sử lớn, có thể huấn luyện mô hình dự đoán riêng bằng **LangChain** hoặc **Python** và kết nối với n8n.

5. **Cảnh Báo SMS**:
   - Nếu muốn gửi SMS thay vì email, thay thế node **SendGrid** bằng **Twilio** và cấu hình lại payload.

---
### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** để tự động hóa dự đoán thời gian chờ sân bay và gửi cảnh báo email tự động, giúp hành khách đến sân bay đúng giờ và tránh trễ chuyến bay. Ngoài ra, dữ liệu dự đoán còn được lưu trữ để phân tích và cải thiện dịch vụ.

**Hãy áp dụng ngay workflow này cho doanh nghiệp du lịch, sân bay hoặc ứng dụng di chuyển của bạn!** Nếu có bất kỳ câu hỏi hoặc gặp khó khăn, hãy để lại comment dưới đây. Chúc các sếp thành công! ✨

---
**🔗 [Xem workflow gốc trên n8n.io](https://n8n.io/workflows/16185)** | **📌 [Tải file JSON](https://n8n.io/workflows/16185/download)**