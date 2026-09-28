---
title: "🚨 **Tự Động Hóa Bài Tập Phishing Red Team: Giả Lập Link Mắc Bẫy & Theo Dõi Click Chi Tiết (Google Sheets)**"
description: "Workflow này giúp các sếp Security tự động hóa bài tập phishing Red Team bằng cách tạo link giả lận, theo dõi lượt click và ghi log chi tiết vào Google Sheets — tiết kiệm thời gian và tăng độ chính xác trong đánh giá nhân viên."
slug: "tieu-dong-hoa-bai-tap-phishing-red-team"
tags: [n8n, automation, security, red-team, google-sheets]
keywords: [tự động hóa phishing red team, theo dõi click link giả lận, n8n security, bài tập phishing tự động, google sheets log]
---

# 🚨 **Tự Động Hóa Bài Tập Phishing Red Team: Giả Lập Link Mắc Bẫy & Theo Dõi Click Chi Tiết**

### **Nỗi Đau Của Các Sếp Security**
Trong quá trình đào tạo **Red Team**, việc tạo và theo dõi **bài tập phishing** thủ công là một công việc **mệt mỏi, tốn thời gian và dễ sai sót**. Các sếp phải:
- **Tạo link giả lận** một cách thủ công (rất dễ bị lộ hoặc sai cấu trúc).
- **Theo dõi lượt click** của nhân viên bằng cách kiểm tra log thủ công.
- **Ghi chép kết quả** vào bảng Excel/Google Sheets, dễ bị lỗi hoặc thiếu dữ liệu.
- **Không có báo cáo tự động**, phải tổng hợp sau khi bài tập kết thúc.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tạo link phishing giả lận tự động** (sử dụng RedirectCloak).
✅ **Theo dõi mỗi lượt click** và ghi log chi tiết (IP, thời gian, nhân viên).
✅ **Ghi dữ liệu vào Google Sheets** một cách tự động.
✅ **Không cần viết code**, chỉ cần cấu hình trong n8n.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**Lợi Ích Cốt Lõi**]
- **Tiết kiệm thời gian**: Không cần tạo link thủ công, chỉ cần kích hoạt workflow.
- **Độ chính xác cao**: Dữ liệu ghi log tự động, không bị lỗi nhân sự.
- **Báo cáo chi tiết**: Theo dõi từng lượt click, IP, và thời gian phản hồi.
- **Tích hợp với Google Sheets**: Dễ dàng phân tích và báo cáo cho ban lãnh đạo.
- **Mô phỏng thực tế**: Link giả lận gần giống với phishing thật, tăng giá trị đào tạo.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Google Sheets** (để lưu log kết quả).
✔ **API Key của RedirectCloak** (để tạo link giả lận).
✔ **Tài khoản n8n Self-hosted** (để chạy workflow 24/7).

