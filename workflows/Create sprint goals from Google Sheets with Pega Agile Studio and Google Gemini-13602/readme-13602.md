---
title: "🚀 Tự Động Hóa Tạo Mục Tiêu Sprint từ Google Sheets với Pega Agile Studio & Google Gemini AI"
description: "Workflow này tự động hóa việc tạo mục tiêu sprint cho Scrum Master và Product Owner bằng cách tích hợp dữ liệu từ Google Sheets, Pega Agile Studio và trí tuệ nhân tạo Gemini. Giúp tiết kiệm thời gian lên tới 80% trong việc phân tích user stories và tạo ra sprint goals cá nhân hóa, chính xác và liên tục."
slug: "tu-dong-hoa-tao-muc-tieu-sprint-google-sheets-pega-agile-studio"
tags: [n8n, automation, project-management, agile, google-sheets, google-gemini, pega-agile-studio, no-code, ai-multimodal]
keywords: [n8n workflow sprint goals, tự động hóa sprint planning, google sheets + pega agile studio, gemini ai cho scrum master, tự động hóa product owner, no-code automation agile]
---

# 🚀 **Tự Động Hóa Tạo Mục Tiêu Sprint từ Google Sheets với Pega Agile Studio & Google Gemini AI**

### **Giải quyết vấn đề gì?**
Các Scrum Master và Product Owner thường phải mất **giờ đồng hồ** để:
- **Tìm kiếm và tổng hợp** thông tin từ hàng chục user stories trong Pega Agile Studio.
- **Phân tích chi tiết** từng tài liệu kèm theo (Excel, Google Docs, Slides) để rút ra mục tiêu sprint.
- **Tạo ra sprint goals** một cách thủ công, dễ bị lỗi và không nhất quán.

Workflow này **tự động hóa toàn bộ quy trình** bằng trí tuệ nhân tạo (Google Gemini) và API tích hợp, giúp các sếp:
✅ **Tiết kiệm 80% thời gian** phân tích dữ liệu.
✅ **Tạo sprint goals chính xác** dựa trên dữ liệu từ user stories và tài liệu kèm theo.
✅ **Cá nhân hóa** mỗi sprint goal theo đặc thù dự án.
✅ **Hoạt động liên tục** 24/7 mà không cần can thiệp thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định và an toàn**, các sếp nên **self-host n8n** trên VPS riêng thay vì dùng phiên bản cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%).
👉 [VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đủ sức mạnh cho workflow này).
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ 5-10 tiếng/tháng xuống còn **1-2 tiếng**.
- **Chính xác cao**: Trí tuệ nhân tạo phân tích toàn bộ dữ liệu từ user stories và tài liệu kèm theo.
- **Cá nhân hóa sprint goals**: Mỗi mục tiêu được tạo dựa trên **ngôn ngữ và cấu trúc cụ thể** của dự án.
- **Hoạt động tự động**: Chỉ cần **click 1 nút**, workflow sẽ chạy liên tục mà không cần can thiệp.
- **Gửi báo cáo email tự động**: Kết quả được gửi qua email cho team mỗi khi sprint bắt đầu.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Google Cloud** (để sử dụng Google Sheets, Google Drive, Google Gemini).
✔ **API Key Google Cloud** (để truy cập Google Sheets, Drive, và Gemini).
✔ **OAuth2 Credentials cho Pega Agile Studio** (để lấy dữ liệu user stories).
✔ **Google Sheet mẫu** (cột "Userstory" chứa danh sách ID user stories cần phân tích).
✔ **Tài khoản Gmail** (để gửi email kết quả sprint goals).

