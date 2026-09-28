---
title: "🚀 Tự Động Hóa Đánh Giá Lead Sẵn Sàng Sản Phẩm (PQL) với Amplitude, AI Claude & PDL – Để Sales Routing Hiệu Quả"
description: "Workflow tự động hóa đánh giá và phân loại Lead sẵn sàng sản phẩm (PQL) từ Amplitude, enrich dữ liệu với AI Claude và PDL, gửi cảnh báo Slack cho Sales – tiết kiệm 80% thời gian phân tích thủ công."
slug: "tieu-dong-hoa-danh-gia-lead-pql-amplitude-claude-pdl"
tags: [n8n, automation, lead-generation, ai-summarization, sales-routing, amplitude, slack-integration]
keywords: [tự động hóa lead pql, n8n workflow amplitude, đánh giá lead sẵn sàng sản phẩm, ai claude trong n8n, enrich lead với pdl, cảnh báo sales slack]
---

# 🚀 **Tự Động Hóa Đánh Giá Lead Sẵn Sàng Sản Phẩm (PQL) với Amplitude, AI Claude & PDL**

## **💡 Giải Pháp Cho Nỗi Đau Của Các Sếp Sales & Marketing**
Bạn đã bao giờ phải:
- **Làm thủ công** phân tích hàng trăm lead từ Amplitude để tìm ra những lead "hot" sẵn sàng mua?
- **Mất thời gian** enrich dữ liệu công ty (size, ngành nghề, tech stack) từ nhiều nguồn khác nhau?
- **Không biết** cách phân loại lead sao cho phù hợp với Sales Team?
- **Chưa có hệ thống cảnh báo** tự động khi lead mới xuất hiện?

Workflow này **tự động hóa toàn bộ quy trình** từ nhận lead từ Amplitude → enrich dữ liệu → đánh giá bằng AI → cảnh báo Slack cho Sales, giúp bạn **tiết kiệm 80% thời gian phân tích thủ công** và **tăng hiệu quả chuyển đổi lead thành khách hàng**.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tự động nhận lead** từ Amplitude khi họ vào cohort PQL.
✅ **Enrich dữ liệu** công ty (size, ngành nghề, tech stack) bằng PDL + AI Perplexity.
✅ **Đánh giá lead** từ 0-10 điểm dựa trên ICP (Ideal Customer Profile) trong Google Docs.
✅ **Phân loại lead** theo mức độ "hot" (High/Medium/Low) và gửi cảnh báo Slack cho Sales.
✅ **Tiết kiệm 80% thời gian** so với cách làm thủ công.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Amplitude Webhook**:
   - Tạo **Cohort Webhook** trong Amplitude với path: `amplitude-pql-cohort`.
   - Chọn cohort PQL của bạn và thiết lập cadence **real-time**.

2. **API Keys & Credentials**:
   - **PDL API Key** (Peopledatalabs) → Enrich dữ liệu công ty.
   - **Perplexity API Key** → Nghiên cứu công ty bằng AI.
   - **Anthropic API Key** (Claude) → Đánh giá lead.
   - **Google Docs OAuth2** → Truy cập file ICP Criteria.
   - **Slack OAuth2** → Gửi cảnh báo.

3. **Google Docs ICP Criteria**:
   - Tạo một **Google Doc** với cấu trúc như sau:
     ```
     IDEAL CUSTOMER PROFILE:
     - Company size: 50-500 employees
     - Industries: SaaS, Tech, Finance
     - Job titles: VP, Director, Manager

     USAGE THRESHOLDS:
     - High: 10+ sessions, 5+ features
     - Medium: 5-9 sessions, 3-4 features
     - Low: <5 sessions
     ```
   - **Chia sẻ file** với quyền "Xem" cho n8n.

