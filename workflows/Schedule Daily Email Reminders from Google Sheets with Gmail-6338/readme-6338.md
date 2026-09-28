---
title: "📧 Tự Động Gửi Nhắc Nhở Email Hàng Ngày Từ Google Sheets (Không Cần Code)"
description: "Workflow tự động hóa gửi email nhắc nhở hàng ngày từ Google Sheets sang Gmail, tiết kiệm thời gian và giảm thiểu lỗi nhớ. Hoạt động 24/7 mà không cần can thiệp thủ công."
slug: "tu-dong-gui-email-nhac-nhom-hang-ngay-tu-google-sheets"
tags: [n8n, automation, google-sheets, gmail, project-management, no-code]
keywords: [n8n workflow gửi email tự động, tự động hóa nhắc nhở hàng ngày, google sheets gmail automation, tự động hóa project management]
---

# 🚀 **Tự Động Gửi Email Nhắc Nhở Hàng Ngày Từ Google Sheets (Không Cần Code)**

### **Giải pháp cho các sếp bị "quên" nhắc nhở khách hàng, đồng nghiệp hay công việc quan trọng**
Có bao giờ các sếp phải mất thời gian thủ công gửi email nhắc nhở hàng ngày cho khách hàng, đồng nghiệp hay các công việc quan trọng? Hay phải lo lắng rằng sẽ quên gửi nhắc nhở cho một khách hàng quan trọng? **Workflow này sẽ tự động hóa toàn bộ quá trình** – chỉ cần cập nhật dữ liệu trên Google Sheets, email sẽ được gửi tự động vào thời gian đã định, **không cần can thiệp thủ công nào!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính bảo mật và không phụ thuộc vào phiên bản miễn phí.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải nhớ hoặc gửi email nhắc nhở thủ công hàng ngày.
- **Chính xác 100%**: Email được gửi tự động vào thời gian đã định, không bị quên hoặc trễ.
- **Dễ dàng cập nhật**: Chỉ cần chỉnh sửa Google Sheets, workflow sẽ tự động phản ánh thay đổi.
- **Hoạt động liên tục**: Thực hiện 24/7 mà không cần can thiệp của con người.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google** (để sử dụng Google Sheets và Gmail).
2. **API Key OAuth2** cho:
   - **Google Sheets** (để đọc dữ liệu từ sheet).
   - **Gmail** (để gửi email tự động).
3. **Google Sheet** đã được cấu trúc với các cột như:
   - `Email` (địa chỉ email nhận nhắc nhở).
   - `Message` (nội dung email).
   - `Date` (ngày gửi, có thể là ngày hôm nay hoặc ngày tương lai).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n.io](https://n8n.io/) và đăng nhập vào tài khoản.
2. Nhấn **Create Workflow** → **Import Workflow**.
3. Chọn file JSON hoặc paste JSON từ [link gốc](https://n8n.io/workflows/6338).

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này bao gồm **4 node chính**, các sếp cần cấu hình kỹ lưỡng như sau:

##### **Node 1: Manual Trigger (Bắt đầu workflow)**
- **Tên node**: "When clicking ‘Execute workflow’"
- **Lưu ý**: Node này được sử dụng để **khởi động workflow thủ công** (hoặc có thể thay thế bằng **Schedule Trigger** để chạy tự động hàng ngày).
  - **Lưu ý nâng cao**: Để workflow chạy **tự động hàng ngày**, các sếp nên thay thế node này bằng **n8n-nodes-base.schedule** và cấu hình thời gian chạy (ví dụ: 8h sáng hàng ngày).

##### **Node 2: Get row(s) in sheet (Lấy dữ liệu từ Google Sheets)**
- **Tên node**: "Get row(s) in sheet"
- **Credentials**: Chọn `googleSheetsOAuth2Api` (đã cấu hình trước khi import).
- **Cấu hình**:
  - **Spreadsheet ID**: ID của Google Sheet (có thể lấy từ URL của sheet: `https://docs.google.com/spreadsheets/d/[SPREADSHEET_ID]/edit`).
  - **Sheet Name**: Tên của sheet (ví dụ: "Nhắc nhở").
  - **Range**: Chọn phạm vi dữ liệu (ví dụ: `Sheet1!A:D`).
  - **Filter**: Có thể thêm điều kiện lọc (ví dụ: `Date = "Today"`).

##### **Node 3: If (Kiểm tra điều kiện)**
- **Tên node**: "If"
- **Lưu ý**: Node này **kiểm tra xem có dữ liệu mới cần gửi không**.
  - **Condition**: Các sếp nên cấu hình để chỉ chạy khi có dữ liệu mới (ví dụ: `{{ $json["Email"] }} != ""`).

##### **Node 4: Send a message (Gửi email qua Gmail)**
- **Tên node**: "Send a message"
- **Credentials**: Chọn `gmailOAuth2` (đã cấu hình trước khi import).
- **Cấu hình**:
  - **To**: `{{ $json["Email"] }}` (địa chỉ email từ Google Sheets).
  - **Subject**: `{{ $json["Subject"] }}` (tiêu đề email, có thể tự định nghĩa trong sheet).
  - **Text**: `{{ $json["Message"] }}` (nội dung email từ sheet).
  - **HTML**: (Nếu muốn gửi email HTML, có thể định nghĩa trong sheet).

---

#### **3. Kích hoạt ⚡️**
1. **Test run dữ liệu mẫu**:
   - Nhấn **Execute Workflow** để kiểm tra nếu email được gửi thành công.
   - Kiểm tra hộp thư đến của địa chỉ email trong sheet.
2. **Bật Active workflow**:
   - Sau khi test thành công, chuyển workflow sang **Active** để hoạt động liên tục.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Thay thế Manual Trigger bằng Schedule Trigger**:
   - Thêm node **n8n-nodes-base.schedule** để workflow chạy **tự động hàng ngày** (không cần nhấn nút thủ công).
   - Cấu hình thời gian chạy (ví dụ: 9h sáng hàng ngày).

2. **Lưu log hoạt động**:
   - Thêm node **n8n-nodes-base.httpRequest** để ghi log vào một Google Sheet hoặc Slack/Telegram khi email được gửi thành công/thất bại.

3. **Gửi email theo khu vực giờ (Time Zone)**:
   - Nếu các sếp muốn gửi email vào thời gian cụ thể theo múi giờ của khách hàng, có thể sử dụng node **n8n-nodes-base.dateTime** để tính toán thời gian chính xác.

4. **Kết hợp với Slack/Telegram**:
   - Thêm node **n8n-nodes-base.slack** hoặc **n8n-nodes-base.telegram** để thông báo khi email được gửi thành công.

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc nhớ gửi email nhắc nhở thủ công, đồng thời **tăng tính chuyên nghiệp** với việc tự động hóa nhắc nhở hàng ngày. **Hãy áp dụng ngay** và không bao giờ quên nhắc nhở khách hàng hoặc đồng nghiệp nữa!

👉 **Bắt đầu tự động hóa ngay hôm nay!** [Tải workflow từ đây](https://n8n.io/workflows/6338) và cài đặt trên VPS để hoạt động 24/7.