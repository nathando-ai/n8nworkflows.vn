---
title: "🤖 Tự Động Quét Thẻ Doanh Nghiệp với Gemini AI & Lưu Trữ Liên Lạc Trên Google Sheets & Lịch - Không Cần Code!"
description: "Workflow tự động hóa hoàn toàn quét, phân tích và lưu trữ thông tin từ thẻ doanh nghiệp bằng AI Gemini 2.5 Flash, đồng thời lập lịch theo dõi và chuẩn bị email gửi lại - tiết kiệm thời gian lên đến 80% cho các sếp!"
slug: "tieu-dong-quet-the-doanh-nghiep-gemini-ai-google-sheets"
tags: [n8n, automation, no-code, google-drive, google-sheets, google-calendar, gemini-ai, ai-summarization]
keywords: [tự động hóa quét thẻ doanh nghiệp, gemini ai n8n, lưu trữ liên lạc google sheets, lập lịch theo dõi email tự động, workflow n8n google drive]
---

# 🚀 **Tự Động Quét Thẻ Doanh Nghiệp với AI Gemini & Lưu Trữ Liên Lạc Mạnh Mẽ**

### **Nỗi Đau Của Các Sếp Khi Làm Thủ Công**
Các sếp đã từng phải:
- **Quét hàng chục thẻ doanh nghiệp** sau mỗi buổi hội nghị, hội thảo, hoặc sự kiện, mất thời gian lên đến **30-60 phút/ngày**.
- **Nhập liệu sai sót** do ghi nhớ không chính xác hoặc viết tay khó đọc, dẫn đến mất liên lạc quan trọng.
- **Quên theo dõi lại** sau khi trao đổi, khiến cơ hội hợp tác bị bỏ lỡ.
- **Không có hệ thống thống nhất** để lưu trữ và quản lý thông tin liên lạc, dẫn đến rối loạn dữ liệu.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Quét tự động** thẻ doanh nghiệp từ Google Drive.
✅ **Phân tích AI** bằng Gemini 2.5 Flash để trích xuất **14 trường thông tin** (tên, công ty, chức vụ, email, điện thoại, địa chỉ, website,...) với độ chính xác cao.
✅ **Lưu trữ tự động** vào Google Sheets với **15 cột chi tiết**, đồng thời **lập lịch theo dõi** trên Google Calendar và **chuẩn bị email gửi lại** sẵn.
✅ **Báo lỗi tự động** nếu quét không thành công (ảnh mờ, chữ khó đọc), giúp các sếp không bỏ sót bất kỳ thông tin nào.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian lên đến 80%** so với cách làm thủ công.
- **Độ chính xác cao** (AI Gemini phân tích và xác minh lại thông tin).
- **Lưu trữ hệ thống hóa** trên Google Sheets với **15 cột chi tiết**, dễ dàng tra cứu và phân tích.
- **Theo dõi tự động** với lịch hẹn trên Google Calendar và email gửi lại sẵn.
- **Không bỏ sót bất kỳ liên lạc nào** nhờ hệ thống báo lỗi tự động.
- **Hoàn toàn tự động hóa**, hoạt động **24/7** mà không cần can thiệp.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google** (Gmail, Google Drive, Google Sheets, Google Calendar) và **API Key của Gemini AI**.
2. **Folder "Business Cards"** trên Google Drive** (để lưu trữ ảnh thẻ doanh nghiệp).
   - *Lấy **Folder ID** từ URL của folder này (ví dụ: `https://drive.google.com/drive/folders/1AbCdEfGhIjKlMnOpQrStUvWxYz` → `1AbCdEfGhIjKlMnOpQrStUvWxYz`).
3. **Bảng Google Sheets** với **15 cột** sau:
   - Full Name, Company, Department, Job Title, Email, Phone, Mobile, Fax, Postal Code, Address, Website, Notes, Source File, Scanned At.
