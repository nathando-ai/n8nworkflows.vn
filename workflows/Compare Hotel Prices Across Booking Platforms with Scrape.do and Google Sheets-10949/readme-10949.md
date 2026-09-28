---
title: "🏨 **So Sánh Giá Khách Sạn Trên Booking.com, Agoda & Expedia Tự Động - Không Cần Code!**"
description: "Workflow n8n tự động so sánh giá khách sạn thời gian thực trên 3 nền tảng lớn nhất thế giới, gửi báo cáo giá tốt nhất qua email. Giúp khách hàng tiết kiệm thời gian và tìm được deal hấp dẫn nhất chỉ trong vài giây."
slug: "so-sanh-gia-khach-san-booking-agoda-expedia"
tags: [n8n, automation, market-research, scraping, google-sheets, email-notification]
keywords: [n8n workflow so sánh giá khách sạn, tự động hóa du lịch, scrape.do, Booking.com API, Agoda API, Expedia API, tìm giá rẻ nhất]
---

# 🚀 **So Sánh Giá Khách Sạn Trên 3 Nền Tảng Lớn Nhất Thế Giới - Tự Động Hóa 100%**

### **Nỗi Đau Của Khách Hàng & Doanh Nghiệp**
Bạn đã bao giờ phải **quét qua hàng chục trang web**, so sánh giá khách sạn trên **Booking.com, Agoda và Expedia** một cách thủ công? Hoặc là bạn là một **cơ quan du lịch, nhà cung cấp dịch vụ khách sạn**, và muốn **tự động hóa quá trình tìm giá tốt nhất** để cung cấp cho khách hàng? Thì **workflow này sẽ giải quyết tất cả những vấn đề đó**!

