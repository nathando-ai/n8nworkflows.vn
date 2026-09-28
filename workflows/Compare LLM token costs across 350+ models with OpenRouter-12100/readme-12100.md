---
title: "💰 So Sánh Chi Phí Token AI Cho 350+ Mô Hình LLM Với OpenRouter - Tự Động Hóa 100% Không Code"
description: "Workflow này giúp các sếp so sánh chi phí token cho hơn 350 mô hình LLM (GPT-4, Claude, Llama, Mistral...) ngay lập tức, tiết kiệm thời gian lên đến 80% so với cách làm thủ công. Kết quả bao gồm chi tiết token input/output và báo cáo chi phí chi tiết cho từng mô hình."
slug: "so-sanh-chi-phi-token-llm-openrouter"
tags: [n8n, automation, ai-chatbot, openrouter, token-cost-tracker]
keywords: [n8n workflow so sánh token LLM, tự động hóa chi phí AI, OpenRouter API, tiết kiệm chi phí mô hình ngôn ngữ, so sánh mô hình GPT-4 vs Claude]
---

# 🚀 **So Sánh Chi Phí Token AI Cho 350+ Mô Hình LLM Với OpenRouter**

## **🔍 Nỗi Đau Của Các Sếp Khi So Sánh Chi Phí AI**
Hiện nay, khi xây dựng chatbot hoặc ứng dụng AI, các sếp thường phải **làm thủ công** việc so sánh chi phí token giữa các mô hình như GPT-4, Claude, Llama, Mistral... Điều này gây ra:
- **Thời gian mất nhiều**: So sánh từng mô hình một, tính toán token input/output, và tính chi phí thủ công.
- **Không chính xác**: Sai sót trong tính toán token hoặc giá token thay đổi liên tục.
- **Không cá nhân hóa**: Không thể so sánh cùng một prompt trên nhiều mô hình một lúc.
- **Không tự động hóa**: Phải làm lại mỗi khi có yêu cầu mới.

**Workflow này giải quyết tất cả vấn đề trên bằng cách tự động so sánh chi phí token cho **350+ mô hình LLM** chỉ trong vài giây!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian lên đến 80%** so với cách làm thủ công.
✅ **So sánh chi phí chính xác** cho cùng một prompt trên nhiều mô hình.
✅ **Báo cáo chi tiết token** (input/output) và chi phí theo mô hình.
✅ **Hoạt động liên tục 24/7** (không cần can thiệp thủ công).
✅ **Cá nhân hóa** theo yêu cầu của từng dự án.
✅ **Dùng cho nhiều mục đích**: So sánh mô hình, tối ưu chi phí, tính toán báo giá cho khách hàng.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **API Key của OpenRouter**:
   - Trang [OpenRouter API Keys](https://openrouter.ai/settings/keys)
   - Tạo **một key mới** và **copy API Key** (sẽ dùng trong cấu hình).
2. **Tài khoản n8n** (nếu chưa có, đăng ký tại [n8n.io](https://n8n.io/)).
3. **Không cần kiến thức code** (workflow đã sẵn sàng sử dụng).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/12100) hoặc copy/paste JSON từ trang này.
- Mở **n8n Editor** → **Import Workflow** → Chọn file JSON đã tải.
- **Hoặc** copy toàn bộ JSON và dán vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này được chia thành **3 phần chính**:
- **Chat Interface** (dùng để test nhanh).
- **Form Interface** (dùng để chọn mô hình và prompt).
- **Backend** (tính toán chi phí token).

##### **A. Cấu Hình API Key OpenRouter**
1. **Node "Get Openrouter models"** (2 node):
   - Mở node → **Authentication** → Chọn **"Bearer YOUR_TOKEN_HERE"**.
   - Click **"Create New Credential"** → Dán **API Key** từ OpenRouter vào.
   - **Lưu** và **đặt tên credential** (ví dụ: `httpBearerAuth`).

2. **Node "OpenRouter"** (node `lmChatOpenRouter`):
   - Mở node → Click **"Create New Credential"** → Dán **API Key** cùng với node trên.
   - **Lưu** và **đặt tên credential** (ví dụ: `openRouterApi`).

##### **B. Cấu Hình Node "Backend"**
- Node **"Backend"** và **"Backend1"** (2 node `executeWorkflow`):
  - Chỉnh **URL** của workflow con (nếu có) hoặc để mặc định.
  - **Không cần thay đổi** nếu chỉ muốn dùng giao diện chat/form.

##### **C. Test Run Trước Khi Bật Active**
- **Test với giao diện Chat**:
  - Mở **Chat Panel** → Nhập một **prompt** (ví dụ: *"Giải thích cách hoạt động của LLM"*).
  - Kết quả sẽ hiển thị **chi phí token** và **báo cáo chi tiết**.
- **Test với giao diện Form**:
  - Mở **Form Submission** → Chọn mô hình (ví dụ: `openai/gpt-4.1-mini`) → Nhập prompt → Submit.
  - Kết quả sẽ hiển thị **AI response**, **chi phí tổng**, và **chi tiết token**.

#### **3. Kích Hoạt ⚡️**
- Sau khi cấu hình xong, **bật Active** cho workflow.
- **Không cần restart** (workflow sẽ hoạt động ngay).

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Sử dụng **node Webhook** để gửi kết quả so sánh chi phí vào Slack/Telegram tự động.
   - Cách làm: Thêm node **HTTP Request** → Chọn **Webhook URL** của Slack/Telegram.

2. **Lưu Log Chi Phí**:
   - Thêm node **Google Sheets** hoặc **Airtable** để lưu lịch sử so sánh chi phí.
   - Cách làm: Sau node **Backend**, thêm node **HTTP Request** → Gửi dữ liệu vào Google Sheets.

3. **Tự Động So Sánh Định Kỳ**:
   - Sử dụng **node Schedule** (n8n Pro) để chạy workflow hàng ngày/tuần.
   - Cách làm: Thêm node **Schedule** → Chọn thời gian chạy → Kết nối với workflow.

4. **Tối Ưu Prompt**:
   - Sử dụng **node LangChain** để phân tích prompt và đề xuất cách viết ngắn gọn hơn để giảm chi phí.

---

### 📌 **Kết Luận**
Workflow **"So Sánh Chi Phí Token AI Cho 350+ Mô Hình LLM"** là **giải pháp hoàn hảo** để các sếp:
✔ **Tiết kiệm thời gian** so sánh chi phí AI.
✔ **So sánh chính xác** giữa GPT-4, Claude, Llama, Mistral...
✔ **Tính toán chi phí token** một cách tự động.
✔ **Dùng cho nhiều mục đích**: So sánh mô hình, tối ưu chi phí, báo giá cho khách hàng.

**🚀 Hãy áp dụng ngay và bắt đầu tiết kiệm chi phí AI từ hôm nay!**
Nếu có vấn đề, các sếp có thể **comment bên dưới** hoặc liên hệ với tác giả [Philflow](https://n8n.io/workflows/12100) để hỗ trợ.

---
**Made with ❤️ by Philflow for n8n community** (Dịch & tối ưu bởi **Tự Động Hóa AI**)