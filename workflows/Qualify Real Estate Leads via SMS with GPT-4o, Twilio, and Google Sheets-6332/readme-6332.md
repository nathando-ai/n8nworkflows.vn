---
title: "🏠 **Tự Động Hóa Xác Minh Lead Bất Động Sản qua SMS với GPT-4o, Twilio & Google Sheets (N8n)**
description: "Workflow tự động hóa 100% không code giúp các sếp bất động sản nhanh chóng xác minh lead qua SMS thông minh, lưu trữ chat history, và chuyển lead chất lượng đến chủ sở hữu với AI GPT-4o. Tiết kiệm thời gian lên đến 80% và tăng tỷ lệ chuyển đổi lead."
slug: "tieu-dong-hoa-xac-minh-lead-bat-dong-san-qua-sms"
tags: [n8n, automation, no-code, real-estate, ai-chatbot, twilio, google-sheets, gpt-4o, lead-nurturing]
keywords: [tự động hóa bất động sản, xác minh lead SMS AI, n8n workflow bất động sản, chatbot bất động sản, tự động hóa Twilio, lưu trữ lead Google Sheets, AI GPT-4o cho lead]
---

# 🚀 **Tự Động Hóa Xác Minh Lead Bất Động Sản qua SMS với AI GPT-4o**

## **Nỗi Đau Của Các Sếp Bất Động Sản**
Hàng ngày, các sếp bất động sản phải:
- **Làm thủ công** cuộc gọi/SMS xác minh lead, tốn thời gian và dễ bị lỡ lead.
- **Không lưu trữ chat history**, dẫn đến mất bối cảnh khi tiếp nhận lead sau này.
- **Tỷ lệ chuyển đổi thấp** vì quá trình xác minh không được cá nhân hóa.
- **Không theo dõi lead** một cách hệ thống, dẫn đến mất cơ hội bán hàng.

