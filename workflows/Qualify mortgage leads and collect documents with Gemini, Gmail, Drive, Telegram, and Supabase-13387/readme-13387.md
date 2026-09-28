---
title: "🏠 **Tự Động Hóa Xử Lý Lead Vay Nhà Với AI Gemini, Gmail, Google Drive & Telegram - Giảm 80% Thời Gian Admin**"
description: "Workflow này tự động nhận, đánh giá và xử lý lead vay nhà bằng AI Gemini, gửi email cá nhân hóa, quản lý tài liệu trên Google Drive và yêu cầu phê duyệt từ Telegram. Giúp các sếp tiết kiệm thời gian, tránh lead chất lượng thấp và tự động hóa toàn bộ quy trình từ nhận lead đến lưu trữ."
slug: "tieu-dong-hoa-lead-vay-nha-voi-ai-gmail-google-drive-telegram"
tags: [n8n, automation, no-code, ai-chatbot, mortgage-lead, google-gemini, google-drive, telegram-bot, supabase]
keywords: [tự động hóa lead vay nhà, n8n workflow mortgage, gemini ai email cá nhân hóa, google drive tự động hóa tài liệu, telegram phê duyệt lead, supabase lưu trữ lead]
---

# 🚀 **Tự Động Hóa Xử Lý Lead Vay Nhà: Từ Nhận Lead Đến Lưu Trữ Tài Liệu Với AI & Telegram**

## **💡 Nỗi Đau Của Các Sếp Trong Xử Lý Lead Vay Nhà**
Hàng ngày, các sếp phải:
- **Làm thủ công** với hàng trăm lead vay nhà, mất thời gian kiểm tra thông tin cá nhân, tính toán khả năng vay.
- **Rủi ro tiếp cận lead không phù hợp** (thu nhập thấp, hồ sơ không đầy đủ) dẫn đến lãng phí thời gian và nguồn lực.
- **Quản lý tài liệu rối loạn**: Khách hàng upload tài liệu lên nhiều nơi khác nhau, khó theo dõi và lưu trữ.
- **Phê duyệt thủ công**: Mỗi lead phải qua nhiều bước kiểm tra, chậm trễ và dễ xảy ra lỗi.

**Workflow này giải quyết tất cả đó bằng:**
✅ **AI Gemini** tự động tạo email cá nhân hóa và đánh giá lead.
✅ **Telegram** để phê duyệt lead trước khi tiếp cận.
✅ **Google Drive** lưu trữ và chia sẻ tài liệu an toàn.
✅ **Supabase** theo dõi và phân tích lead.
✅ **Tự động hóa 100%** – không cần code, chỉ cần cấu hình.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** trong việc xử lý lead và tài liệu.
- **Lọc lead chất lượng** bằng AI và phê duyệt Telegram, tránh tiếp cận lead không phù hợp.
- **Tài liệu an toàn & có tổ chức**: Tất cả tài liệu được lưu trên Google Drive với quyền chia sẻ riêng.
- **Báo cáo tự động**: Supabase lưu trữ và phân tích lead, giúp theo dõi hiệu suất.
- **Hoạt động 24/7**: Không cần can thiệp thủ công, workflow chạy tự động sau khi cấu hình.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản & API Key**:
- **Gmail OAuth 2.0** (để tạo email draft và gửi thông báo).
- **Google Drive OAuth 2.0** (để tạo folder và upload tài liệu).
- **Google Gemini API** (để tạo email cá nhân hóa).
- **Telegram Bot Token** (để gửi thông báo và yêu cầu phê duyệt).
- **Supabase Database** (để lưu trữ và theo dõi lead).
- **Chat ID Telegram** (để nhận thông báo).

