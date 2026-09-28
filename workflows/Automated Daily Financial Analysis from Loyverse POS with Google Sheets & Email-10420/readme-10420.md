---
title: "📊 Tự Động Hóa Phân Tích Tài Chính Hàng Ngày Từ Loyverse Sang Google Sheets & Email (Không Cần Code)"
description: "Workflow tự động hóa lấy dữ liệu bán hàng từ Loyverse, tính toán chỉ số kinh doanh hàng ngày, lưu trữ trên Google Sheets và gửi báo cáo email tự động. Giúp các sếp tiết kiệm 5+ giờ/tháng và theo dõi hiệu suất kinh doanh 24/7."
slug: "tieu-dong-hoa-phan-tich-tai-chinh-loyverse-google-sheets-email"
tags: [n8n, automation, Loyverse, Google Sheets, email automation, financial analysis, no-code]
keywords: [tự động hóa Loyverse, phân tích tài chính hàng ngày, Google Sheets tự động, gửi báo cáo email tự động, n8n workflow tài chính]
---

# 🚀 **Tự Động Hóa Phân Tích Tài Chính Hàng Ngày Từ Loyverse Sang Google Sheets & Email**

### **Giải pháp cho các sếp:**
Bạn có bao giờ phải mất **30-60 phút mỗi ngày** để:
- Lấy dữ liệu bán hàng từ Loyverse?
- Tính toán doanh thu, lợi nhuận, sản phẩm bán chạy?
- Lưu trữ dữ liệu vào Google Sheets?
- Gửi báo cáo email cho đội ngũ?

**Workflow này sẽ tự động hóa toàn bộ quy trình trong 10 phút cài đặt!** Không cần viết code, chỉ cần cấu hình và chạy 24/7.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 5+ giờ/tháng** – Không cần thủ công lấy dữ liệu hàng ngày.
✅ **Dữ liệu chính xác 100%** – Tính toán tự động từ Loyverse.
✅ **Báo cáo email tự động** – Gửi kết quả cho đội ngũ mỗi sáng.
✅ **Lưu trữ dữ liệu dài hạn** – Dữ liệu được ghi vào Google Sheets theo lịch.
✅ **Cá nhân hóa báo cáo** – Thêm logo, tiêu đề, và chỉ số quan trọng.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Loyverse** (để lấy API Token):
   - Tạo **Access Token** tại **Integrations → Access Tokens**.
   - Lưu token vào **n8n** với credential **Bearer YOUR_TOKEN_HERE**.

