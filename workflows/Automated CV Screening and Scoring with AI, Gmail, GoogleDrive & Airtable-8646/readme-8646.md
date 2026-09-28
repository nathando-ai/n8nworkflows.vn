---
title: "🚀 Tự Động Xử Lý & Đánh Giá Sơ Lọc CV Bằng AI: Gmail → Google Drive → Airtable (Không Cần Code)"
description: "Workflow tự động hóa hoàn chỉnh giúp các sếp HR nhận email CV, trích xuất thông tin chi tiết, đánh giá phù hợp và lưu kết quả vào Google Sheets & Airtable chỉ trong vài giây. Giảm thời gian tuyển dụng 90% và tăng độ chính xác đánh giá."
slug: "tuyen-dung-ai-cv-screening-gmail-google-drive-airtable"
tags: [n8n, automation, hr, ai-summarization, google-drive, airtable, no-code, openrouter, langchain]
keywords: [tự động hóa tuyển dụng, cv screening ai, n8n workflow hr, trích xuất cv pdf, đánh giá phù hợp cv, google sheets airtable automation]
---

# 🚀 **Tự Động Xử Lý & Đánh Giá Sơ Lọc CV Bằng AI: Từ Email Đến Airtable (Không Cần Code)**

### **Nỗi Đau Của Các Sếp HR**
Tuyển dụng là một quá trình tốn thời gian và dễ mắc sai lầm. Các sếp thường phải:
- **Làm thủ công**: Quét hàng trăm email CV, trích xuất thông tin từ PDF, đánh giá phù hợp và ghi chép vào bảng Excel.
- **Mất thời gian**: Trích xuất một CV PDF tiêu chuẩn có thể mất **5-10 phút**, cộng với việc đánh giá phù hợp, tổng thời gian cho **100 CV** có thể lên đến **8-10 giờ**.
- **Sai sót cao**: Con người dễ bỏ sót thông tin quan trọng hoặc đánh giá chủ quan, dẫn đến việc tuyển dụng không phù hợp.
- **Không theo dõi được**: Kết quả đánh giá phân tán trên email, Google Sheets hoặc Airtable, khó quản lý và báo cáo.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động nhận email CV** từ Gmail và trích xuất tất cả các file đính kèm.
✅ **Trích xuất thông tin chi tiết** từ CV PDF (tên, email, số điện thoại, kinh nghiệm, kỹ năng).
✅ **Đánh giá phù hợp** bằng AI (điểm từ 1-10) và lý do chi tiết.
✅ **Lưu kết quả vào Google Sheets & Airtable** để theo dõi và báo cáo dễ dàng.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted) để đảm bảo tính riêng tư và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Xử lý **100 CV trong 10 phút** thay vì 8-10 giờ làm thủ công.
- **Độ chính xác cao**: AI trích xuất và đánh giá khách quan, giảm sai sót do con người.
- **Dữ liệu tập trung**: Kết quả lưu vào **Google Sheets** (dễ dàng báo cáo) và **Airtable** (tương tác cao).
- **Tự động hóa hoàn chỉnh**: Không cần can thiệp, hoạt động liên tục 24/7.
- **Cá nhân hóa**: AI cung cấp **lý do chi tiết** cho mỗi điểm đánh giá, giúp các sếp hiểu rõ hơn về ứng viên.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản & API Keys**:
   - **Gmail**: Tài khoản Google với quyền truy cập email (cần **OAuth 2.0**).
   - **Google Drive**: Tài khoản Google với quyền truy cập folder lưu CV (cần **OAuth 2.0 API**).
   - **Google Sheets**: File Sheets đã tạo sẵn để lưu kết quả (cần **OAuth 2.0 API**).
   - **Airtable**: Base Airtable đã tạo sẵn với schema phù hợp (cần **API Token**).
   - **OpenRouter API**: Tài khoản [OpenRouter](https://openrouter.ai/) (miễn phí với model `openai/gpt-oss-20b:free`).

2. **Folder Google Drive**:
   - Tạo một folder trên Google Drive để lưu trữ CV đính kèm từ email.

3. **Google Sheets**:
   - Tạo một bảng Sheets mới với các cột: `Name`, `Email`, `Phone`, `Education`, `Job History`, `Skills`, `Suitability Score`, `Justification`.

4. **Airtable**:
   - Tạo một Base mới với các trường phù hợp với schema trong workflow (ví dụ: `Name`, `Email`, `Score`, `Summary`, `Justification`).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Bước 1**: Tải workflow từ [n8n.io/workflows/8646](https://n8n.io/workflows/8646) hoặc copy JSON từ trang này.
- **Bước 2**: Mở **n8n Editor** và nhấn **Import Workflow** (hoặc **Create New Workflow** > **Import JSON**).
- **Bước 3**: Dán JSON vào và nhấn **Import**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **14 node** với các bước chính sau. Các sếp cần chú ý cấu hình các node sau:

##### **A. Cấu Hình Credentials (Tài Khoản)**
- **Gmail Trigger**:
  - Chọn **gmailOAuth2** và cấu hình OAuth 2.0 từ Google Cloud Console.
  - **Lưu ý**: Cần thiết lập **filter** trong Gmail Trigger để chỉ nhận email có từ khóa như `"CV"`, `"Application"`, hoặc tên vị trí tuyển dụng (ví dụ: `"Developer"`).

- **Google Drive (Upload & Download)**:
  - Chọn **googleDriveOAuth2Api** và cấu hình OAuth 2.0.
  - **Folder ID**: Điền ID của folder bạn tạo trên Google Drive (tham khảo [cách lấy ID folder](https://support.google.com/docs/answer/1016430)).
  - **File Naming**: Workflow tự động đặt tên file theo email của người gửi (ví dụ: `CV_nguyenvananh@gmail.com.pdf`).

- **Google Sheets**:
  - Chọn **googleSheetsOAuth2Api** và cấu hình OAuth 2.0.
  - **Sheet Name**: Điền tên của file Sheets bạn tạo (ví dụ: `CV_Screening`).
  - **Range**: Điền `Sheet1!A1` (hoặc tên sheet cụ thể).

- **Airtable**:
  - Chọn **airtableTokenApi** và điền **API Token** từ Airtable (tìm trong **Settings > API**).
  - **Base ID & Table Name**: Điền ID của Base và tên Table trong Airtable (tham khảo [cách lấy ID](https://airtable.com/api)).

- **OpenRouter API**:
  - Chọn **openRouterApi** và điền **API Key** từ tài khoản OpenRouter.
  - **Model**: Đã cấu hình sẵn là `openai/gpt-oss-20b:free` (miễn phí).

##### **B. Cấu Hình Node Quan Trọng**
1. **Gmail Trigger**:
   - **Filter**: Cấu hình để chỉ nhận email có từ khóa liên quan (ví dụ: `"CV" AND "Developer"`).
   - **Attachments**: Chọn **Include attachments** để trích xuất file CV.

2. **Extract from File**:
   - Node này tự động chuyển đổi PDF thành text. **Không cần cấu hình thêm**.

3. **Information Extractor**:
   - Node này trích xuất thông tin cơ bản như **tên, email, số điện thoại**.
   - **Schema**: Đã cấu hình sẵn, các sếp không cần chỉnh sửa.

4. **AI Agent (OpenRouter)**:
   - Node này **tóm tắt CV** và **đánh giá phù hợp** (điểm 1-10).
   - **Prompt**: Đã tối ưu hóa sẵn, các sếp chỉ cần đảm bảo **OpenRouter API Key** đúng.

5. **Code Node**:
   - Node này **xử lý text** từ AI Agent để trích xuất **Education**, **Job History**, **Skills**, và **Score**.
   - **Lưu ý**: Các sếp không cần chỉnh sửa mã JavaScript trong node này (nếu muốn thay đổi, cần hiểu JS).

6. **Merge**:
   - Node này **kết hợp** dữ liệu từ **Information Extractor** (thông tin cơ bản) và **AI Agent** (tóm tắt + điểm đánh giá).

7. **Append row in sheet (Google Sheets) & Create a record (Airtable)**:
   - Đảm bảo **Sheet Name** và **Table Name** trong Airtable đúng với cấu trúc đã tạo.

---

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Gửi một email mẫu có CV PDF đính kèm đến địa chỉ email được cấu hình trong **Gmail Trigger**.
  - Chạy **Test Run** trong n8n Editor để kiểm tra workflow.
  - Kiểm tra **Google Sheets** và **Airtable** để xác nhận dữ liệu đã lưu đúng.

- **Bật Active**:
  - Sau khi test thành công, chuyển workflow sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tích Hợp Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** để thông báo kết quả đánh giá cho team HR.
   - Ví dụ: Khi AI đánh giá một CV có điểm cao, bot sẽ gửi tin nhắn như:
     > *"CV của [Tên] được đánh giá 9/10 với lý do: [Lý do chi tiết]."*

2. **Lưu Log & Audit**:
   - Thêm node **HTTP Request** để lưu log vào một file CSV hoặc database để theo dõi lịch sử.

3. **Báo Cáo Định Kỳ**:
   - Sử dụng **Google Sheets** kết hợp với **n8n** để tự động tạo báo cáo tuần/month về số lượng CV nhận được, điểm trung bình, và danh sách ứng viên top.

4. **Tùy Chỉnh Schema**:
   - Nếu cần trích xuất thêm thông tin từ CV (ví dụ: **certificate**, **projects**), các sếp có thể chỉnh sửa **Information Extractor** hoặc **AI Agent** bằng cách cập nhật schema.

5. **Kết Hợp với Calendly**:
   - Sử dụng **Calendly** để ứng viên đăng ký phỏng vấn trực tiếp từ CV đã được đánh giá.

---

### 📌 **Kết Luận**
Workflow **Automated CV Screening** này là giải pháp **tự động hóa hoàn chỉnh** cho quá trình tuyển dụng, giúp các sếp:
✔ **Tiết kiệm thời gian** lên đến **90%** so với làm thủ công.
✔ **Tăng độ chính xác** với AI đánh giá khách quan.
✔ **Quản lý dễ dàng** với dữ liệu tập trung trên Google Sheets & Airtable.
✔ **Hoạt động 24/7** mà không cần can thiệp.

**Hành động ngay!**
1. **Import workflow** vào n8n của mình.
2. **Cấu hình credentials** theo hướng dẫn trên.
3. **Test với email mẫu** và bật **Active**.
4. **Tích hợp thêm Slack/Telegram** để thông báo kết quả.

**🚀 Cùng tự động hóa tuyển dụng của mình ngay hôm nay!** Nếu có vấn đề, các sếp có thể comment bên dưới hoặc liên hệ với cộng đồng n8n trên [Discord](https://discord.gg/n8n). Chúc các sếp thành công! 💼🤖