---
title: "🚀 Tự động làm giàu dữ liệu khách hàng truy cập website với Leadfeeder & Clearbit"
description: "Hướng dẫn xây dựng workflow n8n tự động lấy danh sách khách hàng từ Leadfeeder, làm giàu thông tin qua Clearbit và lưu trữ trực tiếp vào Google Sheets."
slug: "tu-dong-lam-giau-du-lieu-khach-hang-leadfeeder-clearbit"
tags: [n8n, automation, leadfeeder, clearbit, google-sheets, sales, marketing]
keywords: [n8n workflow, tự động hóa leadfeeder, clearbit api, google sheets automation, làm giàu dữ liệu khách hàng]
---

# 🚀 Tự động làm giàu dữ liệu khách hàng truy cập website với Leadfeeder & Clearbit

Các sếp có bao giờ đau đầu vì lượng truy cập website đổ về mỗi ngày rất nhiều nhưng đội ngũ Sales lại không biết công ty nào thực sự tiềm năng để tiếp cận? Việc tra cứu thông tin từng doanh nghiệp, lọc các tiêu chí phù hợp rồi nhập thủ công vào Google Sheets thực sự ngốn quá nhiều thời gian và dễ bỏ lỡ cơ hội vàng.

Đừng lo, bài toán này sẽ được giải quyết triệt để với workflow n8n tự động hóa 100% do **Niklas Hatje** (Product Manager tại n8n) thiết kế. Workflow này giúp tự động quét khách hàng từ Leadfeeder, lọc theo tiêu chí, làm giàu dữ liệu doanh nghiệp qua Clearbit và lưu ngay vào Google Sheets một cách mượt mà.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Không còn thao tác thủ công copy-paste từ Leadfeeder sang Google Sheets.
- **Làm giàu dữ liệu thông minh:** Tự động bổ sung thông tin chi tiết về doanh nghiệp (quy mô, ngành nghề, doanh thu...) thông qua Clearbit API.
- **Lọc leads chuẩn xác:** Chỉ tập trung vào những khách hàng thực sự tiềm năng dựa trên tiêu chí về tương tác (engagement) và thông tin công ty.
- **Hoạt động 24/7:** Chạy định kỳ theo lịch trình (Schedule) giúp đội ngũ Sales luôn có danh sách lead mới mỗi sáng.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI "LÊN ĐỒ"]
- Tài khoản và API Token từ **Leadfeeder**.
- Tài khoản và API Key từ **Clearbit**.
- Tài khoản **Google Sheets** để lưu trữ dữ liệu.
- Template Google Sheets chuẩn (Copy ngay: [Google Sheets Template](https://docs.google.com/spreadsheets/d/1a2gfBjZZpN0jiD7apR8fPplRp2aPHVy2_5lp4Yzp778/edit?usp=sharing)).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ n8n.io (Link gốc: [n8n.io/workflows/2113](https://n8n.io/workflows/2113)) và import trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 11 nodes được cấu hình sẵn, các sếp cần chú ý thiết lập các thành phần quan trọng sau:

- **Node `Get all Leedfeeder accounts` & `Get Leads` (HTTP Request):**
  - Cần thêm **Credentials** dạng `httpHeaderAuth`.
  - Tên header: `Authorization`
  - Giá trị: `Token token=yourapitoken` (Lấy token này tại Leadfeeder qua đường dẫn: **Settings -> Personal -> API-Token**).

- **Node `Setup` (Set):**
  - Cấu hình tên tài khoản Leadfeeder các sếp muốn sử dụng và URL của Google Sheets Template đã sao chép ở trên vào đây.

- **Node `Enrich company` (Clearbit):**
  - Kết nối tài khoản Clearbit bằng thông tin `clearbitApi` credentials của sếp.

- **Node `Save leads to Google Sheets` (Google Sheets):**
  - Kết nối tài khoản Google qua `googleSheetsOAuth2Api`.
  - Chọn Operation là `appendOrUpdate` để tự động thêm mới hoặc cập nhật thông tin lead nếu đã tồn tại.
  - Trỏ tới file Google Sheet template đã chuẩn bị.

- **Các node Filter (`Filter Leads by company criteria`, `Only for wanted accounts`, `Filter leads by engagement`):**
  - Điều chỉnh các điều kiện lọc (Engagement criteria, Company criteria) cho phù hợp với mô hình kinh doanh thực tế của công ty các sếp.

- **Node `Schedule Trigger`:**
  - Thiết lập lịch chạy tự động (ví dụ: chạy mỗi sáng lúc 8:00 AM).

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** để test thử với dữ liệu mẫu xem hệ thống chạy trơn tru chưa.
- Sau khi test thành công, gạt công tắc sang **Active** để workflow tự động làm việc thay các sếp 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node Slack hoặc Telegram ngay sau node `Save leads to Google Sheets` để bắn tin nhắn thông báo về kênh nội bộ mỗi khi có khách hàng tiềm năng mới truy cập website.
- **Gửi Email tự động:** Kết hợp với node Gmail hoặc SendGrid để tự động gửi email chào mừng/tiếp cận ngay khi lead được làm giàu thông tin xong.
- **Lưu Log lỗi:** Thêm nhánh Error Trigger để ghi lại các lỗi phát sinh (nếu API Clearbit phản hồi lỗi) vào một sheet riêng để dễ dàng kiểm tra.

### 📌 Kết luận
Việc tự động hóa quy trình thu thập và làm giàu lead từ website chưa bao giờ dễ dàng đến thế với n8n. Hãy thiết lập ngay workflow này để giúp đội ngũ Sales của các sếp tăng tốc độ tiếp cận khách hàng và chốt sale nhanh chóng hơn! Chúc các sếp cài đặt thành công!