4. **Tài khoản Gmail** để nhận email báo lỗi và draft email gửi lại.
5. **N8n Self-hosted** (để workflow chạy 24/7 ổn định).
   :::info[Gợi ý hạ tầng cho n8n]
   Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
   :::
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/15701](https://n8n.io/workflows/15701) và import vào n8n Editor.
- **Copy/paste JSON** từ link trên vào n8n Editor (đường dẫn: `https://n8n.io/workflows/15701/raw`).

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **10 node** chính, các sếp cần cấu hình kỹ lưỡng các node sau:

##### **A. Node "New Card in Drive" (googleDriveTrigger)**
- **Chọn credentials**: `googleDriveOAuth2Api`.
- **Cấu hình**:
  - **Folder ID**: Nhập **Folder ID** của folder "Business Cards" trên Google Drive (lấy từ URL).
  - **File types**: Chỉ chọn `image/*` (ảnh thẻ doanh nghiệp).

##### **B. Node "Gemini 2.5 Flash" (lmChatGoogleGemini)**
- **Chọn credentials**: Nhập **API Key của Gemini AI** (mua tại [Google AI Studio](https://aistudio.google.com/)).
- **Prompt mẫu**:
  ```json
  {
    "role": "user",
    "content": "Extract structured contact information from this business card image. Return JSON with these fields: Full Name, Company, Department, Job Title, Email, Phone, Mobile, Fax, Postal Code, Address, Website, Notes."
  }
  ```

##### **C. Node "Contact Data Parser" (outputParserStructured)**
- **Chọn schema** phù hợp với **14 trường thông tin** từ Gemini.
- **Lưu ý**: Nếu Gemini trả về dữ liệu không chuẩn, cần chỉnh sửa **schema** để phù hợp.

##### **D. Node "Valid Extraction?" (if)**
- **Cấu hình điều kiện**:
  - **Name không rỗng** (`$json["Full Name"].trim() !== ""`).
  - **Độ tin cậy cao** (ví dụ: `$json["Confidence"] > 0.8`).

##### **E. Node "Save to Contact Sheet" (googleSheets)**
- **Chọn credentials**: `googleSheetsOAuth2Api`.
- **Cấu hình**:
  - **Spreadsheet ID**: Nhập **ID của bảng Google Sheets** (lấy từ URL).
  - **Sheet Name**: Chọn **tên sheet** (ví dụ: "Contacts").
  - **Range**: `A1` (để append dữ liệu từ hàng 1).

##### **F. Node "Schedule Follow-up" (googleCalendar)**
- **Chọn credentials**: `googleCalendarOAuth2Api`.
- **Cấu hình**:
  - **Event title**: `"Follow-up with $json['Full Name']"`.
  - **Start time**: `$now.plus({week: 1})` (lập lịch **1 tuần sau**).
  - **Description**: `"Please review and send follow-up email to $json['Email']"`.

##### **G. Node "Draft Follow-up Email" (gmail)**
- **Chọn credentials**: `gmailOAuth2Api`.
- **Cấu hình**:
  - **To**: `$json['Email']`.
  - **Subject**: `"Follow-up from our meeting"`.
  - **Body template**:
    ```html
    <p>Hi $json['Full Name'],</p>
    <p>It was great meeting you at [Event Name]. Here are some key points we discussed:</p>
    <p>1. [Point 1]</p>
    <p>2. [Point 2]</p>
    <p>Let me know if you'd like to schedule a follow-up call. Best regards, [Your Name]</p>
    ```

##### **H. Node "Send Error Alert" (gmail)**
- **Chọn credentials**: `gmailOAuth2Api`.
- **Cấu hình**:
  - **To**: Nhập **email của bạn** (để nhận báo lỗi).
  - **Subject**: `"Error: Failed to extract contact from $file.name"`.
  - **Body**: `"The business card $file.name could not be processed. Please check the image quality."`.

---

#### **3. Kích Hoạt ⚡️**
1. **Test run** với **1 ảnh thẻ doanh nghiệp mẫu** để kiểm tra workflow hoạt động như thế nào.
2. **Bật Active workflow** sau khi đã cấu hình hoàn chỉnh.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[TIẾP CẬN HƠN]
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack/Telegram Webhook** vào sau node **"Valid Extraction?"** để thông báo thành công/thất bại ngay trên chat nhóm.
2. **Lưu log hoạt động**:
   - Thêm node **StickyNote** để ghi lại lịch sử quét và kết quả.
3. **Gửi báo cáo định kỳ**:
   - Sử dụng node **Google Sheets** để tạo **báo cáo tổng hợp** hàng tuần/month về số lượng liên lạc mới được lưu trữ.
4. **Tự động chia sẻ với đội nhóm**:
   - Sau khi lưu vào Google Sheets, sử dụng node **Google Drive** để **tạo bản sao** của sheet cho các thành viên khác trong team.
5. **Cập nhật CRM**:
   - Nếu sử dụng **HubSpot, Salesforce, hoặc CRM khác**, thêm node **API CRM** để tự động đồng bộ dữ liệu.
:::

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc nhàn nhạt là quét và nhập liệu thẻ doanh nghiệp, đồng thời **tăng cường hiệu quả** trong việc theo dõi và quản lý liên lạc. **Không cần code**, chỉ cần **cấu hình vài bước đơn giản**, các sếp đã có một hệ thống **tự động hóa hoàn chỉnh** để quản lý thông tin liên lạc một cách chuyên nghiệp.

**Hãy áp dụng ngay và bắt đầu tự động hóa công việc của mình từ hôm nay!** 🚀

---
**🔗 [Tải workflow nguyên bản tại n8n.io](https://n8n.io/workflows/15701)**
**📌 [Cài đặt n8n Self-hosted trên VPS](https://docs.n8n.io/hosting/installation/installation-on-a-vps/)**