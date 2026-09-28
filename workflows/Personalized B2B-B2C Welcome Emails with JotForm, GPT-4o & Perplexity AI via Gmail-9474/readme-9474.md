---
title: "🤖 **Tự Động Hóa Email Chào Mừng Cá Nhân Hóa B2B & B2C Siêu Tốc Với JotForm, GPT-4o & Perplexity AI**"
description: "Workflow tự động hóa gửi email chào mừng cá nhân hóa cho khách hàng B2B (công ty) và B2C (cá nhân) từ JotForm, sử dụng trí tuệ nhân tạo GPT-4o và Perplexity AI. Giúp doanh nghiệp tiết kiệm 100% thời gian thủ công, tăng tỷ lệ chuyển đổi lên 30%+."
slug: "tieu-dong-hoa-email-chao-mung-b2b-b2c-voi-jotform-gpt-4o-perplexity"
tags: [n8n, automation, no-code, email marketing, ai, gpt-4o, perplexity, jotform, gmail, b2b, b2c]
keywords: [n8n workflow tự động hóa email, gửi email chào mừng cá nhân hóa, tự động hóa bán hàng, ai chatbot, gpt-4o tự động hóa, perplexity ai, jotform automation, email marketing tự động]
---

# 🚀 **Tự Động Hóa Email Chào Mừng Cá Nhân Hóa B2B & B2C Siêu Tốc Với JotForm, GPT-4o & Perplexity AI**

### **Giải pháp cho doanh nghiệp nào?**
Các sếp đang gặp phải vấn đề:
- **Thủ công gửi email chào mừng** tốn thời gian và dễ sai sót.
- **Không phân biệt B2B (công ty) và B2C (cá nhân)**, dẫn đến tỷ lệ mở email thấp.
- **Không cá nhân hóa nội dung**, khiến khách hàng cảm thấy không quan tâm.
- **Không biết cách tự động hóa** mà không cần viết code.

