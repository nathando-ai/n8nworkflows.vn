---
title: "🚀 Tự Động Hóa Ứng Tuyển & Theo Dõi Trạng Thái Với LinkedIn, Indeed & Google Sheets - Giảm 90% Thời Gian Tìm Việc"
description: "Workflow tự động hóa ứng tuyển việc làm, theo dõi trạng thái ứng tuyển hàng ngày, và gửi thông báo email tự động từ Google Sheets đến LinkedIn/Indeed. Giúp các sếp tiết kiệm 10+ giờ/tuần và tối ưu hóa quá trình tìm việc."
slug: "tự-dộng-hoa-ung-tuyen-linkedin-indeed-google-sheets"
tags: [n8n, automation, tìm-việc, google-sheets, linkedin-indeed, email-notification]
keywords: [n8n tự động hóa ứng tuyển, theo dõi trạng thái ứng tuyển, LinkedIn Indeed API, tự động hóa tìm việc, Google Sheets ứng tuyển, email tự động ứng tuyển]
---

# 🚀 **Tự Động Hóa Ứng Tuyển & Theo Dõi Trạng Thái Việc Làm - Giảm 90% Công Việc Thủ Công**

### **Nỗi Đau Của Các Sếp Khi Tìm Việc Làm**
Hàng ngày, các sếp phải:
- **Tìm kiếm và sao chép** thông tin việc làm từ LinkedIn, Indeed, và các trang tuyển dụng khác.
- **Tự động hóa ứng tuyển** với hàng chục ứng dụng mỗi tuần, nhưng vẫn phải viết cover letter riêng cho mỗi công ty.
- **Theo dõi trạng thái ứng tuyển** bằng cách nhắc nhở mình hoặc ghi chép vào Excel, dễ bị quên hoặc sai sót.
- **Gửi email thông báo** cho bản thân hoặc đồng nghiệp khi có phản hồi từ nhà tuyển dụng.

