---
title: "🚀 Tự Động Hóa Form Đăng Ký Email với Hunter.io & SendGrid - Xây Dựng Danh Sách Khách Hàng Miễn Phí"
description: "Workflow tự động hóa hoàn toàn không cần code giúp các sếp thu thập email từ form đăng ký, xác minh tính hợp lệ bằng Hunter.io và tự động thêm vào danh sách SendGrid. Giảm thiểu công việc thủ công, tăng chất lượng danh sách và tối ưu hóa chiến dịch marketing."
slug: "tu-dong-hoa-form-dang-ky-email-hunter-io-sendgrid"
tags: [n8n, automation, marketing, email-marketing, hunter-io]
keywords: [tự động hóa form đăng ký email, danh sách email tự động, hunter io api, sendgrid automation, n8n workflow marketing]
---

# 🚀 **Tự Động Hóa Form Đăng Ký Email với Hunter.io & SendGrid – Không Cần Code, Tăng Chất Lượng Danh Sách Khách Hàng**

## **💥 Nỗi Đau Của Các Sếp Khi Thu Thập Email Thủ Công**
Hàng ngày, các sếp phải:
- **Làm thủ công** việc kiểm tra email từ form đăng ký trên website, blog hay landing page.
- **Lo lắng về chất lượng** danh sách: Email giả, bị chặn, hoặc không hoạt động sẽ làm giảm hiệu quả của chiến dịch email marketing.
- **Tốn thời gian** để nhập liệu vào SendGrid hoặc các công cụ quản lý danh sách, dẫn đến sai sót và hiệu suất thấp.

