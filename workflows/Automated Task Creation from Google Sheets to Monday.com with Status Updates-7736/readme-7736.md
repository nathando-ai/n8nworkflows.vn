---
title: "🚀 Tự Động Hóa Tạo Nhiệm Vụ Từ Google Sheets Sang Monday.com Với Cập Nhật Trạng Thái (N8N)"
description: "Workflow này tự động chuyển đổi các nhiệm vụ từ Google Sheets sang Monday.com khi có cột 'Added = No', đồng thời cập nhật trạng thái thành 'Added = Yes' để tránh trùng lặp. Giúp các sếp tiết kiệm thời gian quản lý dự án và đảm bảo dữ liệu đồng bộ 100%."
slug: "tu-dong-hoa-tao-nhiem-vu-tu-google-sheets-sang-monday-com"
tags: [n8n, automation, project-management, monday-com, google-sheets, no-code]
keywords: [tự động hóa n8n, Monday.com API, Google Sheets tự động, quản lý dự án không code, sync dữ liệu Monday.com]
---

# 🚀 **Tự Động Hóa Tạo Nhiệm Vụ Từ Google Sheets Sang Monday.com Với Cập Nhật Trạng Thái**

### **Giải quyết vấn đề gì?**
Các sếp đang phải **nhập liệu thủ công** từ Google Sheets sang Monday.com để quản lý dự án? Hay phải **kiểm tra và cập nhật trạng thái** mỗi khi có nhiệm vụ mới? Workflow này **tự động hóa toàn bộ quy trình** chỉ với 3 node đơn giản, giúp tiết kiệm **hàng giờ/lần** và giảm thiểu lỗi nhân sự.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Không cần nhập liệu thủ công mỗi khi có nhiệm vụ mới.
✅ **Đồng bộ tự động**: Dữ liệu từ Google Sheets **liên tục** được chuyển sang Monday.com.
✅ **Tránh trùng lặp**: Cột `Added = Yes` ngăn workflow tạo nhiệm vụ trùng lặp.
✅ **Hoạt động liên tục**: Workflow chạy **24/7** trên VPS, không phụ thuộc vào máy tính cá nhân.
✅ **Cập nhật trạng thái tự động**: Khi nhiệm vụ được tạo trên Monday.com, trạng thái trên Google Sheets **tự động được cập nhật**.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Google Drive** (để sử dụng Google Sheets).
✔ **Tài khoản Monday.com** (để tạo nhiệm vụ).
✔ **API Token của Monday.com** (xem hướng dẫn [tại đây](https://developer.monday.com/api-reference/docs/authentication)).
✔ **Google Sheet mẫu** (có cột `Added` với giá trị ban đầu là `No`).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/7736](https://n8n.io/workflows/7736) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** → Nhấn **Import Workflow** → Dán JSON và nhấn **Import**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **A. Cấu hình Google Sheets**
1. **Tạo Google Sheet mới** từ [template này](https://docs.google.com/spreadsheets/d/1KRiAUbZP77dC_9x5pqrvcQvaAkUsoPXkZOZvfU69ILM/edit?gid=876214427#gid=876214427).
2. **Cột bắt buộc**:
   - `Added` (giá trị ban đầu là `No`).
   - Các cột khác như `Task Name`, `Description`, `Due Date`, `Assignee`, `Status`.
3. **Cấu hình node `Get new Monday Tasks`**:
   - **Credentials**: Chọn `googleSheetsOAuth2Api` (đã tạo trước).
   - **Spreadsheet ID**: Copy từ URL Google Sheet (phần giữa `d/.../`).
   - **Worksheet Name**: Tên sheet (ví dụ: `Sheet1`).
   - **Query**: `Added = No` (để lấy chỉ những nhiệm vụ chưa được tạo).

##### **B. Cấu hình Monday.com**
1. **Tạo API Token**:
   - Mở Monday.com → **Admin → API** → **Generate New Token**.
   - Copy token và lưu an toàn.
2. **Tạo Credential trong n8n**:
   - **n8n → Credentials → New → Monday.com API** → Dán token và lưu.
3. **Cấu hình node `Create Monday Task`**:
   - **Credentials**: Chọn credential Monday.com vừa tạo.
   - **Board ID**: Copy từ URL Monday.com (phần sau `/boards/`).
   - **Group ID**: Chọn nhóm (Group) muốn tạo nhiệm vụ.
   - **Mapping fields**:
     - `Task Name` → `name`
     - `Description` → `description`
     - `Due Date` → `due_date`
     - `Assignee` → `assignee` (nếu có)
     - `Status` → `status` (nếu có)

##### **C. Cập nhật trạng thái trên Google Sheets**
- Node `Mark row as Completed` sẽ tự động **cập nhật cột `Added` thành `Yes`** khi nhiệm vụ được tạo thành công trên Monday.com.
- **Lưu ý**:
  - Chọn cùng **credentials Google Sheets** như node đầu tiên.
  - **Operation**: `appendOrUpdate` (để cập nhật giá trị `Added = Yes`).

#### **3. Kích hoạt ⚡️**
- **Test Run**: Nhấn **Run Workflow** với dữ liệu mẫu để kiểm tra.
- **Active Workflow**: Sau khi kiểm tra thành công, nhấn **Active** để workflow chạy tự động.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack Webhook** hoặc **Telegram Bot** để thông báo khi nhiệm vụ được tạo thành công.
2. **Lưu log hoạt động**:
   - Sử dụng node **Set** hoặc **Sticky Note** để ghi lại lịch sử cập nhật.
3. **Tự động tạo nhiệm vụ định kỳ**:
   - Sử dụng **n8n Trigger (Polling)** để chạy workflow mỗi ngày/lần.
4. **Tích hợp với AI (LLM)**:
   - Sử dụng node **AI** để tự động **tạo mô tả nhiệm vụ** từ tiêu đề hoặc phân loại nhiệm vụ.

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc nhập liệu thủ công, đồng thời **đảm bảo dữ liệu đồng bộ** giữa Google Sheets và Monday.com. **Chỉ cần 3 node**, nhưng hiệu quả **tương đương với một nhân viên toàn thời gian**!

👉 **Bắt đầu tự động hóa ngay hôm nay** bằng cách import workflow và cấu hình theo hướng dẫn trên. Nếu cần hỗ trợ **custom hóa thêm**, liên hệ với **Robert Breen** qua [email](mailto:robert@ynteractive.com) hoặc [LinkedIn](https://www.linkedin.com/in/robert-breen-29429625/).

---
**💡 Lời khuyên cuối cùng**: Để workflow **ổn định và an toàn**, các sếp nên **self-host n8n** trên VPS (xem gợi ý ở trên). Chúc các sếp thành công! 🚀