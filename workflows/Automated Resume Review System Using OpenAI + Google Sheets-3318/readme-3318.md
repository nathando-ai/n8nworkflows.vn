---
title: "🚀 Hệ Thống Đánh Giá Tự Động CV với OpenAI + Google Sheets - Giúp HR Tiết Kiệm 100% Thời Gian Chọn Người Tài Năng"
description: "Workflow tự động hóa đánh giá CV bằng AI, trích xuất thông tin chi tiết từ file PDF, tổng hợp và đánh giá tự động bằng OpenAI, lưu trữ kết quả vào Google Sheets. Giúp HR tiết kiệm 80% thời gian so sánh CV thủ công và tăng độ chính xác trong tuyển dụng."
slug: "automated-resume-review-system-openai-google-sheets"
tags: [n8n, automation, hr, ai, openai, google-sheets, no-code, langchain]
keywords: [tự động hóa tuyển dụng, đánh giá cv bằng ai, trích xuất thông tin từ pdf, google sheets tự động, openai trong n8n, workflow hr]
---

# 🚀 **Hệ Thống Đánh Giá CV Tự Động với OpenAI + Google Sheets: Giúp HR Tìm Người Tài Năng Chỉ Với 1 Clic**

## **💡 Nỗi Đau Của HR: So Sánh CV Thủ Công Làm Mất Thời Gian & Tiềm Năng Người Tài Năng**
Hàng ngày, các sếp HR phải:
- **Đọc và so sánh hàng trăm CV** thủ công, mất từ 1-3 giờ cho mỗi ứng viên.
- **Bị mất thông tin quan trọng** trong CV do không có công cụ trích xuất tự động.
- **Không có tiêu chuẩn đánh giá thống nhất**, dẫn đến quyết định tuyển dụng không khách quan.
- **Lưu trữ CV rối loạn**, khó theo dõi tiến trình đánh giá.