Với **n8n**, bạn có thể **tạo một hệ thống tự động so sánh giá thời gian thực**, nhận dữ liệu từ **3 nền tảng lớn nhất**, **xếp hạng theo giá thấp nhất**, và **gửi báo cáo qua email** chỉ trong **vài giây**. Không cần viết một dòng code nào!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ cao, không lag)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian** – Không cần so sánh thủ công trên nhiều trang web.
✅ **Giá chính xác nhất** – Lấy dữ liệu **thời gian thực** từ 3 nền tảng lớn.
✅ **Báo cáo tự động** – Email gửi ngay giá tốt nhất cho khách hàng.
✅ **Dễ dàng mở rộng** – Thêm được nhiều trang web khác (Expedia, Trivago, Airbnb…).
✅ **Hoạt động 24/7** – Không cần can thiệp người dùng.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi **import workflow**, các sếp cần chuẩn bị:
1. **Tài khoản Scrape.do** (để lấy API Token):
   - Đăng ký tại: [https://scrape.do/](https://scrape.do/)
   - **Lấy API Token** và lưu vào **Global Variable** với tên `SCRAPEDO_TOKEN`.
2. **Tài khoản Gmail** (để gửi email báo cáo):
   - Cần **đăng nhập và cấp quyền cho n8n** trong node **"Send a message"**.
3. **Form Submission URL** (để khách hàng gửi yêu cầu):
   - Sau khi import workflow, **copy URL từ node "On form submission"** và chia sẻ cho khách hàng.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/10949](https://n8n.io/workflows/10949) và **import** vào n8n Editor.
- **Cách 2:** **Copy toàn bộ JSON** từ link trên và **paste** vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
##### **A. Cấu Hình Scrape.do (API Token)**
- Trong **Global Variables**, tạo một biến mới:
  - **Key:** `SCRAPEDO_TOKEN`
  - **Value:** **API Token** từ Scrape.do (đã lấy ở bước trên).
- **Kiểm tra:** Node **"Scrape Booking.com"**, **"Scrape Agoda"**, **"Scrape Expedia"** phải **điền vào `Authorization`** với giá trị:
  ```
  Bearer {{ $SCRAPEDO_TOKEN }}
  ```

##### **B. Cấu Hình Form Submission**
- Node **"On form submission"** sẽ **nhận dữ liệu từ khách hàng** (tên khách sạn, thành phố, ngày check-in/check-out, email).
- **Lưu ý:**
  - **Không cần chỉnh sửa** nếu khách hàng gửi dữ liệu theo **mẫu JSON** sau:
    ```json
    {
      "hotelName": "string",
      "city": "string",
      "checkInDate": "YYYY-MM-DD",
      "checkOutDate": "YYYY-MM-DD",
      "email": "user@example.com"
    }
    ```
  - Nếu khách hàng dùng **Google Form**, cần **chuyển đổi dữ liệu** thành JSON trước khi gửi.

##### **C. Cấu Hình Email (Gmail)**
- Trong node **"Send a message"**, chọn **credential Gmail** đã đăng ký.
- **Chỉnh sửa email template** (nếu cần):
  - Mặc định, email sẽ gửi **danh sách giá** và **giá thấp nhất** theo mẫu:
    ```
    Subject: Best Hotel Deal for {{ $hotelName }} in {{ $city }}
    Body: Here are the best prices for {{ $hotelName }} in {{ $city }}:
    - Booking.com: $X
    - Agoda: $Y
    - Expedia: $Z
    Best price: ${{ $lowestPrice }} at {{ $bestPlatform }}
    ```

##### **D. Kiểm Tra Code Node (Nếu Cần Thay Đổi)**
- **Node "Parse & Validate Request"** (Code): Kiểm tra **lógica validate** ngày (định dạng `YYYY-MM-DD`).
- **Node "Parse Booking.com Data"**, **"Parse Agoda Data"**, **"Parse Expedia Data"** (Code): Nếu **HTML cấu trúc của trang web thay đổi**, cần **cập nhật regex** trong code.
- **Node "Code in JavaScript"** (Merge & Xếp hạng): Nếu muốn **thêm logic mới** (ví dụ: **lọc theo sao, vị trí**), chỉnh sửa tại đây.

#### **3. Kích Hoạt ⚡️**
- **Test Run** với dữ liệu mẫu:
  ```json
  {
    "hotelName": "The Oriental",
    "city": "Ho Chi Minh City",
    "checkInDate": "2024-12-15",
    "checkOutDate": "2024-12-20",
    "email": "khachhang@example.com"
  }
  ```
- Nếu **email không gửi được**, kiểm tra:
  - **Gmail đã cấp quyền** cho n8n.
  - **Email trong form** có đúng định dạng không.
- **Bật Active** workflow sau khi test thành công.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Trang Web Khác**
   - Mở rộng bằng cách **thêm node HTTP Request** cho **Trivago, Airbnb, Booking.com Vietnam**.
   - **Cập nhật code parsing** tương ứng.

2. **Chuyển Đổi Tiền Tệ Tự Động**
   - Sử dụng **API Exchange Rate API** (hoặc **Google Sheets + Apps Script**) để **chuyển đổi USD → VND** trong báo cáo.

3. **Lưu Lịch Sử Giá Vào Google Sheets**
   - Thêm node **Google Sheets** sau **"Merge"** để **ghi lại lịch sử giá** cho phân tích sau này.

4. **Gửi Báo Cáo Qua Slack/Telegram**
   - Thay thế node **Gmail** bằng **Slack Webhook** hoặc **Telegram Bot** để **thông báo tức thời**.

5. **Tự Động So Sánh Theo Ngày Đặc Biệt**
   - Sử dụng **n8n Trigger (Schedule)** để **chạy workflow vào ngày lễ, cuối tuần** và **gửi email khuyến mãi**.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp, **tăng trải nghiệm khách hàng** bằng cách **tìm giá tốt nhất tự động**, và **tăng doanh số** khi khách hàng nhận được **báo cáo chi tiết, cá nhân hóa**.

**🚀 Hãy áp dụng ngay!**
- **Import workflow**, **cấu hình Scrape.do & Gmail**, và **chia sẻ link form** cho khách hàng.
- **Không cần code**, **không cần kỹ sư**, chỉ cần **n8n** là đủ!

**Có thắc mắc?** Liên hệ với tác giả **Onur** qua [LinkedIn](https://www.linkedin.com/in/onurdev/) hoặc [GitHub](https://github.com/onurdev) để **cập nhật nâng cao workflow**!

---
**💡 Lưu ý cuối cùng:**
- **Scrape.do có giới hạn request** (miễn phí: 1000 request/tháng). Nếu cần **scale lớn**, xem xét **dịch vụ paid**.
- **Nếu trang web thay đổi HTML**, cần **cập nhật regex** trong code node.