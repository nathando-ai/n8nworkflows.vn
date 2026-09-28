---
title: "🛫 **Tự Động So Sánh Giá Vé Máy Bay Trên Nhiều Trang Booking Và Gửi Báo Cáo Email Tự Động** – Giúp Các Sếp Tiết Kiệm Thời Gian & Lựa Chọn Vé Rẻ Nhất"
description: "Workflow này tự động so sánh giá vé máy bay trên Kayak, Skyscanner, Expedia và Google Flights, sau đó gửi báo cáo chi tiết qua email với đề xuất vé rẻ nhất. Giúp các sếp tiết kiệm thời gian tra cứu thủ công và luôn có quyết định thông minh."
slug: "tieu-dong-so-sanh-gia-ve-may-bay-voi-email-report"
tags: [n8n, automation, no-code, travel, email, scraping, ai-workflow]
keywords: [n8n workflow du lịch, tự động hóa so sánh giá vé máy bay, email báo cáo du lịch, n8n self-hosted, tự động hóa booking, AI du lịch]
---

# 🚀 **Tự Động So Sánh Giá Vé Máy Bay & Gửi Báo Cáo Email – Giải Pháp Cho Các Sếp Bận Rộn**

### **Nỗi Đau Của Các Sếp Khi Tra Cứu Vé Máy Bay**
Hàng ngày, các sếp phải mất **30-60 phút** để tra cứu giá vé trên nhiều trang booking khác nhau (Kayak, Skyscanner, Expedia, Google Flights) và so sánh thủ công. Ngoài ra, còn phải lo lắng về:
❌ **Thiếu thông tin chính xác** (giá thay đổi liên tục).
❌ **Mất thời gian** khi phải copy-paste dữ liệu.
❌ **Không biết đâu là deal tốt nhất** (có thể bỏ lỡ vé rẻ).
❌ **Không lưu lịch sử** để so sánh sau này.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **So sánh giá trên 4 trang booking** trong vài giây.
✅ **Xác định vé rẻ nhất** và đề xuất các lựa chọn tốt nhất.
✅ **Gửi báo cáo email chi tiết** với top 10 kết quả, thống kê giá và liên kết booking.
✅ **Trả lời tự động** cho người dùng biết kết quả như thế nào.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS để đảm bảo tính ổn định và bảo mật.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**).
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow này).
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không phải tra cứu thủ công trên nhiều trang booking.
- **Lựa chọn thông minh**: Nhận đề xuất vé rẻ nhất và top 10 kết quả.
- **Báo cáo chi tiết**: Email bao gồm giá trung bình, số lần dừng, thời gian bay và liên kết booking.
- **Hoạt động liên tục**: Workflow chạy tự động khi có yêu cầu, không phụ thuộc vào giờ làm việc.
- **Trả lời tự động**: Người dùng biết ngay kết quả (thành công hoặc lỗi) qua webhook.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản SSH** (để scraping dữ liệu từ trang booking):
   - **SSH Private Key** (để kết nối với máy chủ scraping).
   - *Lưu ý*: Các trang booking có thể chặn scraping nếu không cấu hình đúng. Nên sử dụng **proxies** hoặc **máy chủ riêng** để tránh bị chặn IP.

2. **Tài khoản Email SMTP** (để gửi báo cáo):
   - **SMTP Credentials** (tên miền, username, password, port).
   - *Gợi ý*: Sử dụng **Gmail SMTP** (cần kích hoạt "Less Secure Apps" hoặc sử dụng OAuth2) hoặc **SendGrid/Mailgun** cho độ tin cậy cao.

3. **Webhook URL** (để nhận yêu cầu từ người dùng):
   - Cung cấp một **URL webhook** (ví dụ: `https://tên-domain.com/flight-price-compare`) để workflow nhận được yêu cầu tra cứu.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow bằng **2 cách**:
- **Tải file JSON** từ [n8n.io/workflows/9788](https://n8n.io/workflows/9788) và import vào **n8n Editor**.
- **Copy JSON** từ trang trên và dán vào **Import Workflow** trong n8n.

👉 **Hướng dẫn chi tiết**:
1. Mở **n8n Editor** (trang chủ của workflow).
2. Nhấn **Import** → **From JSON** → Dán JSON từ link trên.
3. Chọn **Import** để workflow xuất hiện trên canvas.

---

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này có **12 node** quan trọng, các sếp cần cấu hình kỹ lưỡng:

##### **A. Webhook - Nhận Yêu Cầu Tra Cứu Vé**
- **Node**: `Webhook - Receive Flight Request`
- **Cấu hình**:
  - **Path**: `flight-price-compare` (không đổi).
  - **HTTP Method**: `POST`.
  - **Credentials**: Không cần (webhook mặc định).
- **Lưu ý**:
  - Khi người dùng gửi yêu cầu (ví dụ: `{"message": "NYC to London March 25", "email": "user@example.com"}`), workflow sẽ bắt đầu chạy.
  - *Gợi ý*: Sử dụng **Postman** hoặc **cURL** để test:
    ```bash
    curl -X POST https://tên-domain.com/flight-price-compare \
    -H "Content-Type: application/json" \
    -d '{"message": "Hà Nội to TP.HCM 15/10", "email": "sếp@example.com"}'
    ```

##### **B. Parse & Validate Flight Request (Node Code)**
- **Node**: `Parse & Validate Flight Request`
- **Lưu ý**:
  - Workflow tự động **parse** yêu cầu (ví dụ: `"NYC to London March 25"` → `IAD` → `LHR` → `25/03/2024`).
  - **Kiểm tra lỗi**: Nếu yêu cầu không hợp lệ (ví dụ: thiếu ngày bay), workflow sẽ trả về **error response**.

##### **C. Scrape 4 Trang Booking (Kayak, Skyscanner, Expedia, Google Flights)**
- **Nodes**: `Scrape Kayak`, `Scrape Skyscanner`, `Scrape Expedia`, `Scrape Google Flights`
- **Cấu hình**:
  - **SSH Credentials**: Điền **SSH Private Key** (từ VPS hoặc máy chủ scraping).
  - **Lưu ý quan trọng**:
    - **Scraping phải chạy song song** (parallel) để tiết kiệm thời gian.
    - **Timeout**: Đặt **30s** cho mỗi scraper để tránh bị treo.
    - **Nếu bị chặn IP**: Sử dụng **proxies** hoặc **máy chủ scraping riêng** (ví dụ: trên AWS EC2).
    - *Gợi ý*: Nếu không muốn tự scraping, các sếp có thể **sử dụng API chính thức** của các trang booking (nếu có).

##### **D. Aggregate & Analyze Prices (Node Code)**
- **Node**: `Aggregate & Analyze Prices`
- **Lưu ý**:
  - Workflow **tổng hợp** tất cả kết quả từ 4 trang booking.
  - **Xác định vé rẻ nhất** và tính toán thống kê (giá trung bình, số lần dừng, thời gian bay).

##### **E. Format Email Report (Node Code)**
- **Node**: `Format Email Report`
- **Lưu ý**:
  - Email sẽ bao gồm:
    - **Đường bay & ngày**: Ví dụ: `Hà Nội → TP.HCM, 15/10/2024`.
    - **Vé rẻ nhất**: Giá, hãng hàng không, thời gian bay.
    - **Top 10 kết quả**: Danh sách giá từ rẻ đến đắt.
    - **Thống kê**: Giá trung bình, tiết kiệm so với giá cao nhất.
    - **Liên kết booking**: Để người dùng mua vé ngay.

##### **F. Send Email Report**
- **Node**: `Send Email Report`
- **Cấu hình**:
  - **SMTP Credentials**: Điền thông tin SMTP (tên miền, username, password, port).
  - **Lưu ý**:
    - **Nội dung email**: Plain text (dễ đọc).
    - **Người nhận**: Email từ yêu cầu (ví dụ: `user@example.com`).

##### **G. Webhook Response (Success/Error)**
- **Nodes**: `Webhook Response (Success)` và `Webhook Response (Error)`
- **Lưu ý**:
  - Nếu thành công: Trả về JSON như:
    ```json
    {
      "status": "success",
      "best_price": 1200000,
      "airline": "VietJet",
      "total_results": 15
    }
    ```
  - Nếu lỗi: Trả về thông tin chi tiết (ví dụ: yêu cầu không hợp lệ).

---

#### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với dữ liệu mẫu:
   - Gửi yêu cầu test qua webhook (ví dụ: `{"message": "Hà Nội to TP.HCM 15/10", "email": "sếp@example.com"}`).
   - Kiểm tra email nhận được và log trong n8n.

2. **Bật Active**:
   - Nhấn **Active** trên workflow để nó bắt đầu chạy tự động khi có yêu cầu.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Thay vì email, các sếp có thể **gửi báo cáo qua Slack/Telegram** bằng node `slackSend` hoặc `telegramSend`.
   - *Cách làm*: Thêm node `slackSend` sau `Send Email Report` và cấu hình webhook của Slack.

2. **Lưu Log & Dữ Liệu**:
   - Sử dụng node `database` (SQLite, PostgreSQL) để **lưu lịch sử tra cứu** và so sánh giá trong thời gian.
   - *Gợi ý*: Cài **n8n-database** hoặc kết nối với **Google Sheets** để lưu dữ liệu.

3. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng **n8n Trigger** (ví dụ: `setInterval`) để **gửi báo cáo hàng tuần** cho các sếp theo dõi giá vé.

4. **Cải Thiện Scraping**:
   - Nếu bị chặn, các sếp có thể:
     - Sử dụng **Selenium** (quyền hạn cao hơn) thay vì SSH.
     - Mua **API chính thức** của các trang booking (nếu có).

5. **Tự Động Cập Nhật Giá**:
   - Thêm **webhook định kỳ** (ví dụ: hàng ngày) để **so sánh lại giá** và gửi báo cáo cho người dùng.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn:
✔ **Tiết kiệm thời gian** tra cứu vé máy bay.
✔ **Luôn có đề xuất vé rẻ nhất** từ nhiều trang booking.
✔ **Nhận báo cáo chi tiết** qua email mà không cần làm thủ công.

**Hành động ngay!**
1. **Import workflow** vào n8n của mình.
2. **Cấu hình SSH & SMTP** theo hướng dẫn.
3. **Test với yêu cầu mẫu** và **bật Active** để tự động hóa ngay!

👉 **Xem workflow gốc**: [Compare Flight Prices on n8n](https://n8n.io/workflows/9788)
👉 **Cần hỗ trợ?** Đăng ký **VPS n8n** từ [TinoHost](https://tino.vn/vps-n8n?affid=388) và chat với chúng tôi!

---
**Chúc các sếp thành công với tự động hóa du lịch! ✈️**