---
title: "🏥 Tự Động Hóa Theo Dõi Thông Số Sức Khỏe Bệnh Nhân & Cảnh Báo Dị Ứng Với Philips IntelliVue & Google Sheets"
description: "Giải pháp tự động hóa 24/7 thu thập, xử lý và cảnh báo bất thường về thông số sức khỏe bệnh nhân từ Philips IntelliVue, tự động lưu vào Google Sheets và gửi email cảnh báo cho y bác sĩ. Tiết kiệm thời gian, giảm sai sót và nâng cao chất lượng chăm sóc y tế."
slug: "tự-dộng-hoa-theo-doi-thong-so-suc-khoe-benh-nhan"
tags: [n8n, tự động hóa y tế, Philips IntelliVue, Google Sheets, cảnh báo AI, no-code]
keywords: [tự động hóa theo dõi sức khỏe bệnh nhân, cảnh báo dị ứng thông số y tế, n8n workflow y tế, thu thập dữ liệu y tế tự động, Google Sheets y tế]
---

# 🚀 **Tự Động Hóa Theo Dõi Thông Số Sức Khỏe Bệnh Nhân & Cảnh Báo Dị Ứng Với Philips IntelliVue & Google Sheets**

### **Giải pháp tự động hóa 24/7 cho bác sĩ và nhân viên y tế**
Hiện nay, việc theo dõi liên tục các thông số sức khỏe của bệnh nhân (như nhịp tim, oxy máu, huyết áp, nhiệt độ...) là một nhiệm vụ mệt mỏi và dễ gây sai sót khi thực hiện thủ công. **Workflow này tự động hóa toàn bộ quy trình:**
- Thu thập dữ liệu từ **Philips IntelliVue** (máy theo dõi thông số y tế) mỗi **30 giây**.
- Xử lý và kiểm tra dữ liệu để phát hiện **dị ứng** (như nhịp tim bất thường, oxy máu quá thấp, huyết áp cao/ thấp).
- **Lưu tự động** vào **Google Sheets** với cấu trúc chi tiết (bao gồm cả cảnh báo và trạng thái thiết bị).
- **Gửi email cảnh báo** ngay khi phát hiện thông số bất thường đến bác sĩ hoặc nhân viên y tế.

Kết quả? **Tiết kiệm thời gian, giảm sai sót, và nâng cao chất lượng chăm sóc y tế** với một giải pháp **100% tự động hóa, không cần code**.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tự động hóa 24/7**: Không cần nhân viên theo dõi thủ công, giảm thiểu sai sót do mệt mỏi.
- **Cảnh báo tức thời**: Nhận email ngay khi phát hiện thông số bất thường (ví dụ: nhịp tim quá nhanh, oxy máu dưới 90%).
- **Dữ liệu trung tâm**: Tất cả thông số được lưu vào **Google Sheets** với cấu trúc rõ ràng, dễ tra cứu và phân tích.
- **Tiết kiệm chi phí**: Giảm thời gian của y bác sĩ cho việc theo dõi thủ công, tập trung vào chăm sóc bệnh nhân.
- **Dễ mở rộng**: Kết hợp với **Slack/Telegram** để cảnh báo nhóm hoặc sử dụng **AI LLM** để phân tích sâu hơn.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[**CHUẨN BỊ**]
Để workflow hoạt động, các sếp cần chuẩn bị:
✅ **Tài khoản Philips IntelliVue**:
   - **URL Gateway** (địa chỉ API của máy theo dõi thông số).
   - **Tài khoản và mật khẩu** (để xác thực HTTP Basic Auth).

✅ **Tài khoản Google Sheets**:
   - **Google Workspace** (nếu là bệnh viện/đơn vị y tế).
   - **File Google Sheets** đã tạo sẵn với **cấu trúc cột** như sau:
     ```
     patient_id | patient_name | room_number | timestamp | ecg_heart_rate | spo2_oxygen_saturation | nibp_systolic | nibp_diastolic | temperature_celsius | respiration_rate | etco2_end_tidal | cardiac_output | alert_level | alerts | device_status
     ```
   - **Chia sẻ file với n8n** (quyền "Sửa" hoặc "Xem").

