---
title: "🚀 Tự Động Hóa Lead Generation B2B: Scrape Apollo, AI Viết Email & Lưu Trữ Trên Sheets (Không Cần Code)"
description: "Workflow này tự động tìm kiếm và scrape thông tin lead từ Apollo.io theo tiêu chí công việc và vị trí, sử dụng AI Gemini viết email cold outreach cá nhân hóa, lưu toàn bộ dữ liệu vào Google Sheets và gửi báo cáo kết quả qua email. Giúp các sếp tiết kiệm 10-15 giờ/tháng trong quá trình prospecting."
slug: "tieu-dong-hoa-lead-generation-apollo-ai-email-sheets"
tags: [n8n, automation, lead-generation, no-code, google-gemini, browseract, google-sheets, gmail]
keywords: [n8n workflow lead generation, tự động hóa prospecting, scrape Apollo.io, AI viết email cold outreach, Google Gemini tự động hóa, lưu dữ liệu Google Sheets]
---

# 🚀 **Tự Động Hóa Lead Generation B2B: Scrape Apollo, AI Viết Email & Lưu Trữ Trên Sheets**

## **🔍 Nỗi Đau Của Các Sếp Trong Quá Trình Prospecting**
Hàng ngày, các sếp phải:
- **Tìm kiếm thủ công** trên Apollo.io hoặc LinkedIn để lọc lead phù hợp với tiêu chí công việc và vị trí.
- **Gõ email cold outreach** cho từng lead, mất từ **10-15 phút/email**, dẫn đến hiệu suất thấp và không thể mở rộng.
- **Lưu trữ dữ liệu** trong nhiều file Excel rối ren, khó theo dõi và cập nhật.
- **Không có cách nào tự động hóa** toàn bộ quy trình từ tìm kiếm đến gửi email, khiến quá trình prospecting trở nên **chậm chạp và không hiệu quả**.

