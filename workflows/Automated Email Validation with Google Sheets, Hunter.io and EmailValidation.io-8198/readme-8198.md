---
title: "🚀 Tự Động Kiểm Tra Email Hiệu Quả Với Google Sheets, Hunter.io & EmailValidation.io (Không Cần Code)"
description: "Workflow tự động hóa kiểm tra tính hợp lệ của email từ Google Sheets, tích hợp Hunter.io và EmailValidation.io để loại bỏ email sai, tiết kiệm thời gian và nâng cao chất lượng leads cho doanh nghiệp. Hoạt động liên tục 24/7, không cần can thiệp thủ công."
slug: "tieu-dong-kiem-tra-email-google-sheets-hunter-emailvalidation"
tags: [n8n, automation, lead-generation, email-validation, google-sheets]
keywords: [tự động hóa kiểm tra email, n8n workflow, hunter.io, emailvalidation.io, google sheets tự động, lead validation]
---

# 🚀 **Tự Động Kiểm Tra Email Hiệu Quả: Loại Bỏ Email Sai Trong Google Sheets**

### **Nỗi Đau Của Các Sếp**
Làm việc với danh sách email lớn để tìm kiếm khách hàng tiềm năng (leads) là một nhiệm vụ mệt mỏi và dễ sai sót. Các sếp thường phải:
- **Lọc thủ công** email không hợp lệ (đã bị block, không tồn tại, hoặc domain sai).
- **Tốn thời gian** để kiểm tra từng email một, dẫn đến hiệu suất thấp.
- **Mất leads chất lượng** vì không biết email nào thực sự hoạt động.

**Workflow này giải quyết tất cả!** Nó tự động kiểm tra tính hợp lệ của email từ Google Sheets, tích hợp với **Hunter.io** và **EmailValidation.io**, sau đó cập nhật kết quả trực tiếp vào bảng tính. **Không cần code, hoạt động 24/7!**

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Loại bỏ việc kiểm tra email thủ công, tự động hóa trong vài giây.
- **Chất lượng leads cao**: Chỉ giữ lại email hợp lệ, tăng tỷ lệ thành công trong marketing.
- **Cập nhật tự động**: Kết quả kiểm tra được ghi lại ngay vào Google Sheets.
- **Hoạt động liên tục**: Không cần can thiệp, workflow chạy tự động khi có email mới.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets**:
   - Một bảng tính Google Sheets với cột chứa email (ví dụ: `Email`).
   - **Credentials OAuth2** của Google Sheets (cài đặt trong n8n).
2. **Tài khoản Hunter.io hoặc EmailValidation.io**:
   - **API Key** của Hunter.io (đăng ký tại [Hunter.io](https://hunter.io/)) **hoặc**
   - **API Key** của EmailValidation.io (đăng ký tại [EmailValidation.io](https://emailvalidation.io/)).
3. **n8n Self-hosted** (không dùng phiên bản miễn phí của n8n.io).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Bước 1**: Tải workflow từ [n8n.io/workflows/8198](https://n8n.io/workflows/8198) hoặc sao chép JSON từ trang này.
- **Bước 2**: Mở **n8n Editor** → Nhấn **"Import"** → Dán JSON hoặc tải file `.json`.
- **Bước 3**: Chọn **"Create Workflow"** để lưu vào dự án của mình.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **2 phương pháp kiểm tra email**:
- **Phương pháp 1 (Khuyến nghị)**: Sử dụng **EmailValidation.io** (nhanh chóng và chính xác).
- **Phương pháp 2**: Sử dụng **Hunter.io** (nếu đã có tài khoản).

##### **Cấu Hình Google Sheets**
1. **Node "Google Sheets Trigger"**:
   - Chọn **Google Sheets OAuth2** trong **Credentials**.
   - Chọn **Sheet Name** (tên bảng tính) và **Range** (ví dụ: `Sheet1!A2:B`).
   - **Lưu ý**: Cột chứa email phải ở cột đầu tiên (ví dụ: `A`).

2. **Node "Update the Sheets with Validation Status"**:
   - Chọn cùng **Google Sheets OAuth2** như trên.
   - Chọn **Sheet Name** và **Range** tương ứng (ví dụ: `Sheet1!C2:C` để ghi kết quả vào cột `C`).

##### **Cấu Hình Email Validation**
- **Lựa chọn 1: EmailValidation.io**
  - Trong node **"Email Validation API"** (HTTP Request):
    - Thay đổi **URL** thành:
      ```
      https://api.emailvalidation.io/v1/validate?apiKey=YOUR_API_KEY&email={$json["email"]}
      ```
    - Thay `YOUR_API_KEY` bằng API Key của EmailValidation.io.
  - Trong node **"Alternative - Hunter for Email Validation"**, **bỏ qua** (không sử dụng).

- **Lựa chọn 2: Hunter.io**
  - Trong node **"Alternative - Hunter for Email Validation"**:
    - Thay đổi **API Key** trong **Credentials**.
    - **Bỏ node "Email Validation API"** (HTTP Request) ra khỏi workflow.

##### **Cấu Hình Các Node Khác**
- **Node "Filter Empty Cells"**: Loại bỏ hàng trống.
- **Node "Take Email Only"**: Lấy chỉ email từ cột đầu tiên.
- **Node "Take Email and Validation Status"**: Ghi kết quả kiểm tra vào cột mới.

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấn **"Execute Workflow"** với dữ liệu mẫu (ví dụ: `test@example.com`).
   - Kiểm tra kết quả trong Google Sheets.
2. **Bật Active**:
   - Sau khi test thành công, chuyển trạng thái workflow sang **"Active"**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁC TỐT NHẤT]
- **Tích hợp Slack/Telegram**: Gửi thông báo khi có email không hợp lệ.
  ```yaml
  - Node: "slackWebhook" (n8n-nodes-base.slack)
    Tham số: `{"text": "Email {{$json["email"]}} không hợp lệ!"}`
  ```
- **Lưu log**: Sử dụng **Google Sheets** hoặc **n8n Database** để theo dõi lịch sử kiểm tra.
- **Chạy định kỳ**: Sử dụng **n8n Cron** để kiểm tra lại danh sách email hàng tuần.
- **Kết hợp với CRM**: Gửi email hợp lệ vào **HubSpot** hoặc **Salesforce** tự động.
:::

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc lặp đi lặp lại, đồng thời **tăng chất lượng leads** bằng cách loại bỏ email không hợp lệ. **Chỉ cần 10 phút setup**, workflow sẽ hoạt động tự động, tiết kiệm hàng giờ công việc mỗi tuần!

**👉 Bắt đầu ngay bằng cách import workflow và cấu hình theo hướng dẫn trên!**
Nếu gặp vấn đề, hãy để lại comment dưới đây hoặc liên hệ với **Khair Ahammed** (tác giả) qua [LinkedIn](https://www.linkedin.com/in/khair-ahammed/).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::