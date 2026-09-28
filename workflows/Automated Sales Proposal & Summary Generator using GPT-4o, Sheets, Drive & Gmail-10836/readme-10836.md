---
title: "🚀 Tự Động Hóa Tạo Báo Cáo & Tài Liệu Bán Hàng AI (GPT-4o + Sheets + Drive + Gmail) - Giảm 90% Thời Gian Chăm Sóc Khách Hàng"
description: "Workflow tự động hóa hoàn toàn bằng n8n giúp tạo **tài liệu bán hàng cá nhân hóa** (báo cáo tóm tắt, one-pager, và đề xuất bán hàng) từ dữ liệu khách hàng trong Google Sheets, sau đó tự động upload lên Google Drive và gửi báo cáo tổng hợp qua email. Giúp các sếp tiết kiệm **10+ giờ/tuần** và nâng cao chất lượng tương tác với khách hàng."
slug: "tieu-dong-hoa-tao-tai-lieu-ban-hang-ai-gpt4o-sheets-drive-gmail"
tags: [n8n, automation, no-code, crm, ai-multimodal, google-sheets, google-drive, gmail, azure-openai]
keywords: [n8n workflow bán hàng, tự động hóa tài liệu AI, GPT-4o tự động hóa, tự động hóa Google Sheets, tự động hóa email bán hàng, tự động hóa CRM không code]
---

# 🚀 **Tự Động Hóa Tạo Tài Liệu Bán Hàng AI: Từ Dữ liệu Khách Hàng → Tài Liệu Cá Nhân Hóa → Email Tổng Hợp (Không Cần Code!)**

### **Nỗi Đau Của Các Sếp Trong Bán Hàng**
Các sếp bán hàng thường phải mất **giờ đồng hồ** để:
- **Tạo tài liệu bán hàng** (báo cáo tóm tắt, one-pager, đề xuất chi tiết) cho từng khách hàng.
- **Tìm kiếm và cập nhật** dữ liệu khách hàng trong Google Sheets.
- **Upload tài liệu** lên Google Drive và **gửi email báo cáo** cho đội ngũ marketing/sales.
- **Quản lý dữ liệu rối loạn** khi khách hàng không hợp lệ hoặc thiếu thông tin.

**Kết quả?** Thời gian chăm sóc khách hàng bị "ăn cắp" bởi công việc thủ công, dẫn đến **chất lượng tương tác giảm** và **sự chậm trễ** trong quá trình bán hàng.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
Sau khi triển khai workflow này, các sếp sẽ:
✅ **Tiết kiệm 10+ giờ/tuần** bằng cách tự động hóa toàn bộ quy trình tạo tài liệu.
✅ **Tạo tài liệu bán hàng cá nhân hóa** với chất lượng cao, do **GPT-4o** xử lý.
✅ **Tự động upload** tất cả tài liệu lên Google Drive và **cập nhật liên kết** vào Google Sheets.
✅ **Gửi email báo cáo tổng hợp** (HTML) đến đội ngũ marketing/sales **mỗi khi có khách hàng mới**.
✅ **Giảm thiểu lỗi** bằng cách **lọc và log khách hàng không hợp lệ** tự động.
✅ **Nâng cao hiệu quả bán hàng** với tài liệu chuyên nghiệp, được AI tối ưu hóa.

---
### **🔧 Yêu Cầu Cần Thiết**
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài Khoản & API Keys**:
   - **Google Sheets OAuth 2.0** (để đọc/writing dữ liệu khách hàng).
   - **Google Drive OAuth 2.0** (để upload tài liệu).
   - **Gmail OAuth 2.0** (để gửi email báo cáo).
   - **Azure OpenAI API Key** (để sử dụng GPT-4o).
   - **Node LangChain** (đã được cài đặt trong n8n).

2. **Cấu Trúc Google Sheets**:
   - Một **bảng dữ liệu khách hàng** với các cột như:
     - `Company Name`, `Email`, `Booking Status`, `Notes` (nếu có).
   - Một **bảng "Invalid Leads"** để log khách hàng không hợp lệ.
   - Một **bảng "Collateral Data"** (nếu muốn lưu trữ metadata của tài liệu).

