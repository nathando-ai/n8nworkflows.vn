---
title: "💰 Tự Động Hàng Ngày Lấy & Gửi Tỷ Giá GBP - Giúp Các Sếp Tiết Kiệm Thời Gian Theo Dõi Tỷ Lệ Hối Đoái"
description: "Workflow tự động hóa lấy tỷ giá GBP từ API và gửi email hàng ngày cho các sếp, giúp theo dõi thị trường ngoại tệ một cách chính xác và không cần can thiệp thủ công. Giúp tiết kiệm thời gian lên đến 10 giờ/tháng!"
slug: "tu-dong-hoa-lay-ty-gia-gbp-hang-ngay"
tags: [n8n, automation, no-code, gmail, api, tỷ giá ngoại tệ]
keywords: [tự động hóa lấy tỷ giá GBP, gửi email tỷ giá hàng ngày, n8n workflow, API tỷ giá ngoại tệ, tiết kiệm thời gian theo dõi tỷ lệ hối đoái]
---

# 💰 **Tự Động Hàng Ngày Lấy & Gửi Tỷ Giá GBP - Giải Pháp Tiết Kiệm Thời Gian Cho Các Sếp**

### **Nỗi Đau Thực Tế Của Các Sếp**
Theo dõi tỷ giá ngoại tệ hàng ngày là một công việc tẻ nhạt và tốn thời gian, đặc biệt là khi các sếp phải tra cứu tỷ giá GBP từ nhiều nguồn khác nhau (ngân hàng, website, API) và ghi chép vào bảng tính hoặc gửi cho đồng nghiệp. Với **Workflow này**, các sếp sẽ **tự động nhận được email hàng ngày với tỷ giá GBP mới nhất**, giúp quyết định giao dịch hoặc báo cáo tài chính một cách nhanh chóng và chính xác.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần tra cứu tỷ giá thủ công hàng ngày.
- **Dữ liệu chính xác**: Lấy tỷ giá từ API uy tín và tự động cập nhật.
- **Tự động hóa hoàn toàn**: Gửi email hàng ngày mà không cần can thiệp.
- **Dễ dàng theo dõi**: Dữ liệu được lưu vào Google Sheets để tham khảo lâu dài.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Gmail** (để gửi email tự động).
2. **API Key từ một nguồn tỷ giá ngoại tệ** (ví dụ: [ExchangeRate-API](https://www.exchangerate-api.com/)).
3. **Tài khoản Google Sheets** (để lưu lịch sử tỷ giá).
4. **Credentials OAuth2** cho:
   - **Gmail** (để gửi email).
   - **Google Sheets** (để ghi dữ liệu).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/4814](https://n8n.io/workflows/4814) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ trang trên và dán vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **5 node chính**, các sếp cần chú ý cấu hình như sau:

##### **🔹 Node 1: Manual Trigger (Bắt Đầu Workflow)**
- **Tên**: "When clicking ‘Execute workflow’"
- **Lưu ý**: Các sếp có thể thay bằng **Schedule Trigger** (nếu muốn chạy tự động hàng ngày) hoặc giữ nguyên để kích hoạt thủ công.

##### **🔹 Node 2: HTTP Request (Lấy Tỷ Giá GBP)**
- **Tên**: "HTTP Request"
- **Cấu hình**:
  - **Method**: `GET`
  - **URL**: Thay thế bằng API của nguồn tỷ giá (ví dụ: `https://api.exchangerate-api.com/v4/latest/GBP`).
  - **Headers**:
    ```
    Accept: application/json
    ```
  - **Credentials**: Nếu API yêu cầu API Key, thêm vào **Headers** (`Authorization: Bearer YOUR_API_KEY`).

##### **🔹 Node 3: Code (Xử Lý Dữ Liệu)**
- **Tên**: "Code"
- **Lưu ý**: Các sếp có thể chỉnh sửa script JavaScript để lấy tỷ giá GBP từ JSON trả về API.
  ```javascript
  // Ví dụ: Lấy tỷ giá GBP -> USD
  const gbpToUsd = $input.all()[0].json.rates.USD;
  return { gbpToUsd: gbpToUsd };
  ```
  - **Lưu ý**: Nếu không quen với JavaScript, các sếp có thể **xem code mẫu** từ [n8n.io/workflows/4814](https://n8n.io/workflows/4814) và sao chép.

##### **🔹 Node 4: Gmail (Gửi Email)**
- **Tên**: "send email to adress"
- **Cấu hình**:
  - **Credentials**: Chọn `gmailOAuth2`.
  - **To**: Địa chỉ email nhận (ví dụ: `sếp@example.com`).
  - **Subject**: "Tỷ Giá GBP Hôm Nay" (có thể tùy chỉnh).
  - **Body**: Thay thế bằng nội dung email (ví dụ: `Tỷ giá GBP -> USD hôm nay là: $${gbpToUsd}`).

##### **🔹 Node 5: Google Sheets (Lưu Lịch Sử)**
- **Tên**: "Google Sheets"
- **Cấu hình**:
  - **Credentials**: Chọn `googleSheetsOAuth2Api`.
  - **Operation**: `append` (thêm dữ liệu mới vào cuối sheet).
  - **Sheet Name**: Tên sheet muốn lưu (ví dụ: `Tỷ Giá GBP`).
  - **Range**: `A1` (để ghi vào ô A1).
  - **Data**: Chọn `gbpToUsd` từ Node Code.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**: Chạy workflow với dữ liệu mẫu để kiểm tra email và Google Sheets.
2. **Bật Active**: Sau khi kiểm tra thành công, bật **Active** để workflow chạy tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**: Thay vì email, các sếp có thể gửi thông báo trên Slack/Telegram bằng **node Slack** hoặc **node Telegram Bot**.
2. **Lưu Log**: Sử dụng **node StickyNote** để lưu lịch sử chạy workflow.
3. **Báo Cáo Định Kỳ**: Tạo một **workflow khác** để tổng hợp dữ liệu từ Google Sheets và gửi báo cáo hàng tuần/month.
4. **Tự Động Hàng Ngày**: Thay **Manual Trigger** bằng **Schedule Trigger** để workflow chạy tự động mỗi ngày.

---

### 📌 **Kết Luận**
Workflow này giúp các sếp **tự động hóa việc theo dõi tỷ giá GBP**, tiết kiệm thời gian và giảm thiểu lỗi thủ công. **Hãy áp dụng ngay** và không cần lo lắng về việc tra cứu tỷ giá mỗi ngày nữa!

👉 **Bắt đầu tự động hóa ngay**: [Tải workflow từ n8n.io](https://n8n.io/workflows/4814) và cài đặt trên VPS của mình! 🚀