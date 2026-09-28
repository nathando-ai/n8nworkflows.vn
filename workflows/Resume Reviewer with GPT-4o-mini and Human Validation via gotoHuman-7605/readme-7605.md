---
title: "🚀 **Tự Động Hóa Xét Duyệt CV với GPT-4o-mini + Con Người (Human Validation) – Không Cần Code!**"
description: "Giải pháp tự động hóa hoàn toàn cho doanh nghiệp tuyển dụng: Upload CV PDF → Trích xuất nội dung → So sánh với mô tả công việc → Đánh giá tự động bằng AI + Xác nhận cuối cùng bởi con người. Tiết kiệm thời gian lên đến 80% so với cách làm thủ công!"
slug: "tieu-duong-cv-voi-gpt-4o-mini-va-human-validation"
tags: [n8n, automation, ai-summarization, gotoHuman, tuyển-dụng, no-code]
keywords: [tự động hóa tuyển dụng, n8n workflow cv, ai đánh giá cv, gotoHuman n8n, gpt-4o-mini tự động hóa, xét duyệt cv tự động]
---

# 🚀 **Tự Động Hóa Xét Duyệt CV với AI + Con Người – Không Cần Code!**

## **Nỗi Đau Của Các Sếp Trong Việc Xét Duyệt CV**
Hàng ngày, các sếp và nhân viên HR phải mất **giờ đồng hồ** để:
- **Quét và trích xuất** thông tin từ hàng trăm CV PDF.
- **So sánh** từng ứng viên với mô tả công việc chi tiết.
- **Đánh giá chủ quan** dựa trên kinh nghiệm, kỹ năng và phù hợp với văn hóa doanh nghiệp.
- **Lặp lại** quá trình này cho từng ứng viên, dẫn đến **sai sót** và **tốn thời gian** không cần thiết.

**Kết quả?** Các ứng viên phù hợp bị bỏ qua, trong khi những người không phù hợp lại được lọt qua vòng đầu tiên.

---
### **🎯 Giải Pháp Của Chúng Ta: Workflow Tự Động Hóa CV với AI + Con Người**
Dùng **n8n** kết hợp **GPT-4o-mini (OpenAI)** và **gotoHuman**, chúng ta xây dựng một **hệ thống tự động hóa hoàn chỉnh** để:
✅ **Trích xuất** toàn bộ nội dung từ CV PDF.
✅ **So sánh** với mô tả công việc (Job Description) và **đánh giá tự động** điểm số (0–100).
✅ **Tóm tắt** điểm mạnh/điểm yếu của ứng viên.
✅ **Gửi yêu cầu đánh giá** cho **con người** (HR/Manager) để **xác nhận cuối cùng**.
✅ **Lưu trữ** kết quả và **báo cáo** cho quản lý.

**Kết quả?** **Tiết kiệm 80% thời gian**, **giảm sai sót**, và **tăng chất lượng tuyển dụng**!

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài **n8n trên VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản Cloud.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ xử lý nhanh cho AI)
:::

---

### **🎯 Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ **5–10 giờ/tuần** xuống còn **1–2 giờ**, chỉ cần **xác nhận cuối cùng** thay vì làm thủ công.
- **Chính xác cao**: AI **so sánh tự động** với mô tả công việc, giảm **sai sót chủ quan**.
- **Cá nhân hóa đánh giá**: Mỗi ứng viên được **tóm tắt chi tiết** điểm mạnh/điểm yếu.
- **Hoạt động liên tục**: Workflow **chạy 24/7**, không phụ thuộc vào giờ làm việc của HR.
- **Báo cáo tự động**: Kết quả được **lưu trữ** và **gửi định kỳ** cho quản lý.
:::

---

### **🔧 Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản OpenAI** (và **API Key**) để sử dụng **GPT-4o-mini**.
✔ **Tài khoản gotoHuman** (và **API Key**) để **xác nhận cuối cùng** bởi con người.
✔ **Mô tả công việc (Job Description)** dưới dạng **text file** (sẽ được **set** trong workflow).
✔ **File PDF mẫu** để **test workflow** trước khi áp dụng thực tế.

---

