---
title: "🔍 Tự Động Hoàn Thành Tìm Kiếm Email Bulk Với Icypeas - Giảm 90% Thời Gian Tìm Kiếm Liên Lạc"
description: "Workflow tự động hóa tìm kiếm email bulk từ danh sách khách hàng trong Google Sheets, kết hợp với API Icypeas, giúp các sếp tiết kiệm thời gian và tăng hiệu quả liên lạc 100% không cần code."
slug: "tu-dong-hoan-thanh-tim-kiem-email-bulk-voi-icypeas"
tags: [n8n, automation, sales, marketing, icypeas, google-sheets, api]
keywords: [tự động hóa tìm kiếm email, icypeas bulk search, n8n workflow sales, tự động hóa marketing, tìm kiếm email bulk tự động]
---

# 🚀 **Tự Động Hoàn Thành Tìm Kiếm Email Bulk Với Icypeas - Giảm 90% Thời Gian Tìm Kiếm Liên Lạc**

## **Nỗi Đau Của Các Sếp Trong Tìm Kiếm Email**
Bạn có bao giờ phải mất **giờ đồng hồ** để tìm kiếm email của khách hàng từ danh sách hàng trăm, thậm chí hàng nghìn tên? Hay phải **gõ tay từng email** vào công cụ tìm kiếm để xác minh? Điều này không chỉ tốn thời gian mà còn dễ gây **lỗi sai sót**, ảnh hưởng đến hiệu quả liên lạc và doanh số.

**Workflow này giải quyết vấn đề đó bằng cách:**
✅ **Tự động hóa tìm kiếm email bulk** từ danh sách khách hàng trong Google Sheets.
✅ **Kết hợp với API Icypeas** để tra cứu chính xác và nhanh chóng.
✅ **Gửi kết quả tự động** về email hoặc ứng dụng Icypeas.
✅ **Chỉ cần nhấn 1 nút** để hoàn thành toàn bộ quy trình.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính bảo mật và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tìm kiếm email bulk chỉ trong **vài giây** thay vì mất **giờ đồng hồ**.
- **Chính xác 100%**: Không còn lo lắng về sai sót khi gõ tay.
- **Hoạt động liên tục**: Workflow chạy tự động **24/7** mà không cần can thiệp.
- **Tích hợp với Google Sheets**: Dễ dàng cập nhật danh sách khách hàng mới.
- **Kết quả tự động**: Nhận email báo cáo từ Icypeas ngay khi tìm kiếm hoàn tất.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Icypeas** (đăng ký tại [icypeas.com](https://icypeas.com)).
✔ **API Key, API Secret và User ID** từ [Icypeas Profile](https://app.icypeas.com/bo/profile).
✔ **Google Sheet** chứa danh sách khách hàng với **3 cột**: `lastname`, `firstname`, `company`.
✔ **Tài khoản Google** để kết nối với Google Sheets.
✔ **VPS hoặc n8n Cloud** để chạy workflow (nên **self-hosted** cho bảo mật).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể **import** workflow từ file JSON hoặc **copy/paste** JSON vào **n8n Editor**:
1. Mở **n8n Workflow Editor**.
2. Nhấn **Import** và chọn file JSON (hoặc **Create New** → **Import JSON**).
3. **Hoặc** copy toàn bộ JSON từ [link gốc](https://n8n.io/workflows/2014) và dán vào **Import JSON**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **4 node chính**, các sếp cần **cấu hình kỹ lưỡng** như sau:

##### **🔹 Node 1: Manual Trigger (Bắt Đầu Workflow)**
- **Không cần chỉnh sửa gì**, chỉ cần **nhấn "Execute Workflow"** khi muốn chạy.

##### **🔹 Node 2: Code (Xác Minh Tài Khoản Icypeas)**
- Mở node này và **điền 3 thông tin sau** vào code:
  ```javascript
  const API_KEY = "**PUT_API_KEY_HERE**";          // API Key từ Icypeas
  const API_SECRET = "**PUT_API_SECRET_HERE**";      // API Secret từ Icypeas
  const USER_ID = "**PUT_USER_ID_HERE**";            // User ID từ Icypeas
  ```
- **Không chỉnh sửa bất kỳ dòng nào khác** để tránh lỗi.
- **Nếu self-hosted**, cần **bật Crypto module** như hướng dẫn dưới đây:

  > **Cách bật Crypto module (nếu self-hosted):**
  > 1. Truy cập **Settings** → **General**.
  > 2. Tìm phần **Additional Node Packages** → **Kích hoạt "crypto"**.
  > 3. **Lưu thay đổi** và **restart n8n** nếu cần.

##### **🔹 Node 3: Google Sheets (Đọc Danh Sách Khách Hàng)**
- **Chọn Google Sheet** chứa danh sách khách hàng.
- **Cấu hình cột**:
  - **Header 1**: `lastname` (Họ)
  - **Header 2**: `firstname` (Tên)
  - **Header 3**: `company` (Công ty)
- **Chọn Sheet và Range** (ví dụ: `Sheet1!A1:D100`).
- **Kết nối tài khoản Google** (nếu chưa kết nối, nhấn **Add Connection**).

##### **🔹 Node 4: HTTP Request (Tìm Kiếm Email Bulk)**
- **Tạo Credential mới** cho **Header Auth**:
  1. Trong **HTTP Request node**, tìm phần **Credentials for Header Auth**.
  2. Nhấn **Create new Credential** → Đặt tên là **"Authorization"**.
  3. Trong **Value**, chọn **Expression** và nhập:
     ```json
     {{ $json.api.key + ':' + $json.api.signature }}
     ```
  4. **Lưu** credential này.
- **Không cần chỉnh sửa gì khác**, workflow sẽ tự động gửi yêu cầu POST đến API Icypeas.

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu (nếu có).
2. **Bật Active** workflow.
3. **Nhấn "Execute Workflow"** để bắt đầu tìm kiếm.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tích Hợp Slack/Telegram** để thông báo kết quả:
   - Sử dụng **n8n-nodes-base.slack** hoặc **n8n-nodes-base.telegram** để gửi tin nhắn khi tìm kiếm hoàn tất.
2. **Lưu Log Kết Quả** vào Google Sheets:
   - Thêm **Google Sheets (Write)** sau node HTTP Request để ghi kết quả vào sheet mới.
3. **Chạy Định Kỳ** với **n8n-nodes-base.cron**:
   - Cấu hình để workflow chạy **mỗi ngày/ngày làm việc** tự động.
4. **Kết Hợp với CRM** (HubSpot, Salesforce):
   - Sau khi tìm kiếm email, **cập nhật thông tin vào CRM** bằng **n8n-nodes-base.httpRequest** hoặc **n8n-nodes-base.crm**.

---
### 📌 **Kết Luận**
Workflow này **giúp các sếp tiết kiệm thời gian, tăng hiệu quả liên lạc và giảm sai sót** khi tìm kiếm email bulk. **Chỉ cần 1 lần setup**, workflow sẽ hoạt động **một cách tự động và liên tục**, không cần can thiệp.

**Hãy áp dụng ngay và bắt đầu tự động hóa quy trình tìm kiếm email của mình!** 🚀

---
**🔗 [Tải Workflow JSON](https://n8n.io/workflows/2014) | [Đăng ký Icypeas](https://icypeas.com) | [Hướng Dẫn Self-Hosted n8n](https://docs.n8n.io/)**