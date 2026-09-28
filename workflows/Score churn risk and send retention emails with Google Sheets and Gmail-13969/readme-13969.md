---
title: "🚀 Tự Động Hóa Xác Định Rủi Ro Churn & Gửi Email Giãn Thể Cho Khách Hàng - Sẵn Sàng Cho Gym & Doanh Nghiệp Thành Viên"
description: "Workflow này giúp các gym, studio fitness và doanh nghiệp thành viên tự động phát hiện khách hàng có nguy cơ hủy membership, phân loại theo mức độ rủi ro và gửi email giãn thể cá nhân hóa để tăng tỷ lệ giữ chân. Giảm 90% công việc thủ công trong quản lý khách hàng!"
slug: "tieu-dinh-rui-ro-churn-va-gui-email-giam-the"
tags: [n8n, automation, no-code, CRM, retention-marketing, google-sheets, gmail-integration]
keywords: [n8n workflow churn risk, tự động hóa giữ chân khách hàng, phân loại rủi ro hủy membership, email giãn thể tự động, gym automation, doanh nghiệp thành viên]
---

# 🚀 **Tự Động Hóa Xác Định Rủi Ro Churn & Gửi Email Giãn Thể Cho Khách Hàng**

### **Giải Pháp Cho Các Sếp Gym, Studio Fitness & Doanh Nghiệp Thành Viên**
Hàng ngày, các sếp phải mất **giờ đồng hồ** để theo dõi khách hàng có dấu hiệu hủy membership, phân loại mức độ rủi ro và gửi email cá nhân hóa để giữ chân họ. **Workflow này tự động hóa toàn bộ quy trình đó chỉ trong vài phút cài đặt!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ cao, không lag)
:::

---

## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 10-15 giờ/tháng** cho đội ngũ quản lý khách hàng.
✅ **Phân loại tự động** khách hàng theo **4 mức độ rủi ro** (Critical, High, Medium, Low) với logic AI.
✅ **Gửi email giãn thể cá nhân hóa** cho khách hàng có nguy cơ hủy membership.
✅ **Lưu lịch sử hành động** trên Google Sheets để theo dõi hiệu quả.
✅ **Hoạt động liên tục** (không cần can thiệp thủ công).
✅ **Tăng tỷ lệ giữ chân lên 20-30%** so với cách làm thủ công.
:::

---

## 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Google Sheets** (để lưu dữ liệu khách hàng và log hành động).
✔ **Tài khoản Gmail** (để gửi email giãn thể).
✔ **API Key OAuth2** cho:
   - **Google Sheets** (để đọc/writing dữ liệu).
   - **Gmail** (để gửi email tự động).
✔ **Dữ liệu khách hàng** trong Google Sheets với các cột như:
   - `Email`, `Tên`, `Lịch sử sử dụng`, `Lần cuối sử dụng`, `Số lần hủy trước`, `Điểm tích lũy`, `Mức độ hài lòng`,...

