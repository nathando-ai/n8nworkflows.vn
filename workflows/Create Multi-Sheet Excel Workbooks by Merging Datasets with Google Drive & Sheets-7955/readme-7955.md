---
title: "📊 Tự Động Hoà Nhiều Bảng Dữ Liệu Lên File Excel Multi-Sheet Với Google Drive & Sheets (N8N)"
description: "Workflow này tự động hợp nhất 2 dataset thành 1 file Excel có nhiều sheet, đồng thời ghi dữ liệu vào Google Sheets và lưu file lên Google Drive - giúp các sếp tiết kiệm thời gian và tránh sai sót khi làm thủ công."
slug: "tieu-dong-hoa-multi-sheet-excel-google-drive-sheets"
tags: [n8n, automation, google-sheets, google-drive, excel, no-code, data-merging]
keywords: [n8n tự động hóa, tạo file excel nhiều sheet, hợp nhất dữ liệu google sheets, lưu file google drive, workflow n8n google]
---

# 🚀 **Tự Động Hoà Nhiều Bảng Dữ Liệu Lên File Excel Multi-Sheet Với Google Drive & Sheets**

### **Giải pháp cho các sếp bị mệt mỏi với việc copy-paste dữ liệu giữa nhiều bảng Excel**
Hãy tưởng tượng một tình huống: Bạn phải hợp nhất **2 hay nhiều bảng dữ liệu** từ các nguồn khác nhau (ví dụ: dữ liệu từ CRM, báo cáo hàng tháng, hoặc kết quả phân tích AI) thành **1 file Excel có nhiều sheet**, sau đó **ghi dữ liệu vào Google Sheets** và **lưu file lên Google Drive** để chia sẻ với team. Nếu làm thủ công, việc này sẽ tốn **giờ đồng hồ** và dễ xảy ra **sai sót**. **Workflow này giải quyết tất cả!**

Dùng **n8n**, các sếp có thể **tự động hóa toàn bộ quy trình** chỉ với **2 bước kết nối** (Google Sheets và Google Drive), mà **không cần viết một dòng code nào!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian** – Không cần copy-paste dữ liệu giữa nhiều bảng Excel.
✅ **Chính xác 100%** – Hợp nhất dữ liệu tự động, tránh sai sót do con người gây ra.
✅ **Hoạt động liên tục** – Workflow chạy tự động mỗi khi kích hoạt, không phụ thuộc vào giờ làm việc.
✅ **Dữ liệu đồng bộ** – File Excel và Google Sheets luôn cập nhật cùng một lúc.
✅ **Chia sẻ dễ dàng** – File được lưu trực tiếp lên Google Drive, team có thể truy cập ngay.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google** (để kết nối với Google Sheets và Google Drive).
2. **API Key hoặc OAuth2** cho:
   - **Google Sheets** (để ghi dữ liệu).
   - **Google Drive** (để lưu file Excel).