3. **Google Drive**:
   - Một **thư mục "collateral data"** để lưu trữ tất cả tài liệu tự động tạo.

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/10836](https://n8n.io/workflows/10836) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON từ link trên và **paste** vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này có **16 node** với nhiều bước quan trọng. Dưới đây là hướng dẫn chi tiết để cấu hình:

##### **A. Cấu Hình Credentials (Tài Khoản)**
- **Google Sheets & Drive**:
  - Đăng nhập vào [Google Cloud Console](https://console.cloud.google.com/) và tạo **OAuth 2.0 Client ID**.
  - Cấu hình trong **n8n Credentials** với tên:
    - `googleSheetsOAuth2Api`
    - `googleDriveOAuth2Api`
  - **Lưu ý**: Chọn **Google Sheets API** và **Google Drive API** trong quyền truy cập.

- **Gmail**:
  - Tạo **App Password** (nếu sử dụng 2FA) hoặc đăng nhập trực tiếp.
  - Cấu hình trong **n8n Credentials** với tên: `gmailOAuth2`.

- **Azure OpenAI (GPT-4o)**:
  - Mua **API Key** từ [Azure OpenAI](https://azure.microsoft.com/en-us/products/ai-services/openai/).
  - Cấu hình trong **n8n Credentials** với tên: `azureOpenAiApi`.
  - **Model**: Chọn `gpt-4o` (đã được cấu hình sẵn trong workflow).

##### **B. Cấu Hình Google Sheets**
- **Bảng "Lead Records"**:
  - Cột **Booking Status** phải có giá trị **"BOOKED"** để workflow xử lý.
  - Cột **Email** **bắt buộc** (nếu không, khách hàng sẽ được log vào "Invalid Leads").

- **Bảng "Invalid Leads"**:
  - Workflow sẽ tự động log khách hàng **không hợp lệ** (thiếu email hoặc status không phải "BOOKED").

##### **C. Cấu Hình Node AI (LangChain Agent)**
- **Node "Generate Sales Collateral (AI)"**:
  - Workflow sẽ tự động **tạo 3 loại tài liệu**:
    1. **Sales Summary** (tóm tắt ngắn gọn).
    2. **One-Pager** (3 điểm chính + CTA).
    3. **Proposal Draft** (scope, timeline, next steps).
  - **Prompt** đã được tối ưu hóa sẵn, nhưng các sếp có thể **cập nhật** trong node `lmChatAzureOpenAi` nếu cần.

- **Node "Generate Sales Summary Email"**:
  - Tạo **email HTML** tổng hợp với:
    - Danh sách tất cả khách hàng đã xử lý.
    - Liên kết tải tài liệu.
    - **Insights** từ AI (tóm tắt ngắn gọn).
  - **Lưu ý**: Email sẽ được gửi đến **email mặc định** của tài khoản Gmail đã cấu hình.

##### **D. Cấu Hình Node Code (JavaScript)**
- **Node "Parse AI JSON Output"**:
  - Chuyển đổi **JSON thô** từ GPT-4o thành **cấu trúc rõ ràng** (`summary`, `one_pager`, `proposal`).
  - **Không cần chỉnh sửa** nếu không biết JavaScript.

- **Node "Convert Collateral into Text Reports"**:
  - Chuyển đổi **JSON** thành **file `.txt`** với định dạng đọc dễ dàng.
  - **Không cần chỉnh sửa** (n8n tự động xử lý).

- **Node "Map Uploaded Files with Lead Data"**:
  - **Gắn liên kết** giữa tài liệu trên Google Drive và khách hàng trong Google Sheets.
  - **Không cần chỉnh sửa** (n8n tự động map dựa trên index).

##### **E. Cấu Hình Node Google Drive**
- **Node "Upload Sales Collateral to Google Drive"**:
  - Tạo **thư mục "collateral data"** (nếu chưa có).
  - Workflow sẽ **upload tất cả file `.txt`** vào thư mục này.
  - **Lưu ý**: Đảm bảo **quyền truy cập** của Google Drive OAuth được cấp đầy đủ.

##### **F. Cấu Hình Node Gmail**
- **Node "Send Sales Summary Email via Gmail"**:
  - **Người nhận**: Cần **cấu hình** trong node này (ví dụ: `team@company.com`).
  - **Tiêu đề email**: `"Sales Collateral Summary"` (đã cấu hình sẵn).
  - **Nội dung**: HTML tự động tạo bởi AI.

---
#### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với **dữ liệu mẫu**:
   - Chọn **1-2 khách hàng "BOOKED"** trong Google Sheets.
   - Chạy **Manual Trigger** để kiểm tra:
     - Tài liệu có được tạo không?
     - Email có được gửi không?
     - Liên kết trong Google Sheets có được cập nhật không?

2. **Bật Active**:
   - Sau khi test thành công, **bật workflow** để chạy **24/7**.
   - **Lưu ý**: Workflow sẽ **chạy tự động** khi có khách hàng mới được thêm vào Google Sheets (nếu cấu hình **webhook**).

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
1. **Tự Động Chạy Khi Có Khách Hàng Mới**:
   - Thêm **Webhook** vào đầu workflow để **n8n tự động kích hoạt** khi có dữ liệu mới trong Google Sheets.
   - **Cách làm**:
     - Thêm node **`webhook`** vào đầu workflow.
     - Cấu hình **URL Webhook** và **event trigger** (ví dụ: `onRowAdded`).
     - **Lưu ý**: Cần **cấu hình CORS** trong Google Sheets để cho phép Webhook.

2. **Lưu Log & Theo Dõi**:
   - Thêm **node `stickyNote`** để ghi **log hoạt động** (ví dụ: "Workflow chạy thành công vào 10h ngày 1/10").
   - **Cách làm**:
     ```javascript
     // Thêm vào node Code (nếu cần log chi tiết)
     console.log("Workflow executed at: " + new Date().toISOString());
     ```

3. **Gửi Email Cá Nhân Hóa Cho Mỗi Khách Hàng**:
   - Thay vì gửi **email tổng hợp**, có thể **tạo email cá nhân** cho từng khách hàng.
   - **Cách làm**:
     - Thêm node **`gmail`** mới sau khi **upload tài liệu**.
     - Sử dụng **template email** từ GPT-4o (cập nhật trong node `lmChatAzureOpenAi`).

4. **Tích Hợp Slack/Telegram**:
   - Gửi **thông báo** khi workflow hoàn thành thành công.
   - **Cách làm**:
     - Thêm node **`slack`** hoặc **`telegram`** vào cuối workflow.
     - Cấu hình **webhook** của Slack/Telegram.

5. **Tự Động Xóa Khách Hàng Không Hợp Lệ**:
   - Thay vì chỉ **log**, có thể **xóa tự động** khách hàng không hợp lệ sau 7 ngày.
   - **Cách làm**:
     - Thêm node **`googleSheets`** mới với **operation: "deleteRow"**.
     - Sử dụng **node `date`** để kiểm tra ngày tạo.

---
### **📌 Kết Luận**
Workflow **Tự Động Hóa Tạo Tài Liệu Bán Hàng AI** là **giải pháp hoàn hảo** cho các sếp muốn:
✔ **Tiết kiệm thời gian** bằng cách loại bỏ công việc thủ công.
✔ **Nâng cao chất lượng tương tác** với khách hàng bằng tài liệu cá nhân hóa.
✔ **Tự động hóa toàn bộ quy trình** từ dữ liệu → tài liệu → email.

**Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với dữ liệu mẫu** trước khi bật chạy toàn bộ.
3. **Tích hợp vào hệ thống CRM** của công ty để **tăng hiệu quả bán hàng**.

**🎁 Mã giảm giá VPS cho n8n (Self-hosted):**
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**).
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
:::

**Chúc các sếp thành công!** 🚀
Nếu có vấn đề, hãy **đăng câu hỏi** trên [Community n8n](https://community.n8n.io/) hoặc liên hệ với tác giả [Rahul Joshi](https://n8n.io/workflows/10836).