---
title: "🚀 Tự Động So Sánh Giá Vé Máy Bay Từ Skyscanner, Air India & Hàng Đoàn Hãng Khác Với Email Cảnh Báo - Giảm 90% Thời Gian Tìm Kiếm"
description: "Workflow này tự động so sánh giá vé máy bay từ 4 hãng hàng không lớn (Skyscanner, Air India, IndiGo, Akasa Air) và gửi báo cáo giá rẻ nhất qua email hàng ngày. Giúp các sếp tiết kiệm thời gian lên đến 90% so với cách tìm kiếm thủ công, đồng thời đảm bảo không bỏ lỡ deal hấp dẫn."
slug: "tieu-dong-so-sanh-gia-ve-may-bay-skyscanner-air-india-email"
tags: [n8n, automation, market-research, travel, email-alerts]
keywords: [n8n workflow du lịch, tự động hóa tìm kiếm vé máy bay, so sánh giá vé hàng không, email cảnh báo giá vé rẻ, Skyscanner API, Air India API]
---

# 🚀 **Tự Động So Sánh Giá Vé Máy Bay Từ 4 Hãng Hàng Không Lớn Và Nhận Email Cảnh Báo Giá Rẻ Nhất**

### **Nỗi Đau Của Các Sếp Khi Tìm Vé Máy Bay**
Tìm kiếm và so sánh giá vé máy bay giữa nhiều hãng hàng không là một công việc **mệt mỏi, tốn thời gian và dễ bị bỏ lỡ deal hấp dẫn**. Các sếp thường phải:
- **Lặp đi lặp lại** trên nhiều trang web (Skyscanner, Air India, IndiGo, Akasa Air,...) để so sánh giá.
- **Rủi ro bỏ lỡ** những chênh lệch giá nhỏ nhưng có ý nghĩa lớn (ví dụ: 500K vs 3M đồng).
- **Không có báo cáo tự động**, phải nhớ check lại sau mỗi thay đổi giá.
- **Khó theo dõi** giá theo thời gian, đặc biệt khi có nhiều tuyến bay và ngày xuất phát khác nhau.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động so sánh giá** từ **4 hãng hàng không lớn** (Skyscanner, Air India, IndiGo, Akasa Air) trong **vài giây**.
✅ **Gửi báo cáo email hàng ngày** với **giá rẻ nhất** và thông tin chi tiết.
✅ **Đảm bảo không bỏ lỡ deal**, vì workflow chạy **tự động theo lịch trình** (ví dụ: hàng ngày lúc 8h sáng).
✅ **Tiết kiệm thời gian lên đến 90%** so với cách tìm kiếm thủ công.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không phải tra cứu trên nhiều trang web, chỉ cần **nhận email báo cáo** mỗi ngày.
- **Giá vé chính xác nhất**: So sánh **tất cả hãng hàng không** trong một workflow, không bỏ sót deal nào.
- **Cảnh báo kịp thời**: Nhận thông báo **ngay khi giá giảm** hoặc có deal đặc biệt.
- **Dễ dàng theo dõi**: Báo cáo email có **bảng so sánh chi tiết**, bao gồm:
  - Giá vé từ thấp đến cao.
  - Thời gian bay.
  - Hãng hàng không.
  - Link đặt vé.
- **Hoạt động 24/7**: Workflow chạy **tự động theo lịch trình**, không cần can thiệp của người dùng.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản Skyscanner API** (hoặc API key của Skyscanner Partner).
2. **Tài khoản Air India API** (nếu có API chính thức, hoặc sử dụng API công khai của hãng).
3. **Tài khoản IndiGo API** (tương tự như trên).
4. **Tài khoản Akasa Air API** (nếu có API, hoặc sử dụng API của Skyscanner để lấy dữ liệu).
5. **Thông tin chuyến bay**:
   - **Điểm xuất phát (Origin)** (ví dụ: SGN, HAN, HNX).
   - **Điểm đến (Destination)** (ví dụ: SIN, BKK, CNX).
   - **Ngày xuất phát** (hoặc khoảng thời gian).
6. **Thông tin email để nhận báo cáo**:
   - **SMTP credentials** (hoặc tài khoản Gmail/Yahoo để gửi email).
   - **Tên người gửi** (ví dụ: "Flight Alert Bot").
