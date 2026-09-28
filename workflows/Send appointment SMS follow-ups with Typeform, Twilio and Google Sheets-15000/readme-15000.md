---
title: "📱 Tự Động Gửi Lại SMS Nhắc Lịch Hẹn với Typeform, Twilio & Google Sheets – Không Cần Code!"
description: "Workflow tự động hóa gửi SMS nhắc nhở lịch hẹn tự động qua Twilio, thu thập phản hồi trên Typeform và cập nhật dữ liệu vào Google Sheets – tiết kiệm thời gian, tăng tỷ lệ hoàn thành hẹn và cải thiện trải nghiệm khách hàng."
slug: "tu-dong-hoa-gui-sms-nhac-lich-hen-typeform-twilio-google-sheets"
tags: [n8n, automation, lead-nurturing, twilio, google-sheets, typeform, sms-marketing]
keywords: [n8n workflow tự động hóa, gửi SMS nhắc nhở lịch hẹn, Typeform tự động, Twilio API, Google Sheets tự động, lead nurturing, tự động hóa không code]
---

# 🚀 **Tự Động Gửi SMS Nhắc Lịch Hẹn với Typeform, Twilio & Google Sheets**

### **Giải pháp hoàn hảo cho các sếp quản lý lịch hẹn, tư vấn viên, hoặc doanh nghiệp cần nhắc nhở khách hàng**
Bạn có bao giờ phải mất thời gian gọi điện hoặc gửi SMS nhắc nhở khách hàng về lịch hẹn đã đặt? Hay phải theo dõi hàng loạt phản hồi từ khách hàng qua email hoặc Typeform? **Workflow này sẽ tự động hóa toàn bộ quy trình đó chỉ với một cú nhấp chuột!**

Với **n8n**, bạn có thể:
✅ **Gửi SMS nhắc nhở tự động** qua Twilio trước và sau lịch hẹn.
✅ **Thu thập phản hồi khách hàng** trên Typeform và tự động cập nhật vào Google Sheets.
✅ **Tự động hóa theo lịch** (ví dụ: gửi SMS 24h trước và 1h trước lịch hẹn).
✅ **Tiết kiệm thời gian** cho đội ngũ, giảm thiểu lỡ hẹn và cải thiện trải nghiệm khách hàng.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[**Lợi ích thực tế**]
- **Tiết kiệm thời gian**: Không cần gọi điện hoặc gửi SMS thủ công.
- **Tăng tỷ lệ hoàn thành hẹn**: Nhắc nhở tự động giảm tỷ lệ khách hàng quên lịch.
- **Dữ liệu thống kê tự động**: Tất cả phản hồi và lịch hẹn được lưu vào Google Sheets, dễ dàng phân tích.
- **Cá nhân hóa**: Gửi tin nhắn với thông tin cụ thể (tên khách hàng, thời gian hẹn).
- **Hoạt động 24/7**: Workflow chạy tự động theo lịch, không cần can thiệp.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[**CHUẨN BỊ**]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Twilio**:
   - **Account SID** và **Auth Token** (mã API của Twilio).
   - **Số điện thoại Twilio** (đã mua và kích hoạt).
   - **Số điện thoại khách hàng** (định dạng quốc tế, ví dụ: `+841234567890`).

2. **Tài khoản Typeform**:
   - **API Key** của Typeform (tìm trong **Settings > API**).
   - **ID Form** của form nhắc nhở (để thu thập phản hồi).