**Workflow này giải quyết tất cả vấn đề trên bằng AI + Tự Động Hóa 100% không cần code!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo bảo mật và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 80% thời gian** so sánh CV thủ công.
✅ **Trích xuất thông tin chính xác** từ CV (tên, học vị, kinh nghiệm, kỹ năng) bằng AI.
✅ **Đánh giá tự động** bằng OpenAI với hệ thống điểm (1-10) và nhận xét chi tiết.
✅ **Lưu trữ toàn bộ dữ liệu** vào Google Sheets, dễ theo dõi và phân tích.
✅ **Cá nhân hóa đánh giá** theo yêu cầu vị trí tuyển dụng (ví dụ: "Tìm kỹ sư Python có 3+ năm kinh nghiệm").
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google** (để kết nối Google Sheets & Google Drive).
2. **API Key OpenAI** (đăng ký tại [OpenAI](https://platform.openai.com/)).
3. **Google Sheet mẫu** (cấu trúc sẽ được tự động tạo khi workflow chạy đầu tiên).
4. **Form submission** (có thể sử dụng Google Forms hoặc tạo form đơn giản bằng n8n).

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Từ file JSON**
1. Tải workflow từ [n8n.io](https://n8n.io/workflows/3318) (chọn "Export").
2. Mở n8n Editor → Nhấn **"Import"** → Chọn file JSON vừa tải.
3. **Chọn "Create a new workflow"** và đặt tên (ví dụ: **"Resume Review System"**).

#### **Phương pháp 2: Copy/Paste JSON**
1. Copy toàn bộ mã JSON từ [n8n.io/workflows/3318](https://n8n.io/workflows/3318).
2. Trong n8n Editor → Nhấn **"Import"** → Chọn **"Paste JSON"** và dán mã.

---

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này có **12 node** quan trọng, các sếp cần cấu hình kỹ lưỡng:

#### **🔹 Node 1: "On form submission" (n8n-nodes-base.formTrigger)**
- **Cấu hình:**
  - Chọn **"Form"** (nếu sử dụng Google Forms) hoặc **"Manual Trigger"** (nếu muốn kích hoạt thủ công).
  - **Lưu ý:** Nếu dùng Google Forms, cần kết nối với **Google Sheets OAuth2** (sau này sẽ cấu hình ở node Google Sheets).

#### **🔹 Node 2-3: "Resume extraction" (n8n-nodes-base.extractFromFile)**
- **Cấu hình:**
  - **Operation:** Chọn **"PDF"** (nếu ứng viên upload CV dạng PDF).
  - **Credentials:** Không cần, nhưng cần đảm bảo file được upload đúng vào Google Drive (node sau sẽ xử lý).

#### **🔹 Node 4-5: "Personal Info" & "Qualification" (n8n-nodes-langchain.informationExtractor)**
- **Cấu hình:**
  - **Prompt:** Workflow đã tự động cấu hình sẵn, **không cần chỉnh sửa** (nếu muốn tối ưu, có thể cập nhật prompt để trích xuất thông tin cụ thể hơn).
  - **Example:**
    ```json
    "prompt": "Extract the following details from the resume text: {name, email, phone, city, education, work_experience}"
    ```

#### **🔹 Node 6: "wanted profile" (n8n-nodes-base.set)**
- **Cấu hình:**
  - Đây là **yêu cầu vị trí tuyển dụng** (ví dụ: "Kỹ sư Python có 3+ năm kinh nghiệm").
  - **Lưu ý:** Nếu muốn thay đổi, chỉnh sửa giá trị ở **`value`** trong node này.
  - **Ví dụ:**
    ```json
    "value": "Chúng tôi đang tìm kiếm một kỹ sư Python có kinh nghiệm trong phát triển backend, với ít nhất 3 năm kinh nghiệm trong Docker và AWS."
    ```

#### **🔹 Node 7: "OpenAI Chat Model" (n8n-nodes-langchain.lmChatOpenAi)**
- **Cấu hình:**
  - **Credentials:** Chọn **"openAiApi"** (cần đã cấu hình trước ở **Settings → Credentials**).
  - **Model:** Đã mặc định là **"gpt-4o-mini"** (rẻ và hiệu quả).
  - **Prompt:** Workflow tự động cấu hình, nhưng các sếp có thể **cập nhật để phù hợp với yêu cầu tuyển dụng**.
  - **Lưu ý:**
    - Nếu API Key hết hạn, workflow sẽ báo lỗi **"OpenAI API error"**.
    - Đảm bảo tài khoản OpenAI có **tiền để gọi API** (gpt-4o-mini ~0.15$/1M tokens).

#### **🔹 Node 8: "Summarizer" (n8n-nodes-langchain.chainSummarization)**
- **Cấu hình:**
  - **Model:** Đã mặc định là **"gpt-4o-mini"**.
  - **Prompt:** Tự động cấu hình, nhưng có thể **thêm yêu cầu cụ thể** (ví dụ: "Tóm tắt kinh nghiệm làm việc trong 3 câu").

#### **🔹 Node 9: "HR Expert" (n8n-nodes-langchain.chainLlm)**
- **Cấu hình:**
  - **Prompt:** Đây là **câu hỏi đánh giá** cho ứng viên (ví dụ: "Đánh giá ứng viên này cho vị trí [wanted profile] với thang điểm 1-10 và giải thích lý do").
  - **Ví dụ prompt mặc định:**
    ```json
    "prompt": "Based on the extracted resume data and the wanted profile, evaluate the candidate's fit for the role. Provide a score between 1-10 and explain why."
    ```
  - **Lưu ý:** Các sếp có thể **cập nhật prompt** để phù hợp với tiêu chuẩn đánh giá của công ty.

#### **🔹 Node 10-11: "Google Sheets" (n8n-nodes-base.googleSheets)**
- **Cấu hình:**
  - **Credentials:** Chọn **"googleSheetsOAuth2Api"** (cần đã cấu hình trước ở **Settings → Credentials**).
  - **Operation:** **"Append"** (thêm dữ liệu mới vào sheet).
  - **Sheet Name:** Đặt tên sheet (ví dụ: **"Resume Review Log"**).
  - **Lưu ý:**
    - Nếu sheet chưa tồn tại, workflow sẽ **tự động tạo** khi chạy lần đầu.
    - **Cấu trúc cột tự động** bao gồm: Tên ứng viên, Email, Điểm đánh giá, Tóm tắt CV, Yêu cầu vị trí, Ghi chú HR.

#### **🔹 Node 12: "Upload to google drive" (n8n-nodes-base.googleDrive)**
- **Cấu hình:**
  - **Credentials:** Chọn **"googleDriveOAuth2Api"** (cần đã cấu hình trước).
  - **Folder Path:** Chọn thư mục lưu CV (ví dụ: **"Resume Submissions"**).
  - **Lưu ý:** Nếu thư mục chưa tồn tại, workflow sẽ **tự động tạo**.

---

### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run (Kiểm tra dữ liệu mẫu):**
   - Nhấn **"Run"** trên node **"On form submission"**.
   - Upload một **CV PDF mẫu** (có thể là CV của bạn).
   - Kiểm tra kết quả:
     - Thông tin được trích xuất chính xác không?
     - Điểm đánh giá có hợp lý không?
     - Dữ liệu có được lưu vào Google Sheets không?

2. **Bật Active:**
   - Sau khi test thành công, nhấn **"Active"** ở góc trên bên phải.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **🔹 Kết Nối với Slack/Telegram để Báo Cáo Kết Quả**
- **Cách làm:**
  1. Thêm node **"Slack"** (n8n-nodes-base.slack) sau node **"Google Sheets"**.
  2. Cấu hình:
     - **Credentials:** Thêm Slack OAuth2 (cấu hình ở **Settings → Credentials**).
     - **Message:** Cấu hình tin nhắn tự động (ví dụ: `"🚀 CV mới được đánh giá: {json($.name)} - Điểm: {json($.score)}"`).
  3. Kết quả: Mỗi khi có CV mới, hệ thống sẽ **gửi tin nhắn tự động** lên Slack.

### **🔹 Lưu Log & Gửi Báo Cáo Định Kỳ**
- **Cách làm:**
  1. Thêm node **"HTTP Request"** (n8n-nodes-base.httpRequest) sau node **"Google Sheets"**.
  2. Cấu hình:
     - **Method:** POST
     - **URL:** Địa chỉ API của một **dịch vụ lưu log** (ví dụ: Logflare, Google Cloud Logging).
     - **Body:** `{ "resume_data": $json, "timestamp": $now }`
  3. **Kết quả:** Tất cả dữ liệu đánh giá sẽ được **lưu trung tâm** và có thể **xuất báo cáo định kỳ**.

### **🔹 Tối Ưu Hóa Prompt cho Đánh Giá Chuyên Nghiệp**
- **Cách làm:**
  - Mở node **"HR Expert"** và chỉnh sửa **prompt** để phù hợp với ngành nghề:
    - **Ví dụ cho kỹ sư phần mềm:**
      ```json
      "prompt": "Evaluate the candidate's fit for a Senior Software Engineer role. Focus on skills in Python, Docker, and AWS. Provide a score (1-10) and explain how their experience aligns with our tech stack."
      ```
    - **Ví dụ cho marketing:**
      ```json
      "prompt": "Assess the candidate for a Digital Marketing Specialist role. Prioritize skills in SEO, Google Ads, and social media strategy. Give a score (1-10) and suggest areas for improvement."
      ```

### **🔹 Sử Dụng Google Drive để Lưu CV & Tệp Đính Kèm**
- **Cách làm:**
  - Đảm bảo node **"Upload to google drive"** được cấu hình đúng **folder path**.
  - **Lưu ý:** Nếu muốn **xóa CV sau khi đánh giá**, thêm node **"Google Drive Delete"** sau node này.

---

## 📌 **Kết Luận: Tự Động Hóa Tuyển Dụng Bằng AI - Đã Đến Thời Điểm!**

Workflow này **giải phóng HR khỏi công việc thủ công**, giúp:
✔ **Tiết kiệm 80% thời gian** so sánh CV.
✔ **Tăng độ chính xác** trong tuyển dụng với AI đánh giá.
✔ **Lưu trữ dữ liệu chuyên nghiệp** vào Google Sheets.
✔ **Cá nhân hóa đánh giá** theo yêu cầu vị trí.

**Hành động ngay:**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với CV mẫu** để đảm bảo hiệu quả.
3. **Bật Active** và bắt đầu tự động hóa tuyển dụng!

**🚀 Nếu các sếp muốn tối ưu hơn, có thể:**
- **Kết nối với CRM** (HubSpot, Salesforce) để tự động chuyển CV phù hợp.
- **Thêm node Slack/Telegram** để báo cáo kết quả ngay khi có CV mới.
- **Tự động gửi email phản hồi** cho ứng viên (sử dụng node **n8n-nodes-base.email**).

**Chia sẻ workflow này với đồng nghiệp HR của mình để cùng tự động hóa tuyển dụng!** 💼🤖