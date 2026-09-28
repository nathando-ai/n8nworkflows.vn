---
title: "🚀 Tự Động Hóa Quá Trình Phỏng Vấn HR: Theo Dõi, Nhắc Nhở & Báo Cáo Tự Động Với Google Calendar, Sheets & Gmail"
description: "Giải pháp tự động hóa 100% không code giúp HR theo dõi lịch phỏng vấn, gửi nhắc nhở tự động và cập nhật kết quả cho ứng viên và quản lý. Tiết kiệm thời gian lên tới 80% trong quản lý quy trình tuyển dụng!"
slug: "tieu-dong-hoa-qua-trinh-phong-van-hr"
tags: [n8n, automation, hr, google-calendar, google-sheets, gmail, no-code]
keywords: [tự động hóa phỏng vấn HR, theo dõi lịch phỏng vấn tự động, nhắc nhở ứng viên, báo cáo kết quả tuyển dụng, n8n workflow HR]
---

# 🚀 **Tự Động Hóa Quá Trình Phỏng Vấn HR: Từ Nhắc Nhở Đến Báo Cáo Kết Quả Tự Động**

### **Nỗi Đau Của Các Sếp HR**
Quản lý quá trình phỏng vấn thủ công không chỉ tốn thời gian mà còn dễ gây lỗi như:
- **Quên nhắc nhở ứng viên** trước ngày phỏng vấn.
- **Không theo dõi kịp thời** kết quả phỏng vấn và cập nhật cho quản lý.
- **Lưu trữ dữ liệu rối loạn** trên email hoặc Google Sheets, khó tra cứu.
- **Tốn nhiều giờ mỗi tuần** để gửi email, cập nhật sheet và báo cáo.

**Workflow này giải quyết tất cả!** Với **Google Calendar, Sheets & Gmail**, bạn có thể:
✅ **Theo dõi tất cả lịch phỏng vấn** trong Google Calendar.
✅ **Gửi nhắc nhở tự động** cho ứng viên 24h trước ngày phỏng vấn.
✅ **Cập nhật kết quả** (đậu/rớt) ngay sau khi nhận thông tin từ quản lý.
✅ **Báo cáo tự động** cho quản lý và ứng viên với nội dung cá nhân hóa.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động 24/7 ổn định, các sếp nên **self-host n8n** trên VPS riêng:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** quản lý phỏng vấn (không cần gửi email thủ công).
- **Tăng độ chính xác** với cập nhật tự động kết quả vào Google Sheets.
- **Cá nhân hóa thông báo** cho ứng viên và quản lý (email động).
- **Hoạt động liên tục** 24/7, không phụ thuộc vào giờ làm việc.
- **Dữ liệu tập trung** trên Google Sheets, dễ tra cứu và phân tích.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google** (đã kết nối với **Google Calendar, Google Sheets & Gmail**).
2. **API Keys & Credentials**:
   - **Google Calendar OAuth2** (để lấy lịch phỏng vấn).
   - **Google Sheets API** (để cập nhật dữ liệu).
   - **Gmail OAuth2** (để gửi email nhắc nhở và báo cáo kết quả).
