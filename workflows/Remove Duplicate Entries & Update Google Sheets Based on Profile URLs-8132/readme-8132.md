---
title: "🔍 Xóa Trùng Lặp & Cập Nhật Google Sheets Tự Động Từ URL Profile (Không Cần Code)"
description: "Workflow tự động hóa xóa trùng lặp dữ liệu trong Google Sheets và cập nhật thông tin mới từ URL profile, tiết kiệm thời gian và giảm sai sót cho các sếp quản lý danh sách khách hàng/nhân viên."
slug: "xoa-trung-lap-cap-nhat-google-sheets-tu-url-profile"
tags: [n8n, automation, google-sheets, data-cleaning, no-code]
keywords: [n8n workflow xóa trùng lặp, tự động hóa google sheets, cập nhật dữ liệu từ URL, loại bỏ dữ liệu trùng, tự động hóa quản lý khách hàng]
---

# 🔍 **Xóa Trùng Lặp & Cập Nhật Google Sheets Từ URL Profile (Không Cần Code)**

### **Nỗi Đau Của Các Sếp**
Các sếp thường phải chịu những vấn đề sau khi quản lý danh sách khách hàng, nhân viên hoặc dữ liệu liên lạc bằng tay:
- **Thời gian mất mát**: Phải tra cứu và xóa trùng lặp thủ công, tốn nhiều giờ làm việc.
- **Sai sót cao**: Rủi ro bỏ sót hoặc xóa nhầm dữ liệu quan trọng.
- **Không cập nhật kịp thời**: Dữ liệu không được đồng bộ từ nguồn mới (như URL profile) dẫn đến thông tin lỗi thời.

Workflow này **giải quyết tất cả** bằng cách tự động:
✅ **Xóa trùng lặp** trong Google Sheets một cách chính xác.
✅ **Cập nhật dữ liệu mới** từ URL profile (ví dụ: LinkedIn, website cá nhân) vào bảng tính.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Xóa trùng lặp và cập nhật dữ liệu chỉ trong vài giây thay vì nhiều giờ.
- **Dữ liệu chính xác**: Không còn lo lắng về trùng lặp hoặc thông tin lỗi thời.
- **Tự động hóa hoàn toàn**: Cập nhật liên tục từ URL profile mà không cần can thiệp.
- **Dễ dàng mở rộng**: Thêm các nguồn dữ liệu khác (như API, CRM) vào workflow.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google** với quyền quản trị Google Sheets và Google Drive.
2. **URL profile** của mỗi bản ghi trong Google Sheets (ví dụ: LinkedIn, website cá nhân).
3. **Bảng Google Sheets** chứa dữ liệu cần xử lý (cột chứa URL profile phải được định danh rõ ràng).
4. **API Key OAuth2** cho Google Sheets và Google Drive (cài đặt trong n8n).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n.io](https://n8n.io/) và mở **n8n Editor**.
2. Nhấp vào **"Import"** và chọn file JSON (hoặc copy/paste JSON từ [link gốc](https://n8n.io/workflows/8132)).
3. Chọn **"Import"** để tải workflow vào.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này bao gồm **5 node** chính. Các sếp cần chú ý cấu hình sau:

##### **Node 1: Manual Trigger (Bắt Đầu Workflow)**
- **Tên node**: "When clicking ‘Execute workflow’"
- **Lưu ý**: Node này chỉ là điểm khởi động. Các sếp có thể thay thế bằng **Webhook** để kích hoạt tự động (ví dụ: từ Slack, Zapier).

##### **Node 2: Get Row(s) in Sheet (Lấy Dữ liệu từ Google Sheets)**
- **Tên node**: "Get row(s) in sheet"
- **Cấu hình cần thiết**:
  - **Credentials**: Chọn `"googleSheetsOAuth2Api"` (đã cài đặt trước).
  - **Sheet Name**: Nhập tên bảng Google Sheets chứa dữ liệu.
  - **Range**: Chọn phạm vi dữ liệu (ví dụ: `"Sheet1!A:Z"`).
  - **Query**: Thêm điều kiện lọc nếu cần (ví dụ: `where="URLProfile is not empty"`).

##### **Node 3: Remove Duplicates (Xóa Trùng Lặp)**
- **Tên node**: "Remove Duplicates"
- **Cấu hình cần thiết**:
  - **Key**: Chọn cột chứa **URL profile** (ví dụ: `"URLProfile"`).
  - **Case Sensitive**: Bật nếu cần phân biệt chữ hoa/chữ thường.

##### **Node 4: Convert to File (Chuyển Dữ liệu Sang File CSV)**
- **Tên node**: "Convert to File"
- **Lưu ý**: Node này chuyển dữ liệu đã xóa trùng thành file CSV để cập nhật vào Google Drive.

##### **Node 5: Update File (Cập Nhật File Trên Google Drive)**
- **Tên node**: "Update file"
- **Cấu hình cần thiết**:
  - **Credentials**: Chọn `"googleDriveOAuth2Api"`.
  - **File ID**: Nhập ID của file CSV trên Google Drive (tìm trong liên kết chia sẻ file).
  - **Operation**: Đảm bảo chọn `"update"`.
  - **File Content**: Chọn dữ liệu từ node `Convert to File`.

---
#### **3. Kích Hoạt ⚡️**
1. **Test Run**: Nhấp vào nút **"Execute"** để chạy workflow với dữ liệu mẫu.
2. **Kiểm tra kết quả**:
   - Mở Google Sheets để xác nhận trùng lặp đã được xóa.
   - Mở Google Drive để kiểm tra file CSV đã được cập nhật.
3. **Bật Active**: Sau khi kiểm tra thành công, chuyển workflow sang trạng thái **"Active"**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram** để thông báo khi workflow hoàn thành.
   - Ví dụ: Gửi tin nhắn `"Xóa trùng lặp thành công! Cập nhật {số lượng bản ghi} bản ghi mới."`.

2. **Lưu Log Dữ Liệu**:
   - Thêm node **Google Sheets** hoặc **Airtable** để lưu lịch sử hoạt động (ngày giờ, số bản ghi xử lý).

3. **Cập Nhật Định Kỳ**:
   - Sử dụng **n8n Cron Trigger** để chạy workflow hàng ngày/tuần (ví dụ: `"0 0 * * *"` để chạy mỗi ngày 00:00).

4. **Tự Động Hóa Từ API**:
   - Nếu dữ liệu nguồn từ API (ví dụ: CRM), thêm node **HTTP Request** để lấy dữ liệu trước khi xử lý.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc thủ công mệt mỏi, đồng thời **đảm bảo dữ liệu luôn chính xác và cập nhật**. Bằng cách tự động hóa quá trình xóa trùng lặp và cập nhật từ URL profile, các sếp có thể tập trung vào những nhiệm vụ chiến lược hơn.

**Hãy thử ngay!** Import workflow vào n8n của mình và bắt đầu tự động hóa dữ liệu của doanh nghiệp.

---
🔗 **Tài liệu tham khảo**:
- [Workflow gốc trên n8n.io](https://n8n.io/workflows/8132)
- [Hướng dẫn cài đặt OAuth2 cho Google Sheets](https://docs.n8n.io/integrations/builtins/nodes/n8n-nodes-base.googleSheets.html#credentials)