3. **Tài khoản Google Sheets**:
   - **File Google Sheets** đã tạo sẵn (cấu trúc cột: `Tên Khách Hàng`, `Số Điện Thoại`, `Lịch Hẹn`, `Phản Hồi`, `Trạng Thái`).
   - **Credentials OAuth 2.0** (đăng ký trong [Google Cloud Console](https://console.cloud.google.com/)).

4. **N8n Self-hosted** (không dùng phiên bản miễn phí):
   - Để workflow chạy 24/7 ổn định, các sếp nên cài n8n trên **VPS riêng**.
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%).
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/15000](https://n8n.io/workflows/15000) (chọn **Export as JSON**).
2. Trên **n8n Editor**, nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **Create new workflow** và nhấn **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. Tải JSON từ [n8n.io/workflows/15000](https://n8n.io/workflows/15000) (chọn **Export as JSON**).
2. Trên **n8n Editor**, nhấn **Import** → Chọn **Paste JSON** và dán nội dung.
3. Chọn **Create new workflow** và nhấn **Import**.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này sử dụng **Schedule Trigger** (nhắc nhở theo lịch) và **Twilio Trigger** (gửi SMS). Dưới đây là các node quan trọng cần cấu hình:

#### **🔹 Node 1: Schedule Trigger (n8n-nodes-base.scheduleTrigger)**
- **Cấu hình**:
  - **Time**: Chọn thời gian gửi SMS (ví dụ: `24 hours before` và `1 hour before` lịch hẹn).
  - **Time Zone**: Chọn múi giờ phù hợp (ví dụ: `Asia/Ho_Chi_Minh`).
  - **Repeat**: Chọn `Every day` (nếu muốn gửi hàng ngày) hoặc `Manual` (nếu muốn kích hoạt thủ công).

#### **🔹 Node 2: Google Sheets (n8n-nodes-base.googleSheets)**
- **Cấu hình**:
  - **Credentials**: Chọn **OAuth 2.0** và đăng nhập Google.
  - **File**: Chọn file Google Sheets đã tạo.
  - **Sheet Name**: Chọn sheet chứa dữ liệu lịch hẹn.
  - **Operation**: Chọn **Get rows** (lấy dữ liệu lịch hẹn) hoặc **Create row** (cập nhật phản hồi).

#### **🔹 Node 3: Twilio (n8n-nodes-base.twilio)**
- **Cấu hình**:
  - **Credentials**: Nhập **Account SID** và **Auth Token** từ Twilio.
  - **From**: Số điện thoại Twilio (ví dụ: `+1234567890`).
  - **To**: Điền vào `{{$json["phone_number"]}}` (định dạng quốc tế, ví dụ: `+841234567890`).
  - **Body**: Nội dung SMS (ví dụ: `Xin chào {{$json["name"]}}, nhắc nhở lịch hẹn vào {{$json["appointment_time"]}}`).
  - **Template**: Nếu dùng Twilio Studio, điền **Template SID**.

#### **🔹 Node 4: Typeform (n8n-nodes-base.typeformTrigger)**
- **Cấu hình**:
  - **Credentials**: Nhập **API Key** từ Typeform.
  - **Form ID**: Điền **ID Form** của form nhắc nhở.
  - **Operation**: Chọn **Create response** (gửi phản hồi từ khách hàng).

#### **🔹 Node 5: Split Out (n8n-nodes-base.splitOut)**
- **Cấu hình**:
  - Chọn **Path**: `$.data` (để tách dữ liệu lịch hẹn).
  - **Operation**: Chọn **Split** để xử lý từng khách hàng riêng biệt.

#### **🔹 Node 6: Sticky Note (n8n-nodes-base.stickyNote)**
- **Cấu hình**:
  - Dùng để ghi chú hoặc debug (không bắt buộc).

---
### **3. Kích hoạt ⚡️**
1. **Test Run** (kiểm tra trước khi chạy thực tế):
   - Nhấn **Run Workflow** và chọn **Test Execution**.
   - Điền dữ liệu mẫu (ví dụ: tên, số điện thoại, thời gian hẹn).
   - Kiểm tra SMS đã gửi thành công và dữ liệu đã cập nhật vào Google Sheets.

2. **Bật Active Workflow**:
   - Sau khi test thành công, nhấn **Active** để workflow chạy tự động.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::info[**Cải thiện hiệu suất**]
1. **Kết hợp với Slack/Telegram**:
   - Sử dụng node **Slack** hoặc **Telegram Bot** để thông báo khi khách hàng trả lời form.

2. **Lưu log hoạt động**:
   - Thêm node **Set** (n8n-nodes-base.set) để lưu trạng thái (ví dụ: `Đã gửi SMS`, `Khách hàng trả lời`).

3. **Gửi báo cáo định kỳ**:
   - Sử dụng **Schedule Trigger** để gửi báo cáo tổng hợp vào cuối tuần qua email (node **Email**).

4. **Tự động phân loại phản hồi**:
   - Sử dụng **LLM Node** (n8n-nodes-base.llm) để phân tích phản hồi khách hàng và tự động cập nhật trạng thái.

5. **Tích hợp với CRM**:
   - Nếu dùng **HubSpot** hoặc **Salesforce**, kết nối với node **HubSpot** hoặc **Salesforce** để cập nhật dữ liệu.
:::

---
## 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc nhắc nhở khách hàng thủ công, đồng thời **tăng tỷ lệ hoàn thành hẹn** và **cải thiện trải nghiệm khách hàng**. **Hãy áp dụng ngay và tự động hóa quy trình của mình!**

👉 **Bắt đầu với n8n Self-hosted** để workflow chạy 24/7 ổn định:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N**).
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).

**Chúc các sếp thành công!** 🚀