3. **Google Sheet mẫu** (cấu trúc bao gồm cột: `Tên Ứng Viên`, `Ngày Phỏng Vấn`, `Kết Quả`, `Ghi Chú`).
4. **Webhook URL** (để quản lý gửi kết quả phỏng vấn vào workflow).

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Từ File JSON**
1. Tải workflow từ [n8n.io/workflows/10081](https://n8n.io/workflows/10081) (chọn **Export as JSON**).
2. Trên **n8n Editor**, nhấn **Import** → Chọn file JSON vừa tải.
3. **Hoặc** copy toàn bộ JSON từ link trên và paste vào **Import Workflow** trong n8n.

#### **Phương pháp 2: Copy/Paste JSON**
1. Mở [n8n.io/workflows/10081](https://n8n.io/workflows/10081) → Nhấn **Export as JSON**.
2. Copy toàn bộ mã JSON.
3. Trên **n8n Editor**, nhấn **Import** → Chọn **Paste JSON** và dán vào.

---
### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **2 phần chính**:
#### **Phần 1: Theo Dõi & Nhắc Nhở Phỏng Vấn (Chạy Tự Động Mỗi 5 Phút)**
| **Node** | **Cấu Hình Cần Thay Đổi** | **Hướng Dẫn** |
|----------|---------------------------|----------------|
| **Check Every 5 Minutes** | Thiết lập thời gian chạy (đã mặc định là 5 phút). | Không cần chỉnh, trừ khi muốn thay đổi thời gian. |
| **Get Calendar Events** | **Credentials**: Chọn `googleCalendarOAuth2Api` (đã tạo trước). | - Chọn **Google Calendar** cần theo dõi. <br> - **Operation**: `getAll` (lấy tất cả sự kiện). |
| **Filter Upcoming Interviews** | **Filter Rule**: Lọc sự kiện có `status: "confirmed"` và `endTime` trong 7 ngày tới. | - Thêm điều kiện: `{{ $json.end }} > {{ $now }}` (lọc sự kiện trong tương lai). <br> - **Tên sự kiện** phải chứa từ khóa như "Phỏng vấn", "Interview". |
| **Add to Google Sheet** | **Credentials**: `googleApi`. <br> **Sheet Name**: Đặt tên sheet (ví dụ: `Lịch Phỏng Vấn`). <br> **Range**: `Sheet1!A1` (đầu tiên). | - Chọn **Sheet** và **Range** phù hợp. <br> - **Headers**: Bật để tự động tạo tiêu đề cột. |
| **Send Reminder to Candidate** | **Credentials**: `gmailOAuth2`. <br> **Email Template**: Tùy chỉnh nội dung nhắc nhở. | - **Subject**: `📅 Nhắc Nhở: Phỏng Vấn Sắp Đến - {{ $json.summary }}`. <br> - **Body**: `Xin chào {{ $json.guestName }}, <br> Lịch phỏng vấn của bạn vào ngày {{ $json.start }} đã đến gần. <br> Địa điểm: {{ $json.location }}`. |

#### **Phần 2: Nhận & Xử Lý Kết Quả Phỏng Vấn (Thông Qua Webhook)**
| **Node** | **Cấu Hình Cần Thay Đổi** | **Hướng Dẫn** |
|----------|---------------------------|----------------|
| **Webhook: Submit Interview Result** | **Path**: `interview-result` (không đổi). <br> **HTTP Method**: `POST`. | - **Credentials**: Không cần (webhook công khai). <br> - **Payload Type**: `application/json`. |
| **Update Sheet with Result** | **Credentials**: `googleApi`. <br> **Range**: Chọn ô tương ứng với kết quả (ví dụ: `Sheet1!D2`). | - **Headers**: Bật để cập nhật tiêu đề. <br> - **Value**: `{{ $json.result }}` (đậu/rớt). |
| **Check if Passed** | **Condition**: Kiểm tra `{{ $json.result }} === "Passed"`. | - Nếu kết quả = "Passed", chạy nhánh **Email Candidate - Passed**. |
| **Email Candidate - Passed/Failed** | **Credentials**: `gmailOAuth2`. <br> **Template**: Tùy chỉnh nội dung. | - **Passed**: `Xin chúc mừng! Bạn đã vượt qua phỏng vấn. Chúng tôi sẽ liên hệ trong 24h.`. <br> - **Failed**: `Cảm ơn bạn đã tham gia phỏng vấn. Chúng tôi sẽ liên hệ nếu có cơ hội khác.`. |
| **Email Manager** | **Credentials**: `gmailOAuth2`. <br> **Template**: Báo cáo tổng hợp. | - **Subject**: `📊 Báo Cáo Kết Quả Phỏng Vấn - {{ $json.candidateName }}`. <br> - **Body**: `Kết quả phỏng vấn của {{ $json.candidateName }}: {{ $json.result }}. <br> Ghi chú: {{ $json.notes }}`. |

---
### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Sử dụng **Webhook Simulator** (tools như [Postman](https://www.postman.com/) hoặc [RequestBin](https://requestbin.com/)) để gửi dữ liệu mẫu:
     ```json
     {
       "candidateName": "Nguyễn Văn A",
       "result": "Passed",
       "notes": "Giỏi về kỹ năng mềm"
     }
     ```
   - Gửi POST đến URL webhook của workflow (hiển thị trên tab **Webhook: Submit Interview Result**).
2. **Bật Active**:
   - Nhấn **Active** trên tab **Workflow Settings**.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết Nối Với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** để thông báo kết quả ngay khi có.
   - Ví dụ: Khi kết quả "Passed", gửi tin nhắn Slack: `🎉 Ứng viên {{ $json.candidateName }} đã đậu phỏng vấn!`.

2. **Lưu Log & Báo Cáo Định Kỳ**:
   - Sử dụng node **Google Sheets** để lưu lịch sử tất cả kết quả.
   - Thêm node **Schedule Trigger** chạy hàng tuần để gửi báo cáo tổng hợp cho quản lý.

3. **Tự Động Gửi Email Cảm ơn**:
   - Thêm nhánh email cảm ơn cho ứng viên đã tham gia phỏng vấn (dùng node **Gmail** với điều kiện `{{ $json.result }} === "Failed"`).

4. **Cập Nhật Lịch Phỏng Vấn Tự Động**:
   - Nếu sử dụng **Google Meet**, bạn có thể tự động tạo link phỏng vấn trong Google Calendar bằng API.

---
## 📌 **Kết Luận**
Workflow **Automated Interview Tracker** là **giải pháp hoàn hảo** để các sếp HR:
✔ **Tiết kiệm thời gian** với tự động hóa nhắc nhở và báo cáo.
✔ **Tăng độ chính xác** với cập nhật kết quả tự động.
✔ **Cải thiện trải nghiệm ứng viên** với email cá nhân hóa.

**Hành động ngay!**
1. **Import workflow** theo hướng dẫn trên.
2. **Cấu hình credentials** và sheet mẫu.
3. **Bật Active** và bắt đầu tự động hóa quy trình phỏng vấn của bạn!

**🚀 Cần hỗ trợ?** Đăng ký [VPS n8n](https://tino.vn/vps-n8n?affid=388) và liên hệ **Oneclick AI Squad** qua [Facebook](https://facebook.com/oneclickaisquad) để được tư vấn chi tiết!

---