---
title: "🚀 Tự Động Xem Xét & Đánh Giá CV Tài Năng Sử Dụng Google Gemini + Gmail (Không Cần Code)"
description: "Workflow tự động hóa HR giúp các sếp đánh giá CV ứng viên bằng AI Gemini, lưu trữ kết quả vào bảng dữ liệu, và tự động phân loại/ thông báo cho HR với email cá nhân hóa. Giúp tiết kiệm thời gian lên đến 80% trong quá trình tuyển dụng."
slug: "tieu-dong-xem-xet-danh-gia-cv-voi-google-gemini"
tags: [n8n, automation, hr, ai-summarization, google-gemini, no-code]
keywords: [tự động hóa tuyển dụng, đánh giá cv bằng ai, google gemini n8n, lưu trữ cv ứng viên, email tự động hr]
---

# 🚀 **Tự Động Xem Xét & Đánh Giá CV Tài Năng Sử Dụng AI Gemini + Gmail**

### **Giải Phóng Tay Sếp Từ Quá Trình Xem Xét CV Bằng AI**
Hiện nay, việc xem xét hàng chục, hàng trăm CV mỗi ngày khiến các sếp HR mệt mỏi và dễ bị bỏ lỡ những ứng viên tiềm năng. Thay vì phải đọc từng CV một, **workflow này tự động hóa toàn bộ quy trình**:
- **Trích xuất nội dung** từ file PDF CV.
- **Đánh giá tự động** bằng AI Gemini với hệ thống điểm số chi tiết.
- **Lưu trữ kết quả** vào bảng dữ liệu (Google Sheets/Excel).
- **Phân loại ứng viên** theo độ ưu tiên (cao/tiêu chuẩn).
- **Gửi email tự động** thông báo cho HR và ứng viên.