4. **Slack Workspace**:
   - Tạo **Slack App** và cấp quyền `chat:write`, `channels:read`.
   - Lấy **channel ID** (vd: `C01234ABCDE`) để gửi cảnh báo.
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/10010](https://n8n.io/workflows/10010) hoặc copy/paste JSON vào **n8n Editor**.
- **Nhấn "Import"** và chọn **Create New Workflow**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **A. Cấu hình Webhook Amplitude**
- Trong node **"Amplitude Cohort Webhook"**, đảm bảo:
  - **Path**: `amplitude-pql-cohort` (không đổi).
  - **HTTP Method**: `POST`.
  - **Credentials**: Không cần (webhook sẽ tự động nhận dữ liệu từ Amplitude).

##### **B. Thiết lập PDL Enrichment**
- Trong node **"PDL Enrich"**:
  - **Credentials**: Chọn `httpHeaderAuth` (tạo trước trong n8n).
  - **Header Name**: `X-Api-Key`.
  - **Header Value**: Nhập **PDL API Key** của bạn.

##### **C. Cấu hình Perplexity AI Research**
- Trong node **"Company Research"**:
  - **Credentials**: Chọn `perplexityApi` (tạo trước).
  - **API Key**: Nhập key từ [perplexity.ai](https://www.perplexity.ai/).

##### **D. Kết nối Google Docs ICP Criteria**
- Trong node **"ICP Guidelines"**:
  - **Credentials**: Chọn `googleDocsOAuth2Api`.
  - **Operation**: `get`.
  - **File ID**: Nhập **ID của Google Doc ICP** (lấy từ liên kết share: `https://docs.google.com/document/d/[ID]/edit`).

##### **E. Cấu hình Slack Alert**
- Trong node **"Send Hot PQL Alert"**:
  - **Credentials**: Chọn `slackOAuth2`.
  - **Channel ID**: Nhập **channel ID** của Slack (vd: `C01234ABCDE`).
  - **Message Format**: Đã tự động cấu hình, **không cần chỉnh** (n8n sẽ tự động format).

##### **F. Cấu hình AI Claude (Anthropic)**
- Trong node **"Anthropic Chat Model"**:
  - **Model**: `claude-sonnet-4-20250514` (đã mặc định).
  - **Credentials**: Chọn `anthropicApi` (tạo trước với API Key từ [anthropic.com](https://www.anthropic.com/)).

##### **G. Merge & Parse Data**
- Các node **"Merge All Sources"**, **"Merge PQL Data"**, **"Parse & Structure PQL"** đều **không cần chỉnh** (n8n tự động xử lý).

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gửi một **test event** từ Amplitude (vd: tạo một lead giả vào cohort PQL).
   - Kiểm tra **Slack** xem có nhận được cảnh báo không.
2. **Bật Active**:
   - Nhấn **"Active"** trên workflow.
   - **Xem log** để đảm bảo không có lỗi.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Lưu log vào Google Sheets/Database**:
   - Thêm node **Google Sheets** sau **"Send Hot PQL Alert"** để lưu lịch sử lead đã cảnh báo.
   - Cấu hình **append mode** để không bị trùng dữ liệu.

2. **Gửi báo cáo định kỳ cho Sales**:
   - Sử dụng **n8n + Google Calendar** để gửi **báo cáo hàng tuần** về lead hot nhất.
   - Ví dụ: "Top 5 Lead Hot nhất tuần qua" với score cao nhất.

3. **Kết hợp với CRM (HubSpot/Salesforce)**:
   - Thêm node **HubSpot API** sau **"Parse & Structure PQL"** để tự động cập nhật lead vào CRM.
   - Cấu hình **properties** như `pql_score`, `routing_category`, `sales_guidance`.

4. **Tối ưu ICP Criteria**:
   - Cập nhật **Google Docs ICP** định kỳ để phản ánh thay đổi thị trường.
   - Sử dụng **node "Set"** để tự động update rules trong workflow.

5. **Cảnh báo đa kênh**:
   - Thêm node **Email** (Gmail/SendGrid) để gửi cảnh báo cho Sales nếu Slack không phù hợp.

---

### 📌 **Kết luận**
Workflow này **giải phóng Sales Team** khỏi công việc phân tích lead thủ công, đồng thời **tăng hiệu quả chuyển đổi** bằng cách tự động:
✔ **Nhận lead** từ Amplitude.
✔ **Enrich & đánh giá** bằng AI Claude + PDL.
✔ **Phân loại & cảnh báo** Slack cho Sales.
✔ **Hoạt động 24/7** mà không cần can thiệp.

**🚀 Hãy áp dụng ngay workflow này và xem Sales Team của bạn sẽ tiết kiệm bao nhiêu thời gian!**
Nếu có vấn đề, hãy **comment bên dưới** hoặc liên hệ với tác giả [Connor Provines](https://n8n.io/workflows/10010) để hỗ trợ.

---
**🔥 Bắt đầu tự động hóa Sales Routing ngay hôm nay!** 🔥