2. **Google Sheets API** (để lưu trữ dữ liệu):
   - Tạo **Google Sheets OAuth2** trong n8n.
   - **Bắt buộc**: Sếp phải **copy** file mẫu từ [đây](https://docs.google.com/spreadsheets/d/1DlEUo3mQUaxn2HEp34m7VAath8L3RDuPy5zFCljSZHE/edit?usp=sharing).

3. **SMTP hoặc Gmail** (để gửi email tự động):
   - Cấu hình **SMTP** (hoặc dùng Gmail với OAuth2).

4. **Thời gian cài đặt**: ~10-15 phút (chỉ cần chỉnh cấu hình).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/10420](https://n8n.io/workflows/10420).
- **Cách 1**: Nhấn **Import** trong n8n Editor và chọn file JSON.
- **Cách 2**: Copy toàn bộ JSON và dán vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow có **4 bước cài đặt chính**, các sếp làm theo thứ tự:

##### **📌 Bước 1: Cấu hình Credentials (Bắt buộc)**
- **Loyverse**:
  - Tạo **API Token** tại Loyverse → **Integrations → Access Tokens**.
  - Trong n8n, tạo **credential mới** với loại **Generic/Bearer** và nhập token.
- **Google Sheets**:
  - Tạo **Google Sheets OAuth2** trong n8n.
  - **Chia sẻ file mẫu** cho n8n (theo hướng dẫn trong **MASTER CONFIG**).
- **Email (SMTP/Gmail)**:
  - Cấu hình **SMTP** hoặc dùng **Gmail OAuth2**.

##### **📌 Bước 2: Chỉnh MASTER CONFIG (Node Code)**
Mở node **MASTER CONFIG** và chỉnh các biến sau:
```javascript
// Thay đổi các giá trị này theo cấu trúc của sếp
module.exports = {
  google_sheet_settings: {
    SpreadsheetID: "ID_CỦA_FILE_GOOGLE_SHEETS", // Lấy từ URL file
    ProductListSheet: "Sheet_Danh_Sách_Sản_Phẩm", // Tên sheet lưu sản phẩm
    SalesDataSheet: "Sheet_Dữ_Liệu_Bán_Hàng"    // Tên sheet lưu doanh thu
  },
  loyverse_settings: {
    api_base_url: "https://api.loyverse.com/v1/", // URL API Loyverse
    shift_start_time: "08:00:00", // Thời gian bắt đầu ca làm việc
    shift_end_time: "22:00:00"    // Thời gian kết thúc ca làm việc
  },
  email_settings: {
    from: "tiengianh@doanhnghiep.com", // Email gửi
    subject: "BÁO CÁO DOANH THU HÀNG NGÀY {{ $date }}",
    body: "Xin chào, đây là báo cáo doanh thu từ {{ $date }}."
  }
};
```
- **Lưu ý**:
  - **SpreadsheetID** lấy từ URL Google Sheets (ví dụ: `1DlEUo3mQUaxn2HEp34m7VAath8L3RDuPy5zFCljSZHE`).
  - **shift_start_time & shift_end_time** điều chỉnh theo giờ mở cửa của cửa hàng.

##### **📌 Bước 3: Cấu hình Google Sheets (Save Product List & Save Latest Sales Data)**
- **Node "Save Product List"**:
  - Chọn **Document**: "LoyverseDataTool" (file đã copy).
  - **Sheet**: `{{ $node["MASTER CONFIG"].json.google_sheet_settings.ProductListSheet }}`
  - **Map Each Column Manually**: Ghép cột từ node **Format Product Data**.

- **Node "Save Latest Sales Data"**:
  - Chọn **Document**: "LoyverseDataTool".
  - **Sheet**: `{{ $node["MASTER CONFIG"].json.google_sheet_settings.SalesDataSheet }}`
  - **Không cần map cột** (node tự động ghi dữ liệu).

##### **📌 Bước 4: Chỉnh lịch chạy (Schedule Trigger)**
- Mở node **Run Daily at 8:15AM** và chỉnh thời gian chạy (ví dụ: **8:00 sáng**).
- **Lưu ý**: Nếu muốn chạy thủ công, có thể dùng **Manual Trigger** thay thế.

#### **3. Kích hoạt ⚡️**
- **Test Run**:
  - Chạy **Manual Trigger** để kiểm tra dữ liệu lấy từ Loyverse.
  - Kiểm tra **Google Sheets** và **email** có nhận được không.
- **Bật Active**:
  - Sau khi test thành công, **bật Active** workflow.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Thêm Logo & Tiêu Đề Email**:
   - Trong node **emailSend**, chỉnh **HTML Body** để thêm logo và thiết kế chuyên nghiệp.
   ```html
   <table>
     <tr><td><img src="https://tiengianh.com/logo.png" width="100"></td></tr>
     <tr><td><h2>BÁO CÁO DOANH THU {{ $date }}</h2></td></tr>
   </table>
   ```

2. **Lưu Log Dữ Liệu**:
   - Thêm node **StickyNote** để ghi log lỗi hoặc thành công.
   ```javascript
   // Trong node Code, thêm:
   $output.current.json.log = "Dữ liệu đã xử lý thành công!";
   ```

3. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng **Schedule Trigger** để gửi báo cáo hàng tuần/tháng.
   - Ví dụ: Chạy **Thứ 2 hàng tuần** để tổng hợp báo cáo tháng.

4. **Kết hợp Slack/Telegram**:
   - Thêm node **Slack Webhook** hoặc **Telegram Bot** để thông báo khi có lỗi.

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào chiến lược kinh doanh thay vì làm thủ công. **Chỉ cần 10 phút cài đặt**, bạn sẽ có:
✔ **Dữ liệu bán hàng tự động** từ Loyverse.
✔ **Báo cáo email hàng ngày** gửi tự động.
✔ **Google Sheets cập nhật liên tục**.

**Hãy thử ngay và tiết kiệm 5+ giờ/tháng!** 🚀

---
**🔗 [Tải workflow nguyên bản](https://n8n.io/workflows/10420)**
**📌 [Hướng dẫn chi tiết trên n8n.io](https://n8n.io/workflows/10420)**