**Kết quả?** Các sếp tiết kiệm **80% thời gian** trong tuyển dụng, giảm thiểu sai sót, và tập trung vào việc phỏng vấn những ứng viên thực sự phù hợp.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 **[VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ cao cho AI)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Xem xét **50+ CV/ngày** chỉ trong vài giây.
✅ **Độ chính xác cao**: AI Gemini đánh giá khách quan dựa trên mô hình ngôn ngữ tiên tiến.
✅ **Phân loại tự động**: Ứng viên được chia thành **cao ưu tiên** (điểm cao) và **tiêu chuẩn** (điểm trung bình).
✅ **Lưu trữ dữ liệu**: Tất cả kết quả được ghi vào **bảng dữ liệu** (Google Sheets) để theo dõi lâu dài.
✅ **Email tự động**: HR và ứng viên nhận thông báo ngay lập tức.
✅ **Cá nhân hóa**: Email phản hồi được tự động hóa với nội dung phù hợp.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google** (để sử dụng **Google Gemini API** và **Gmail**).
2. **API Key Google Gemini**:
   - Đăng ký tại [Google AI Studio](https://aistudio.google.com/) và tạo **API Key**.
   - Thêm vào **Credentials** của n8n với tên `googlePalmApi`.
3. **Tài khoản Gmail** (để gửi email tự động):
   - Cấu hình **OAuth 2.0** trong n8n với tên `googleApi`.
4. **Bảng dữ liệu Google Sheets/Excel** (để lưu trữ thông tin ứng viên):
   - Tạo một **Google Sheet** mới và chia sẻ với n8n (quyền chỉnh sửa).
   - Cấu hình **Sheet Name** trong node `Save Candidate Info`.
5. **Form nhận CV** (cần thiết để bắt đầu workflow):
   - Sử dụng **Google Form**, **Typeform**, hoặc **n8n Form Trigger** để ứng viên tải CV (PDF).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/16030](https://n8n.io/workflows/16030) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON từ link trên và **paste** vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này gồm **11 node** quan trọng, các sếp cần cấu hình kỹ như sau:

##### **A. Node "When Form Submitted" (Bắt đầu từ Form)**
- **Cấu hình**:
  - Chọn **Google Form** hoặc **n8n Form Trigger** làm nguồn dữ liệu.
  - **Yêu cầu bắt buộc**:
    - Field `email` (để gửi email xác nhận).
    - Field `resume` (upload file PDF CV).

##### **B. Node "Set HR and Job Details" (Cài đặt thông tin HR & công việc)**
- **Điền thông tin**:
  - `hrEmail`: Email của sếp HR (ví dụ: `hr@congty.com`).
  - `companyName`: Tên công ty (ví dụ: "Công Ty TNHH ABC").
  - `jobTitle`: Tên vị trí tuyển dụng (ví dụ: "Chuyên Viên Marketing").
  - `jobDescription`: Mô tả công việc (sử dụng **Markdown** để dễ đọc).

##### **C. Node "Extract CV Text" (Trích xuất văn bản từ PDF)**
- **Lưu ý**:
  - Node này tự động trích xuất **toàn bộ văn bản** từ file PDF CV.
  - Nếu CV có **format đặc biệt**, có thể cần **cài đặt node `extractFromFile`** với **mô hình OCR** (nếu PDF là hình ảnh).

##### **D. Node "CV Screening Agent" (AI Gemini đánh giá CV)**
- **Cấu hình**:
  - **Prompt mẫu** (có thể tùy chỉnh):
    ```plaintext
    Analyze the following resume for the role of [Job Title] at [Company Name].
    Evaluate based on:
    1. Skills (50%)
    2. Experience (30%)
    3. Education (20%)
    Return a structured JSON with:
    - "score": number (0-100)
    - "skills": list of relevant skills
    - "recommendation": "High Priority" or "Standard"
    ```
  - **Lưu ý**:
    - Nếu AI trả về kết quả không chuẩn, cần **cập nhật `outputParserStructured`** để phù hợp.

##### **E. Node "Parse Analysis Output" (Phân tích kết quả AI)**
- **Cấu hình**:
  - **Schema JSON** phải khớp với output của Gemini (ví dụ):
    ```json
    {
      "score": 85,
      "skills": ["Python", "Machine Learning", "NLP"],
      "recommendation": "High Priority"
    }
    ```
  - Nếu AI trả về **dạng văn bản**, cần **tùy chỉnh regex** trong node này.

##### **F. Node "Save Candidate Info" (Lưu vào Google Sheets)**
- **Cấu hình**:
  - **Sheet Name**: Tên bảng (ví dụ: `Candidate_Assessment`).
  - **Headers**: Cần khớp với cột trong Google Sheets (ví dụ: `Email`, `Name`, `Score`, `Skills`, `Recommendation`).
  - **Operation**: Chọn `upsert` để **cập nhật** nếu ứng viên đã tồn tại.

##### **G. Node "Check Score Threshold" (Kiểm tra ngưỡng điểm)**
- **Cấu hình**:
  - **Score Threshold**: Đặt ngưỡng điểm (ví dụ: `70`).
    - Nếu `score >= 70` → **High Priority**.
    - Nếu `score < 70` → **Standard**.

##### **H. Node "Send Candidate Confirmation" (Gửi email xác nhận ứng viên)**
- **Cấu hình**:
  - **Template Email**: Tùy chỉnh nội dung (ví dụ):
    ```plaintext
    Chào [Candidate Name],

    Cảm ơn bạn đã gửi CV cho vị trí [Job Title] tại [Company Name].
    Chúng tôi sẽ liên hệ lại trong vòng 5-7 ngày làm việc.

    Trân trọng,
    Đội ngũ HR [Company Name]
    ```
  - **Dynamic Fields**: Sử dụng `{{ $json["email"] }}`, `{{ $json["name"] }}`.

##### **I. Node "Notify HR (High Priority)" & "Notify HR for Standard Candidate"**
- **Cấu hình**:
  - **Template Email cho HR**:
    - **High Priority**:
      ```plaintext
      Chào [HR Name],

      Ứng viên [Name] (Email: [Email]) đã được đánh giá **High Priority** với điểm số [Score].
      Skills: [Skills]

      Liên hệ ngay: [Candidate Email]
      ```
    - **Standard**:
      ```plaintext
      Chào [HR Name],

      Ứng viên [Name] (Email: [Email]) đã được đánh giá **Standard** với điểm số [Score].
      Skills: [Skills]

      Xem chi tiết: [Google Sheets Link]
      ```

---

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhập một **CV mẫu** vào form và chạy **Test Execution**.
   - Kiểm tra:
     - AI có đánh giá đúng không?
     - Email có gửi đúng không?
     - Dữ liệu có lưu vào Google Sheets không?
2. **Bật Active**:
   - Sau khi kiểm tra thành công, **bật workflow** và **đặt lịch chạy tự động** (nếu cần).

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack Webhook** hoặc **Telegram Bot** để thông báo ngay khi có ứng viên **High Priority**.
2. **Lưu log hoạt động**:
   - Sử dụng node **Sticky Note** hoặc **Google Drive** để ghi lại lịch sử đánh giá.
3. **Tự động gửi báo cáo định kỳ**:
   - Sử dụng **n8n Scheduler** để gửi **báo cáo tuần/month** về số lượng ứng viên, điểm trung bình, và phân loại.
4. **Tùy chỉnh mô hình đánh giá**:
   - Cập nhật **prompt** trong node `CV Screening Agent` để phù hợp với **mô tả công việc cụ thể** của công ty.
5. **Xử lý file CV khác**:
   - Nếu ứng viên gửi **Word/Excel**, cần thêm node **`extractFromFile`** với **mô hình trích xuất văn bản** khác.

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp HR khỏi công việc mệt mỏi là **xem xét CV thủ công**, đồng thời **tăng cường độ chính xác** nhờ AI Gemini. **Chỉ cần 5 phút cấu hình**, các sếp đã có một **hệ thống tuyển dụng tự động hóa hoàn chỉnh**.

**Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với CV mẫu** trước khi áp dụng cho thực tế.
3. **Tối ưu hóa email & prompt** để phù hợp với quy trình tuyển dụng của công ty.

**Nếu workflow này giúp tiết kiệm thời gian cho doanh nghiệp, hãy ủng hộ tác giả [Jay Nguyen](https://nguyenthieutoan.com) một ly cà phê qua [đây](https://nguyenthieutoan.com/payment/)** 😊.

---
**Cần hỗ trợ?** Đăng ký **VPS n8n** tại [TinoHost](https://tino.vn/vps-n8n?affid=388) và liên hệ **GenStaff** qua [Facebook](https://facebook.com/nguyenthieutoan) để được tư vấn chi tiết!