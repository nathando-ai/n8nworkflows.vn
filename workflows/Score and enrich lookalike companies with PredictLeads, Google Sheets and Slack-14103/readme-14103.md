---
title: "🚀 Tự Động Tìm & Đánh Giá Công Ty Tương Tự (Lookalike) với AI – Từ Dữ Liệu Khách Hàng Tốt Nhất"
description: "Workflow tự động hóa 100% không code để tìm kiếm, đánh giá và lọc công ty tương tự (lookalike) của khách hàng hiện tại, enrich dữ liệu bằng tin tức, việc làm mới và công nghệ sử dụng, sau đó gửi cảnh báo Slack và email outreach tự động qua Gmail. Giúp các sếp tiết kiệm thời gian tìm kiếm lead chất lượng và tăng cường chiến lược outbound marketing."
slug: "tieu-dong-tim-danh-gia-lookalike-company-ai"
tags: [n8n, automation, lead-generation, ai-summarization, google-sheets, slack, gmail, predictleads]
keywords: [tự động hóa n8n, tìm kiếm công ty tương tự, lead scoring, enrich dữ liệu công ty, AI outreach email, PredictLeads API, tự động hóa marketing]
---

# 🚀 **Tự Động Tìm & Đánh Giá Công Ty Tương Tự (Lookalike) với AI – Giải Pháp Tối Ưu Hóa Lead Generation**

### **Nỗi Đau Của Các Sếp Trong Tìm Kiếm Lead Chất Lượng**
Các sếp thường phải mất **từ 5-10 giờ/tuần** để:
- **Tìm kiếm thủ công** công ty tương tự (lookalike) của khách hàng hiện tại.
- **Đánh giá** thông tin về tin tức mới, việc làm, và công nghệ sử dụng của họ.
- **Lọc và ưu tiên** lead có tiềm năng cao nhất.
- **Gửi email outreach** cá nhân hóa để tiếp cận.

Kết quả? **Thời gian dài, hiệu quả thấp, và dễ bỏ lỡ lead tiềm năng**.

**Workflow này giải quyết tất cả vấn đề trên bằng cách:**
✅ **Tự động hóa toàn bộ quy trình** từ tìm kiếm đến đánh giá lead.
✅ **Enrich dữ liệu** bằng tin tức mới, việc làm, và công nghệ sử dụng.
✅ **Đánh giá tự động** với hệ thống điểm số (0-100) dựa trên nhiều yếu tố.
✅ **Cảnh báo Slack** cho lead có tiềm năng cao.
✅ **Gửi email outreach tự động** qua Gmail với nội dung AI-generated.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** so với cách làm thủ công.
- **Tăng chất lượng lead** với hệ thống đánh giá tự động (scoring).
- **Cảnh báo ngay lập tức** khi phát hiện công ty đang phát triển mạnh (growth signals).
- **Outreach tự động** với email cá nhân hóa, tăng tỷ lệ phản hồi.
- **Dữ liệu được lưu trữ** trên Google Sheets để theo dõi và phân tích dài hạn.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** với:
   - Một sheet chứa **cột "domain"** (danh sách domain của khách hàng tốt nhất).
   - Một sheet mới tên **"Scored Lookalikes"** để lưu kết quả.
