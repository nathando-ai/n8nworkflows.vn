---
title: "🚀 Tự Động Hóa Xử Lý CV Tự Động Từ Google Drive Đến ClickUp Với GPT-4o & AI - Giảm Thời Gian Hiring 90%"
description: "Workflow tự động hóa hoàn toàn không cần code giúp HR tự động tải CV từ Google Drive, phân tích nội dung bằng GPT-4o, lưu dữ liệu vào Google Sheets và tạo nhiệm vụ tuyển dụng trên ClickUp. Giúp tiết kiệm 10+ giờ/ngày và giảm thiểu sai sót trong quá trình tuyển dụng."
slug: "tieu-dong-hoa-xu-ly-cv-tu-google-drive-den-clickup"
tags: [n8n, automation, hr, ai-summarization, google-drive, clickup, gpt-4o, self-hosted]
keywords: [tự động hóa tuyển dụng, n8n workflow cv, ai phân tích cv, google drive automation, clickup tự động hóa, gpt-4o trong tuyển dụng]
---

# 🚀 **Tự Động Hóa Xử Lý CV Từ Google Drive Đến ClickUp Với AI GPT-4o - Giải Pháp Tuyển Dụng 100% Không Code**

### **Nỗi Đau Của HR Trong Quá Trình Tuyển Dụng**
Các sếp HR thường phải mất **giờ đồng hồ** để:
- **Tải và phân loại** hàng trăm CV từ email, Google Drive hoặc ứng dụng tuyển dụng.
- **Nhập thủ công** thông tin vào bảng Excel/Google Sheets, dẫn đến **sai sót và mất thời gian**.
- **Phân tích từng CV** để đánh giá phù hợp với vị trí tuyển dụng, gây **chậm trễ trong quá trình tuyển dụng**.
- **Quên theo dõi** ứng viên sau khi gửi email xác nhận, dẫn đến **trải nghiệm ứng viên kém**.

**Workflow này giải quyết tất cả vấn đề trên bằng cách:**
✅ **Tự động tải CV** từ Google Drive khi mới được upload.
✅ **Phân tích AI** bằng GPT-4o để **trích xuất thông tin chính** (tên, email, kinh nghiệm, kỹ năng, học vấn).
✅ **Lưu dữ liệu** vào Google Sheets với **cấu trúc chuẩn**, dễ dàng theo dõi và phân tích.
✅ **Tạo nhiệm vụ tự động** trên ClickUp để **bắt đầu quá trình phỏng vấn** ngay lập tức.

---
## 🎯 **Kết Quả Các Sếp Nhận Được**

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/ngày** cho việc nhập liệu và phân tích CV.
- **Giảm sai sót** do nhập thủ công xuống **0%** nhờ AI tự động trích xuất.
- **Tăng tốc độ tuyển dụng** với **quá trình tự động hóa hoàn chỉnh** (từ tải CV đến tạo nhiệm vụ).
- **Dữ liệu trung tâm** trên Google Sheets, dễ dàng **lọc, sắp xếp và báo cáo**.
- **Tích hợp hoàn hảo** với ClickUp, giúp **quản lý tuyển dụng và phỏng vấn** một cách chuyên nghiệp.
- **Hoạt động 24/7** mà không cần can thiệp của con người.
:::

---
## 🔧 **Yêu Cầu Cần Thiết**

:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
✔ **Tài khoản Google Drive** (để lưu CV và kích hoạt trigger mới file).
✔ **Google Sheets** (để lưu trữ cơ sở dữ liệu ứng viên).
✔ **ClickUp** (để tạo nhiệm vụ tuyển dụng).
✔ **API Key Azure OpenAI** (để sử dụng GPT-4o trong phân tích CV).
✔ **Thư mục Google Drive** được đặt tên là **"Resume_store"** (hoặc cấu hình lại trong node trigger).
:::

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/8529](https://n8n.io/workflows/8529) và import vào n8n Editor.
- **Cách 2:** Copy toàn bộ JSON từ link trên và **paste vào n8n Editor** (trong tab "Import").
- **Cách 3:** Sử dụng **n8n CLI** để import:
  ```bash
  n8n import /path/to/workflow.json
  ```

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

#### **🔹 Node 1: Watch for New Resumes (Google Drive Trigger)**
- **Thiết lập folder:** Đặt tên folder là **"Resume_store"** (hoặc thay đổi trong `folderId`).
- **Thời gian refresh:** Cài đặt **1 phút** để nhanh chóng phát hiện CV mới.
- **Loại file:** Chỉ chọn **PDF** (AI không phân tích được file hình ảnh).

#### **🔹 Node 2: Download Resume File (Google Drive)**
- **Sử dụng credentials:** Chọn **"googleDriveOAuth2Api"** (đã cấu hình trước).
- **File ID:** Auto lấy từ node trigger, **không cần chỉnh sửa**.

#### **🔹 Node 3: Convert PDF to Text (ExtractFromFile)**
- **Chọn operation:** **"pdf"** (đã mặc định).
- **Kiểm tra output:** Nếu không xuất text, thử lại với file PDF khác (tránh file có hình ảnh).

#### **🔹 Node 4: AI Language Model (Azure OpenAI)**
- **Model:** Chọn **"gpt-4o-mini"** (rẻ và hiệu quả).
- **API Key:** Điền vào **"azureOpenAiApi"** (cấu hình trong n8n Credentials).
- **Prompt mẫu (có thể chỉnh sửa):**
  ```json
  {
    "instruction": "Extract structured data from the resume text. Return in JSON format with these keys: name, email, phone, years_of_experience, current_role, skills, education. If any field is missing, return 'N/A'.",
    "text": "{{$node["Convert PDF to Text"].json["text"]}}"
  }
  ```

#### **🔹 Node 5: Clean AI Response (Code)**
- **Mã JavaScript mặc định** đã xử lý:
  - Loại bỏ code block (````json```).
  - Chuyển JSON thành dạng chuẩn.
  - **Không cần chỉnh sửa** trừ khi có yêu cầu đặc biệt.

#### **🔹 Node 6: Save Candidate to Database (Google Sheets)**
- **Credentials:** Chọn **"googleSheetsOAuth2Api"**.
- **Sheet Name:** Đặt tên là **"Candidate Database"** (hoặc thay đổi).
- **Operation:** **"appendOrUpdate"** (tự động cập nhật nếu ứng viên cũ).

#### **🔹 Node 7: Create Hiring Task (ClickUp)**
- **Credentials:** Chọn **"clickUpApi"**.
- **Project ID:** Điền ID của dự án tuyển dụng trên ClickUp.
- **Task Title:** Sử dụng mẫu:
  `"{name} - Hiring Process"` (trích từ JSON của AI).
- **Assignee:** Chọn thành viên HR phụ trách tuyển dụng.

---
### **3. Kích Hoạt ⚡️**
1. **Test Run** với 1-2 CV mẫu để kiểm tra:
   - AI có trích xuất dữ liệu chính xác không?
   - Dữ liệu có lưu vào Google Sheets không?
   - Nhiệm vụ có tạo trên ClickUp không?
2. **Bật Active** workflow sau khi kiểm tra thành công.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **🔹 Tích Hợp Slack/Telegram để Báo Lệ**
- **Sử dụng node Slack/Telegram** sau node **"Save Candidate to Database"** để gửi thông báo:
  > *"📩 CV mới được xử lý: [Tên ứng viên] - [Email] - [Kỹ năng chính]"*

### **🔹 Lưu Log Lịch Sử**
- **Thêm node StickyNote** để ghi lại:
  - Thời gian xử lý.
  - Trạng thái (thành công/thất bại).
  - Dữ liệu đầu vào/đầu ra.

### **🔹 Gửi Báo Cáo Định Kỳ**
- **Sử dụng node Google Sheets + Email** để tự động gửi báo cáo hàng tuần:
  - Số lượng CV mới.
  - Ứng viên phù hợp nhất.
  - Thống kê kỹ năng phổ biến.

### **🔹 Cải Tiến Prompt AI**
- **Định hướng AI** để trích xuất thông tin cụ thể hơn:
  ```json
  {
    "instruction": "Extract skills in Vietnamese, not English. Also, add a confidence score (0-1) for each extracted field.",
    "text": "{{$node["Convert PDF to Text"].json["text"]}}"
  }
  ```

---
## 📌 **Kết Luận**

Workflow này **giải phóng HR khỏi công việc nhàn nhạt** như nhập liệu và phân tích CV, thay vào đó **tự động hóa toàn bộ quy trình tuyển dụng** từ đầu đến cuối. Với **AI GPT-4o**, dữ liệu được trích xuất chính xác và **tích hợp với ClickUp**, giúp quản lý tuyển dụng trở nên **nhanh chóng và chuyên nghiệp**.

**Hành động ngay:**
1. **Cài đặt n8n Self-hosted** trên VPS để workflow hoạt động 24/7.
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Upload CV đầu tiên** vào Google Drive và **nhận nhiệm vụ tuyển dụng tự động** trong vòng 2 phút!

👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) với mã giảm giá **VPSN8N** (giảm tới 39%) để tự động hóa quy trình tuyển dụng của doanh nghiệp!**

---