✔ **Thông tin cấu hình**:
- **Mức thu nhập tối thiểu** (để lọc lead).
- **Folder cha trên Google Drive** (để tạo folder mới cho mỗi lead).
- **Template email** (nếu muốn tùy chỉnh).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/13387](https://n8n.io/workflows/13387) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://github.com/n8n-io/n8n-workflows/blob/main/workflows/13387.json) và paste vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **24 node** với các bước chính sau. Các sếp cần chú ý cấu hình các node quan trọng:

##### **🔹 Bước 1: Nhận & Lọc Lead (Form Trigger + If)**
- **Node "On form submission"** (formTrigger):
  - Cấu hình **URL form** (ví dụ: `https://tinohost.vn/lead-form`) để nhận lead từ website.
  - **Lưu ý**: Cần tạo form trên **Google Forms** hoặc **Typeform** và kết nối với n8n.

- **Node "Check income threshold"** (if):
  - **Điền số thu nhập tối thiểu** (ví dụ: `50,000,000 VND/tháng`).
  - Nếu lead không đáp ứng, workflow sẽ **đăng ký lead vào Supabase** và **gửi thông báo Telegram** (node "Log declined lead").

##### **🔹 Bước 2: Yêu Cầu Phê Duyệt Telegram (If + Telegram)**
- **Node "Request Email Approval1"** (telegram):
  - **Thiết lập chat ID** của Telegram (cần lấy từ `@username` hoặc `@id` của bot).
  - **Template thông báo phê duyệt**:
    ```
    🔍 Lead mới: {{ $node["On form submission"].json["name"] }}
    💰 Thu nhập: {{ $node["On form submission"].json["income"] }}
    📞 Số điện thoại: {{ $node["On form submission"].json["phone"] }}
    👍 Phê duyệt (YES) hoặc từ chối (NO)
    ```
  - **Chế độ "sendAndWait"** để chờ phản hồi trước khi tiếp tục.

##### **🔹 Bước 3: Tạo Email Cá Nhân Hóa & Folder Google Drive**
- **Node "Generate Personalized Email"** (googleGemini):
  - **Prompt mẫu**:
    ```
    Tạo email cá nhân hóa cho lead vay nhà:
    - Tên: {{ $node["On form submission"].json["name"] }}
    - Thu nhập: {{ $node["On form submission"].json["income"] }}
    - Số điện thoại: {{ $node["On form submission"].json["phone"] }}
    - Nội dung:
      "Chào {{ $node["On form submission"].json["name"] }},
      Tôi là [Tên của bạn] từ [Tên Công Ty]. Sau khi phê duyệt lead của bạn, tôi sẽ liên hệ để hỗ trợ vay nhà với điều kiện phù hợp.
      Vui lòng upload các tài liệu sau:
      1. CMND/CCCD
      2. Bảng lương
      3. Sổ tiết kiệm ngân hàng
      Link upload: [LINK DRIVE]
      Xin cảm ơn!"
    ```
  - **Cấu hình API Key** của Google Gemini trong `googlePalmApi`.

- **Node "Create Drive Folder"** (googleDrive):
  - **Điền tên folder**: `Lead_{{ $node["On form submission"].json["name"] }}_{{ $node["On form submission"].json["phone"] }}`.
  - **Folder cha**: Chọn folder đã cấu hình trước (ví dụ: `Mortgage Leads`).

##### **🔹 Bước 4: Chia Sẻ Folder & Yêu Cầu Upload Tài Liệu**
- **Node "Share Drive Folder"** (googleDrive):
  - **Chia sẻ với email** của khách hàng (được lấy từ form).
  - **Cấp quyền**: "Viewer" (đọc) hoặc "Editor" (sửa).

- **Node "Upload ID1", "Upload Payslip1", "Upload Bank Statement1"** (googleDrive):
  - **Cấu hình tên file**:
    - ID: `ID_{{ $node["On form submission"].json["name"] }}.pdf`
    - Payslip: `Payslip_{{ $node["On form submission"].json["name"] }}.pdf`
    - Bank Statement: `BankStatement_{{ $node["On form submission"].json["name"] }}.pdf`
  - **Lưu ý**: Các node này sẽ **chờ khách hàng upload** và trả về trạng thái thành công/thất bại.

##### **🔹 Bước 5: Kiểm Tra & Lưu Trữ**
- **Node "Check all uploads successful"** (if):
  - **Kiểm tra trạng thái upload** từ các node `Upload ID1`, `Upload Payslip1`, `Upload Bank Statement1`.
  - Nếu tất cả thành công → **lưu lead vào Supabase** và **gửi thông báo Telegram**.
  - Nếu có lỗi → **cập nhật log lỗi** và **gửi thông báo Telegram**.

- **Node "Store in Database"** (supabase):
  - **Cấu hình bảng**: `leads` (cần tạo trước trên Supabase).
  - **Cột cần lưu**: `name`, `phone`, `income`, `status`, `drive_folder_id`, `email_draft_id`.

##### **🔹 Bước 6: Gửi Thông Báo Kết Quả**
- **Node "Send Success Notification"** (telegram):
  - **Template thành công**:
    ```
    ✅ Lead {{ $node["On form submission"].json["name"] }} đã hoàn thành!
    📄 Tài liệu đã upload thành công.
    📁 Folder: [LINK DRIVE]
    ```
- **Node "Send Partial Failure Notification"** (telegram):
  - **Template lỗi**:
    ```
    ⚠️ Lead {{ $node["On form submission"].json["name"] }} có lỗi:
    - {{ $node["Evaluate upload results"].json["missing_files"] }}
    🔄 Vui lòng yêu cầu khách hàng upload lại.
    ```

#### **3. Kích Hoạt Workflow ⚡️**
- **Test Run**:
  - Nhập một lead mẫu vào form và kiểm tra từng node.
  - Đảm bảo **Telegram Bot** trả lời YES/NO cho yêu cầu phê duyệt.
- **Bật Active**:
  - Sau khi kiểm tra xong, **bật workflow** và **đặt lịch chạy tự động** (nếu cần).

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết Nối Slack/Email Thông Báo**:
   - Thêm node **Slack** hoặc **Email** để gửi thông báo thay vì chỉ Telegram.
   - Ví dụ: Sau khi phê duyệt, gửi email thông báo đến team.

2. **Lưu Log Chi Tiết**:
   - Sử dụng node **Supabase** để lưu **log hoạt động** (thời gian upload, người phê duyệt, trạng thái).

3. **Báo Cáo Định Kỳ**:
   - Tạo một workflow riêng để **tổng hợp báo cáo** từ Supabase và gửi qua **Google Sheets** hoặc **Email**.

4. **Tự Động Xóa Lead Sau Thời Gian**:
   - Thêm node **Supabase (Delete)** để xóa lead sau 30 ngày nếu không hoàn thành.

5. **Tùy Chỉnh Email Template**:
   - Sử dụng **Google Gemini** để tạo nhiều template email khác nhau cho từng loại lead (ví dụ: vay mua nhà, vay tiêu dùng).

---

### 📌 **Kết Luận: Tự Động Hóa Lead Vay Nhà Đã Đơn Giản**
Workflow này **giải phóng thời gian** của các sếp để tập trung vào việc **tăng doanh số và phục vụ khách hàng** thay vì làm thủ công. Bằng cách:
✔ **Lọc lead chất lượng** bằng AI và phê duyệt Telegram.
✔ **Tự động tạo email và quản lý tài liệu** trên Google Drive.
✔ **Lưu trữ và phân tích lead** trên Supabase.

**Hành động ngay hôm nay:**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với lead mẫu** để đảm bảo hoạt động.
3. **Bật workflow** và bắt đầu tự động hóa!

**🚀 Cần hỗ trợ thêm?** Đăng ký **VPS n8n** từ TinoHost để chạy workflow ổn định 24/7:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (Mã giảm giá: **VPSN8N**)

---
**Chúc các sếp thành công với việc tự động hóa lead vay nhà!** 🏡💰