**Kết quả?** Thời gian và năng lượng bị "chôn vùi" trong công việc thủ công, trong khi các ứng viên khác đã được ưu tiên xử lý.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tuần** với việc tự động hóa ứng tuyển và theo dõi trạng thái.
- **Chính xác 100%** với việc cập nhật trạng thái tự động từ LinkedIn/Indeed.
- **Cá nhân hóa ứng tuyển** với cover letter tự động sinh thành từ dữ liệu Google Sheets.
- **Hoạt động 24/7** mà không cần can thiệp thủ công.
- **Lưu trữ toàn bộ lịch sử** ứng tuyển trong Google Sheets, dễ dàng phân tích và báo cáo.
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow này hoạt động, các sếp cần chuẩn bị:
1. **Google Sheets** với cấu trúc dữ liệu chuẩn (xem chi tiết dưới đây).
2. **Tài khoản Gmail** để gửi email thông báo tự động.
3. **Tài liệu CV** được lưu trên Google Drive (để tự động đính kèm khi ứng tuyển).
4. **API Key của LinkedIn/Indeed** (nếu muốn kết nối thực tế; hiện workflow sử dụng mock data).
5. **Thời gian** để cấu hình ban đầu (~30 phút).
:::

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Bước 1:** Tải file JSON từ [n8n.io/workflows/5906](https://n8n.io/workflows/5906) hoặc copy toàn bộ JSON từ trang này.
- **Bước 2:** Mở **n8n Editor** và chọn **"Import Workflow"** → Dán JSON hoặc tải file JSON.
- **Bước 3:** Chọn **"Create Workflow"** để lưu vào hệ thống của bạn.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **2 phần chính**:
- **Phần 1: Ứng Tuyển Tự Động** (chạy hàng ngày).
- **Phần 2: Theo Dõi Trạng Thái** (chạy hàng 2 ngày).

##### **📌 Cấu Hình Google Sheets**
- **Node "📖 Read Jobs Sheet" & "📖 Read Applied Jobs":**
  - Điền **Spreadsheet ID** từ liên kết Google Sheets (ví dụ: `https://docs.google.com/spreadsheets/d/SPREADSHEET_ID/edit` → `SPREADSHEET_ID`).
  - Chọn **Sheet Name** là tên tab chứa dữ liệu (ví dụ: `"Job Listings"`).
  - **Cấu trúc cột bắt buộc** (xem chi tiết dưới đây).

- **Node "📝 Prepare Application Data":**
  - Thêm **URL CV** (Google Drive link) vào trường `resumeUrl`.
  - Cấu hình **template cover letter** trong `coverLetterTemplate` (sử dụng biến `${job.Title}` để thay thế tên công việc).

##### **📌 Cấu Hình Email Notification**
- **Node "📧 Send Application Notification" & "📧 Send Status Update":**
  - Chọn **Gmail Credentials** (cài đặt trước trong n8n).
  - Điền **email nhận** (ví dụ: `email@của-bạn.com`).
  - **Thêm biến** vào email template:
    ```json
    {
      "subject": "📩 Ứng tuyển việc làm: ${job.Title} đã được gửi!",
      "text": "Xin chào,\n\nBạn đã tự động ứng tuyển cho vị trí ${job.Title} tại ${job.Company}.\n\nChi tiết: ${job.Job_URL}\n\nTrạng thái: ${job.Status}",
      "html": "<p>Xin chào,<br><br>Bạn đã tự động ứng tuyển cho vị trí <strong>${job.Title}</strong> tại <strong>${job.Company}</strong>.<br><br><a href='${job.Job_URL}'>Xem chi tiết</a><br><br>Trạng thái: <strong>${job.Status}</strong></p>"
    }
    ```

##### **📌 Cấu Hình API LinkedIn/Indeed (Nâng Cao)**
- **Hiện tại**, workflow sử dụng **mock data** cho LinkedIn và Indeed.
- **Để kết nối thực tế**, các sếp cần:
  - **LinkedIn:** Sử dụng **API LinkedIn Recruiter** (nếu có quyền truy cập).
  - **Indeed:** Sử dụng **Indeed API** (đăng ký tại [Indeed Developer Portal](https://developer.indeed.com/)).
  - **Cập nhật node "💼 Apply via LinkedIn" & "🔍 Apply via Indeed"** với URL API và headers xác thực.

##### **📌 Cấu Hình Cron Job**
- **Node "🕘 Daily Application Trigger":**
  - Thiết lập **lịch chạy hàng ngày** (ví dụ: `0 8 * * *` để chạy lúc 8h sáng).
- **Node "🕐 Status Check Trigger":**
  - Thiết lập **lịch chạy hàng 2 ngày** (ví dụ: `0 8 */2 * *` để chạy lúc 8h sáng, ngày lẻ).

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
1. **Kết Nối Slack/Telegram:**
   - Thêm **node Slack/Telegram** sau các node gửi email để thông báo tức thời.
   - Ví dụ: Sau `"📧 Send Status Update"`, thêm node `webhook` để gửi tin nhắn Slack.

2. **Lưu Log Lịch Sử:**
   - Thêm **node StickyNote** để ghi lại lịch sử ứng tuyển và trạng thái.
   - Ví dụ: Sau `"📝 Update Job Status"`, thêm node `stickyNote` với nội dung:
     ```json
     {
       "key": "application_history",
       "value": {
         "jobId": "{{$node["📝 Update Job Status"].json()["Job_ID"]}}",
         "status": "{{$node["📝 Update Job Status"].json()["Status"]}}",
         "timestamp": "{{$node["📝 Update Job Status"].json()["Last_Checked"]}}"
       }
     }
     ```

3. **Báo Cáo Định Kỳ:**
   - Sử dụng **node Google Sheets** để tạo **báo cáo tổng hợp** hàng tháng.
   - Ví dụ: Tạo một sheet mới với dữ liệu tổng hợp từ `"Job Listings"` và gửi email báo cáo tự động.

4. **Tối Ưu Hóa Cover Letter:**
   - Sử dụng **LLM (n8n-node-llm)** để sinh cover letter cá nhân hóa.
   - Thêm node `n8n-node-llm` sau `"📝 Prepare Application Data"` với prompt:
     ```json
     {
       "prompt": "Tạo một cover letter chuyên nghiệp cho vị trí {{job.Title}} tại {{job.Company}}. Đảm bảo nhắc đến kinh nghiệm {{job.Requirements}} và lý do bạn phù hợp với vị trí này. Sử dụng giọng điệu chuyên nghiệp và ngắn gọn.",
       "model": "gpt-3.5-turbo"
     }
     ```

---
### **📌 Cấu Trúc Google Sheets Chuẩn**
Workflow này yêu cầu **Google Sheets** với các cột sau (đặt tên chính xác):

| **Tên Cột**          | **Loại Dữ liệu** | **Mô Tả**                          |
|-----------------------|------------------|-------------------------------------|
| `Job_ID`              | Text             | Mã duy nhất cho mỗi việc làm        |
| `Company`             | Text             | Tên công ty tuyển dụng              |
| `Position`            | Text             | Tiêu đề công việc                  |
| `Status`              | Text             | `Not Applied`, `Applied`, `Interview`, `Rejected`, `Hired` |
| `Applied_Date`        | Date             | Ngày ứng tuyển                     |
| `Last_Checked`        | Date             | Ngày cuối cùng kiểm tra trạng thái  |
| `Application_ID`      | Text             | ID ứng tuyển từ LinkedIn/Indeed     |
| `Notes`               | Text             | Ghi chú thêm (nếu có)               |
| `Job_URL`             | URL              | Link trực tiếp việc làm             |
| `Priority`            | Text             | `High`, `Medium`, `Low`             |
| `Resume_URL`          | URL              | Link CV (Google Drive)               |
| `Cover_Letter_Template`| Text            | Template cover letter (nếu có)       |

---
### **🔧 Cách Cài Đặt Hệ Thống N8N 24/7**
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)**
:::

---
### **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào việc **nâng cao kỹ năng** và **phỏng vấn** thay vì mắc kẹt trong công việc thủ công. Với **tự động hóa ứng tuyển và theo dõi trạng thái**, bạn sẽ:
✅ **Áp dụng nhiều hơn** với cùng một nỗ lực.
✅ **Không bỏ lỡ bất kỳ cơ hội nào** nhờ thông báo tự động.
✅ **Tối ưu hóa quá trình tìm việc** như một chuyên gia.

**Hành động ngay hôm nay!**
1. **Import workflow** vào n8n của bạn.
2. **Cấu hình Google Sheets** và email.
3. **Bật Active** và bắt đầu tự động hóa!

---
**💡 Lưu ý cuối cùng:**
- **Không sử dụng mock data** trong sản xuất. Thay vào đó, **cập nhật API LinkedIn/Indeed** để kết nối thực tế.
- **Backup Google Sheets** định kỳ để tránh mất dữ liệu.
- **Monitor logs** trong n8n để phát hiện lỗi nếu có.

**Chúc các sếp thành công trong việc tìm việc và tự động hóa cuộc sống!** 🚀