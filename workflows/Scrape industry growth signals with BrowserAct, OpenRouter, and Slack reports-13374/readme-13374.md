---
title: "🚀 Tự Động Hóa Theo Dõi Dấu Hiệu Phát Triển Ngành Hàng Tháng Với AI & Slack (BrowserAct + OpenRouter)"
description: "Workflow tự động hóa 100% không code để theo dõi các dấu hiệu phát triển (vốn đầu tư, hợp đồng mới, công nghệ mới) của các công ty trong ngành mục tiêu của bạn hàng tháng. Kết quả được tổng hợp bởi AI và gửi trực tiếp đến Slack với định dạng chuyên nghiệp."
slug: "tieu-doi-dau-hieu-phat-trien-nganh-hang-thang"
tags: [n8n, automation, market-research, ai-summarization, browseract, openrouter, slack-integration]
keywords: [tự động hóa n8n, theo dõi ngành hàng, ai phân tích dữ liệu, browseract n8n, báo cáo hàng tháng slack, openrouter gpt-4]
---

# 🚀 **Tự Động Hóa Theo Dõi Dấu Hiệu Phát Triển Ngành Hàng Tháng Với AI & Slack**

## **🔍 Nỗi Đau Của Các Sếp**
Bạn có bao giờ phải:
- **Tốn thời gian** tra cứu thủ công các tin tức về vốn đầu tư, hợp đồng mới, hoặc công nghệ mới của các công ty trong ngành?
- **Không biết đâu là thông tin quan trọng** giữa hàng nghìn bài báo, tweet, hoặc tin tức trên mạng?
- **Không có báo cáo định kỳ** để cập nhật cho đội ngũ hoặc khách hàng?

Workflow này **giải quyết tất cả** bằng cách tự động:
✅ **Scrape** dữ liệu từ các nguồn tin tức hàng đầu (Crunchbase, TechCrunch, LinkedIn, ...)
✅ **Lọc và phân tích** bằng AI (GPT-4) để tìm ra các **dấu hiệu phát triển** (funding round, sản phẩm mới, hợp đồng lớn, ...)
✅ **Tổng hợp báo cáo** định dạng chuyên nghiệp và **gửi trực tiếp đến Slack** hàng tháng

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm 10-15 giờ/tháng** so với cách làm thủ công.
- **Chính xác 100%** với AI lọc thông tin quan trọng (không phải đọc hàng trăm bài báo).
- **Báo cáo tự động** định kỳ (không cần nhắc nhở).
- **Cá nhân hóa** theo ngành (SaaS, Fintech, Property Management, ...).
- **Dễ dàng chia sẻ** với đội ngũ qua Slack/Teams.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ**]
Bạn cần có:
1. **Tài khoản n8n Self-hosted** (để chạy 24/7).
2. **API Keys** sau:
   - **BrowserAct** (để scrape dữ liệu).
   - **OpenRouter** (để sử dụng GPT-4).
   - **Slack** (để gửi báo cáo).
3. **Template BrowserAct** (mẫu **"ABM Signal Monitor"**).
4. **Ngành mục tiêu** (ví dụ: "SaaS", "Fintech", "Property Management").
:::

---