2. **API Key PredictLeads** (đăng ký tại [predictleads.com](https://predictleads.com)).
3. **Credentials Slack** (để gửi cảnh báo).
4. **Credentials Gmail** (để gửi email outreach tự động).
5. **OpenAI API Key** (để tạo nội dung email AI).
6. **VPS Self-hosted n8n** (để workflow chạy 24/7).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [link gốc](https://n8n.io/workflows/14103) và import vào n8n Editor.
- **Cách 2:** Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/14103) và dán vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **19 node**, các sếp cần chú ý cấu hình các node sau:

##### **A. Node "Read Best Client Domains" (Google Sheets)**
- **Chọn credentials:** Lựa chọn tài khoản Google Sheets đã kết nối.
- **Chọn sheet:** Chọn sheet chứa **cột "domain"** (ví dụ: `Sheet1`).
- **Lưu ý:** Sheet phải có **cột tên "domain"** (không case-sensitive).

##### **B. Node "PredictLeads" (3 node)**
- **Credentials:** Điền **API Key PredictLeads** (mã API từ [predictleads.com](https://predictleads.com)).
- **Node "Retrieve Company"**: Không cần cấu hình thêm.
- **Node "Retrieve Company News Events"**: Đảm bảo **operation = "newsEvents"**.
- **Node "Retrieve Company Job Openings"**: Đảm bảo **operation = "jobOpenings"**.
- **Node "Retrieve Technologies"**: Đảm bảo **operation = "technologyDetections"**.

##### **C. Node "Detect Growth Signals" (Code)**
- **Mở node này** và chỉnh sửa **mảng `growthSignals`** (nếu muốn thay đổi tiêu chí phát hiện growth).
- **Ví dụ mặc định:**
  ```javascript
  const growthSignals = [
    "launch", "partnership", "funding", "new hire", "product update"
  ];
  ```

##### **D. Node "Calculate Composite Score" (Code)**
- **Điểm số mặc định** là **0-100**, dựa trên:
  - **Tin tức mới** (tỷ lệ gần đây).
  - **Việc làm mới** (số lượng).
  - **Công nghệ tương đồng** (trùng khớp với danh sách mục tiêu).
  - **Tương đồng vùng miền**.
- **Lưu ý:** Các sếp có thể **thay đổi trọng số** trong code để ưu tiên yếu tố nào.

##### **E. Node "Filter High Scores" (If)**
- **Điểm ngưỡng mặc định** là **70**. Nếu muốn thay đổi, chỉnh sửa **value** trong node này.

##### **F. Node "Build Outreach Prompt" & "Generate Outreach Email" (Code + HTTP Request)**
- **OpenAI API Key** phải được đặt trong **environment variables** của n8n.
- **Node "Generate Outreach Email"** sử dụng API **GPT-3.5** để tạo email outreach tự động.

##### **G. Node "Send Outreach Email" (Gmail)**
- **Chọn credentials Gmail** đã kết nối.
- **Địa chỉ email mặc định** là `{{$json["email"]}}` (cần đảm bảo dữ liệu email được enrich từ PredictLeads).

##### **H. Node "Send Growth Alert" & "Send High Score Alert" (Slack)**
- **Chọn channel Slack** để nhận cảnh báo.
- **Thông báo mẫu** sẽ tự động hiển thị thông tin công ty, điểm số, và growth signals.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với **dữ liệu mẫu** (ví dụ: 1-2 domain từ sheet).
2. **Bật Active** workflow sau khi kiểm tra không có lỗi.
3. **Monitor** trên Slack và Google Sheets để xem kết quả.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết hợp với Zapier/Make** để tự động cập nhật lead vào CRM (HubSpot, Salesforce).
2. **Lưu log hoạt động** vào Google Sheets hoặc Firebase để theo dõi hiệu suất.
3. **Tự động gửi báo cáo hàng tuần** qua Slack/Email với lead mới được phát hiện.
4. **Thêm node AI chatbot** (n8n-nodes-ai) để trả lời tin nhắn từ lead.
5. **Tối ưu score** bằng cách thêm yếu tố **số lượng khách hàng hiện tại** của công ty.
:::

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn:
✔ **Tự động hóa lead generation** mà không cần viết code.
✔ **Tăng chất lượng lead** với hệ thống đánh giá tự động.
✔ **Tiết kiệm thời gian** để tập trung vào chiến lược outbound.

**Hãy áp dụng ngay để bắt đầu tìm kiếm và tiếp cận lead chất lượng trong vài phút!**

---
:::note[CHÚ Ý CUỐI CUNG]
- **N8n Self-hosted** là lựa chọn tối ưu để workflow chạy 24/7.
- **Dữ liệu API PredictLeads** có giới hạn, các sếp nên kiểm tra tài khoản.
- **Email outreach** có thể bị đánh dấu spam nếu không cấu hình Gmail đúng.
:::

---
**👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (Mã giảm giá: **VPSN8N** - giảm tới 39%) để tự động hóa workflow 24/7!**