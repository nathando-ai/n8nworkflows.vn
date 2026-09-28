---
title: "📊 Hệ Thống Theo Dõi Đăng Ký Thực Tế với Google Sheets + Gmail (Không Cần Code)"
description: "Tự động hóa việc thu thập, theo dõi và gửi thông báo xác nhận/nhắc nhở đăng ký cho học viên/khách hàng qua form webhook, Google Sheets và email tự động. Giúp tiết kiệm 80% thời gian quản lý thủ công."
slug: "tieu-dong-ho-trac-vu-dang-ky-thuc-te-google-sheets-gmail"
tags: [n8n, automation, no-code, google-sheets, gmail, webhook, education-automation]
keywords: [tự động hóa đăng ký học viên, theo dõi form webhook, gửi email tự động, google sheets n8n, workflow n8n giáo dục]
---

# 🚀 **Tự Động Hóa Hệ Thống Theo Dõi Đăng Ký Thực Tế với Google Sheets & Gmail**

### **Giải pháp cho các sếp giáo dục, doanh nghiệp cần:**
- **Thu thập dữ liệu đăng ký** từ form web tự động.
- **Gửi email xác nhận** ngay lập tức cho học viên.
- **Theo dõi trạng thái đăng ký** trên Google Sheets.
- **Gửi nhắc nhở** tự động trước ngày khai giảng.
- **Không cần viết code** – chỉ cần cấu hình n8n.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động 24/7 mà không gián đoạn, các sếp nên **self-host n8n** trên VPS ổn định:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ cao)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Không cần nhập liệu thủ công vào Google Sheets.
✅ **Trải nghiệm học viên tốt**: Nhận email xác nhận ngay sau khi đăng ký.
✅ **Theo dõi dễ dàng**: Dữ liệu đăng ký tự động cập nhật trên Google Sheets.
✅ **Nhắc nhở tự động**: Gửi email nhắc nhở trước ngày khai giảng.
✅ **Mở rộng dễ dàng**: Thêm logic mới chỉ bằng drag-and-drop.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google** (để kết nối Google Sheets và Gmail).
2. **API Key OAuth2** cho:
   - [Google Sheets](https://developers.google.com/sheets/api/quickstart/python) (cài đặt [Google Cloud SDK](https://developers.google.com/sheets/api/quickstart/python)).
   - [Gmail](https://developers.google.com/gmail/api/quickstart/python).
3. **Google Sheet** đã tạo sẵn với các tab:
   - `Student List` (danh sách học viên).
   - `FormResponses` (dữ liệu đăng ký mới).
4. **Địa chỉ email** để gửi xác nhận/nhắc nhở (cùng tài khoản Gmail OAuth2).
5. **URL Webhook** (để form đăng ký gửi dữ liệu đến n8n).

---
:::note[LƯU Ý QUAN TRỌNG]
- **Google Sheets** phải có **cấu trúc cột phù hợp** với dữ liệu form đăng ký (ví dụ: `Name`, `Email`, `Phone`, `Course`, `Registration Date`).
- **Gmail OAuth2** cần **quyền "Send Email as a Bot"** (cài đặt trong [Google Cloud Console](https://console.cloud.google.com/)).
:::

---

## 🚀 **Cách Import & Cấu Hình Workflow**

### **1. Import Workflow từ JSON**
Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/9580](https://n8n.io/workflows/9580) và import vào n8n Editor.
- **Copy toàn bộ JSON** và paste vào **Import Workflow** trong n8n.

:::tip[Cách import nhanh]
1. Mở n8n Editor → **Menu (⋮) → Import Workflow**.
2. Dán JSON từ file hoặc link trực tiếp.
3. Chọn **Import** và bắt đầu cấu hình.
:::

---

### **2. Các bước cấu hình BẮT BUỘC**

#### **A. Cấu hình Credentials (OAuth2)**
Các sếp cần thiết lập **2 credentials** trong n8n:
1. **Google Sheets OAuth2**:
   - Tạo trong **Settings → Credentials → Add Credential → Google Sheets OAuth2**.
   - Chọn **Google Sheets API** và hoàn tất OAuth2 (theo hướng dẫn [Google](https://developers.google.com/sheets/api/quickstart/python)).
2. **Gmail OAuth2**:
   - Tạo trong **Settings → Credentials → Add Credential → Gmail OAuth2**.
   - Chọn **Gmail API** và cấp quyền **Send Email**.

#### **B. Cấu hình Google Sheets**
Workflow sử dụng **3 tab Google Sheets**:
1. **`Student List`**: Danh sách học viên hiện có.
2. **`FormResponses`**: Lưu dữ liệu đăng ký mới.
3. **`Student List1`** (dùng cho nhắc nhở).

:::warning[CẤU TRÚC CỐT LÕI]
Các tab phải có **các cột tương ứng** với dữ liệu form đăng ký (ví dụ):
| Name       | Email          | Phone       | Course      | Registration Date |
|------------|----------------|-------------|-------------|-------------------|
| (Dữ liệu)  | (Dữ liệu)      | (Dữ liệu)   | (Dữ liệu)   | (Dữ liệu)         |
:::

#### **C. Cấu hình Webhook**
Workflow sử dụng **2 Webhook**:
1. **`Webhook1`** (path: `2235781f-4371-4f6e-8767-41c352ed171f`):
   - Dùng để **nhận dữ liệu đăng ký** từ form.
   - Cấu hình trong **Webhook1 → Key Parameters → Path** (không cần thay đổi).
2. **`Webhook - send-acknowledgements`** (path: `send-acknowledgements`):
   - Dùng để **gửi email xác nhận**.
3. **`Webhook - send-reminder`** (path: `send-reminder`):
   - Dùng để **gửi nhắc nhở**.

:::tip[Lấy URL Webhook]
1. Mở **Webhook1** trong n8n.
2. Chọn **Copy URL** từ tab **General**.
3. Sử dụng URL này trong **form đăng ký** (ví dụ: `<form action="https://your-n8n-url/webhook/2235781f-4371-4f6e-8767-41c352ed171f" method="POST">`).
:::

#### **D. Cấu hình Email (Gmail)**
Workflow tự động gửi **2 loại email**:
1. **Xác nhận đăng ký** (quy trình `Send Acknowledgements`).
2. **Nhắc nhở trước ngày khai giảng** (quy trình `Send Reminders`).

:::note[Cấu hình Gmail]
- Trong node **`Send a message`** và **`Send a message1`**:
  - **From**: Địa chỉ email bạn muốn hiển thị (ví dụ: `noreply@coursename.edu`).
  - **Subject**: Tùy chỉnh (ví dụ: **"Xác nhận đăng ký khóa học [Tên Khóa Học]"**).
  - **Body**: Sử dụng **Code Node** để động thái hóa nội dung (xem phần sau).
:::

#### **E. Cấu hình Code Node (Dynamic Content)**
Workflow sử dụng **2 Code Node** để **chỉnh sửa nội dung email**:
1. **`Code - Prepare Messages`** (dùng cho email xác nhận).
2. **`Code - Prepare Messages1`** (dùng cho email nhắc nhở).

:::example[Ví dụ Code Node]
```javascript
// Code - Prepare Messages (Xác nhận đăng ký)
return {
  subject: `Xác nhận đăng ký khóa ${json.course}`,
  body: `Chào ${json.name},\n\nBạn đã đăng ký thành công khóa ${json.course}!\n\nChi tiết:\n- Ngày khai giảng: ${json.registrationDate}\n- Địa điểm: ${json.location || "Chưa xác định"}\n\nCảm ơn bạn đã lựa chọn chúng tôi!`
};
```
:::

---

### **3. Kích hoạt Workflow**
1. **Test Run** với dữ liệu mẫu:
   - Gửi một **dữ liệu đăng ký giả** đến Webhook1 để kiểm tra.
   - Kiểm tra **Google Sheets** có cập nhật dữ liệu không.
   - Kiểm tra **Gmail** có nhận email xác nhận không.
2. **Bật Active**:
   - Chuyển trạng thái workflow từ **Inactive** sang **Active**.

---

## ✍️ **Mẹo & Gợi ý Nâng Cao**

### **1. Tích hợp với FormBuilder**
- Sử dụng **Google Form** hoặc **Typeform** kết nối với Webhook để thu thập dữ liệu đăng ký.
- Cấu hình **Google Form** gửi dữ liệu POST đến URL Webhook1 của n8n.

### **2. Lưu Log & Theo Dõi**
- Thêm **node `Set`** sau Google Sheets để lưu **ID đăng ký** vào một cột riêng.
- Sử dụng **node `StickyNote`** để ghi chú lỗi hoặc cập nhật.

### **3. Gửi Email Nhóm**
- Sử dụng **node `gmail`** với **tham số `to` là danh sách email** (ví dụ: `email1@example.com,email2@example.com`).
- Tích hợp với **Slack/Telegram** để báo cáo lỗi (sử dụng node `slack` hoặc `telegram`).

### **4. Cập Nhật Định Kỳ**
- Sử dụng **node `Set Interval`** để chạy quy trình nhắc nhở hàng tuần.
- Ví dụ: Gửi email nhắc nhở **7 ngày trước ngày khai giảng**.

### **5. Xử Lý Trùng Lặp**
- Thêm **node `Filter`** trước Google Sheets để loại bỏ dữ liệu trùng lặp.
- Sử dụng **Code Node** để kiểm tra `Email` đã tồn tại trong `Student List`.

---

## 📌 **Kết Luận**
Workflow này giúp **tự động hóa toàn bộ quy trình đăng ký**, từ thu thập dữ liệu đến gửi thông báo, **không cần viết một dòng code**. Các sếp giáo dục, doanh nghiệp dịch vụ hoặc tổ chức có thể:
✔ **Tiết kiệm 80% thời gian quản lý**.
✔ **Cải thiện trải nghiệm học viên** với email tự động.
✔ **Theo dõi dễ dàng** trên Google Sheets.

**Hành động ngay hôm nay!**
1. **Import workflow** vào n8n.
2. **Cấu hình Google Sheets & Gmail**.
3. **Test và bật Active** để bắt đầu tự động hóa!

---
**Cần hỗ trợ?** Đăng ký **VPS n8n** từ [TinoHost](https://tino.vn/vps-n8n?affid=388) để workflow chạy ổn định 24/7! 🚀