---
:::note[LƯU Ý QUAN TRỌNG]
Workflow này **không hoạt động** nếu thiếu **API Key Google Cloud** hoặc **credentials Pega Agile Studio**. Các sếp phải **cấu hình đầy đủ** các node liên quan trước khi chạy.
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import:
- **Tải file JSON** từ [n8n.io/workflows/13602](https://n8n.io/workflows/13602) và import vào **n8n Editor**.
- **Copy toàn bộ JSON** từ link trên và **paste** vào **Import Workflow** trong n8n.

:::tip[Cách import nhanh]
1. Mở **n8n Editor**.
2. Nhấn **Import Workflow** → **Paste JSON**.
3. Chọn **Create from JSON**.
4. Workflow sẽ xuất hiện trên canvas.
:::

---

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

##### **A. Cấu hình Google Sheets**
- **Node: "Retrieve_Data_From_Sheet"**
  - Điền **Google Sheet ID** vào `Sheet ID` (thường là chuỗi dài ở cuối URL Google Sheets).
  - Chọn **Range** là `Sheet1!A:Z` (hoặc cột chứa "Userstory").
  - **Credentials**: Chọn `googleSheetsOAuth2Api`.

##### **B. Cấu hình Pega Agile Studio**
- **Node: "Retrieve Agile Studio US"**
  - Điền **URL API** của Pega Agile Studio (ví dụ: `https://your-pega-agile-studio/api/userstories`).
  - **Headers**:
    - `Authorization: Bearer {API_KEY_PEGA}` (điền API Key từ Pega).
    - `Content-Type: application/json`.
  - **Credentials**: Chọn `httpRequestTool` (nếu có) hoặc tạo mới.

##### **C. Cấu hình Google Gemini AI**
- **Node: "Google Gemini Chat Model"**
  - Điền **API Key Google Cloud** vào `Google Cloud API Key`.
  - **System Prompt** (cần chỉnh sửa theo yêu cầu):
    ```json
    "You are an Agile Sprint Goal Generator. For each userstory, analyze the description, attachments, and related data to create a clear and actionable sprint goal. Follow this format:
    - [Sprint Goal]
    - [Key Metrics to Track]
    - [Dependencies]"
    ```
  - **Credentials**: Chọn `googleGemini`.

##### **D. Cấu hình Subworkflows (đối với tài liệu kèm theo)**
Workflow này **tách nhỏ** việc xử lý 3 loại file:
1. **Google Sheets** → Sử dụng API Google Sheets.
2. **Google Docs** → Sử dụng API Google Docs.
3. **Google Slides** → Sử dụng API Google Slides.
4. **File .xlsx** → **Tải xuống và xử lý** (do API Google không hỗ trợ).

- **Node: "Call 'Get Attachments - Agile Studio US'"**
  - Đây là **subworkflow** xử lý tài liệu kèm theo.
  - **Lưu ý**: Các sếp **phải publish subworkflows** này trước khi chạy workflow chính.
  - **Credentials**: Chọn `toolWorkflow` và điền **Workflow ID** của subworkflow.

##### **E. Cấu hình Email (Gmail)**
- **Node: "Send a message"**
  - Điền **Email nhận** (ví dụ: `team@doanhnghiep.com`).
  - **Subject**: `Sprint Goals - [Tên Dự án]`.
  - **Credentials**: Chọn `gmailOAuth2Api`.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Execute Workflow** và chọn **Manual Trigger**.
   - Kiểm tra **log** để đảm bảo không có lỗi.
2. **Bật Active**:
   - Sau khi test thành công, **bật Active** và chọn **Manual Trigger** hoặc **Execute Workflow Trigger** (nếu kết nối với workflow khác).

---
:::warning[LỖI THƯỜNG GẶP]
- **"Google Sheets not found"**: Kiểm tra lại **Sheet ID** và **credentials**.
- **"Pega API unauthorized"**: Đảm bảo **API Key Pega** đúng và không hết hạn.
- **"Gemini API error"**: Kiểm tra **API Key Google Cloud** và **quota** của Gemini.
:::

---

### ✍️ **Mẹo & gợi ý nâng cao**

#### **1. Tối ưu hóa System Prompt cho Gemini**
- **Chỉnh sửa System Prompt** để phù hợp với **ngôn ngữ và quy trình** của dự án.
- Ví dụ:
  ```json
  "You are a senior Scrum Master. For each userstory, extract:
  - Primary goal (1 sentence).
  - Risks (if any).
  - Acceptance criteria (if missing).
  Format output as JSON: { 'goal': '...', 'risks': [], 'criteria': [] }"
  ```

#### **2. Gửi báo cáo định kỳ**
- **Kết hợp với node `Set`** để lưu **lịch sử sprint goals** vào Google Sheets.
- **Sử dụng node `executeWorkflowTrigger`** để chạy workflow hàng tuần.

#### **3. Kết nối với Slack/Telegram**
- Thay vì email, **gửi kết quả qua Slack/Telegram** bằng node `webhook`.
- Cài đặt **webhook** từ Slack/Telegram và kết nối vào node `Send a message`.

#### **4. Lưu log hoạt động**
- **Sử dụng node `stickyNote`** để ghi lại **lịch sử chạy workflow**.
- **Export log** vào Google Sheets để theo dõi.

#### **5. Xử lý lỗi tự động**
- **Sử dụng node `filter` + `switch`** để **bỏ qua** user stories có lỗi.
- **Gửi email cảnh báo** khi có lỗi xảy ra.

---
### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các Scrum Master và Product Owner muốn **tự động hóa sprint planning** mà không cần viết code. Với **Google Gemini AI**, nó không chỉ **tiết kiệm thời gian** mà còn **tăng chất lượng** của sprint goals.

**Hành động ngay:**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với dữ liệu mẫu** trước khi áp dụng toàn bộ.
3. **Bật Active** và **nhận sprint goals tự động** mỗi khi cần!

👉 **Bắt đầu tự động hóa sprint của bạn ngay hôm nay!** 🚀

---
:::success[CHÚC MỪNG]
Các sếp đã có **công cụ mạnh mẽ** để quản lý sprint một cách **chuyên nghiệp và hiệu quả**! Nếu có vấn đề, hãy để lại **comment** dưới đây, mình sẽ hỗ trợ ngay. 😊
:::

---
**📌 Tham khảo thêm:**
- [Tutorial Pega Agile Studio API](https://developer.pega.com/)
- [Google Gemini API Docs](https://developers.gemini.google/)
- [n8n Workflow Official](https://n8n.io/workflows/13602)