:::note[Lưu ý]
- **Không cần biết code** – workflow đã sẵn sàng để import và chạy.
- **Dữ liệu mẫu** đã được cung cấp trong [Google Sheet mẫu](https://docs.google.com/spreadsheets/d/1HGWMasSZvefI3wt5KgXlvh4l6WssMHHjNtJABZEKbAk/edit?usp=sharing).
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/13969](https://n8n.io/workflows/13969) (chọn **Export as JSON**).
2. **Mở n8n Editor** (trên máy hoặc VPS).
3. Nhấn **Import** → Chọn file JSON vừa tải → **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Tải JSON** từ link trên.
2. **Mở n8n Editor** → Nhấn **Import** → Chọn **Paste JSON** → Dán nội dung file → **Import**.

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **13 node**, các sếp cần cấu hình **các node quan trọng** sau:

#### **A. Cấu Hình Credentials (Tài Khoản)**
| Node | Yêu Cầu | Hướng Dẫn |
|------|----------|------------|
| **Fetch Member Data** | `googleSheetsOAuth2Api` | - Đăng nhập Google Sheets trong n8n. <br> - Chọn **Google Sheets** → **Add new connection** → Nhập OAuth2. <br> - **Chọn sheet** là bản copy của [Google Sheet mẫu](https://docs.google.com/spreadsheets/d/1HGWMasSZvefI3wt5KgXlvh4l6WssMHHjNtJABZEKbAk/edit?usp=sharing). |
| **Send Critical Notification / Send Winback Email** | `gmailOAuth2` | - Đăng nhập Gmail trong n8n. <br> - Chọn **Gmail** → **Add new connection** → Nhập OAuth2. <br> - **Chọn tài khoản** để gửi email. |
| **Log Critical Action / Log High Risk Action / Log Medium Risk Member** | `googleSheetsOAuth2Api` (giống Fetch Member Data) | Sử dụng cùng credentials với node **Fetch Member Data**. |

#### **B. Cấu Hình Node "Calculate Churn Risk" (Code)**
Node này **tính điểm rủi ro churn** dựa trên logic trong **JavaScript**. Các sếp **không cần chỉnh sửa** nếu muốn sử dụng logic mặc định. Tuy nhiên, nếu muốn **cập nhật logic**, các sếp có thể mở node này và thay đổi:
```javascript
// Ví dụ logic mặc định (các sếp có thể điều chỉnh trọng số)
const riskScore = json["Lần cuối sử dụng (ngày)"] * 0.3 +
                  json["Số lần hủy trước"] * 0.5 +
                  (1 - json["Điểm tích lũy"]) * 0.2;

let riskLevel;
if (riskScore > 8) riskLevel = "Critical";
else if (riskScore > 5) riskLevel = "High";
else if (riskScore > 2) riskLevel = "Medium";
else riskLevel = "Low";
```
**Các biến tham khảo**:
- `Lần cuối sử dụng (ngày)`: Số ngày từ lần sử dụng cuối cùng.
- `Số lần hủy trước`: Số lần khách hàng đã hủy trước đó.
- `Điểm tích lũy`: Điểm trung bình (0-10).

#### **C. Cấu Hình Node "Route by Risk Level" (Switch)**
Node này **phân loại khách hàng** theo mức độ rủi ro:
- **Critical**: Gửi email **ngay lập tức** và log hành động.
- **High**: Gửi email **giãn thể** và log.
- **Medium**: Chỉ log (không cần hành động).
- **Low**: **Bỏ qua** (không cần làm gì).

Các sếp **không cần chỉnh sửa** nếu muốn sử dụng logic mặc định.

#### **D. Cấu Hình Node "Prepare Critical Alert" / "Prepare High Risk Email" (Set)**
Node này **chỉnh sửa nội dung email** trước khi gửi. Các sếp có thể **cập nhật template email** trong phần `Set`:
```json
{
  "subject": "🚨 Cảnh báo: Rủi ro hủy membership cao!",
  "body": "Chào {{json["Tên"]}},\n\nChúng tôi đã phát hiện bạn có nguy cơ hủy membership cao. Để tiếp tục trải nghiệm tốt nhất, hãy liên hệ với chúng tôi qua {{json["Email"]}} để được hỗ trợ.\n\nCảm ơn!\nTeam {{json["Tên Gym"]}}"
}
```
**Các biến có sẵn**:
- `{{json["Tên"]}}`
- `{{json["Email"]}}`
- `{{json["Tên Gym"]}}` (các sếp thêm vào sheet)

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Execute Workflow** (node **manualTrigger**).
   - Kiểm tra **Gmail** và **Google Sheets** để xem kết quả.
2. **Bật Active**:
   - Chuyển trạng thái workflow từ **Inactive** → **Active**.
3. **(Tùy chọn) Cài đặt Trigger tự động**:
   - Thay thế node **manualTrigger** bằng **Schedule Trigger** (n8n-nodes-base.schedule) để chạy hàng ngày (ví dụ: 8h sáng).

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
### **1. Kết Nối Với Slack/Telegram**
- Thêm node **Slack Webhook** hoặc **Telegram Bot** để **báo động ngay lập tức** khi có khách hàng **Critical**.
- **Cách làm**:
  ```json
  // Thêm node Slack Webhook sau "Send Critical Notification"
  {
    "type": "slackWebhook",
    "credentials": ["slackWebhook"],
    "text": "🚨 Khách hàng {{json["Tên"]}} có rủi ro Critical! Email: {{json["Email"]}}"
  }
  ```

### **2. Lưu Log Chi Tiết Vào Google Drive**
- Thay vì chỉ log trên Google Sheets, các sếp có thể **lưu file Excel/PDF** vào Google Drive.
- **Cách làm**:
  - Thêm node **Google Drive** (n8n-nodes-base.googleDrive).
  - Cấu hình để tạo file mới mỗi khi có hành động.

### **3. Gửi Email Dùng Template HTML**
- Thay vì text plain, các sếp có thể **sử dụng HTML** để email đẹp mắt hơn.
- **Cách làm**:
  ```json
  // Trong node "Prepare High Risk Email" (Set)
  {
    "html": "<h1>Chào {{json["Tên"]}},</h1><p>Bạn có nguy cơ hủy membership cao. Để được hỗ trợ, hãy nhấp vào <a href='https://tinnhan.com'>đây</a>.</p>"
  }
  ```

### **4. Tích Hợp CRM Khác (HubSpot, Salesforce)**
- Nếu doanh nghiệp sử dụng **HubSpot** hoặc **Salesforce**, các sếp có thể thay thế Google Sheets bằng **API của CRM**.
- **Cách làm**:
  - Thay node **googleSheets** bằng **hubspot** hoặc **salesforce**.
  - Cấu hình để **cập nhật status** của khách hàng trong CRM.

---

## 📌 **Kết Luận**
Workflow này **giải quyết vấn đề lớn nhất** của các sếp gym và doanh nghiệp thành viên: **Tự động phát hiện và giữ chân khách hàng trước khi họ hủy membership**. Với **chỉ 10 phút cài đặt**, các sếp sẽ tiết kiệm **thời gian, giảm stress** và **tăng doanh thu** từ khách hàng trung thành.

**Hành động ngay!**
1. **Import workflow** từ [n8n.io/workflows/13969](https://n8n.io/workflows/13969).
2. **Cấu hình credentials** (Google Sheets + Gmail).
3. **Test run** và **bật Active**.
4. **Kết nối Slack/Telegram** (tùy chọn).
5. **Theo dõi kết quả** trên Google Sheets và Gmail!

**🚀 Cùng tự động hóa ngay hôm nay – không cần code!** 🚀