**Workflow này sẽ giúp các sếp:**
✅ **Tự động nhận lead từ JotForm** và phân loại ngay lập tức.
✅ **Phân biệt email công ty (B2B) và email cá nhân (B2C)**.
✅ **Sử dụng Perplexity AI** để nghiên cứu công ty (nếu là B2B).
✅ **Sử dụng GPT-4o** để viết email cá nhân hóa **một cách tự động**.
✅ **Gửi email qua Gmail** một cách hoàn toàn tự động.

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng** cho bộ phận Marketing/Sales.
- **Tăng tỷ lệ mở email lên 30%+** nhờ nội dung cá nhân hóa.
- **Phân loại tự động B2B vs B2C** mà không cần con người can thiệp.
- **Hoạt động 24/7** mà không cần giám sát.
- **Cải thiện trải nghiệm khách hàng** với email phù hợp với từng loại lead.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản JotForm** (để nhận lead từ form đăng ký).
   - Form phải có **các trường `name` và `email`** (có thể thêm trường `company` để cải thiện chất lượng).
   - [Đăng ký JotForm miễn phí](https://www.jotform.com/?partner=fahmifahreza) (sử dụng mã giới thiệu `fahmifahreza` để nhận bonus).

2. **API Key của Perplexity AI** (để nghiên cứu công ty).
   - [Đăng ký Perplexity API](https://www.perplexity.ai/api) (miễn phí cho một số lượng request nhất định).

3. **API Key của OpenAI** (để sử dụng GPT-4o viết email).
   - [Đăng ký OpenAI API](https://platform.openai.com/signup) (đăng ký tài khoản và tạo API key).

4. **Tài khoản Gmail** (để gửi email tự động).
   - **Không dùng Gmail cá nhân** (sử dụng Gmail doanh nghiệp hoặc tạo một tài khoản riêng cho automation).
   - Cài đặt **2FA** và tạo **OAuth2 credentials** trong n8n.

5. **n8n Self-hosted** (để workflow chạy 24/7).
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow này:
- **Cách 1: Import từ file JSON**
  1. Tải workflow từ [n8n.io/workflows/9474](https://n8n.io/workflows/9474).
  2. Trên trang workflow, nhấn **Export** (icon ba chấm) → Chọn **JSON**.
  3. Trên n8n Editor, nhấn **Import** → Chọn file JSON vừa tải.
- **Cách 2: Copy/Paste JSON**
  1. Trên trang workflow, nhấn **Export** → Chọn **JSON**.
  2. Trên n8n Editor, nhấn **Import** → Chọn **Paste JSON**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Sau khi import, các sếp **phải cấu hình** các node sau:

##### **🔹 Node 1: "On New JotForm Submission" (jotFormTrigger)**
- **Chọn credentials**: `jotFormApi` (đã tạo khi đăng ký JotForm).
- **Chọn form**: Chọn form đăng ký của các sếp.
- **Kiểm tra trường dữ liệu**:
  - **Bắt buộc**: `name` và `email`.
  - **Khuyến nghị**: `company` (nếu có) để cải thiện chất lượng email B2B.

##### **🔹 Node 2: "Extract Domain from Email" (set)**
- **Node này tự động trích xuất domain** (ví dụ: `jane@mycompany.com` → `mycompany.com`).
- **Không cần chỉnh sửa**, n8n sẽ tự động xử lý.

##### **🔹 Node 3: "If Work Email" (if)**
- **Cấu hình điều kiện**:
  - **Nếu email là công ty (B2B)**: Chỉnh sửa danh sách domain công ty (ví dụ: `gmail.com`, `@company.vn`, `@corp.com`).
  - **Nếu email là cá nhân (B2C)**: Sử dụng danh sách domain cá nhân (ví dụ: `gmail.com`, `yahoo.com`, `icloud.com`).

##### **🔹 Node 4: "Research Company via Perplexity AI" (perplexity)**
- **Chọn credentials**: `perplexityApi`.
- **Model**: Đã mặc định là `sonar-pro` (tốt nhất cho nghiên cứu công ty).
- **Prompt mẫu**:
  ```plaintext
  Research the company {company_name} and provide:
  1. Industry
  2. Size (number of employees)
  3. Recent news (last 3 months)
  4. Key products/services
  ```
  (Các sếp có thể **tùy chỉnh prompt** để phù hợp với ngành nghề.)

##### **🔹 Node 5: "OpenAI Chat Model" (lmChatOpenAi)**
- **Chọn credentials**: `openAiApi`.
- **Model**: Đã mặc định là `gpt-4o` (mô hình mới nhất của OpenAI).
- **Prompt mẫu cho B2B**:
  ```plaintext
  You are a professional email writer. Draft a B2B welcome email for {name} from {company_name}.
  Include:
  - Personalized greeting
  - Reference to their industry/company size
  - Mention recent news about their company
  - Call-to-action to schedule a call
  ```
- **Prompt mẫu cho B2C**:
  ```plaintext
  You are a friendly email writer. Draft a B2C welcome email for {name}.
  Keep it warm, personal, and direct. Include:
  - Personalized greeting
  - Brief introduction about the product/service
  - Soft call-to-action to explore further
  ```

##### **🔹 Node 6: "AI Company Email Writer" & "AI Personal Email Writer" (agent)**
- **Node này sử dụng LangChain Agent** để viết email tự động.
- **Không cần chỉnh sửa**, nhưng các sếp có thể **cải thiện prompt** trong node `lmChatOpenAi` trước đó.

##### **🔹 Node 7: "Send Welcome Email" (gmail)**
- **Chọn credentials**: `gmailOAuth2`.
- **Kiểm tra thiết lập OAuth2**:
  - Đảm bảo **Gmail đã cho phép quyền gửi email tự động**.
  - **Không dùng Gmail cá nhân** (sử dụng Gmail doanh nghiệp hoặc tạo một tài khoản riêng).

---

#### **3. Kích hoạt ⚡️**
1. **Test run với dữ liệu mẫu**:
   - Nhập một email mẫu vào JotForm (ví dụ: `jane@mycompany.com` hoặc `john@gmail.com`).
   - Chạy workflow và kiểm tra email đã được gửi chưa.
2. **Bật Active workflow**:
   - Đảm bảo tất cả node đều **đỏ (active)**.
   - Nhấn **Active** ở góc trên bên phải.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::info[CẢI TIẾN CHẤT LƯỢNG]
1. **Thêm trường dữ liệu vào JotForm**:
   - Nếu form có trường `company_size` hoặc `industry`, **các sếp có thể sử dụng dữ liệu này** trong prompt để email càng cá nhân hóa càng tốt.

2. **Tùy chỉnh tone của email**:
   - Nếu doanh nghiệp có **phong cách riêng** (ví dụ: chuyên nghiệp, thân mật, hài hước), **các sếp hãy chỉnh sửa prompt** trong node `lmChatOpenAi`.

3. **Lưu log email đã gửi**:
   - Thêm node **Google Sheets** hoặc **Notion** sau node `Send Welcome Email` để **lưu lịch sử email** và theo dõi hiệu quả.

4. **Gửi báo cáo định kỳ**:
   - Sử dụng **n8n + Google Sheets** để tự động tạo báo cáo số liệu (ví dụ: số email đã gửi, tỷ lệ mở, tỷ lệ chuyển đổi).

5. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram** để **báo động khi có lead mới** hoặc **email đã gửi thành công**.

6. **Sử dụng AI để phân tích lead**:
   - Nếu lead là B2B, **Perplexity AI** có thể nghiên cứu thêm về **người quyết định** (decision-maker) trong công ty để email càng hiệu quả càng tốt.

---

### 📌 **Kết luận**
Workflow này **giải phóng các sếp khỏi công việc thủ công gửi email chào mừng**, đồng thời **tăng tỷ lệ chuyển đổi lên 30%+** nhờ nội dung cá nhân hóa hoàn toàn tự động.

**Hành động ngay hôm nay:**
1. **Chuẩn bị tài khoản** (JotForm, Perplexity, OpenAI, Gmail).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Test run** và **bật workflow** để tự động hóa email chào mừng!

**🚀 Nếu các sếp cần hỗ trợ**, có thể liên hệ với tác giả [Fahmi Fahreza](https://n8n.io/workflows/9474) hoặc tham gia **community n8n** để chia sẻ kinh nghiệm.

---
**Chúc các sếp thành công với tự động hóa email chào mừng siêu cá nhân hóa!** 🎉