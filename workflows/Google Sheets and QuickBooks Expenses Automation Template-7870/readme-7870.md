---
title: "🚀 Tự động hóa đồng bộ chi phí từ Google Sheets lên QuickBooks Online với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình nhập liệu chi phí từ Google Sheets lên QuickBooks Online, giúp tiết kiệm thời gian và giảm thiểu sai sót kế toán."
slug: "tu-dong-hoa-chi-phi-google-sheets-quickbooks-n8n"
tags: [n8n, automation, accounting, google-sheets, quickbooks, no-code]
keywords: [n8n workflow, tự động hóa kế toán, google sheets quickbooks, qbo automation, quan ly chi phi]
---

# 🚀 Tự động hóa đồng bộ chi phí từ Google Sheets lên QuickBooks Online

Các sếp làm kế toán hoặc chủ doanh nghiệp chắc chắn đã quá ngán ngẩm cảnh phải ngồi nhập thủ công hàng đống hóa đơn, chứng từ sao kê ngân hàng lên phần mềm kế toán QuickBooks Online (QBO) mỗi cuối tháng. Việc này không chỉ tốn hàng giờ đồng hồ mà còn dễ dẫn đến sai sót số liệu.

Đừng lo, bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ xịn sò được thiết kế bởi **Rosh Ragel**, giúp tự động hóa toàn bộ quá trình đọc dữ liệu chi phí đã được phân loại từ Google Sheets và đẩy thẳng lên QuickBooks Online một cách mượt mà!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không cần nhập liệu thủ công từng dòng chi phí hay hóa đơn vào QBO nữa.
- **Phân quyền thông minh:** Cho phép nhân sự hoặc cộng tác viên phân loại chi phí trực tiếp trên Google Sheets mà không cần cấp quyền truy cập trực tiếp vào hệ thống QuickBooks nhạy cảm.
- **Đồng bộ hai chiều chính xác:** Workflow tự động làm mới danh sách Nhà cung cấp (Vendor), Tài khoản kế toán (Chart of Accounts) và ghi nhận lại mã giao dịch (Txn ID) sau khi đẩy thành công.
- **Xử lý lỗi thông minh:** Tự động ghi lại các thông báo lỗi vào Google Sheets nếu giao dịch không thành công để dễ dàng kiểm tra, xử lý.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản QuickBooks Online:** Có quyền truy cập API và lấy được thông tin Realm ID.
- **Tài khoản Google Drive / Google Sheets:** Để kết nối với bảng tính quản lý chi phí.
- **Template Google Sheets mẫu:** Tải template chuẩn tại [Google Sheets Template mẫu](https://docs.google.com/spreadsheets/d/1dmkXHeMghVp5AHrdyU1vrwjUHWNaoDfkk9UOuG-SNKI/edit?usp=sharing).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp tiến hành copy toàn bộ mã JSON của workflow này, sau đó dán (paste) trực tiếp vào giao diện n8n Editor của mình hoặc sử dụng tính năng Import từ file.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy trơn tru, các sếp cần cấu hình chính xác các node quan trọng sau:

- **Get Active Vendors in QuickBooks & Create New Vendors in QuickBooks (`quickbooks`):**
  - Kết nối tài khoản `quickBooksOAuth2Api`.
  - Đảm bảo quyền truy cập QBO đã được cấp phép đầy đủ (Read/Write Vendor).
- **Get Chart of Accounts & Add an Expense to QBO (`httpRequest`):**
  - Cấu hình kết nối API gọi trực tiếp đến QBO sử dụng chung credential `quickBooksOAuth2Api`.
- **Set Realm ID for Custom API Call (`set`):**
  - Điền chính xác **Realm ID** (Company ID) lấy từ tài khoản QBO Developer của các sếp để đảm bảo gọi đúng môi trường công ty.
- **Các node Google Sheets (`googleSheets`):**
  - Bao gồm: *Add Accounts to Google Sheet Template*, *Get New Vendors from Google Sheets*, *Refresh Vendors in Google Sheet Template*, *Get New Expense Transactions*, *Record Txn ID in Google Sheets*, *Record Error Message*.
  - Các sếp cần kết nối `googleSheetsOAuth2Api`, sau đó trỏ đến File Google Sheets mẫu đã chuẩn bị ở phần chuẩn bị và chọn đúng tên Sheet tương ứng.

#### 3. Kích hoạt ⚡️
- Nhấn nút **When clicking ‘Execute workflow’** để test thử với một vài dòng dữ liệu mẫu trên Google Sheets.
- Kiểm tra kết quả trả về trong QBO và Google Sheets (xem Txn ID đã được cập nhật chưa).
- Bật công tắc **Active** để sẵn sàng sử dụng.

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống tự động hóa hoàn hảo hơn, các sếp có thể mở rộng thêm một số tính năng sau:
- **Tích hợp Thông báo:** Thêm node Telegram hoặc Slack ở cuối workflow để bắn thông báo ngay lập tức về nhóm chat khi có lô chi phí mới được đồng bộ thành công hoặc gặp lỗi.
- **Tự động hóa lịch chạy (Cron):** Thay thế node `manualTrigger` bằng `Schedule Trigger` để n8n tự động đồng bộ chi phí định kỳ vào mỗi cuối ngày hoặc cuối tuần mà không cần bấm tay.
- **Lọc dữ liệu nâng cao:** Tinh chỉnh node `Remove Empties` và `Remove Duplicates` để loại bỏ hoàn toàn các dòng trống hoặc giao dịch bị trùng lặp do người nhập liệu thao tác nhầm.

### 📌 Kết luận
Với workflow n8n kết hợp giữa Google Sheets và QuickBooks Online này, công việc kế toán thủ công rườm rà sẽ được giải quyết gọn gàng chỉ trong một nốt nhạc. Hãy áp dụng ngay vào doanh nghiệp của các sếp để tối ưu hóa hiệu suất vận hành tài chính nhé!