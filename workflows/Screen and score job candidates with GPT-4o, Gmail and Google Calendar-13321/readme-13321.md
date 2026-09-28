---
title: "🤖 **Tự Động Học Viên Tiềm Năng với GPT-4o: Đánh Giá & Lựa Chọn Ứng Viên HR Mạnh Mẽ (Không Cần Code!)""
description: "Workflow tự động hóa đánh giá ứng viên từ CV PDF đến lịch phỏng vấn trên Google Calendar, giảm thời gian tuyển dụng 70% và loại bỏ thiên vị. Sử dụng GPT-4o, Gmail và Google Calendar để đánh giá toàn diện: tín hiệu ứng viên, xác thực CV, phù hợp văn hóa và kinh nghiệm."
slug: "tieu-dong-hoa-danh-gia-ung-vien-hr-gpt-4o"
tags: [n8n, automation, hr-automation, ai-summarization, gpt-4o, google-calendar, gmail-integration]
keywords: [tự động hóa tuyển dụng, đánh giá ứng viên AI, n8n workflow hr, gpt-4o tuyển dụng, google calendar tự động hóa]
---

# 🚀 **Tự Động Học Viên Tiềm Năng: Đánh Giá Ứng Viên HR với GPT-4o, Gmail & Google Calendar**

### **Giải pháp cho HR bị chìm trong hàng trăm CV mỗi ngày**
Các sếp HR đang phải mất **giờ đồng hồ** để đọc, đánh giá và lọc ứng viên từ hàng trăm CV PDF, email và form ứng tuyển. Thậm chí, việc **xác thực CV**, **đánh giá phù hợp văn hóa** hoặc **lên lịch phỏng vấn** còn phải làm thủ công, dẫn đến:
✅ **Thời gian tuyển dụng kéo dài** (thường mất 30-60 ngày)
✅ **Thiên vị không tự giác** (nhân viên đánh giá chủ quan)
✅ **Lỗi xác thực CV** (ứng viên giả mạo kinh nghiệm)
✅ **Scheduling phức tạp** (quên lịch, trùng lịch, không đồng bộ)