7. **VPS hoặc máy chủ n8n** (để workflow chạy 24/7).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Bước 1**: Tải workflow từ [đây](https://n8n.io/workflows/6054) hoặc sao chép JSON từ trang này.
- **Bước 2**: Mở **n8n Editor** và chọn **"Import"** → Dán JSON hoặc tải file JSON.
- **Bước 3**: Chọn **"Create Workflow"** để lưu vào dự án của mình.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **11 node**, nhưng các node quan trọng nhất cần cấu hình kỹ là:

##### **A. Cấu Hình API (4 Node `httpRequest`)**
Các node này gọi API để lấy dữ liệu giá vé từ các hãng hàng không. Các sếp cần:
1. **Thêm credentials API** cho mỗi node:
   - **Skyscanner API**:
     - URL: `https://skyscanner-skyscanner-flight-search-v1.p.rapidapi.com/apiservices/browse/rates`
     - Tham số cần thiết: `currency`, `locale`, `originplace`, `destinationplace`, `outbounddate`, `inbounddate` (nếu có).
     - **Lưu ý**: Nếu không có API chính thức, có thể sử dụng **API công khai của Skyscanner** (nhưng cần kiểm tra điều khoản sử dụng).
   - **Air India API**:
     - URL: `https://api.airindia.in/v1/flights/search`
     - Tham số: `origin`, `destination`, `departureDate`, `returnDate` (nếu có).
   - **IndiGo API**:
     - URL: `https://api.indigoflying.com/v1/flights/search`
     - Tham số: `origin`, `destination`, `departureDate`.
   - **Akasa Air API**:
     - Nếu không có API chính thức, có thể sử dụng **Skyscanner API** với mã hãng Akasa Air (`AK`).

2. **Thêm `Authorization` hoặc `API Key`** vào header của mỗi request:
   - Ví dụ:
     ```json
     {
       "Authorization": "Bearer YOUR_API_KEY",
       "Content-Type": "application/json"
     }
     ```

##### **B. Cấu Hình `Set Input Data` (Node `set`)**
- **Điền thông tin chuyến bay**:
  - `originplace`: Mã sân bay xuất phát (ví dụ: `SGN` cho Tân Sơn Nhất).
  - `destinationplace`: Mã sân bay đến (ví dụ: `SIN` cho Changi).
  - `outbounddate`: Ngày xuất phát (định dạng `YYYY-MM-DD`).
  - `currency`: Mã tiền tệ (ví dụ: `VND`).
  - `locale`: Ngôn ngữ (ví dụ: `vi-VN`).

##### **C. Cấu Hình `Send Response via Email` (Node `emailSend`)**
1. **Thêm credentials SMTP**:
   - Nếu sử dụng **Gmail**:
     - **Host**: `smtp.gmail.com`
     - **Port**: `587`
     - **Username**: Email của bạn.
     - **Password**: App Password (nếu đã bật 2FA).
   - Nếu sử dụng **SMTP khác**, tham khảo [hướng dẫn SMTP của n8n](https://docs.n8n.io/integrations/builtins/nodes/n8n-nodes-base.emailSend.html).
2. **Cấu hình email**:
   - **From**: `Flight Alert Bot <your-email@gmail.com>`.
   - **To**: Email của mình (hoặc nhóm).
   - **Subject**: `🔍 Báo cáo giá vé máy bay [Origin] -> [Destination] (Ngày: ${{ $json.outbounddate }})`.
   - **HTML Template**: Sử dụng template mặc định hoặc tùy chỉnh để hiển thị bảng so sánh giá.

##### **D. Cấu Hình `Set Schedule` (Node `scheduleTrigger`)**
- **Chọn lịch trình chạy**:
  - Ví dụ: `0 8 * * *` (chạy hàng ngày lúc 8h sáng).
  - Tham khảo [cú pháp cron](https://docs.n8n.io/integrations/trigger/n8n-nodes-base.scheduleTrigger.html#cron-syntax).

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Chạy workflow với **dữ liệu mẫu** để kiểm tra:
     - API trả về dữ liệu không?
     - Email được gửi thành công không?
     - Bảng so sánh giá có hiển thị rõ ràng không?
2. **Bật Active**:
   - Sau khi kiểm tra xong, **bật Active** để workflow chạy tự động theo lịch trình.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::note[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết hợp với Slack/Telegram**:
   - Thay vì chỉ gửi email, có thể **gửi thông báo trên Slack/Telegram** khi có deal đặc biệt.
   - **Cách làm**:
     - Thêm node `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram`.
     - Cấu hình webhook của Slack/Telegram và gửi thông báo khi giá giảm.

2. **Lưu log vào Google Sheets/Notion**:
   - Để theo dõi lịch sử giá, có thể **lưu dữ liệu vào Google Sheets** hoặc **Notion**.
   - **Cách làm**:
     - Thêm node `n8n-nodes-base.googleSheets` hoặc `n8n-nodes-base.notion`.
     - Cấu hình để ghi dữ liệu vào sheet mới mỗi ngày.

3. **Cảnh báo giá giảm bằng IFTTT/Zapier**:
   - Nếu giá vé giảm dưới một ngưỡng nhất định, có thể **gửi thông báo push** hoặc **call SMS**.
   - **Cách làm**:
     - Sử dụng node `n8n-nodes-base.httpRequest` để gọi API của IFTTT/Zapier.
     - Cấu hình trigger khi giá < X (ví dụ: 2M đồng).

4. **Tùy chỉnh email theo nhu cầu**:
   - Thêm **đoạn code JavaScript** trong node `function` để:
     - Lọc chỉ những deal có **giá < Y** (ví dụ: 3M đồng).
     - Thêm **link đặt vé nhanh** vào email.
     - Thêm **bảng so sánh chi tiết** với hình ảnh.

5. **Chạy workflow cho nhiều tuyến bay**:
   - Sử dụng **loop trong node `set`** để chạy workflow cho **nhiều cặp điểm bay** (ví dụ: SGN-SIN, SGN-BKK, HNX-SIN).
   - **Cách làm**:
     - Tạo một **mảng JSON** chứa danh sách tuyến bay.
     - Sử dụng node `n8n-nodes-base.foreach` để chạy workflow cho từng tuyến.
:::

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tự động hóa tìm kiếm vé máy bay**, tiết kiệm thời gian và **không bỏ lỡ deal hấp dẫn**. Với chỉ **vài bước cấu hình**, các sếp có thể:
✔ **So sánh giá từ 4 hãng hàng không** trong một workflow.
✔ **Nhận báo cáo email hàng ngày** với giá rẻ nhất.
✔ **Hoạt động 24/7** mà không cần can thiệp.

**Hành động ngay hôm nay!**
1. **Cài đặt n8n trên VPS** (để workflow chạy 24/7).
2. **Import workflow** và cấu hình API.
3. **Bật Active** và **nhận email báo cáo** mỗi ngày!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**Chia sẻ và áp dụng ngay để trở thành "người tìm vé máy bay thông minh"!** ✈️💻