**Workflow này giải quyết tất cả!** Sử dụng **AI GPT-4o** để tự động xác minh lead qua SMS, lưu trữ chat history trên **Supabase**, và chuyển lead chất lượng đến chủ sở hữu thông qua **Twilio**. Kết quả? **Tiết kiệm 80% thời gian**, tăng tỷ lệ chuyển đổi lead, và hoạt động **24/7 tự động**.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính bảo mật và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tự động hóa 100% quá trình xác minh lead** qua SMS, không cần can thiệp thủ công.
✅ **AI GPT-4o** đặt câu hỏi chuyên nghiệp, xác minh nhu cầu mua bán một cách chính xác.
✅ **Lưu trữ chat history** trên **Supabase**, giúp chủ sở hữu tiếp nhận lead một cách bối cảnh.
✅ **Chuyển lead chất lượng** đến chủ sở hữu thông qua SMS tự động.
✅ **Lưu trữ lead vào Google Sheets** để theo dõi và phân tích hiệu suất.
✅ **Hoạt động 24/7**, không giới hạn số lượng lead xử lý.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Twilio** (để gửi/receive SMS):
   - [Đăng ký Twilio](https://login.twilio.com/) và mua số điện thoại hỗ trợ SMS.
   - **API Key** và **Account SID** (tìm trong Dashboard Twilio).
2. **Tài khoản OpenAI** (để sử dụng GPT-4o):
   - [Đăng ký OpenAI](https://platform.openai.com/) và lấy **API Key**.
3. **Tài khoản Google Cloud** (để kết nối Google Sheets):
   - [Tạo OAuth2 Credentials](https://developers.google.com/sheets/api/quickstart/python) và lấy **Client ID/Secret**.
4. **Tài khoản Supabase** (để lưu trữ chat history):
   - [Đăng ký Supabase](https://supabase.com/) và lấy **PostgreSQL credentials** (Host, Username, Password, Database Name).
5. **Google Sheet mẫu** (cần sao chép và cập nhật ID):
   - [Lấy mẫu Google Sheet](https://docs.google.com/spreadsheets/d/1jSlYXSBA9BJvSuMiqFUJo3omztNJtbejNYEopfbGWN8/edit?usp=sharing).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/6332](https://n8n.io/workflows/6332) và import vào **n8n Editor**.
- **Cách 2:** Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/6332) và dán vào **Create Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Sau khi import, các sếp cần cấu hình **các node quan trọng** như sau:

##### **A. Cấu Hình Twilio (SMS)**
- **Node:** `Initial Text Message`, `Wait for Text Response`, `Thank Your Text`, `Response Text from Agent`, `Send Lead to Owner`.
- **Thao tác:**
  - Vào **Credentials** trong n8n → Thêm **Twilio API**.
  - Nhập:
    - **Account SID** (từ Twilio Dashboard).
    - **Auth Token** (từ Twilio Dashboard).
    - **From Number** (số điện thoại Twilio bạn mua).
    - **To Number** (số điện thoại của lead, sẽ được lấy từ form).

##### **B. Cấu Hình OpenAI (GPT-4o)**
- **Node:** `OpenAI Chat Model1`, `OpenAI Chat Model2`, `Real Estate Qualifier`, `Summarize Transcript`.
- **Thao tác:**
  - Vào **Credentials** → Thêm **OpenAI API**.
  - Nhập **API Key** từ OpenAI.
  - Đảm bảo **model** được chọn là `gpt-4o` (hoặc `gpt-4o-mini` nếu tiết kiệm chi phí).

##### **C. Cấu Hình Supabase (Lưu Trữ Chat History)**
- **Node:** `Postgres Chat Memory`, `Query Supabase for conversation history`.
- **Thao tác:**
  - Vào **Credentials** → Thêm **PostgreSQL**.
  - Nhập thông tin từ Supabase:
    - **Host**: `db.supabase.co` (hoặc host của bạn).
    - **Username/Password**: Từ **Database > Connection Info** trên Supabase.
    - **Database Name**: Tên database của bạn.
  - Trong **AI Agent node**, liên kết **PostgreSQL credentials** để lưu trữ chat history.

##### **D. Cấu Hình Google Sheets (Lưu Lead)**
- **Node:** `Store results in google`.
- **Thao tác:**
  - Vào **Credentials** → Thêm **Google Sheets OAuth2 API**.
  - Chọn **Google Sheet** đã sao chép từ mẫu.
  - Cập nhật **Sheet Name** và **Range** (ví dụ: `Sheet1!A1`).
  - Chọn **Operation: Append** để thêm lead mới vào sheet.

##### **E. Cấu Hình Form Trigger (Bắt Đầu Workflow)**
- **Node:** `On form submission`.
- **Thao tác:**
  - Nếu sử dụng **Google Form**, liên kết với **Webhook** trong n8n.
  - Nếu sử dụng **form khác**, đảm bảo **payload** chứa số điện thoại lead (`phone_number`).

#### **3. Kích Hoạt ⚡️**
- **Test Run:** Chạy **Test Execution** với dữ liệu mẫu (ví dụ: số điện thoại `0901234567`).
- **Bật Active:** Sau khi kiểm tra thành công, **bật Active** workflow.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tùy Chỉnh Câu Hỏi AI** (Node `Real Estate Qualifier`):
   - Mở rộng prompt để hỏi thêm thông tin như:
     - "Bạn đang tìm mua/bán nhà ở đâu?"
     - "Ngân sách dự kiến là bao nhiêu?"
     - "Thời gian muốn mua/bán là khi nào?"
   - Ví dụ:
     ```json
     "prompt": "Bạn là một chuyên gia bất động sản. Hỏi lead về nhu cầu mua/bán nhà với các câu hỏi sau:
     1. Bạn đang tìm mua/bán nhà ở đâu? (TP.HCM, Hà Nội, tỉnh khác...)
     2. Ngân sách dự kiến là bao nhiêu triệu?
     3. Thời gian muốn mua/bán là khi nào? (Ngay lập tức, 3 tháng, 6 tháng...)
     4. Bạn có yêu cầu về diện tích, tầng, vị trí đặc biệt không?"
     ```

2. **Gửi Báo Cáo Định Kỳ** (Node `twilio` + `googleSheets`):
   - Thêm một **workflow phụ** để gửi **báo cáo hàng tuần** về lead mới đến Slack/Email.
   - Sử dụng **n8n-nodes-base.email** hoặc **n8n-nodes-base.slack** để thông báo.

3. **Lưu Log Chat** (Node `stickyNote`):
   - Thêm **Sticky Note** để ghi lại lỗi hoặc thông tin debug (ví dụ: `Error: Twilio API failed`).

4. **Kết Nối với CRM** (Ngoài Google Sheets):
   - Thêm **Airtable** hoặc **HubSpot** để tự động sync lead vào hệ thống quản lý.

5. **Tối Ưu Hiệu Suất GPT-4o**:
   - Sử dụng **gpt-4o-mini** để tiết kiệm chi phí (nếu độ chính xác đủ).
   - Thêm **temperature** trong prompt để AI trả lời linh hoạt hơn.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp bất động sản, giúp họ tập trung vào **quyết định chiến lược** thay vì làm thủ công. Với **AI GPT-4o**, lead được xác minh một cách **chuyên nghiệp và cá nhân hóa**, trong khi **chat history** được lưu trữ an toàn trên **Supabase**. Cuối cùng, lead chất lượng được chuyển đến chủ sở hữu thông qua **SMS tự động**, tăng tỷ lệ chuyển đổi lên **30-50%**.

**🚀 Hãy áp dụng ngay và bắt đầu tự động hóa lead của bạn!**
Nếu gặp vấn đề, liên hệ tác giả tại **rbreen@ynteractive.com** hoặc comment bên dưới.

---
**#TựĐộngHóaBấtĐộngSản #AIQuảnLýLead #N8nWorkflow #TwilioSMS #GPT4oBấtĐộngSản**