## **🚀 Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/7605](https://n8n.io/workflows/7605) (chọn **Download JSON**).
2. **Mở n8n Editor** → Nhấn **Import** → Chọn file JSON vừa tải.
3. **Chọn "Import"** → Workflow sẽ xuất hiện trên **canvas**.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Tải JSON** từ link trên.
2. Trong **n8n Editor**, nhấn **Import** → Chọn **Paste JSON** → Dán nội dung file vào.
3. **Nhấn "Import"** → Workflow sẽ được tạo.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **🔹 Node 1: "Resume Submission" (formTrigger)**
- **Cấu hình form**:
  - Thêm **1 trường upload file** (kiểu **PDF**).
  - **Tên trường**: `resumeFile` (phải trùng với **key** trong node sau).
  - **Lưu ý**: Form này sẽ **chỉ hoạt động** khi **Active** và **URL** được chia sẻ với ứng viên.

#### **🔹 Node 2: "Extract from File" (extractFromFile)**
- **Chọn operation**: `pdf` (đã được cấu hình sẵn).
- **Lưu ý**:
  - Nếu file PDF **không có text** (chỉ hình ảnh), workflow sẽ **báo lỗi**.
  - **Test** với file PDF có **nội dung rõ ràng** trước khi áp dụng.

#### **🔹 Node 3: "Set Job Description" (set)**
- **Điền mô tả công việc**:
  - Mở **Sticky Note** (nút ghim) bên cạnh node này.
  - **Sửa nội dung** thành mô tả công việc của bạn (ví dụ: *"Chuyên viên Marketing cần có kinh nghiệm SEO, Content Writing, và quản lý mạng xã hội"*).
  - **Lưu ý**: Nếu không điền, AI sẽ **không so sánh** được với CV.

#### **🔹 Node 4: "Review Resume" (agent)**
- **Đây là node AI chính**:
  - **Input**:
    - `resumeText` (từ node **Extract from File**).
    - `jobDescription` (từ node **Set Job Description**).
  - **Output**:
    - `summary` (tóm tắt điểm mạnh/điểm yếu).
    - `score` (điểm số từ 0–100).
  - **Lưu ý**:
    - Nếu **score < 50**, AI sẽ **gợi ý loại bỏ** ứng viên.
    - Nếu **score > 70**, AI sẽ **khuyến nghị gọi phỏng vấn**.

#### **🔹 Node 5: "OpenAI Chat Model" (lmChatOpenAi)**
- **Chọn model**: `gpt-4o-mini` (đã được cấu hình sẵn).
- **Credentials**:
  - **Tên**: `openAiApi` (phải trùng với **credentials** trong n8n).
  - **API Key**: Điền **API Key** từ OpenAI (cần **nạp tiền** để sử dụng).
  - **Lưu ý**:
    - **GPT-4o-mini** rẻ hơn **GPT-4**, nhưng **chất lượng vẫn cao**.
    - Nếu **API Key hết hạn**, workflow sẽ **báo lỗi**.

#### **🔹 Node 6: "Send to GoToHuman" (gotoHuman)**
- **Credentials**:
  - **Tên**: `gotoHumanApi` (phải trùng với **credentials** trong n8n).
  - **API Key**: Điền **API Key** từ gotoHuman.
- **Review Template**:
  - **Template ID**: Nhập **ID template** từ gotoHuman (ví dụ: `SLFm3wk8I1kGuEmRbmIr`).
  - **Fields Mapping**:
    - `Resume` → `{{$('Extract from File').item.json.text}}` (nội dung CV).
    - `Summary` → `{{$json.output.summary}}` (tóm tắt AI).
    - `Rating` → `{{$json.output.score}}` (điểm số AI).
  - **Schema**:
    - `Resume (string)`, `Summary (string)`, `Rating (number)`.
  - **Lưu ý**:
    - **GoToHuman sẽ chờ** HR/Manager **xác nhận** trước khi tiếp tục workflow.
    - Nếu **không có người nào review**, workflow sẽ **bị treo**.

#### **🔹 Node 7: "Structured Output Parser" (outputParserStructured)**
- **Chỉ cần để mặc định** (n8n sẽ tự **parse** kết quả từ AI).
- **Lưu ý**:
  - Nếu **AI trả về format sai**, workflow sẽ **báo lỗi**.
  - **Test** với **1–2 CV** trước khi áp dụng toàn bộ.

---

### **3. Kích hoạt ⚡️**
1. **Test Run** với **1 file CV mẫu**:
   - Upload **PDF test** vào form.
   - Kiểm tra **output** từ mỗi node:
     - **Extract from File**: Có trích xuất được text không?
     - **Review Resume**: Điểm số và tóm tắt có hợp lý không?
     - **GoToHuman**: Có gửi yêu cầu review không?
