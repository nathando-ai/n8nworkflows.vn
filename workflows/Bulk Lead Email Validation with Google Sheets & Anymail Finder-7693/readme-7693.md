---
title: "🚀 Tự Động Hóa Kiểm Tra Email Bulk Cho Lead Marketing Với Google Sheets & Anymail Finder"
description: "Workflow tự động hóa kiểm tra tính hợp lệ của hàng trăm email lead từ Google Sheets chỉ trong vài giây, giúp các sếp tiết kiệm thời gian và tối ưu hóa chiến dịch marketing. Kết quả: Dữ liệu lead chính xác 100%, giảm tỷ lệ bounce email, tăng hiệu quả chuyển đổi."
slug: "tieu-dong-hoa-kiem-tra-email-lead-google-sheets"
tags: [n8n, automation, lead-generation, google-sheets, email-validation, no-code]
keywords: [tự động hóa email lead, kiểm tra email bulk, n8n workflow, Anymail Finder API, Google Sheets tự động hóa]
---

# 🚀 **Tự Động Hóa Kiểm Tra Email Bulk Cho Lead Marketing Với Google Sheets & Anymail Finder**

### **Nỗi Đau Của Các Sếp Trong Chiến Dịch Marketing**
Các sếp thường phải mất **giờ đồng hồ** để kiểm tra tính hợp lệ của hàng trăm email lead thủ công, dẫn đến:
- **Tỷ lệ bounce cao** (email không tồn tại hoặc bị chặn) làm giảm hiệu quả email marketing.
- **Dữ liệu lead không chính xác**, gây lãng phí chi phí quảng cáo.
- **Thời gian làm việc bị gián đoạn** khi phải kiểm tra từng email một.