:::info[**Gợi ý hạ tầng cho n8n**]
Để workflow hoạt động **ổn định và an toàn**, các sếp nên cài n8n trên **VPS riêng** (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/6509](https://n8n.io/workflows/6509).
- **Mở n8n Editor** → Nhấn **"Import"** → Chọn file JSON vừa tải.
- **Hoặc copy/paste JSON** từ file vào n8n Editor.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **5 node chính**, các sếp cần cấu hình kỹ lưỡng:

##### **🔹 Node 1: ⚡ Trigger RedirectCloak (Manual Trigger)**
- **Chức năng**: Khởi động workflow khi cần tạo link phishing mới.
- **Lưu ý**:
  - **Không cần cấu hình gì** (node này chỉ dùng để kích hoạt).
  - **Kích hoạt bằng nút "Run Workflow"** trong n8n Editor.

##### **🔹 Node 2: 🔗 Generate Redirect Link (Set Node)**
- **Chức năng**: Tạo link giả lận (phishing) từ RedirectCloak.
- **Cấu hình cần thiết**:
  - **Input Data**:
    ```json
    {
      "url": "https://redirectcloak.com/your-tracking-link" // Thay bằng URL thật của RedirectCloak
    }
    ```
  - **Output**:
    - Workflow sẽ tự động tạo link giả lận (ví dụ: `https://fake-phishing-link.com`).

##### **🔹 Node 3: 🛰️ Simulate Redirect Hit (Set Node)**
- **Chức năng**: Khi người dùng click link, RedirectCloak sẽ gửi dữ liệu về node này.
- **Cấu hình cần thiết**:
  - **Input Data** (tự động từ RedirectCloak):
    ```json
    {
      "ip": "192.168.1.1", // IP của người click
      "timestamp": "2024-05-20T10:00:00Z", // Thời gian click
      "userAgent": "Mozilla/5.0..." // Thông tin trình duyệt
    }
    ```
  - **Không cần chỉnh sửa**, node này tự động nhận dữ liệu từ RedirectCloak.

##### **🔹 Node 4: Google Sheets (Append Redirect Logs)**
- **Chức năng**: Ghi log click vào Google Sheets.
- **Cấu hình cần thiết**:
  - **Credentials**:
    - Tạo **Service Account** trong Google Cloud Console (nếu chưa có).
    - Cấp quyền cho Google Sheets bằng **JSON Key File**.
  - **Sheet Name**: Đặt tên sheet (ví dụ: **"Phishing_Logs"**).
  - **Headers** (cột trong Google Sheets):
    ```
    IP, Timestamp, User Agent, Employee Name (nếu có)
    ```
  - **Append Mode**: Chọn **"Append"** để thêm dữ liệu mới vào cuối bảng.

##### **🔹 Node 5: 📄 Append Redirect Logs (Google Sheets - Lần 2)**
- **Chức năng**: Ghi thêm thông tin chi tiết (nếu cần).
- **Lưu ý**:
  - Nếu chỉ cần ghi log cơ bản, **node 4 đã đủ**.
  - Nếu muốn thêm cột **"Status"** (ví dụ: "Success" hoặc "Failed"), cấu hình ở đây.

#### **3. Kích Hoạt ⚡️ Workflow**
- **Test Run**:
  - Nhấn **"Run Workflow"** để kiểm tra.
  - Kiểm tra **Google Sheets** xem dữ liệu có ghi đúng không.
- **Bật Active**:
  - Sau khi test thành công, **bật "Active"** để workflow chạy tự động khi kích hoạt.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tích Hợp Slack/Telegram**:
   - Sử dụng **node Slack/Telegram** để thông báo khi có lượt click mới.
   - Cấu hình:
     ```json
     {
       "text": "🚨 New Phishing Click Detected! IP: {{$node["🛰️ Simulate Redirect Hit"].json()["ip"]}}"
     }
     ```

2. **Lưu Log vào Database (MySQL/PostgreSQL)**:
   - Thay thế **Google Sheets** bằng **node Database** để lưu trữ dài hạn.

3. **Tự Động Gửi Báo Cáo Định Kỳ**:
   - Sử dụng **node Set** + **node Email/Slack** để gửi báo cáo hàng tuần.

4. **Mô Phỏng Phishing Đa Loại**:
   - Tạo nhiều **workflow riêng biệt** cho từng loại phishing (email, SMS, link).

---
### 📌 **Kết Luận**
Workflow này **giúp các sếp Security tự động hóa bài tập phishing Red Team một cách hiệu quả**, tiết kiệm thời gian và tăng độ chính xác. **Không cần viết code**, chỉ cần cấu hình trong n8n là có thể:
✔ **Tạo link giả lận** một cách tự động.
✔ **Theo dõi từng lượt click** và ghi log chi tiết.
✔ **Tích hợp với Google Sheets** để báo cáo dễ dàng.

**Hãy áp dụng ngay để nâng cao hiệu quả đào tạo Red Team của doanh nghiệp!** 🚀

---
**🔗 [Xem workflow gốc tại n8n.io](https://n8n.io/workflows/6509)**
**📩 Có thắc mắc? Hãy liên hệ với Adnan Tariq (Founder CYBERPULSE AI) tại [LinkedIn](https://linkedin.com/in/adnan-tariq-4b2a1a47)**