3. **Dữ liệu mẫu** (nếu muốn test workflow, các sếp có thể sử dụng **2 dataset giả mạo** trong Code nodes).

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow này:
#### **Cách 1: Import từ file JSON**
1. Tải file workflow từ [đây](https://n8n.io/workflows/7955) (hoặc copy JSON từ link trên).
2. Mở **n8n Editor** → Nhấn **"Import"** → Dán JSON và nhấn **"Import"**.
3. Workflow sẽ xuất hiện trên canvas.

#### **Cách 2: Copy/Paste JSON**
1. Mở **n8n Editor** → Nhấn **"Create new workflow"**.
2. Nhấn **"Import"** → Chọn **"Import from JSON"** → Dán JSON từ [đây](https://n8n.io/workflows/7955) → Nhấn **"Import"**.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **🔹 Bước 1: Kết nối Google Sheets (OAuth2)**
1. **Tạo credential Google Sheets**:
   - Vào **n8n → Credentials → New → Google Sheets (OAuth2)**.
   - Đăng nhập tài khoản Google và **cho phép quyền truy cập**.
   - **Lưu credential** (ví dụ: tên credential là `googleSheetsOAuth2Api`).

2. **Chỉnh node "Save to google sheets"**:
   - Mở node **"Save to google sheets"** → Chọn credential vừa tạo (`googleSheetsOAuth2Api`).
   - **Chọn Spreadsheet và Sheet** muốn ghi dữ liệu:
     - **Spreadsheet**: Tạo hoặc sử dụng **bảng mẫu** từ [đây](https://docs.google.com/spreadsheets/d/1G6FSm3VdMZt6VubM6g8j0mFw59iEw9npJE0upxj3Y6k/edit?gid=1978181834) (hoặc **copy sheet** này).
     - **Sheet**: Chọn **tab** muốn ghi dữ liệu (ví dụ: `Dataset_Merged`).

#### **🔹 Bước 2: Kết nối Google Drive (OAuth2)**
1. **Tạo credential Google Drive**:
   - Vào **n8n → Credentials → New → Google Drive (OAuth2)**.
   - Đăng nhập tài khoản Google (cùng tài khoản với Sheets) và **cho phép quyền truy cập**.
   - **Lưu credential** (ví dụ: tên credential là `googleDriveOAuth2Api`).

2. **Chỉnh node "Export Excel file"**:
   - Mở node **"Export Excel file"** → Chọn credential (`googleDriveOAuth2Api`).
   - **Chọn folder** trong Google Drive muốn lưu file Excel:
     - Ví dụ: Tạo một folder mới tên **"Automated Reports"** và chọn nó.

#### **🔹 Bước 3: Cập nhật dữ liệu trong Code nodes**
Workflow có **2 Code node** (`Data Set 1` và `Data Set 2`) để tạo dữ liệu mẫu. Các sếp có thể:
- **Sử dụng dữ liệu mẫu hiện có** (không cần chỉnh).
- **Chỉnh sửa dữ liệu** để phù hợp với nhu cầu:
  ```javascript
  // Ví dụ cho Data Set 1 (chỉnh theo nhu cầu)
  return [
    { "Name": "Product A", "Revenue": 1000, "Quarter": "Q1" },
    { "Name": "Product B", "Revenue": 1500, "Quarter": "Q1" }
  ];
  ```

#### **🔹 Bước 4: Kích hoạt Workflow**
1. **Test Run** (để kiểm tra):
   - Nhấn **"Execute workflow"** (node `manualTrigger`).
   - Kiểm tra:
     - Dữ liệu có được ghi vào **Google Sheets** không?
     - File Excel có được tạo và lưu vào **Google Drive** không?
2. **Bật Active**:
   - Sau khi test thành công, **bật Active** để workflow chạy tự động khi kích hoạt.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Gửi file Excel qua Email tự động**:
   - Thêm node **Email** (ví dụ: Gmail) sau node `Export Excel file` để gửi file cho team.
   - Ví dụ: `n8n-nodes-base.email` với template:
     ```plaintext
     Xin chào team,
     File báo cáo đã được tự động tạo và gửi kèm.
     Tải file tại: [LINK_GOOGLE_DRIVE]
     Trân trọng,
     Team
     ```

2. **Lưu log hoạt động**:
   - Thêm node **Slack/Telegram** để thông báo khi workflow hoàn thành thành công/thất bại.
   - Ví dụ: `n8n-nodes-base.slack` với message:
     ```plaintext
     🚀 Workflow hoàn thành! File Excel đã được tạo và lưu tại: [LINK_GOOGLE_DRIVE]
     ```

3. **Tự động chạy hàng tuần**:
   - Sử dụng **n8n Cron Trigger** để chạy workflow vào **một ngày cụ thể hàng tuần** (ví dụ: thứ 2 hàng tuần).
   - Cài đặt trong node `manualTrigger` → Chọn **"Cron"** và nhập biểu thức:
     ```plaintext
     0 0 * * 1  # Chạy vào thứ 2 hàng tuần lúc 00:00
     ```

4. **Tách dữ liệu theo điều kiện**:
   - Sử dụng **Code node** để lọc dữ liệu trước khi hợp nhất (ví dụ: chỉ lấy dữ liệu của một **campaign** cụ thể).
   - Ví dụ:
     ```javascript
     const filteredData = data.filter(item => item.Campaign === "Spring_Sale");
     return filteredData;
     ```

5. **Tạo báo cáo định kỳ**:
   - Kết hợp với **Google Calendar** để gửi báo cáo tự động vào ngày hẹn.
   - Sử dụng node `n8n-nodes-base.googleCalendar` để tạo sự kiện và gắn file Excel vào nó.
:::

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc **copy-paste dữ liệu thủ công**, đồng thời **giảm thiểu sai sót** và **tăng cường hiệu suất** trong việc báo cáo. **Chỉ với 2 bước kết nối**, các sếp đã có một **hệ thống tự động hóa hoàn chỉnh** để hợp nhất dữ liệu, lưu file và chia sẻ với team.

**Hãy thử ngay!** Nếu có nhu cầu **tùy chỉnh thêm** (ví dụ: thêm Slack notification, gửi email tự động, hoặc lọc dữ liệu theo điều kiện), các sếp có thể liên hệ với tác giả **Robert Breen** qua:
- 📧 **rbreen@ynteractive.com**
- 🔗 [LinkedIn](https://www.linkedin.com/in/robert-breen-29429625/)
- 🌐 [Website](https://ynteractive.com)

**🚀 Cùng tự động hóa công việc của mình ngay hôm nay!**