✅ **Tài khoản Email (SMTP)**:
   - **Gmail** (hoặc tài khoản email doanh nghiệp) để gửi cảnh báo.
   - **API Key SMTP** (nếu dùng Gmail, có thể sử dụng **Less Secure Apps** hoặc **OAuth2**).

✅ **n8n Self-hosted** (không dùng n8n Cloud):
   - Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng**.
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/7317](https://n8n.io/workflows/7317) (chọn **Export JSON**).
2. **Mở n8n Editor** (trên VPS hoặc n8n Cloud).
3. **Nhấn "Import"** và chọn file JSON vừa tải.
4. **Chọn "Create new workflow"** và nhấn **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Tải JSON** từ link trên.
2. **Mở n8n Editor** → **Create new workflow** → **Import from JSON**.
3. **Dán JSON** và nhấn **Import**.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **7 node chính**, mỗi node cần cấu hình kỹ lưỡng:

#### **🔹 Node 1: Poll Device Data Every 30s (Cron)**
- **Cấu hình**:
  - **Schedule**: `*/30 * * * *` (lặp mỗi 30 giây).
  - **Time Zone**: Chọn **UTC** hoặc **múi giờ của bệnh viện**.
  - **Không cần thay đổi gì khác**.

#### **🔹 Node 2: Fetch from IntelliVue Gateway (HTTP Request)**
- **Cấu hình**:
  - **Method**: `GET` (hoặc `POST` nếu API yêu cầu).
  - **URL**: Điền **URL API của Philips IntelliVue** (ví dụ: `https://your-intellivue-gateway/api/data`).
  - **Authentication**:
    - Chọn **HTTP Basic Auth**.
    - Điền **Username** và **Password** từ tài khoản Philips IntelliVue.
  - **Headers** (nếu cần):
    - Thêm `Content-Type: application/json` nếu API yêu cầu.

#### **🔹 Node 3 & 4: Process Device Data & Validate & Enrich Data (Code)**
- **Lưu ý**:
  - **Không cần chỉnh sửa** nếu đã import từ file JSON gốc (n8n sẽ tự động xử lý logic).
  - Nếu cần **cập nhật logic**, các sếp cần **hiểu rõ API của Philips IntelliVue** và sửa code trong **n8n Code Node**.
  - **Dữ liệu đầu ra** phải tuân theo **cấu trúc Google Sheets** (xem phần **Google Sheet Structure** dưới đây).

#### **🔹 Node 5: Save to Patient Database (Google Sheets)**
- **Cấu hình**:
  - **Credentials**: Chọn **googleApi** (đã cấu hình trước khi import).
  - **Spreadsheet ID**: Điền **ID của file Google Sheets** (tìm trong URL: `https://docs.google.com/spreadsheets/d/[ID]/edit`).
  - **Sheet Name**: Điền **tên sheet** (ví dụ: `PatientVitals`).
  - **Operation**: Đã mặc định là **append** (thêm dữ liệu mới vào cuối).
  - **Row Data**: **Không cần chỉnh**, n8n sẽ tự động truyền dữ liệu từ node **Process Device Data**.

#### **🔹 Node 6: Send Clinical Alert (Email Send)**
- **Cấu hình**:
  - **Credentials**: Chọn **smtp** (đã cấu hình trước khi import).
  - **To**: Điền **email của bác sĩ/nhân viên y tế** (ví dụ: `doc.nguyen@benhvien.com`).
  - **Subject**: Đã mặc định là **"🚨 Cảnh báo thông số sức khỏe bất thường"** (có thể chỉnh).
  - **HTML Content**: **Không cần chỉnh**, n8n sẽ tự động tạo email cảnh báo với thông tin:
     ```
     <p>🚨 Bệnh nhân: {{$node["Process Device Data"].json["patient_name"]}</p>
     <p>Phòng: {{$node["Process Device Data"].json["room_number"]}</p>
     <p>Thông số bất thường: {{$node["Process Device Data"].json["alerts"]}}</p>
     ```
  - **Nếu dùng Gmail**:
     - Cần **bật "Less Secure Apps"** (nếu không dùng OAuth2).
     - **Không kích hoạt 2FA** (nếu dùng OAuth2, cấu hình thêm trong **Credentials SMTP**).

#### **🔹 Node 7: Switch (Switch)**
- **Lưu ý**:
  - **Không cần chỉnh**, node này **lọc dữ liệu** để chỉ gửi email khi có **cảnh báo** (`alert_level` ≠ `normal`).
  - Nếu muốn **cập nhật điều kiện**, cần chỉnh trong **n8n Code Node**.

---
### **3. Kích hoạt ⚡️**
1. **Test Run (Kiểm tra thử)**:
   - Nhấn **Run Workflow** để kiểm tra dữ liệu mẫu.
   - Kiểm tra **Google Sheets** và **email** để đảm bảo dữ liệu được lưu và cảnh báo được gửi.
2. **Bật Active**:
   - Sau khi test thành công, **bật Active** để workflow chạy tự động.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::tip[**CÁC Ý TƯỞNG MỞ RỘNG**]
- **Kết hợp với Slack/Telegram**:
  - Thêm **node Slack Webhook** hoặc **Telegram Bot** để cảnh báo ngay trên ứng dụng chat.
  - **Cách làm**:
    1. Tạo **webhook Slack** hoặc **bot Telegram**.
    2. Thêm **node `n8n-nodes-base.slack`** hoặc `n8n-nodes-base.telegram` vào workflow.
    3. Chỉnh **message template** để hiển thị thông tin cảnh báo.

- **Lưu log vào Google Drive**:
  - Thêm **node `n8n-nodes-base.googleDrive`** để lưu **log chi tiết** của cảnh báo.
  - **Cấu trúc log**:
    ```
    timestamp | patient_id | alert_type | device_status | action_taken
    ```

- **Sử dụng AI LLM để phân tích sâu**:
  - Thêm **node `n8n-nodes-ai.llm`** (nếu dùng n8n với AI integration).
  - **Prompt ví dụ**:
    ```
    "Analyze the following patient vitals data and suggest possible medical conditions:
    - Heart rate: 120 bpm
    - SpO2: 85%
    - Temperature: 39.5°C
    - Respiration rate: 30 breaths/min"
    ```

- **Báo cáo định kỳ**:
  - Thêm **node `n8n-nodes-base.cron`** để chạy **tối ngày** và gửi **báo cáo tổng hợp** về tình trạng bệnh nhân qua email.
  - **Dữ liệu báo cáo**:
    - Số lượng cảnh báo trong ngày.
    - Thống kê thông số trung bình.
    - Bệnh nhân có nguy cơ cao nhất.

- **Kết hợp với Philips HealthSuite**:
  - Nếu bệnh viện dùng **Philips HealthSuite**, có thể **tích hợp API** để tự động cập nhật dữ liệu vào hệ thống quản lý bệnh viện.
:::

---
## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** để tự động hóa theo dõi và cảnh báo thông số sức khỏe bệnh nhân, giúp **giảm tải cho y bác sĩ**, **tăng tính chính xác** và **nâng cao chất lượng chăm sóc y tế**.

👉 **Hành động ngay**:
1. **Chuẩn bị tài khoản** (Philips IntelliVue, Google Sheets, Email SMTP).
2. **Import workflow** và **cấu hình** theo hướng dẫn.
3. **Test Run** và **bật Active** để workflow chạy tự động.

**Nếu có vấn đề**, các sếp có thể:
- **Tra cứu tài liệu chính thức** của Philips IntelliVue.
- **Liên hệ The AI Squad** (tác giả workflow) qua [n8n.io](https://n8n.io/) để hỗ trợ.

**Chúc các sếp thành công với việc tự động hóa y tế!** 🚀🏥