**Workflow này giải quyết tất cả vấn đề trên bằng cách:**
✅ **Tự động scrape lead** từ Apollo.io theo tiêu chí công việc và vị trí.
✅ **AI Gemini viết email cold outreach cá nhân hóa** cho từng lead.
✅ **Lưu toàn bộ dữ liệu** (thông tin lead + email draft) vào **Google Sheets**.
✅ **Gửi báo cáo kết quả** qua email khi hoàn thành batch.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10-15 giờ/tháng** trong quá trình prospecting thủ công.
- **Email cold outreach cá nhân hóa** với tỷ lệ mở cao hơn 30% so với email thông thường.
- **Dữ liệu lead được lưu trữ sạch sẽ** trên Google Sheets, dễ dàng theo dõi và phân tích.
- **Hoạt động tự động 24/7**, không phụ thuộc vào thời gian làm việc của cá nhân.
- **Báo cáo tự động** gửi qua email khi hoàn thành batch, giúp quản lý dễ dàng.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Apollo.io** (để scrape lead) hoặc **BrowserAct Workflow ID** (nếu sử dụng BrowserAct).
✔ **Google Sheets** với **các cột chuẩn** (id, name, email, job_title, profile_url, company, location, email_draft).
✔ **Google Gemini API Key** (để sử dụng AI viết email).
✔ **Tài khoản Gmail** (để gửi báo cáo kết quả).
✔ **Credentials OAuth2** cho:
   - **Google Sheets** (Service Account hoặc OAuth2).
   - **Gmail** (OAuth2).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/13170](https://n8n.io/workflows/13170) hoặc copy/paste JSON vào **n8n Editor**.
- **Nhấp vào "Import"** và chọn file JSON đã tải.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **9 node chính**, các sếp cần chú ý cấu hình sau:

##### **🔹 Node 1: Receive Lead Criteria (formTrigger)**
- **Không cần chỉnh sửa**, node này sẽ nhận **tiêu chí tìm kiếm** (vị trí, công việc) từ form.
- **Lưu ý:** Đảm bảo **form được kết nối** với node này trong n8n Editor.

##### **🔹 Node 2: Scrape Apollo via BrowserAct (browserAct)**
- **Chỉnh sửa Workflow ID**:
  - Mở node này, nhấp vào **"Run a workflow"** và **điền Workflow ID** của BrowserAct.
  - **Nếu chưa có BrowserAct Workflow ID**:
    - Tạo một **BrowserAct Workflow** mới trên [BrowserAct](https://browseract.com/).
    - Chọn **Apollo.io** hoặc trang web tương tự để scrape.
    - **Lưu Workflow ID** và điền vào node này.

##### **🔹 Node 3: Clean & Flatten JSON (code)**
- **Không cần chỉnh sửa**, node này **tự động chuẩn hóa dữ liệu** từ JSON thô.
- **Nếu dữ liệu không hợp lệ**, có thể mở node này và **sửa logic** trong phần code.

##### **🔹 Node 4: Map Columns (set)**
- **Đảm bảo các cột trong Google Sheets** khớp với **các trường dữ liệu** sau:
  - `id`, `name`, `email`, `job_title`, `profile_url`, `company`, `location`, `email_draft`.
- **Nếu thiếu cột**, mở node này và **cập nhật lại mapping**.

##### **🔹 Node 5: Save to Google Sheets (googleSheets)**
- **Chọn file Google Sheets** đã tạo trước đó.
- **Chọn operation = "append"** (để thêm dữ liệu mới vào cuối sheet).
- **Kiểm tra credentials**:
  - Nếu dùng **Service Account**, điền **JSON Key** của Google Sheets.
  - Nếu dùng **OAuth2**, đăng nhập và cấp quyền cho n8n.

##### **🔹 Node 6 & 7: Basic LLM Chain + Google Gemini Chat Model (chainLlm & lmChatGoogleGemini)**
- **Điền API Key Google Gemini**:
  - Mở node **Google Gemini Chat Model**, nhấp vào **"Add"** và điền **GooglePalmApi** (từ n8n Credentials).
  - **Nếu chưa có API Key**:
    - Đăng ký tại [Google AI Studio](https://aistudio.google/).
    - Tạo **API Key** và thêm vào **Credentials** của n8n.

##### **🔹 Node 8: Send a message (gmail)**
- **Chọn tài khoản Gmail** muốn gửi báo cáo.
- **Kiểm tra credentials OAuth2** đã được cấu hình.
- **Cập nhật nội dung email** (nếu cần thay đổi template).

##### **🔹 Node 9: Merge (merge)**
- **Không cần chỉnh sửa**, node này **ghép dữ liệu lead + email draft** thành một dataset duy nhất.

---

#### **3. Kích Hoạt ⚡️**
- **Test Run** với **dữ liệu mẫu**:
  - Nhập **tiêu chí tìm kiếm** (vị trí, công việc) vào form.
  - Chạy **Test Execution** để kiểm tra workflow.
- **Bật Active** khi đã kiểm tra xong.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack Webhook** hoặc **Telegram Bot** để **báo cáo kết quả ngay khi hoàn thành**.
   - Cách làm: Sau node **Send a message (gmail)**, thêm node **Slack Webhook** và gửi thông báo.

2. **Lưu Log Dữ Liệu**:
   - Thêm node **Google Drive** hoặc **AWS S3** để **backup dữ liệu lead** định kỳ.
   - Cách làm: Sau node **Save to Google Sheets**, thêm node **Google Drive** và lưu file CSV.

3. **Tự Động Gửi Email Cho Lead**:
   - Sau khi AI viết email draft, có thể **tự động gửi** qua Gmail hoặc **SendGrid**.
   - Cách làm: Thêm node **Gmail Send Email** sau node **Merge** và cấu hình template email.

4. **Phân Tích Dữ Liệu**:
   - Sử dụng **Google Sheets + Apps Script** để **tính toán tỷ lệ mở email** và **đánh giá hiệu quả**.
   - Cách làm: Tạo một **script Apps Script** trong Google Sheets để tự động tính toán.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc prospecting thủ công, đồng thời **tăng hiệu quả outreach** với email cá nhân hóa. **Bắt đầu tự động hóa ngay hôm nay** và xem cách nó **tăng gấp đôi sản lượng lead** mà không cần tăng nhân sự!

👉 **Bắt đầu import workflow và cấu hình ngay!** Nếu có vấn đề, hãy để lại comment dưới đây, các sếp sẽ được hỗ trợ chi tiết. 🚀

---
**#TựĐộngHóa #LeadGeneration #AI #GoogleGemini #n8n #Prospecting**