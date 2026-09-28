---
title: "🚀 Tự Động Hóa Email Outreach B2B Cá Nhân Hóa với AI Nghiên Cứu & OpenRouter (N8n)"
description: "Workflow này tự động tạo email outreach B2B cá nhân hóa bằng AI nghiên cứu thông tin công ty từ Tavily và viết nội dung chuyên nghiệp bằng OpenRouter, giúp các sếp tiết kiệm thời gian và tăng tỷ lệ phản hồi hiệu quả."
slug: "tieu-dong-hoa-email-outreach-b2b-ai"
tags: [n8n, automation, no-code, lead-nurturing, ai-multimodal, google-sheets, instantlyai]
keywords: [n8n workflow outreach, tự động hóa email B2B, AI nghiên cứu công ty, OpenRouter, Tavily, Google Sheets, instantlyAI]
---

# 🚀 **Tự Động Hóa Email Outreach B2B Cá Nhân Hóa với AI Nghiên Cứu & OpenRouter (N8n)**

### **🔥 Nỗi Đau Của Các Sếp Trong Outreach B2B**
Các sếp đã từng phải:
- **Tìm kiếm thủ công** thông tin về công ty mục tiêu (website, LinkedIn, tin tức mới nhất) để viết email cá nhân hóa.
- **Viết email một cách chung chung**, không phản ánh được giá trị cụ thể của doanh nghiệp đối tác.
- **Phải theo dõi hàng trăm lead** trên Google Sheets mà không có hệ thống tự động hóa để cập nhật hoặc gửi email tự động.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Nghiên cứu** thông tin công ty từ Tavily (bao gồm tin tức mới nhất, sản phẩm/dịch vụ, và chiến lược).
✅ **Viết email** cá nhân hóa bằng OpenRouter LLM, dựa trên dữ liệu nghiên cứu.
✅ **Cập nhật log** vào Google Sheets và **gửi email** qua InstantlyAI (nếu cần).

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần tìm kiếm thủ công thông tin công ty hoặc viết email từ đầu.
- **Email cá nhân hóa cao**: Dựa trên dữ liệu mới nhất từ Tavily, giúp tỷ lệ mở và phản hồi tăng gấp đôi.
- **Hoạt động liên tục**: Workflow tự động chạy 24/7, không cần can thiệp của con người.
- **Dữ liệu thống kê**: Tất cả thông tin và email được lưu vào Google Sheets, dễ dàng theo dõi và phân tích.
- **Gửi email tự động**: Kết nối với **InstantlyAI** để gửi email một cách chuyên nghiệp và theo dõi kết quả.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** với:
   - Một **bảng tính** chứa dữ liệu lead (cột: `Name`, `Company`, `Email`, `Status`).
   - **Thao tác quyền**: Chỉnh quyền cho n8n truy cập bằng **OAuth 2.0**.
