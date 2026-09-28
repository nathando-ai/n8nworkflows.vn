---
title: "💰 Tự Động Hóa Báo Cáo Lệ Phí Hối Đổi Tiền Hàng Ngày Từ API CurrencyFreaks → Email & WhatsApp (Không Code)"
description: "Giải pháp tự động hóa hoàn toàn cho doanh nghiệp, nhà đầu tư crypto và cá nhân theo dõi tỷ giá hối đoái 24/7, nhận báo cáo định kỳ qua Email và WhatsApp mỗi sáng. Tiết kiệm 30+ giờ/tháng so với cách làm thủ công!"
slug: "tu-dong-hoa-bo-cao-ty-gia-hoi-doi-tien-hang-ngay"
tags: [n8n, automation, crypto-trading, api-integration, email-whatsapp-automation]
keywords: [tự động hóa tỷ giá hối đoái, n8n workflow crypto, báo cáo định kỳ email whatsapp, api currencyfreaks, tự động hóa tài chính]
---

# 🚀 **Tự Động Hóa Báo Cáo Tỷ Giá Hối Đổi Tiền Hàng Ngày: Từ API → Email & WhatsApp**

### **Nỗi Đau Của Các Sếp Và Giải Pháp N8n**
Bạn là nhà đầu tư crypto, doanh nghiệp thương mại quốc tế, hoặc cá nhân theo dõi tỷ giá hối đoái hàng ngày? Thì chắc chắn bạn đã gặp phải những vấn đề sau:
- **Tốn thời gian**: Phải truy cập nhiều trang web hoặc API để lấy tỷ giá, sau đó tổng hợp và gửi cho đồng nghiệp/nhóm đầu tư.
- **Rủi ro sai sót**: Nhập sai số liệu, quên gửi báo cáo, hoặc mất thông tin quan trọng khi không theo dõi kịp thời.
- **Không cá nhân hóa**: Báo cáo chung chung, không thể tùy chỉnh theo nhu cầu riêng của từng người nhận.
- **Không hoạt động 24/7**: Phải làm thủ công, dẫn đến báo cáo không kịp thời hoặc thiếu chính xác.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Lấy tỷ giá hối đoái mới nhất** từ API CurrencyFreaks (INR, CAD, AUD, CNY, EUR, USD,...) hàng ngày.
✅ **Tổng hợp và gửi báo cáo** dưới dạng Email + WhatsApp với định dạng chuyên nghiệp.
✅ **Hoạt động tự động** mỗi sáng (7:30 AM IST) mà không cần can thiệp của bạn.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 30+ giờ/tháng**: Không phải làm thủ công mỗi ngày.
- **Chính xác 100%**: Dữ liệu từ API chính thức, không sai sót.
- **Cá nhân hóa hoàn toàn**: Chỉ cần chỉnh sửa danh sách email/number và nội dung.
- **Hoạt động liên tục**: Báo cáo được gửi tự động mỗi sáng, ngay cả khi bạn ngủ.
- **Dễ dàng mở rộng**: Thêm/loại tiền tệ, thay đổi thời gian gửi, hoặc kết nối với Slack/Telegram.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **API Key CurrencyFreaks**:
   - Đăng ký miễn phí tại [CurrencyFreaks](https://currencyfreaks.com/) để lấy API Key.
   - Lưu ý: API Key này sẽ được sử dụng trong node `Fetch Exchange Rates`.

2. **Tài khoản Email (SMTP)**:
   - Cấu hình SMTP cho Email (ví dụ: Gmail, Outlook, hoặc SMTP của nhà cung cấp hosting).
   - Các sếp cần:
     - **Tên miền miền** (domain).
     - **Tên người dùng** và **mật khẩu ứng dụng** (không phải mật khẩu chính).
     - **Port** (thường là 587 cho TLS).
     - **Tên miền SMTP** (ví dụ: `smtp.gmail.com` cho Gmail).

3. **Số điện thoại WhatsApp**:
   - Một số WhatsApp để nhận báo cáo (cần đăng ký **WhatsApp Business API** hoặc sử dụng số điện thoại cá nhân với **WhatsApp Web**).
   - **Lưu ý**: Nếu sử dụng WhatsApp cá nhân, cần cài đặt **n8n-nodes-whatsapp** và đăng ký credentials `whatsAppApi` với số điện thoại đó.

4. **Danh sách tiền tệ theo dõi** (ví dụ: `INR, CAD, AUD, CNY, EUR, USD`).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [liên kết gốc](https://n8n.io/workflows/6120) hoặc sao chép JSON từ trang này.
- Trong **n8n Editor**, nhấn `Import` → Chọn file JSON hoặc dán JSON vào ô `Import Workflow`.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **8 node** chính, các sếp cần chú ý cấu hình các node sau:

##### **A. Node `Daily Trigger (7:30 AM IST)`**
- **Lưu ý**: Thời gian này được đặt theo **IST (Indian Standard Time)**. Nếu các sếp muốn thay đổi thời gian, hãy:
  1. Nhấn vào node `scheduleTrigger`.
  2. Chọn tab `Configuration`.
  3. Đổi giá trị `cron` hoặc `time` theo định dạng mong muốn (ví dụ: `0 30 7 * * ?` để gửi lúc 7:30 AM hàng ngày).

##### **B. Node `Set Config: API Key & Currencies`**
- **Cấu hình**:
  - Thêm `API Key` vào trường `apiKey`.
  - Thêm danh sách tiền tệ cần theo dõi vào trường `currencies` (ví dụ: `["INR", "USD", "EUR", "CAD"]`).
  - **Ví dụ**:
    ```json
    {
      "apiKey": "YOUR_CURRENCYFREAKS_API_KEY",
      "currencies": ["INR", "USD", "EUR", "CAD"]
    }
    ```

##### **C. Node `Fetch Exchange Rates (CurrencyFreaks)`**
- **Cấu hình**:
  - **Method**: `GET`.
  - **URL**: `https://api.currencyfreaks.com/latest?apikey={{$node["Set Config: API Key & Currencies"].json()["apiKey"]}}&base=INR`.
  - **Headers**:
    - `Content-Type`: `application/json`.
  - **Body**: Trống (do API không yêu cầu body).

##### **D. Node `Set Email & WhatsApp Recipients`**
- **Cấu hình**:
  - Thêm danh sách email vào trường `emails` (ví dụ: `["email1@example.com", "email2@example.com"]`).
  - Thêm danh sách số WhatsApp vào trường `whatsappNumbers` (ví dụ: `["+1234567890", "+9876543210"]`).
  - **Ví dụ**:
    ```json
    {
      "emails": ["sếp@example.com", "nhân viên@example.com"],
      "whatsappNumbers": ["+84123456789", "+84987654321"]
    }
    ```

##### **E. Node `Create Message Subject & Body`**
- **Cấu hình**:
  - **Subject**: `Today's Currency Exchange Rates – {{$node["Daily Trigger (7:30 AM IST)"].json()["date"]}}`.
  - **Body**: Sử dụng template động để hiển thị tỷ giá. Ví dụ:
    ```json
    {
      "subject": "Today's Currency Exchange Rates – {{$node["Daily Trigger (7:30 AM IST)"].json()["date"]}}",
      "body": "Chào các sếp,\n\nDưới đây là tỷ giá hối đoái mới nhất (base: INR):\n\n{{$node["Fetch Exchange Rates (CurrencyFreaks)"].json()["rates"] | toArray | map(item) | join(\"\\n\") | replaceAll(\"\\{\\\"key\\\":\\\"\", \"\") | replaceAll(\"\\\",\\\"value\\\":\\\"\", \": \") | replaceAll(\"\\\"\\\", \"\") }}"
    }
    ```
    - **Lưu ý**: Template này sử dụng hàm `map` và `join` để chuyển đổi đối tượng `rates` thành danh sách dễ đọc. Nếu không quen, các sếp có thể sử dụng **Sticky Note** để debug dữ liệu trước khi gửi.

##### **F. Node `Send WhatsApp Alert`**
- **Cấu hình**:
  - **Credentials**: Chọn `whatsAppApi` (đã cấu hình trước).
  - **Message**: Sử dụng dữ liệu từ node `Create Message Subject & Body` (ví dụ: `{{$node["Create Message Subject & Body"].json()["body"]}}`).
  - **Phone Number**: `{{$node["Set Email & WhatsApp Recipients"].json()["whatsappNumbers"] | first}}` (hoặc lặp qua danh sách).

##### **G. Node `Send Email Alert`**
- **Cấu hình**:
  - **Credentials**: Chọn `smtp` (đã cấu hình trước).
  - **To**: `{{$node["Set Email & WhatsApp Recipients"].json()["emails"] | join(\",\")}}`.
  - **Subject**: `{{$node["Create Message Subject & Body"].json()["subject"]}}`.
  - **Text**: `{{$node["Create Message Subject & Body"].json()["body"]}}`.

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Nhấn `Execute Workflow` để kiểm tra dữ liệu mẫu.
  - Kiểm tra Email và WhatsApp để đảm bảo nội dung đúng.
- **Bật Active**:
  - Sau khi test thành công, chuyển trạng thái workflow sang `Active`.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[MỞ RỘNG THÊM]
1. **Kết Nối Với Slack/Telegram**:
   - Thêm node `slack` hoặc `telegramBot` để gửi báo cáo lên kênh nhóm.
   - **Cách làm**:
     - Cài đặt `n8n-nodes-slack` hoặc `n8n-nodes-telegram`.
     - Cấu hình credentials và gửi tin nhắn với nội dung tương tự.

2. **Lưu Log Dữ Liệu**:
   - Thêm node `set` hoặc `stickyNote` để lưu dữ liệu tỷ giá vào **Google Sheets** hoặc **Airtable** để theo dõi lịch sử.
   - **Cách làm**:
     - Cài đặt `n8n-nodes-google-sheets`.
     - Cấu hình credentials và ghi dữ liệu vào sheet mới.

3. **Thay Đổi Thời Gian Gửi**:
   - Nếu các sếp muốn gửi báo cáo vào giờ khác (ví dụ: 8 AM GMT+7), chỉnh sửa node `scheduleTrigger` như hướng dẫn ở phần **2.B**.

4. **Tùy Chỉnh Nội Dung Email/WhatsApp**:
   - Sử dụng **Sticky Note** để debug và chỉnh sửa template nội dung trước khi gửi.
   - Thêm biểu đồ hoặc biểu tượng vào Email để làm đẹp (nếu sử dụng SMTP hỗ trợ HTML).

5. **Báo Cáo Định Kỳ Tuần/Tháng**:
   - Sử dụng node `scheduleTrigger` với cron khác (ví dụ: `0 0 1 * * ?` để gửi mỗi đầu tháng).
   - Thêm logic lọc dữ liệu theo ngày trong node `set` hoặc `httpRequest`.
:::

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa báo cáo tỷ giá hối đoái hàng ngày mà **không cần viết một dòng code**. Với chỉ vài bước cấu hình, bạn sẽ:
✔ **Tiết kiệm thời gian** và tập trung vào công việc quan trọng hơn.
✔ **Nhận báo cáo chính xác** mỗi sáng qua Email và WhatsApp.
✔ **Mở rộng dễ dàng** để kết nối với nhiều dịch vụ khác.

**Hành động ngay hôm nay!**
1. **Cài đặt n8n** trên VPS (Self-hosted) để workflow hoạt động 24/7.
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

2. **Import workflow** và cấu hình theo hướng dẫn trên.
3. **Bật Active** và bắt đầu tự động hóa!

**Chúc các sếp thành công!** 🚀
---