2. **Bật Active workflow**:
   - Nhấn **Active** trên **canvas**.
   - **Chia sẻ URL form** với ứng viên (ví dụ: `https://tên-vps-của-bạn/n8n/workflows/123`).

---

## **✍️ Mẹo & gợi ý nâng cao**

### **🔹 1. Tối ưu hóa mô tả công việc (Job Description)**
- **Định dạng rõ ràng**:
  - **Yêu cầu kỹ năng**: *"Kinh nghiệm SEO từ 2 năm trở lên"*.
  - **Mô tả nhiệm vụ**: *"Quản lý content cho 5+ trang web"*.
- **Tránh từ khóa quá rộng**: *"Chuyên viên Marketing"* → *"Chuyên viên SEO & Content Marketing"*.

### **🔹 2. Kết hợp với Slack/Telegram để báo cáo**
- **Thêm node Slack/Telegram** sau **GoToHuman** để:
  ```json
  {
    "name": "Notify Slack",
    "type": "slackWebhook",
    "credentials": ["slackWebhook"],
    "keyParameters": {
      "text": "📄 CV mới được review: {{$json.output.resume}} \n📊 Điểm số: {{$json.output.score}} \n👤 Người review: {{$json.output.reviewer}}"
    }
  }
  ```
- **Lưu ý**: Cần **cài node Slack/Telegram** và **cấu hình webhook**.

### **🔹 3. Lưu log tất cả CV vào Google Sheets/Airtable**
- **Thêm node Google Sheets** sau **GoToHuman** để:
  ```json
  {
    "name": "Log to Google Sheets",
    "type": "googleSheets",
    "credentials": ["googleSheets"],
    "keyParameters": {
      "sheetName": "CV_Review_Log",
      "data": {
        "Resume": "{{$('Extract from File').item.json.text}}",
        "Summary": "{{$json.output.summary}}",
        "Score": "{{$json.output.score}}",
        "ReviewedBy": "{{$json.output.reviewer}}",
        "ReviewedAt": "{{$json.output.reviewedAt}}"
      }
    }
  }
  ```
- **Lưu ý**: Cần **cài node Google Sheets** và **cấu hình credentials**.

### **🔹 4. Gửi báo cáo định kỳ cho quản lý**
- **Thêm node Email (SendGrid/Mailgun)** để:
  ```json
  {
    "name": "Send Weekly Report",
    "type": "sendGrid",
    "credentials": ["sendGrid"],
    "keyParameters": {
      "to": "quanly@doanhnghiep.com",
      "subject": "Báo cáo xét duyệt CV tuần này",
      "html": "<h1>Tổng kết CV được review</h1><p>Tổng số CV: {{$json.length}}</p><p>Trung bình điểm số: {{($json.output.score | sum) / $json.length}}</p>"
    }
  }
  ```
- **Lưu ý**: Cần **cài node SendGrid** và **cấu hình credentials**.

---

## **📌 Kết luận**
### **🚀 Tại sao các sếp nên áp dụng ngay?**
- **Tiết kiệm thời gian** lên đến **80%** so với cách làm thủ công.
- **Giảm sai sót** do đánh giá chủ quan.
- **Tăng chất lượng tuyển dụng** với **AI + Con người**.
- **Hoạt động 24/7**, không phụ thuộc vào giờ làm việc của HR.

### **🔥 Bước tiếp theo**
1. **Test workflow** với **1–2 CV mẫu**.
2. **Cấu hình hoàn chỉnh** (OpenAI, GoToHuman, Job Description).
3. **Chia sẻ URL form** với ứng viên và **bắt đầu tự động hóa tuyển dụng!**

---
**💡 Cần hỗ trợ thêm?**
- **Robert Breen** (Tác giả workflow) có thể **custom hóa** cho doanh nghiệp của các sếp:
  📧 [robert@ynteractive.com](mailto:robert@ynteractive.com)
  🔗 [LinkedIn](https://www.linkedin.com/in/robert-breen-29429625/)
  🌐 [ynteractive.com](https://ynteractive.com)

---
**🎁 Đăng ký VPS n8n với mã giảm giá VPSN8N để chạy workflow ổn định!**
👉 **[TinoHost](https://tino.vn/vps-n8n?affid=388)** (Giảm **39%**)
👉 **[BNIX](https://my.bnix.one