**Workflow này giải quyết tất cả!** Với **n8n**, các sếp có thể tự động:
✅ **Xác minh email** bằng Hunter.io (miễn phí 50 credit/tháng).
✅ **Lọc bỏ email không hợp lệ** để tránh spam và bị chặn.
✅ **Tự động thêm email hợp lệ** vào danh sách SendGrid.
✅ **Tiết kiệm thời gian** và tập trung vào nội dung marketing chất lượng cao.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng** không phải kiểm tra email thủ công.
- **Danh sách email sạch** (không spam, không bị chặn), tăng tỷ lệ mở và chuyển đổi.
- **Hoạt động 24/7** mà không cần can thiệp của con người.
- **Tối ưu hóa chi phí** với Hunter.io (50 credit miễn phí/tháng) và SendGrid (gói free cho 500 email/tháng).
- **Cải thiện SEO** khi danh sách email chất lượng giúp chiến dịch content marketing hiệu quả hơn.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần:
1. **Tài khoản Hunter.io** (đăng ký tại [Hunter.io](https://hunter.io/)) và **API Key**.
   - Miễn phí **50 credit/tháng** (đủ để xác minh ~50 email).
   - Hướng dẫn lấy API Key:
     - Đăng nhập → **Settings** → **API Keys** → Tạo mới.
2. **Tài khoản SendGrid** (đăng ký tại [SendGrid](https://sendgrid.com/)) và **API Key**.
   - Gói **Free** cho đến 500 email/tháng (đủ cho nhiều doanh nghiệp nhỏ).
   - Hướng dẫn lấy API Key:
     - Đăng nhập → **Settings** → **API Keys** → Tạo mới.
3. **Form đăng ký email** trên website/blog (có thể là form HTML đơn giản hoặc sử dụng công cụ như Typeform, JotForm).
4. **n8n Self-hosted** (không dùng phiên bản cloud để đảm bảo dữ liệu an toàn).
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).

---
## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [đây](https://n8n.io/workflows/2709) (nút **Export**).
2. Trên **n8n Editor**, nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **Create new workflow** và nhấn **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. Mở file JSON từ [đây](https://n8n.io/workflows/2709) và copy toàn bộ nội dung.
2. Trên **n8n Editor**, nhấn **Import** → Chọn **Paste JSON** → Dán và nhấn **Import**.

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **5 node** chính. Dưới đây là hướng dẫn chi tiết để cấu hình:

#### **Node 1: Submit form (n8n-nodes-base.formTrigger)**
- **Chức năng**: Nhận dữ liệu từ form đăng ký email.
- **Cấu hình**:
  - **Trigger**: Chọn **Form Trigger** (nếu form trên website).
  - **Fields**: Đảm bảo form có **email** là trường bắt buộc.
  - **Example**:
    ```json
    {
      "email": "nguyenvananh@example.com"
    }
    ```
  - **Lưu ý**:
    - Nếu sử dụng form ngoài n8n (ví dụ: Typeform), thay thế bằng **Webhook** (node `n8n-nodes-base.http`) để nhận dữ liệu từ URL trả về.

#### **Node 2: Check if the email is valid (n8n-nodes-base.if)**
- **Chức năng**: Kiểm tra email có hợp lệ hay không.
- **Cấu hình**:
  - **Condition**: Chọn **email** từ node trước.
  - **Operator**: `is not empty` (đảm bảo email không trống).
  - **If true**: Tiến đến node **Verify email**.
  - **If false**: Tiến đến node **Email is not valid, do nothing** (bỏ qua).

#### **Node 3: Verify email (n8n-nodes-base.hunter)**
- **Chức năng**: Xác minh email bằng Hunter.io.
- **Cấu hình**:
  - **Credentials**: Chọn **hunterApi** (đã cấu hình trước).
  - **Operation**: `emailVerifier`.
  - **Parameters**:
    - `email`: `$json["email"]` (lấy email từ node trước).
    - **Optional**: Thêm `domain` (nếu muốn kiểm tra domain cụ thể).
  - **Lưu ý**:
    - Hunter.io trả về **status** (`valid`, `invalid`, `disposable`, `role-based`).
    - Chỉ **email có status = "valid"** mới được thêm vào danh sách.

#### **Node 4: Email is not valid, do nothing (n8n-nodes-base.noOp)**
- **Chức năng**: Dừng workflow nếu email không hợp lệ.
- **Cấu hình**: Không cần thiết gì, chỉ để **bỏ qua** email không hợp lệ.

#### **Node 5: Add contact to list (n8n-nodes-base.sendGrid)**
- **Chức năng**: Thêm email hợp lệ vào danh sách SendGrid.
- **Cấu hình**:
  - **Credentials**: Chọn **sendGridApi** (đã cấu hình trước).
  - **Resource**: `contact`.
  - **Parameters**:
    - `email`: `$json["email"]` (lấy email đã xác minh).
    - **Optional**: Thêm `name`, `custom_fields` (nếu cần).
  - **Lưu ý**:
    - SendGrid sẽ trả về **status code 202** nếu thành công.
    - Nếu gặp lỗi, kiểm tra **API Key** và **danh sách đã tồn tại**.

---
### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gửi email mẫu (ví dụ: `test@example.com`) từ form.
   - Kiểm tra node **Verify email** có trả về `status: "valid"` không.
   - Nếu thành công, email sẽ được thêm vào SendGrid.
2. **Bật Active**:
   - Nhấn **Active** trên workflow.
   - **Lưu ý**: Nếu form trên website, đảm bảo **Webhook URL** trong form trùng với URL của node **formTrigger** trong n8n.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**
### **1. Kết hợp với Slack/Telegram để báo cáo**
- Thêm node **Slack** (`n8n-nodes-base.slack`) sau node **Verify email** để thông báo:
  ```json
  {
    "text": `Email ${email} đã được xác minh và thêm vào danh sách!`,
    "username": "n8n-Bot"
  }
  ```
- **Lợi ích**: Các sếp được thông báo ngay khi có email mới hợp lệ.

### **2. Lưu log hoạt động**
- Thêm node **Sticky Note** (`n8n-nodes-base.stickyNote`) để ghi lại:
  - Email đã xác minh.
  - Thời gian xử lý.
  - Trạng thái (thành công/thất bại).
- **Lợi ích**: Dễ dàng theo dõi và debug nếu có vấn đề.

### **3. Gửi email xác nhận cho người dùng**
- Thêm node **SendGrid Email** (`n8n-nodes-base.sendGrid`) sau node **Add contact to list** để gửi email xác nhận:
  ```json
  {
    "to": "$json.email",
    "subject": "Xác nhận đăng ký danh sách email của chúng tôi!",
    "html": "<p>Chúng tôi đã xác nhận email của bạn: <strong>${$json.email}</strong>!</p>"
  }
  ```
- **Lợi ích**: Tăng độ tin cậy và giảm tỷ lệ email bị bỏ qua.

### **4. Xử lý email disposable (tạm thời)**
- Thêm node **If** mới sau **Verify email** để kiểm tra `status === "disposable"`.
- Nếu đúng, gửi email thông báo cho người dùng:
  ```json
  {
    "to": "$json.email",
    "subject": "Lỗi: Email của bạn không hợp lệ!",
    "html": "<p>Email ${$json.email} không được chấp nhận vì là email tạm thời.</p>"
  }
  ```
- **Lợi ích**: Tránh thêm email tạm thời vào danh sách.

---
## **📌 Kết Luận**
Workflow này giúp các sếp **tự động hóa hoàn toàn** quá trình thu thập và xác minh email, tiết kiệm thời gian và nâng cao chất lượng danh sách. **Không cần code**, chỉ cần **n8n + Hunter.io + SendGrid** là đủ!

👉 **Bắt đầu ngay!**
1. **Cài đặt n8n trên VPS** (đăng ký [tại đây](https://tino.vn/vps-n8n?affid=388) với mã giảm giá **VPSN8N**).
2. **Cấu hình Hunter.io và SendGrid** theo hướng dẫn trên.
3. **Import workflow** và **bật Active**.
4. **Theo dõi kết quả** trên Slack/Telegram và **tối ưu hóa** theo nhu cầu.

**Chia sẻ workflow này với đồng nghiệp để cùng tự động hóa công việc marketing!** 🚀

---
### **📚 Tài Liệu Tham Khảo**
- [Case Study: Tạo Form Đăng Ký Email Miễn Phí với n8n & SendGrid](https://rumjahn.com/create-email-capture-forms-for-free-using-n8n-and-sendgrid-and-easily-grow-your-subscriber-list/)
- [Tutorial Video](https://www.youtube.com/watch?v=NgvEHwu19Rs&t=2s)
- [Hướng Dẫn Hunter.io API](https://hunter.io/docs/api)
- [Hướng Dẫn SendGrid API](https://sendgrid.com/docs/api-reference/)