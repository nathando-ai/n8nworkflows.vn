---
title: "🔍 Kiểm tra Email & Trích Xuất Domain Tự Động - Không Cần Code!"
description: "Workflow tự động hóa kiểm tra tính hợp lệ của email và trích xuất domain từ địa chỉ email chỉ trong vài giây. Giúp các sếp tiết kiệm thời gian và giảm thiểu lỗi khi xử lý dữ liệu email hàng loạt."
slug: "kiem-tra-email-trich-xuat-domain-tu-dong"
tags: [n8n, automation, email-validation, domain-extraction, no-code]
keywords: [n8n workflow email, kiểm tra email tự động, trích xuất domain, tự động hóa dữ liệu email, n8n building blocks]
---

# 🔍 Kiểm tra Email & Trích Xuất Domain Tự Động - Không Cần Code!

Bạn có bao giờ phải kiểm tra hàng trăm địa chỉ email để xác định tính hợp lệ và trích xuất domain để phân loại, phân tích hoặc gửi thông báo? Hoặc phải làm thủ công trên Excel, mất nhiều thời gian và dễ mắc sai sót? **Workflow này sẽ giải quyết tất cả những vấn đề đó chỉ trong vài giây!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động 24/7 và không bị gián đoạn, các sếp nên cài đặt n8n trên **VPS riêng** (Self-hosted) để đảm bảo tính ổn định và bảo mật cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần kiểm tra email thủ công trên Excel hoặc Google Sheets.
- **Độ chính xác cao**: Trích xuất domain và xác minh email một cách tự động, giảm thiểu sai sót.
- **Dễ dàng mở rộng**: Dữ liệu được lưu trữ và có thể kết nối với các công cụ khác (Slack, CRM, database...).
- **Hoạt động liên tục**: Chạy 24/7 trên VPS, không phụ thuộc vào thời gian làm việc của nhân viên.
:::

---

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow này hoạt động, các sếp cần:
- **Tài khoản n8n**: Đã cài đặt và cấu hình n8n trên máy chủ hoặc VPS.
- **Dữ liệu email**: Một danh sách email (có thể là từ file CSV, Google Sheets, hoặc nhập thủ công).
- **Không cần API key**: Workflow này sử dụng các chức năng cơ bản của n8n, không yêu cầu API bên thứ ba.
:::

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Bước 1: Truy cập [n8n Editor](https://n8n.io/) và chọn **Import Workflow**.
Bước 2: Chọn file JSON của workflow (tải từ [đây](https://n8n.io/workflows/2239)) hoặc copy/paste JSON từ file vào ô nhập liệu.
Bước 3: Nhấn **Import** để workflow xuất hiện trên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm **3 node chính**, nhưng **node Debug Helper** chỉ là ví dụ để test. Các sếp cần thay thế nó bằng **nguồn dữ liệu thực tế** của mình. Dưới đây là hướng dẫn chi tiết:

##### **Node 1: Manual Trigger (Bắt đầu workflow)**
- **Tên node**: "When clicking 'Test workflow'"
- **Lưu ý**: Node này chỉ dùng để test. Sau khi thay thế node Debug Helper, các sếp có thể **bỏ node này** và thay bằng **Webhook** hoặc **Trigger từ API** để tự động kích hoạt workflow khi có dữ liệu mới.

##### **Node 2: Set (Trích xuất domain và kiểm tra email)**
- **Tên node**: "Set these fields to extract domain"
- **Cấu hình**:
  - **Field 1**: `email` (địa chỉ email đầu vào).
  - **Field 2**: `domain` (trích xuất từ email bằng công thức: `split(email, '@')[1]`).
  - **Field 3 (tùy chọn)**: `isValid` (kiểm tra email có hợp lệ không bằng cách kiểm tra định dạng cơ bản).
  - **Lưu ý**:
    - Nếu muốn kiểm tra email **cực kỳ chính xác**, các sếp có thể kết hợp với **node Email Validator** (n8n-nodes-email) hoặc API bên thứ ba như [Hunter.io](https://hunter.io/) hoặc [ZeroBounce](https://www.zerobounce.net/).
    - Ví dụ cấu hình cho `domain`:
      ```json
      {
        "jsonpath": "$['email'].split('@')[1]"
      }
      ```

##### **Node 3: Debug Helper (Thay thế bằng nguồn dữ liệu thực tế)**
- **Tên node**: "Generate random data" (chỉ dùng để test).
- **Lưu ý**:
  - **Bỏ node này** và thay bằng một trong các nguồn dữ liệu sau:
    - **Google Sheets**: Node `Google Sheets` để lấy dữ liệu từ sheet.
    - **CSV/Excel**: Node `File System` hoặc `HTTP Request` để đọc file.
    - **API**: Node `HTTP Request` để lấy dữ liệu từ API.
    - **Webhook**: Node `Webhook` để nhận dữ liệu từ bên ngoài.
  - **Ví dụ thay thế bằng Google Sheets**:
    1. Thêm node `Google Sheets` vào workflow.
    2. Cấu hình:
       - **Action**: `Get rows`.
       - **Sheet Name**: Tên sheet chứa email.
       - **Credentials**: Thêm OAuth 2.0 credentials của Google.
    3. Kết nối node `Google Sheets` với node `Set` để truyền dữ liệu email vào.

#### 3. Kích hoạt ⚡️
- **Test run**: Sau khi cấu hình xong, nhấn **Run Workflow** để kiểm tra kết quả.
- **Bật Active**: Sau khi test thành công, chuyển trạng thái workflow sang **Active** để chạy tự động.

---

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết nối với Slack/Telegram**:
   - Thêm node `Slack` hoặc `Telegram Bot` sau node `Set` để gửi kết quả kiểm tra email về kênh chat.
   - Ví dụ: Khi email không hợp lệ, bot sẽ gửi thông báo: *"Email `abc@example.com` không hợp lệ!"*.

2. **Lưu log vào database**:
   - Thêm node `MySQL` hoặc `PostgreSQL` để lưu kết quả kiểm tra vào bảng dữ liệu.
   - Có thể sử dụng node `n8n-nodes-database` để kết nối với cơ sở dữ liệu.

3. **Gửi báo cáo định kỳ**:
   - Sử dụng node `n8n-nodes-schedule` để chạy workflow hàng ngày và gửi báo cáo tổng hợp về email hoặc Slack.
   - Ví dụ: *"Tổng số email hợp lệ: 100, không hợp lệ: 5 trong ngày hôm nay."*

4. **Tích hợp với CRM**:
   - Nếu sử dụng CRM như HubSpot, Salesforce, hoặc Zoho CRM, các sếp có thể kết nối workflow này để **tự động loại bỏ email không hợp lệ** trong pipeline bán hàng.

---

### 📌 Kết luận
Workflow này là **công cụ mạnh mẽ** giúp các sếp tự động hóa việc kiểm tra email và trích xuất domain **không cần viết một dòng code**. Bằng cách thay thế node Debug Helper bằng nguồn dữ liệu thực tế, workflow sẽ hoạt động hiệu quả và tiết kiệm thời gian cho các nhiệm vụ lặp đi lặp lại.

**Hãy áp dụng ngay và tự động hóa công việc của mình!** 🚀
Nếu có bất kỳ câu hỏi hoặc cần hỗ trợ, hãy để lại comment bên dưới. Chúc các sếp thành công! 💪