2. **API Key Tavily**:
   - Đăng ký tại [Tavily](https://tavily.com/) và thêm vào n8n dưới **Credentials** (`tavilyApi`).
3. **API Key OpenRouter**:
   - Đăng ký tại [OpenRouter](https://openrouter.ai/) và thêm vào n8n dưới **Credentials** (`openRouterApi`).
4. **Tài khoản InstantlyAI** (tùy chọn):
   - Nếu muốn gửi email tự động, đăng ký tại [InstantlyAI](https://instantly.ai/) và cấu hình trong node `Add Lead to Instantly AI`.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/10009](https://n8n.io/workflows/10009) hoặc copy/paste JSON vào **n8n Editor**.
- **Cách import**:
  1. Mở **n8n Editor** → Nhấn `+` → Chọn `Import Workflow`.
  2. Dán JSON hoặc tải file `.json` lên.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
##### **A. Node `Get Business card data extraction` (Google Sheets)**
- **Chọn Credentials**: `googleSheetsOAuth2Api` (đã cấu hình trước).
- **Chọn Sheet**: Chọn bảng chứa dữ liệu lead (cột `Status = "ready"`).
- **Range**: Chọn toàn bộ dữ liệu hoặc chỉ cột cần lấy (`Name`, `Company`, `Email`).

##### **B. Node `Limit(Test)` (Xóa trong sử dụng thực tế)**
- **Lưu ý quan trọng**: Node này chỉ dùng để **test**, **xóa nó đi** khi chạy chính thức để tránh quá tải dữ liệu.

##### **C. Node `Tavily` (Nghiên cứu thông tin công ty)**
- **Credentials**: Chọn `tavilyApi` (đã thêm API Key).
- **Prompt**: Cấu hình để Tavily trả về thông tin chi tiết về công ty (ví dụ: "Tìm kiếm thông tin về công ty [Company Name], bao gồm sản phẩm, tin tức mới nhất và chiến lược").

##### **D. Node `Generate Outreach Message` (LLM Chain)**
- **Model**: Chọn `OpenRouter Chat Model2` hoặc `Model3` (đã cấu hình `openRouterApi`).
- **Prompt**: Sử dụng template mặc định (có thể tùy chỉnh để phù hợp với ngành nghề):
  ```
  You are an AI assistant that writes professional outreach emails.
  Based on the company research data from Tavily, create a concise and personalized email for [Name] at [Company].
  Include:
  - A brief introduction about [Your Company].
  - Key points about [Company]'s recent updates or offerings.
  - A clear call-to-action (e.g., "Let's schedule a call to discuss how we can help").
  ```

##### **E. Node `Add Lead to Instantly AI` (Tùy chọn)**
- **Credentials**: Nếu muốn gửi email tự động, cấu hình API Key của InstantlyAI.
- **Tham số**: Điền `Email`, `Name`, `Company`, và nội dung email đã tạo.

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Chọn một lead từ Google Sheets và chạy **manual trigger** để kiểm tra workflow.
   - Kiểm tra kết quả trong **Structured Output Parser** và **Google Sheets**.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, chuyển workflow sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tùy chỉnh Prompt cho từng ngành**:
   - Ví dụ: Nếu outreach cho ngành **tech**, thêm yêu cầu về "công nghệ mới nhất" vào prompt.
   - Nếu outreach cho **dịch vụ marketing**, nhấn mạnh vào "kết quả đã đạt được".

2. **Lưu Log & Báo Cáo Định Kỳ**:
   - Sử dụng **Google Apps Script** để tự động gửi báo cáo tuần/month về hiệu suất email.

3. **Kết nối với Slack/Telegram**:
   - Thêm node **Slack Webhook** hoặc **Telegram Bot** để thông báo khi email được gửi thành công.

4. **Sử dụng AI Agent để phân tích sentiment**:
   - Nếu muốn phân tích phản hồi từ khách hàng, thêm node **LLM Chain** để đánh giá tình cảm (positive/negative).

5. **Tăng tốc độ với Batch Processing**:
   - Sử dụng node **Split in Batches** để xử lý nhiều lead cùng một lúc (giảm thời gian chờ).

---

### 📌 **Kết Luận**
Workflow này không chỉ **tự động hóa** quá trình outreach B2B mà còn **cải thiện chất lượng** email bằng AI nghiên cứu và viết nội dung chuyên nghiệp. Các sếp có thể:
✔ **Tiết kiệm thời gian** từ 80% trong việc viết email.
✔ **Tăng tỷ lệ phản hồi** nhờ email cá nhân hóa.
✔ **Theo dõi toàn bộ quá trình** trên Google Sheets.

**Hành động ngay!** Import workflow, cấu hình và bắt đầu tự động hóa outreach của mình. 🚀

---
**💡 Gợi ý thêm**: Nếu cần hỗ trợ cấu hình chi tiết, các sếp có thể liên hệ với [n8n Community](https://community.n8n.io/) hoặc [Tavily Support](https://tavily.com/support).