**Workflow này giải quyết tất cả!** Sử dụng **GPT-4o** (AI mạnh nhất hiện nay) để:
✔ **Trích xuất nội dung CV** từ PDF/Word tự động
✔ **Đánh giá ứng viên** theo 4 tiêu chí: **Tín hiệu ứng viên, Xác thực CV, Phù hợp văn hóa, Kinh nghiệm**
✔ **Gửi email tự động** cho ứng viên được chọn/làm lại
✔ **Lên lịch phỏng vấn** trên Google Calendar
✔ **Log kết quả** vào Google Sheets (nếu cần)

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Giảm thời gian tuyển dụng 70%** (từ 30 ngày xuống còn 7-10 ngày)
- **Loại bỏ thiên vị** với đánh giá tiêu chuẩn hóa bằng AI
- **Xác thực CV chính xác** (không còn lừa đảo kinh nghiệm)
- **Tự động lên lịch phỏng vấn** (không quên, không trùng lịch)
- **Tiết kiệm chi phí** (giảm công việc thủ công của HR)
- **Cá nhân hóa phản hồi** cho ứng viên (tự động gửi email)
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[**CHUẨN BỊ**]
Để workflow hoạt động, các sếp cần:
✅ **Tài khoản OpenAI** (API Key cho GPT-4o & GPT-4o-mini)
✅ **Tài khoản Gmail** (để gửi email tự động cho ứng viên)
✅ **Tài khoản Google Calendar** (để lên lịch phỏng vấn)
✅ **Form ứng tuyển** (có thể là Google Form, Typeform, hoặc webhook từ trang tuyển dụng)
✅ **File CV PDF/Word** (ứng viên nộp qua email hoặc form)
✅ **Mô hình đánh giá** (các tiêu chí đánh giá ứng viên, ví dụ: kinh nghiệm 3+ năm, phù hợp văn hóa công ty)
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể **import workflow** từ file JSON hoặc **copy/paste JSON** vào **n8n Editor**:
1. **Tải workflow** từ [n8n.io/workflows/13321](https://n8n.io/workflows/13321) (chọn **Export as JSON**)
2. **Mở n8n Editor** (trên VPS hoặc n8n.cloud)
3. **Nhấn "Import"** và chọn file JSON đã tải
4. **Hoặc copy toàn bộ JSON** và dán vào **Import Workflow** trong n8n

:::note[**Lưu ý quan trọng**]
- **Không thay đổi cấu trúc** của workflow (sắp xếp node theo thứ tự)
- **Không xóa node** trừ khi các sếp biết rõ tác dụng của nó
:::

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **A. Cấu hình OpenAI API (GPT-4o & GPT-4o-mini)**
- **Tại node "OpenAI Model - Orchestrator"** và các node khác (`Signal Agent`, `CV Agent`, `Trust Agent`, `Experience Agent`):
  - **Điền API Key** vào **Credentials** (tên: `openAiApi`)
  - **Không thay đổi model** (sử dụng `gpt-4o` cho Orchestrator, `gpt-4o-mini` cho các Agent khác)

#### **B. Cấu hình Gmail (Gửi email tự động)**
- **Tại node "Gmail Tool"**:
  - **Thêm credentials** mới (tên: `gmailOAuth2`)
  - **Chọn email chính** của công ty (để gửi email tự động)
  - **Cấu hình email mẫu** (có thể chỉnh sửa template trong node `Send Approval Email` và `Send Rejection Email`)

#### **C. Cấu hình Google Calendar (Lên lịch phỏng vấn)**
- **Tại node "Google Calendar Tool"**:
  - **Thêm credentials** mới (tên: `googleCalendarOAuth2Api`)
  - **Chọn calendar** muốn sử dụng (ví dụ: "Lịch phỏng vấn tuyển dụng")
  - **Điền thông tin lịch** (người chủ trì, địa điểm, mô tả)

#### **D. Cấu hình Form Trigger (Nhận CV từ ứng viên)**
- **Tại node "Candidate Application Form"**:
  - **Chọn loại trigger** phù hợp:
    - **Webhook** (nếu có API từ trang tuyển dụng)
    - **Google Form** (nếu ứng viên nộp qua Google Form)
    - **Email** (nếu ứng viên gửi CV qua email và workflow trích xuất từ đó)

#### **E. Cấu hình Prompt cho AI Agents (Nếu cần chỉnh sửa)**
- **Các node `agentTool`** (Signal Agent, CV Verification, Trust Assessment, Experience Agent) sử dụng **prompt mặc định** để đánh giá ứng viên.
- **Nếu muốn thay đổi tiêu chí đánh giá**, các sếp cần chỉnh sửa **content** trong node `Orchestrator Agent` và các Agent Tool tương ứng.
  - Ví dụ:
    ```json
    "prompt": "Bạn là một chuyên gia tuyển dụng. Đánh giá ứng viên dựa trên tiêu chí sau: [Điền tiêu chí cụ thể]"
    ```

#### **F. Cấu hình Email Template (Tự động gửi phản hồi)**
- **Tại node `Send Approval Email` và `Send Rejection Email`**:
  - **Chỉnh sửa nội dung email** để phù hợp với văn hóa công ty
  - **Thêm logo, link ứng tuyển mới** (nếu có)

---

### **3. Kích hoạt ⚡️**
1. **Test Run** với **dữ liệu mẫu** (ví dụ: một CV PDF mẫu)
   - Nhấn **Run Workflow** và kiểm tra kết quả:
     - AI có trích xuất nội dung CV không?
     - AI có đánh giá ứng viên theo 4 tiêu chí không?
     - Email tự động có gửi được không?
     - Lịch phỏng vấn có lên được không?
2. **Bật Active** khi đã kiểm tra xong

---

## ✍️ **Mẹo & gợi ý nâng cao**

### **1. Kết hợp với Google Sheets (Log kết quả)**
- **Thêm node `googleSheetsTool`** sau node `Log Results` để lưu kết quả đánh giá vào Google Sheets.
- **Cách làm**:
  - Tạo một sheet mới (ví dụ: "Đánh giá ứng viên")
  - Thêm credentials `googleSheetsOAuth2`
  - Chọn sheet và sheet name trong node

### **2. Gửi báo cáo định kỳ (Slack/Email)**
- **Thêm node `slackTool`** để gửi báo cáo tổng hợp hàng tuần.
- **Cách làm**:
  - Tạo một channel Slack (ví dụ: `#tuyen-dung`)
  - Thêm credentials `slackWebhook`
  - Chỉnh sửa message template để gửi báo cáo

### **3. Tự động chuyển ứng viên qua các stage**
- **Sử dụng node `googleCalendarTool`** để tự động chuyển ứng viên từ "Đã nộp" → "Đã phỏng vấn" → "Đã tuyển".
- **Cách làm**:
  - Tạo các event type trong Google Calendar (ví dụ: "Stage 1: Phỏng vấn kỹ thuật", "Stage 2: Phỏng vấn HR")
  - Cấu hình node `Google Calendar Tool` để tự động tạo event khi ứng viên được chọn

### **4. Chỉnh sửa tiêu chí đánh giá theo ngành nghề**
- **Nếu công ty tuyển dụng kỹ sư**, các sếp có thể chỉnh sửa prompt để AI đánh giá **kinh nghiệm kỹ thuật** hơn.
- **Nếu tuyển dụng marketing**, AI sẽ tập trung vào **kinh nghiệm branding, SEO, quảng cáo**.
- **Cách làm**:
  - Mở node `Orchestrator Agent` và chỉnh sửa **prompt** trong `content`.

### **5. Sử dụng Sticky Note để ghi chú**
- **Node `stickyNote`** cho phép các sếp **ghi chú thêm** về ứng viên (ví dụ: "Ứng viên này có liên hệ cũ", "Cần phỏng vấn thêm").
- **Cách làm**:
  - Chỉnh sửa nội dung trong node `stickyNote` để hiển thị ghi chú khi xem workflow.

---

## 📌 **Kết luận**
Workflow này **giải phóng HR khỏi công việc thủ công**, giúp các sếp:
✅ **Tuyển dụng nhanh chóng** (70% thời gian tiết kiệm)
✅ **Đánh giá công bằng** (không thiên vị)
✅ **Tự động hóa toàn bộ quy trình** (từ nhận CV đến phỏng vấn)
✅ **Cá nhân hóa phản hồi** cho ứng viên

**Hãy áp dụng ngay!** Nếu các sếp muốn **tùy chỉnh thêm**, có thể liên hệ với tác giả [Dr. Cheng Siong CHIN](https://n8n.io/workflows/13321) để xây dựng mô hình đánh giá riêng.

---
:::info[**Gợi ý hạ tầng cho n8n**]
Để workflow chạy **ổn định 24/7**, các sếp nên cài **n8n trên VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

**Bắt đầu tự động hóa tuyển dụng ngay hôm nay!** 🚀