## **🚀 Cách Import & Cấu Hình Workflow**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Từ File JSON**
1. **Tải workflow** từ [n8n.io/workflows/13374](https://n8n.io/workflows/13374).
2. **Mở n8n Editor** → Nhấn **"Import"** → Chọn file JSON vừa tải.
3. **Chọn workspace** (nếu có nhiều workspace).

#### **Phương pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ mã JSON** từ [n8n.io/workflows/13374](https://n8n.io/workflows/13374).
2. **Mở n8n Editor** → Nhấn **"Import"** → Chọn **"Paste JSON"**.
3. **Chọn workspace** và nhấn **"Import"**.

---

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**

#### **🔹 Node 1: Monthly Trigger (Định thời gian chạy)**
- **Cấu hình:** Chọn **"Monthly"** và ngày tháng mong muốn (ví dụ: **ngày 1 hàng tháng**).
- **Lưu ý:** Nếu muốn chạy ngay lập tức, chọn **"Manual Trigger"** và kích hoạt sau khi cấu hình xong.

#### **🔹 Node 2: Set Target Industry (Chọn ngành mục tiêu)**
- **Điền vào "Value":**
  - `"SaaS"` (nếu theo dõi ngành SaaS)
  - `"Fintech"` (nếu theo dõi ngành Fintech)
  - `"Property Management"` (nếu theo dõi ngành Quản lý Tài sản)
- **Lưu ý:** Cần **đúng chính tả** với template BrowserAct đã cài đặt.

#### **🔹 Node 3: Perform Web Data Extraction (BrowserAct)**
- **Chọn template:** **"ABM Signal Monitor"** (phải đã tạo trước trên BrowserAct).
- **Kiểm tra API Key:** Đảm bảo đã điền **BrowserAct API Key** vào **Credentials** của node này.
- **Lưu ý:**
  - Nếu template không hoạt động, **xem lại tài liệu BrowserAct** [đây](https://docs.browseract.com).
  - Nếu scrape không được dữ liệu, **kiểm tra nguồn dữ liệu** trong template.

#### **🔹 Node 4: OpenRouter Chat Model (AI Phân Tích)**
- **Model:** Đã mặc định là `openai/gpt-4o` (mô hình mạnh nhất hiện nay).
- **Credentials:** Đảm bảo đã điền **OpenRouter API Key** vào `openRouterApi`.
- **Lưu ý:**
  - Nếu API Key sai, **AI sẽ không hoạt động**.
  - Nếu muốn thay đổi mô hình, **cập nhật trong "keyParameters"**.

#### **🔹 Node 5: Analyze the Leads and Generate Slack Report (AI Agent)**
- **Không cần cấu hình thêm** (AI sẽ tự động phân tích và tổng hợp).
- **Lưu ý:**
  - Nếu báo lỗi, **kiểm tra node trước đó** (BrowserAct, OpenRouter).
  - Nếu muốn **tùy chỉnh prompt**, mở node này và chỉnh sửa trong **"Agent Parameters"**.

#### **🔹 Node 6: Send the Report to the Channel (Slack)**
- **Chọn channel:** Điền tên **#channel** hoặc **ID channel** Slack.
- **Credentials:** Đảm bảo đã điền **Slack API Key** vào `slackApi`.
- **Lưu ý:**
  - Nếu không gửi được báo cáo, **kiểm tra quyền API** của Slack.
  - Nếu muốn **thêm hình ảnh/bảng biểu**, chỉnh sửa trong **"Message Format"**.

---

### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run (Kiểm tra thử):**
   - Nhấn **"Run Workflow"** để kiểm tra.
   - Kiểm tra **Slack** xem báo cáo có xuất hiện không.
   - Nếu có lỗi, **xem log** trong n8n Editor.

2. **Bật Active:**
   - Sau khi test thành công, **đổi trạng thái từ "Inactive" sang "Active"**.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **🔹 1. Tùy Chỉnh Ngành Theo Mùa**
- **Ví dụ:** Nếu theo dõi ngành **Du lịch**, bạn có thể **thay đổi keyword** trong node **"Set Target Industry"** theo mùa:
  - **Hè:** `"hotel booking", "travel tech"`
  - **Đông:** `"ski resort", "winter tourism"`

### **🔹 2. Lưu Log Dữ Liệu Cho Phân Tích Sau**
- **Thêm node "Set" sau node BrowserAct** để lưu dữ liệu scrape vào **Google Sheets** hoặc **Airtable**.
- **Cách làm:**
  1. Thêm node **"Set"** mới.
  2. Chọn **"Google Sheets"** (hoặc **Airtable**).
  3. Điền **API Key** và **Sheet Name**.
  4. Chọn **"Append Row"** để thêm dữ liệu mới mỗi tháng.

### **🔹 3. Gửi Báo Cáo qua Email (Ngoài Slack)**
- **Thêm node "Email"** (n8n-nodes-base.email) sau node **"Send the report to the channel"**.
- **Cấu hình:**
  - **From:** `noreply@companyname.com`
  - **To:** `team@companyname.com`
  - **Subject:** `Monthly Industry Growth Report - [Ngành]`
  - **Body:** Sử dụng **template HTML** từ Slack.

### **🔹 4. Tự Động Cập Nhật Template BrowserAct**
- **Nếu template BrowserAct cũ**, bạn có thể:
  - **Tạo template mới** với **keyword mới**.
  - **Thay đổi node "BrowserAct"** sang template mới.

---

## **📌 Kết Luận**
Workflow này **giải phóng bạn khỏi công việc tra cứu thủ công**, giúp bạn **nhận được báo cáo định kỳ, chính xác và chuyên nghiệp** mỗi tháng. **Không cần code**, chỉ cần **cấu hình đúng các API Key** và **chọn ngành mục tiêu** là xong!

**🚀 Hãy áp dụng ngay và bắt đầu theo dõi ngành của bạn một cách thông minh!**

---
:::info[**Gợi Ý Hạ Tầng Cho n8n**]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::