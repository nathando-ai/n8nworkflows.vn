---
title: "🤖 Tự Động Học Vị & Đánh Giá Ứng Viên HR Với GPT-4.1 + Dữ Liệu LinkedIn (CSV/XLSX) - Giảm 80% Thời Gian Làm Thủ Công"
description: "Workflow tự động hóa hoàn toàn không cần code để phân tích hồ sơ ứng viên từ CSV/XLSX, enrich dữ liệu LinkedIn thông qua Apify, đánh giá AI với GPT-4.1, và tự động hóa báo cáo với Google Sheets. Giảm thời gian từ 15-20 phút xuống chỉ vài giây cho mỗi ứng viên."
slug: "tieu-dong-hoa-danh-gia-ung-vien-hr-gpt-4-1-linkedin"
tags: [n8n, automation, no-code, ai, linkedin, google-sheets, openai, apify]
keywords: [tự động hóa tuyển dụng, đánh giá ứng viên AI, n8n workflow, enrich linkedin, gpt-4.1 tự động hóa, csv xlsx tự động hóa]
---

# 🚀 **Tự Động Học Vị & Đánh Giá Ứng Viên HR Với GPT-4.1 + Dữ Liệu LinkedIn (CSV/XLSX)**

### **Giải pháp cho các sếp HR:**
Hiện nay, việc tuyển dụng ứng viên chất lượng là thách thức lớn đối với các doanh nghiệp. Các sếp thường phải:
- **Làm thủ công** phân tích hồ sơ từ hàng trăm ứng viên (CSV/XLSX).
- **Tốn thời gian** để tra cứu thông tin LinkedIn (bài viết gần đây, hoạt động chuyên môn).
- **Khó đánh giá** khách quan dựa trên các tiêu chí như kỹ năng, kinh nghiệm, và phù hợp với văn hóa doanh nghiệp.
- **Không có hệ thống tự động** để cập nhật và báo cáo kết quả.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động hóa hoàn toàn** từ upload hồ sơ đến đánh giá AI.
✅ **Enrich dữ liệu LinkedIn** (3 bài viết gần nhất của ứng viên) thông qua Apify.
✅ **Đánh giá AI với GPT-4.1** (điểm 0-100) + giải thích chi tiết (tùy chọn tiếng Hebrew).
✅ **Tự động hóa báo cáo** với Google Sheets (sắp xếp, lọc, định dạng chuyên nghiệp).
✅ **Báo lỗi tự động** qua email nếu có vấn đề trong quá trình xử lý.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian:** Giảm từ **15-20 phút/ứng viên** xuống **chỉ vài giây**.
- **Đánh giá khách quan:** AI đánh giá ứng viên dựa trên **tiêu chí chuẩn hóa** (kỹ năng, kinh nghiệm, phù hợp văn hóa).
- **Dữ liệu LinkedIn enrich:** Lấy **3 bài viết gần nhất** của ứng viên để đánh giá hoạt động chuyên môn.
- **Báo cáo tự động:** Google Sheets được **sắp xếp, lọc, định dạng** theo điểm số và tiêu chí.
- **Báo lỗi tự động:** Nếu có lỗi trong quá trình xử lý, hệ thống sẽ **gửi email cảnh báo** cho admin.
- **Chi phí thấp:** **~$0.05/ứng viên** (do sử dụng GPT-4.1 và API LinkedIn).
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản và API Keys:**
   - **Google Drive & Google Sheets:** OAuth2 API (để upload/download file và quản lý bảng tính).
   - **OpenAI API Key:** Để sử dụng GPT-4.1 (mua tại [OpenAI](https://platform.openai.com/)).
   - **Apify API Key:** Để enrich dữ liệu LinkedIn (mua tại [Apify](https://apify.com/)).
   - **Gmail OAuth2:** Để gửi email cảnh báo lỗi (nếu cần).

2. **File mẫu:**
   - File **CSV/XLSX** chứa dữ liệu ứng viên (cột cần thiết: `name`, `email`, `linkedin_url`, `skills`, `experience`).
   - **Google Sheet** để lưu kết quả đánh giá (cần tạo trước và chia sẻ quyền chỉnh sửa).

3. **Cấu hình thêm:**
   - **Prompt cho GPT-4.1:** Các sếp có thể tùy chỉnh yêu cầu đánh giá (ví dụ: yêu cầu giải thích bằng tiếng Việt thay vì Hebrew).
   - **Cấu hình Apify:** Chọn **Actor** phù hợp để lấy dữ liệu LinkedIn (ví dụ: [LinkedIn Profile Scraper](https://apify.com/elayguez/linkedin-profile-scraper)).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/8775](https://n8n.io/workflows/8775) và import vào **n8n Editor**.
- **Cách 2:** Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/8775) và paste vào **Create Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **5 bước chính**, các sếp cần chú ý cấu hình các node sau:

##### **📌 Bước 1: Upload & Chuẩn bị Dữ liệu (Nodes: `formTrigger`, `googleDrive`, `extractFromFile`)**
- **Node `formTrigger`:**
  - Tạo **form upload file** cho ứng viên (CSV/XLSX) hoặc sử dụng **Google Drive** để upload trực tiếp.
  - **Lưu ý:** File cần có **cột bắt buộc** như `name`, `linkedin_url`, `skills`, `experience`.
- **Node `googleDrive` (Upload/Download):**
  - Chọn **credentials `googleDriveOAuth2Api`** đã cấu hình trước.
  - **File mẫu:** Các sếp có thể tạo một file mẫu CSV/XLSX để test (ví dụ: [mẫu này](https://docs.google.com/spreadsheets/d/1XYZ/edit)).

##### **📌 Bước 2: Chuẩn bị Dữ liệu cho AI (Nodes: `code`, `set`, `merge`)**
- **Node `Format Columns1` (Code):**
  - Mở **Code Editor** và chỉnh sửa logic để **đảm bảo dữ liệu đúng định dạng** (ví dụ: chuyển đổi `skills` thành mảng JSON).
  - **Mẫu code tham khảo:**
    ```javascript
    // Chuyển đổi cột skills thành mảng JSON
    return {
      json: {
        ...node.inputData,
        skills: JSON.parse(node.inputData.skills.replace(/'/g, '"'))
      }
    };
    ```
- **Node `Set` (Format Columns):**
  - Đảm bảo các cột như `name`, `linkedin_url` được **định dạng chuẩn** trước khi gửi cho AI.

##### **📌 Bước 3: Enrich Dữ liệu LinkedIn (Nodes: `apifyTool`, `merge`)**
- **Node `Run an Actor in Apify`:**
  - Chọn **Actor** phù hợp (ví dụ: [LinkedIn Profile Scraper](https://apify.com/elayguez/linkedin-profile-scraper)).
  - **Cấu hình:**
    - Input: `linkedin_url` từ file CSV/XLSX.
    - Output: Lấy **3 bài viết gần nhất** của ứng viên.
  - **Lưu ý:** Apify có **limit free tier**, các sếp cần mua **API Key** nếu xử lý nhiều ứng viên.
- **Node `Merge1`:**
  - Ghép dữ liệu **CSV gốc** với **dữ liệu LinkedIn enrich** để tạo input cho AI.

##### **📌 Bước 4: Đánh Giá AI với GPT-4.1 (Nodes: `lmChatOpenAi`, `agent`, `outputParserStructured`)**
- **Node `GPT-4.1` (lmChatOpenAi):**
  - **Prompt mẫu** (có thể tùy chỉnh):
    ```
    Analyze the candidate profile based on the following criteria:
    1. Skills (must match job requirements)
    2. Recent LinkedIn activity (last 3 posts)
    3. Experience (years, industries, achievements)
    4. Cultural fit (alignment with company values)
    Assign a score from 0-100 and provide a detailed explanation in Vietnamese.
    ```
  - **Cấu hình:**
    - Model: `gpt-4-1`.
    - Input: Dữ liệu ghép từ `Merge1` (CSV + LinkedIn).
    - **Lưu ý:** Chi phí ~$0.05/ứng viên (do sử dụng GPT-4.1).
- **Node `Structured Output Parser1`:**
  - Chỉ định **schema output** để AI trả về **dữ liệu có cấu trúc** (ví dụ: `{"score": 85, "explanation": "..."}`).

##### **📌 Bước 5: Lưu Kết Quả & Báo Cáo (Nodes: `googleSheets`, `switch`, `gmail`)**
- **Node `Convert to Google Sheet`:**
  - Chọn **Google Sheet** đã tạo trước và **chia sẻ quyền chỉnh sửa**.
  - **Cấu hình:**
    - Operation: `appendOrUpdate`.
    - Cột cần thêm: `ai_score`, `ai_explanation`, `linkedin_posts`.
- **Node `Send a message` (gmail):**
  - **Báo lỗi tự động:** Nếu có lỗi trong quá trình xử lý (ví dụ: API fail, file không đúng định dạng), hệ thống sẽ **gửi email cảnh báo** cho admin.
  - **Cấu hình:**
    - Chọn **credentials `gmailOAuth2`**.
    - Nội dung email mẫu:
      ```
      Error occurred in workflow "Candidate Evaluation":
      - Error: {{$node.error.message}}
      - Candidate: {{$node.inputData.name}}
      ```

##### **📌 Node quan trọng khác:**
- **`AI Agent`:** Tùy chọn để **tự động hóa các bước phức tạp** (ví dụ: gọi API, xử lý lỗi).
- **`Error Trigger`:** Đảm bảo **tất cả lỗi** được bắt và báo cáo.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run:**
   - Upload **file mẫu CSV/XLSX** (ví dụ: [mẫu này](https://docs.google.com/spreadsheets/d/1XYZ/edit)).
   - Kiểm tra **Google Sheet** và **email** để xác nhận kết quả.
2. **Bật Active:**
   - Sau khi test thành công, **bật workflow** và **lưu lại**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tùy chỉnh Prompt cho GPT-4.1:**
   - Thay đổi yêu cầu đánh giá để phù hợp với **mô hình tuyển dụng** của doanh nghiệp (ví dụ: ưu tiên kỹ năng mềm).
   - **Ví dụ:** Yêu cầu AI **so sánh ứng viên với top 3 ứng viên đã tuyển trước đó**.

2. **Lưu Log & Audit:**
   - Sử dụng **Google Sheets** để lưu **lịch sử đánh giá** (cột `created_at`, `updated_at`).
   - **Mẹo:** Tạo **bảng tính riêng** để theo dõi **tỷ lệ thành công** của workflow.

3. **Kết hợp với Slack/Telegram:**
   - Sử dụng **node `webhook`** để gửi **kết quả đánh giá** lên Slack/Telegram khi có ứng viên mới.
   - **Cấu hình:**
     - Tạo **webhook** tại Slack/Telegram.
     - Thêm node `httpRequest` để gửi thông báo.

4. **Báo cáo Định Kỳ:**
   - Sử dụng **Google Apps Script** hoặc **n8n Schedule Node** để **tự động gửi báo cáo** hàng tuần/tháng.
   - **Ví dụ:** Báo cáo top 10 ứng viên có điểm cao nhất.

5. **Optimize Cost:**
   - Sử dụng **GPT-3.5** thay vì GPT-4.1 nếu ngân sách hạn chế (giảm chi phí ~50%).
   - **Lưu ý:** Đảm bảo **prompt vẫn rõ ràng** để kết quả không sai lệch.

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp HR khỏi công việc **lặp đi lặp lại** và **tự động hóa toàn bộ quy trình tuyển dụng** từ upload hồ sơ đến đánh giá AI. Với **chi phí thấp (~$0.05/ứng viên)** và **tính chính xác cao**, đây là **giải pháp lý tưởng** cho các doanh nghiệp muốn **tuyển dụng nhanh chóng và hiệu quả**.

**Hành động ngay:**
1. **Import workflow** và cấu hình các API key.
2. **Test với file mẫu** để đảm bảo hoạt động.
3. **Bật workflow** và **tự động hóa tuyển dụng** của doanh nghiệp!

---
**💡 Cần hỗ trợ thêm?**
- **Join Cộng đồng n8n Việt Nam:** [Facebook Group](https://www.facebook.com/groups/n8nvietnam/)
- **Hỗ trợ kỹ thuật:** [n8n.io/support](https://n8n.io/support)