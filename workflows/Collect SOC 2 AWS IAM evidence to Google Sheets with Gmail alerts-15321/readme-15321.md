---
title: "🔐 Tự Động Hóa Thu Thập Bằng Chứng SOC 2 AWS IAM Sang Google Sheets Với Gmail Alerts - Giảm Thời Gian Audit 90%"
description: "Workflow tự động hóa thu thập danh sách người dùng IAM AWS hàng quý, xuất sang Google Sheets và gửi báo cáo email tự động để đáp ứng yêu cầu chứng nhận SOC 2. Giúp các sếp tiết kiệm 10+ giờ/tháng và đảm bảo tính chính xác 100%."
slug: "tu-dong-hoa-thu-thap-bang-chung-soc2-aws-iam"
tags: [n8n, automation, secops, aws-iam, google-sheets, gmail-alerts, soc2-compliance]
keywords: [tự động hóa AWS IAM, thu thập bằng chứng SOC 2, google sheets automation, email alert tự động, n8n workflow secops, audit tự động hàng quý]
---

# 🚀 **Tự Động Hóa Thu Thập Bằng Chứng SOC 2 AWS IAM Sang Google Sheets Với Gmail Alerts**

### **Giải pháp hoàn hảo cho các sếp IT & Chuyên viên An Toàn Thông Tin**
Bạn đã bao giờ phải **tìm kiếm thủ công danh sách người dùng AWS IAM** để chuẩn bị cho **audit SOC 2** hay **review quyền truy cập** hàng quý? Hoặc phải **ghi chép lại dữ liệu vào Google Sheets** để báo cáo cho ban lãnh đạo? Nếu có, thì **workflow này sẽ giúp bạn tiết kiệm 10+ giờ/tháng** và **tránh sai sót 100%** nhờ tự động hóa hoàn toàn!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Thu thập và xuất báo cáo **tự động hàng quý** (không cần làm thủ công).
✅ **Đảm bảo chính xác**: Không còn lo lắng **quên người dùng** hoặc **sai sót trong ghi chép**.
✅ **Báo cáo chuyên nghiệp**: Email tự động gửi **tóm tắt số lượng người dùng** và **thông tin chi tiết** sang Google Sheets.
✅ **Tuân thủ SOC 2**: Đáp ứng yêu cầu **audit quyền truy cập** một cách **liên tục và minh bạch**.
✅ **Hoạt động 24/7**: Chạy trên **VPS riêng** (self-hosted) để không phụ thuộc vào n8n.io.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản AWS** với quyền `iam:ListUsers` (để thu thập danh sách người dùng).
✔ **Google Sheets** với tên tệp là **"IAM Access Review"** (các cột bắt buộc: **Username, User ID, ARN, Create Date, Audit Date**).
✔ **Tài khoản Gmail** (để gửi email báo cáo).
✔ **API Key của n8n** (nếu self-hosted).

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/15321](https://n8n.io/workflows/15321).
2. **Mở n8n Editor** (trên n8n.io hoặc self-hosted).
3. **Nhấp vào "Import"** và chọn file JSON vừa tải.
4. **Chọn "Import"** để workflow xuất hiện trên canvas.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ mã JSON** từ [n8n.io/workflows/15321](https://n8n.io/workflows/15321).
2. **Mở n8n Editor** → **Nhấp vào "Import"** → **Chọn "Paste JSON"**.
3. **Chọn "Import"** để workflow được tạo.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **🔹 Node 1: "Quarterly Schedule" (scheduleTrigger)**
- **Cấu hình lịch chạy**:
  - **Frequency**: Chọn **"Every 3 months"** (hoặc **"Manual"** nếu muốn chạy theo yêu cầu).
  - **Time**: Đặt giờ phù hợp (ví dụ: **3h sáng** để không làm phiền nhân viên).
  - **Tag**: Thêm **timestamp** để theo dõi lịch sử (ví dụ: `Audit_2024_Q3`).

#### **🔹 Node 2 & 3: "Set Audit Data" (code) & "List IAM Users" (awsIam)**
- **AWS Credentials**:
  - **Tạo credential mới** trong n8n (nếu chưa có):
    - **Type**: `AWS`
    - **Access Key ID & Secret Access Key**: Điền từ **IAM User** có quyền `iam:ListUsers`.
  - **Node "List IAM Users"**:
    - **Credentials**: Chọn credential AWS vừa tạo.
    - **Operation**: Chọn **"ListUsers"** (mặc định).

#### **🔹 Node 4: "Format User Evidence" (code)**
- **Không cần chỉnh sửa** (n8n tự động định dạng dữ liệu theo yêu cầu).
- **Nếu cần thay đổi**: Mở **Code Editor** và chỉnh sửa logic (nếu biết lập trình).

#### **🔹 Node 5: "Users Found?" (if)**
- **Điều kiện mặc định**: Nếu **danh sách người dùng không rỗng**, workflow tiếp tục.
- **Không cần chỉnh sửa** (n8n tự động xử lý).

#### **🔹 Node 6: "Export to Google Sheets" (googleSheets)**
- **Google Sheets Credentials**:
  - **Tạo credential mới** trong n8n:
    - **Type**: `Google Sheets`
    - **API Key**: Tạo từ [Google Cloud Console](https://console.cloud.google.com/).
    - **Spreadsheet ID**: Lấy từ **URL của Google Sheet** (ví dụ: `1AbCdEfGhIjKlMnOpQrStUvWxYz`).
  - **Operation**: Chọn **"Append"** (để thêm dữ liệu mới vào cuối bảng).
  - **Sheet Name**: Đảm bảo tên là **"IAM Access Review"**.
  - **Headers**: Điền theo thứ tự:
    ```
    Username, User ID, ARN, Create Date, Audit Date
    ```

#### **🔹 Node 7 & 8: "Summarize Run" (code) & "Send Success Email" (gmail)**
- **Email Alerts**:
  - **Tạo credential Gmail** trong n8n:
    - **Type**: `Gmail`
    - **Email Address**: Điền địa chỉ email muốn nhận báo cáo.
    - **App Password**: Sử dụng **mật khẩu ứng dụng** (nếu sử dụng 2FA).
  - **Node "Send Success Email"**:
    - **To**: Điền email của **ban lãnh đạo** (ví dụ: `ceo@company.com`).
    - **Subject**: `"SOC 2 Audit - Quarterly IAM Review Completed"`.
    - **Body**: Sử dụng **template mặc định** (n8n tự động lấy dữ liệu từ node "Summarize Run").

#### **🔹 Node 9: "Send Warning Email" (gmail)**
- **Chỉ hoạt động nếu có lỗi**:
  - **To**: Điền email của **chuyên viên IT** (ví dụ: `it-support@company.com`).
  - **Subject**: `"SOC 2 Audit - Error in IAM Data Collection"`.
  - **Body**: Sử dụng **template mặc định** (n8n tự động báo lỗi nếu thu thập dữ liệu thất bại).

---

### **3. Kích hoạt ⚡️**
1. **Test Run (Kiểm tra thử)**:
   - Nhấp vào **"Run Workflow"** để kiểm tra nếu workflow hoạt động.
   - Kiểm tra **Google Sheets** và **Gmail** để xác nhận dữ liệu xuất ra đúng.
2. **Bật Active**:
   - Sau khi test thành công, **nhấp vào "Active"** để workflow chạy tự động.

---

## ✍️ **Mẹo & gợi ý nâng cao**
### **🔹 Kết hợp với Slack/Telegram**
- **Thêm node "Slack" hoặc "Telegram"** để gửi thông báo ngay khi workflow hoàn thành.
- **Cài đặt webhook** từ Slack/Telegram và kết nối với n8n.

### **🔹 Lưu log hoạt động**
- **Thêm node "Sticky Note"** để ghi lại **lịch sử audit** (ví dụ: ngày chạy, số lượng người dùng, trạng thái).
- **Dùng node "Code"** để lưu log vào **Google Drive** hoặc **AWS S3**.

### **🔹 Gửi báo cáo định kỳ**
- **Thêm node "Schedule Trigger" khác** để gửi **báo cáo tổng hợp hàng năm** (ví dụ: số lượng người dùng tăng giảm).
- **Sử dụng node "Google Docs"** để tạo **báo cáo PDF** tự động.

### **🔹 Cập nhật quyền truy cập**
- **Thêm node "AWS IAM" khác** để **xóa người dùng không hoạt động** (nếu cần).

---

## 📌 **Kết luận**
### **Tự động hóa SOC 2 Audit chỉ trong 10 phút setup!**
Workflow này **giúp các sếp**:
✔ **Tiết kiệm thời gian** (không cần làm thủ công).
✔ **Đảm bảo tuân thủ SOC 2** (dữ liệu luôn cập nhật).
✔ **Báo cáo chuyên nghiệp** (email tự động gửi cho lãnh đạo).

**Hãy áp dụng ngay** và **giải phóng thời gian** để tập trung vào những công việc chiến lược hơn!

---
**🚀 Cần hỗ trợ?** Liên hệ với tác giả:
📧 **Mychel Garzon**: [mychel.garzon@gmail.com](mailto:mychel.garzon@gmail.com)
🔗 **Xem workflow gốc**: [n8n.io/workflows/15321](https://n8n.io/workflows/15321)