**Workflow này giải quyết tất cả vấn đề trên bằng cách tự động hóa toàn bộ quy trình kiểm tra email bulk chỉ trong vài giây!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động 24/7 mà không bị gián đoạn, các sếp nên **self-host n8n trên VPS** để đảm bảo tính bảo mật và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Kiểm tra **tất cả email lead chỉ trong vài giây** thay vì thủ công mất nhiều giờ.
✅ **Dữ liệu lead chính xác 100%**: Loại bỏ email không tồn tại hoặc bị chặn trước khi gửi.
✅ **Tăng hiệu quả email marketing**: Giảm tỷ lệ bounce, tăng tỷ lệ mở và chuyển đổi.
✅ **Hoạt động liên tục**: Workflow tự động chạy mỗi khi có lead mới được thêm vào Google Sheets.
✅ **Tích hợp AI**: Sử dụng API Anymail Finder để kiểm tra email với độ chính xác cao.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Google Sheets** (đã clone mẫu sheet từ [đây](https://docs.google.com/spreadsheets/d/108sjf89zpKRyZbGq9MjcNFQOezP4hi97SJ_uAkXc8WI/edit?usp=sharing))
✔ **API Key của Anymail Finder** (miễn phí trong giai đoạn thử nghiệm)
✔ **Credentials OAuth2 cho Google Sheets** (để n8n có thể đọc và cập nhật sheet)
✔ **Tài khoản n8n** (cài đặt trên máy chủ hoặc VPS)

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/7693) (nút "Export").
- **Trên n8n Editor**, nhấn **"Import"** và chọn file JSON đã tải.
- **Hoặc**, copy toàn bộ JSON từ [đây](https://n8n.io/workflows/7693) và dán vào **"Import from JSON"** trong Editor.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này bao gồm **5 node chính**, các sếp cần cấu hình kỹ lưỡng như sau:

##### **🔹 Node 1: Manual Trigger (Bắt đầu thủ công)**
- **Chức năng**: Khởi động workflow khi các sếp nhấn nút **"Run Workflow"**.
- **Lưu ý**: Có thể thay thế bằng **Webhook** nếu muốn tự động chạy khi có sự kiện mới.

##### **🔹 Node 2: Get Leads (Lấy dữ liệu từ Google Sheets)**
- **Cấu hình**:
  - **Credentials**: Chọn **"googleSheetsOAuth2Api"** (đã cấu hình trước).
  - **Sheet Name**: Điền tên sheet từ mẫu đã clone (ví dụ: **"Leads"**).
  - **Range**: Điền `"Sheet1!A2:B"` (giả sử cột A là Email, cột B là Status).
  - **Test Run**: Nhấn **"Test"** để đảm bảo kết nối thành công.

##### **🔹 Node 3: Loop Over Items (Lặp qua từng email)**
- **Chức năng**: Chia dữ liệu thành batch để kiểm tra từng email một.
- **Lưu ý**:
  - **Batch Size**: Đặt số lượng email trong mỗi batch (ví dụ: **100**).
  - **Kiểm tra**: Nếu sheet có **1000 email**, workflow sẽ chạy **10 lần** (mỗi lần 100 email).

##### **🔹 Node 4: Check Email Status (Kiểm tra email với Anymail Finder)**
- **Cấu hình**:
  - **Credentials**: Tạo mới **HTTP Header Auth** với tên **"Anymail Finder"**.
    - **Name**: `Authorization`
    - **Value**: `Bearer YOUR_API_KEY` (thay `YOUR_API_KEY` bằng API Key của Anymail Finder).
  - **HTTP Method**: `POST`
  - **URL**: `https://api.anymailfinder.com/v1/email/validate`
  - **Body**:
    ```json
    {
      "email": "{{$node["Loop Over Items"].json["$.email"]}}"
    }
    ```
  - **Test Run**: Nhấn **"Test"** và đảm bảo trả về kết quả như:
    ```json
    {
      "email": "test@example.com",
      "valid": true,
      "disposable": false,
      "role": false,
      "smtp_check": "OK"
    }
    ```

##### **🔹 Node 5: Update Email Status (Cập nhật trạng thái vào Google Sheets)**
- **Cấu hình**:
  - **Credentials**: Chọn **"googleSheetsOAuth2Api"** (giống Node 2).
  - **Range**: Đặt `"Sheet1!B2:B"` (cập nhật cột Status).
  - **Update Values**:
    ```json
    {
      "status": "{{$node["Check email status"].json["valid"] ? "VALID" : "INVALID"}}"
    }
    ```
  - **Test Run**: Kiểm tra sheet có cập nhật trạng thái mới không.

#### **3. Kích Hoạt ⚡️**
- **Test Run**: Chạy workflow với **dữ liệu mẫu** (ví dụ: 5 email) để đảm bảo mọi thứ hoạt động.
- **Bật Active**: Sau khi kiểm tra thành công, nhấn **"Active"** để workflow chạy tự động khi được kích hoạt.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tích Hợp Slack/Telegram**:
   - Thêm **node Slack/Telegram** sau Node 5 để thông báo kết quả kiểm tra (ví dụ: "Đã kiểm tra 100 email, 95% hợp lệ").
   - **Cách làm**:
     - Sử dụng **node `n8n-nodes-base.slack`** hoặc **`n8n-nodes-base.telegram`**.
     - Gửi tin nhắn tự động khi workflow hoàn thành.

2. **Lưu Log Kiểm Tra**:
   - Thêm **node `n8n-nodes-base.chronicle`** (nếu có) để lưu lịch sử kiểm tra email.
   - **Ưu điểm**: Các sếp có thể theo dõi lịch sử và phân tích xu hướng.

3. **Chạy Định Kỳ**:
   - Sử dụng **node `n8n-nodes-base.schedule`** để chạy workflow **hàng ngày/tuần** thay vì thủ công.
   - **Cấu hình**:
     - Chọn **"Cron"** (ví dụ: `0 0 * * *` để chạy mỗi ngày lúc 00:00).

4. **Tích Hợp CRM**:
   - Nếu sử dụng **HubSpot, Salesforce, hoặc Zoho CRM**, các sếp có thể thay thế Google Sheets bằng **node CRM tương ứng** để tự động cập nhật trạng thái lead.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc kiểm tra email thủ công, đồng thời **tăng hiệu quả chiến dịch marketing** bằng cách loại bỏ email không hợp lệ. **Chỉ cần 5 phút để import và cấu hình**, sau đó workflow sẽ hoạt động tự động mỗi khi có lead mới!

**Hành động ngay**:
1. **Clone sheet mẫu** từ [đây](https://docs.google.com/spreadsheets/d/108sjf89zpKRyZbGq9MjcNFQOezP4hi97SJ_uAkXc8WI/edit?usp=sharing).
2. **Cấu hình API Key Anymail Finder** và **credentials Google Sheets**.
3. **Import workflow** và **bật Active** để bắt đầu tự động hóa!

**🚀 Cùng tự động hóa marketing của mình ngay hôm nay!** 🚀