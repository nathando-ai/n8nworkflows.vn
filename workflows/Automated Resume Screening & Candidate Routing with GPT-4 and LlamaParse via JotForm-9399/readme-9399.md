---
title: "🤖 **Tự Động Học Viên Xét Lựa & Phân Loại Ứng Viên với GPT-4 + LlamaParse (Không Cần Code!)**"
description: "Workflow tự động hóa tuyển dụng giúp HR tiết kiệm **50% thời gian** trong việc xét duyệt hồ sơ ứng viên bằng AI GPT-4 và công cụ phân tích văn bản LlamaParse. Từ đó phân loại ứng viên thành **Mạnh, Trung Bình, Yếu** và tự động gửi email phản hồi cá nhân hóa."
slug: "tuyen-dung-tu-dong-hoa-gpt-4-llamaparse"
tags: [n8n, automation, recruitment, ai, gpt-4, llama, jotform, gmail, no-code]
keywords: [tự động hóa tuyển dụng, xét duyệt hồ sơ ứng viên, gpt-4 tuyển dụng, llama parse n8n, workflow tuyển dụng không code, ai trong tuyển dụng]
---

# **🚀 Tự Động Học Viên Xét Lựa & Phân Loại Ứng Viên với GPT-4 + LlamaParse**

### **📌 Nỗi Đau Của HR Trong Quá Trình Tuyển Dụng**
Các sếp HR thường phải mất **từ 2-5 tiếng/ngày** để:
- **Xem xét hàng trăm hồ sơ** ứng viên.
- **Phân loại** ứng viên theo phù hợp với vị trí.
- **Gửi email phản hồi** một cách cá nhân hóa.
- **Lọc ra ứng viên mạnh** để gọi phỏng vấn.

**Kết quả?** Thời gian và năng suất bị "chôn vùi" trong công việc lặp lại, trong khi ứng viên tốt có thể bị bỏ qua vì thiếu thời gian kiểm tra kỹ lưỡng.

**Giải pháp?** **Workflow này tự động hóa toàn bộ quá trình** bằng AI GPT-4 và công cụ phân tích văn bản **LlamaParse**, giúp HR:
✅ **Tiết kiệm 50% thời gian** trong việc xét duyệt hồ sơ.
✅ **Phân loại ứng viên** thành **Mạnh/Moderate/Yếu** một cách chính xác.
✅ **Gửi email tự động** với nội dung cá nhân hóa cho từng loại ứng viên.
✅ **Lọc ra ứng viên ưu tiên** để HR gọi phỏng vấn.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài **n8n trên VPS riêng (Self-hosted)** để tránh giới hạn free tier.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 5-10 tiếng/ngày** trong việc xét duyệt hồ sơ.
- **Phân loại ứng viên chính xác** (Mạnh/Moderate/Yếu) bằng AI GPT-4.
- **Email tự động** với nội dung cá nhân hóa cho từng loại ứng viên.
- **HR chỉ cần tập trung vào ứng viên ưu tiên** (Mạnh) thay vì phải xem xét tất cả.
- **Không cần viết code** – chỉ cần cấu hình và chạy.
:::

---

### **🔧 Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản JotForm** (để ứng viên nộp hồ sơ).
2. **API Key JotForm** (để n8n lấy dữ liệu form).
3. **Tài khoản LlamaCloud** (để phân tích PDF hồ sơ).
4. **API Key LlamaCloud** (để upload và phân tích văn bản).
5. **Tài khoản OpenAI** (để sử dụng GPT-4 phân tích ứng viên).
6. **Tài khoản Gmail** (để gửi email tự động phản hồi ứng viên và HR).

---

### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/9399](https://n8n.io/workflows/9399) và import vào **n8n Editor**.
- **Cách 2:** Copy toàn bộ JSON và dán vào **Create Workflow** → **Import JSON**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **16 node**, các sếp cần chú ý cấu hình **các node quan trọng sau**:

##### **🔹 Node 1: JotForm Trigger**
- **Cấu hình:**
  - Thêm **credentials JotForm** (tên: `jotFormApi`).
  - Chọn **Form ID** của form tuyển dụng (sử dụng template [Job Application](https://www.jotform.com/form-templates/job-application)).
  - **Lưu ý:** Form phải có **field để upload CV (PDF)**.

##### **🔹 Node 2-5: LlamaCloud (Phân Tích PDF)**
- **Cấu hình:**
  - Thêm **credentials HTTP Header Auth** (tên: `httpHeaderAuth`).
  - **Header:** `Authorization = Bearer YOUR_LLAMACLOUD_API_KEY`.
  - **Cần thiết:** Cấu hình cho **Download Resume**, **Upload to LlamaCloud**, **Check Parsing**, **Retrieve Result**.

##### **🔹 Node 6-7: AI Agent & GPT-4 Phân Tích**
- **Cấu hình:**
  - Thêm **credentials OpenAI** (tên: `openAiApi`).
  - **Model:** Chọn `gpt-4o-mini` (hoặc `gpt-4` nếu có budget).
  - **Prompt AI:** Workflow đã tự động cấu hình, **không cần chỉnh sửa** (nếu muốn tối ưu, có thể thêm **custom prompt** trong node `Clean Data`).

##### **🔹 Node 8-11: Gmail Tự Động Gửi Email**
- **Cấu hình:**
  - Thêm **credentials Gmail OAuth2** (tên: `gmailOAuth2`).
  - **Cần thiết:** Cấu hình cho **Send Email_1**, **Send Email_2**, **Send Email_3**, **Send Email to HR**.
  - **Thay thế placeholder** trong email:
    - `[Company Name]` → Tên công ty của bạn.
    - `[HR Manager Name]` → Tên HR quản lý.
    - `[Interview Date]` → Ngày phỏng vấn (nếu ứng viên mạnh).

##### **🔹 Node 12: Clean Data (Code)**
- **Lưu ý:** Node này **xóa dữ liệu nhạy cảm** (ví dụ: email, số điện thoại) trước khi gửi email phản hồi.
- **Không cần chỉnh sửa** trừ khi muốn **tùy chỉnh logic xóa dữ liệu**.

##### **🔹 Node 13: Get Form Data**
- **Cấu hình:**
  - Sử dụng **credentials HTTP Header Auth** (cùng với LlamaCloud).
  - **Header:** `APIKEY = YOUR_JOTFORM_API_KEY`.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với **dữ liệu mẫu** (nộp form JotForm với CV PDF).
2. **Kiểm tra:**
   - AI có phân tích đúng không?
   - Email phản hồi có được gửi không?
   - HR có nhận được báo cáo ứng viên mạnh không?
3. **Bật Active** workflow sau khi test thành công.

---

### **✍️ Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram:**
   - Thêm node **Slack Webhook** để thông báo khi có ứng viên mạnh.
   - **Cách làm:** Thêm node `httpRequest` (Slack API) sau node `Switch`.

2. **Lưu Log Phân Tích:**
   - Thêm node **Google Sheets** hoặc **Airtable** để lưu lịch sử phân tích ứng viên.
   - **Ưu điểm:** Dễ dàng theo dõi và báo cáo cho lãnh đạo.

3. **Tự Động Gửi Báo Cáo Định Kỳ:**
   - Sử dụng **node `gmail`** để gửi **tóm tắt ứng viên mới** vào cuối tuần.
   - **Cách làm:** Thêm node `switch` kiểm tra ngày và gửi email tự động.

4. **Tối ưu Prompt AI:**
   - Nếu muốn **AI phân tích chi tiết hơn**, chỉnh sửa node `Clean Data` (JavaScript) để **cập nhật logic**.
   - **Ví dụ:**
     ```javascript
     // Thêm yêu cầu phân tích kỹ năng cụ thể
     return {
       ...node.input,
       analysis: "Phân tích kỹ năng: JavaScript, Python, SQL; đánh giá mức độ phù hợp với vị trí."
     };
     ```

---

### **📌 Kết Luận**
Workflow này **giải phóng HR khỏi công việc lặp lại**, giúp tập trung vào **các ứng viên ưu tiên** và **quyết định tuyển dụng thông minh**. Với **AI GPT-4 + LlamaParse**, việc phân tích hồ sơ trở nên **chính xác và nhanh chóng**, trong khi **email tự động** đảm bảo ứng viên được phản hồi kịp thời.

**🚀 Hành động ngay:**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với 1-2 ứng viên mẫu** trước khi áp dụng toàn bộ.
3. **Tối ưu hóa email** để phù hợp với brand của công ty.

**Không cần code, không cần chuyên gia IT – chỉ cần n8n!** 🎉

---
**🔗 [Tải workflow nguyên bản](https://n8n.io/workflows/9399)**
**💬 Có thắc mắc? Để lại comment bên dưới!**