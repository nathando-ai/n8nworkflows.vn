---
title: "🤖 Tự Động Hóa Bot Trợ Giúp IT Hỗ Trợ Bằng Cổng Hỗ Trợ Hiện Có - Không Cần Code!"
description: "Workflow này giúp các sếp xây dựng một bot hỗ trợ IT thông minh, tự động trả lời câu hỏi từ cổng hỗ trợ hiện có của doanh nghiệp, tiết kiệm thời gian và cải thiện trải nghiệm khách hàng. Sử dụng AI + API search để trả lời chính xác, không cần xây dựng vector store phức tạp."
slug: "tay-dong-hoa-bot-tro-giup-it-bang-cong-hop-ho-tro-hien-co"
tags: [n8n, automation, ai-chatbot, support-portal, no-code, langchain]
keywords: [n8n workflow hỗ trợ IT, tự động hóa bot chatbot, AI trả lời câu hỏi từ cổng hỗ trợ, không cần code, RAG với API search, OpenAI GPT-4o-mini]
---

# 🚀 **Bot Trợ Giúp IT Tự Động Hóa Từ Cổng Hỗ Trợ Hiện Có**

## **Giới Thiệu: Giải Pháp Tiết Kiệm Thời Gian Cho Đội Ngũ Hỗ Trợ IT**
Các sếp đã từng phải chịu đựng những câu hỏi lặp đi lặp lại từ nhân viên như:
- *"Làm thế nào để kết nối iCloud với Acuity Scheduling?"*
- *"Tôi không tìm thấy hóa đơn trước đây ở đâu?"*
- *"Lỗi này xảy ra vì sao và cách khắc phục như thế nào?"*

Thay vì phải trả lời hàng chục lần một ngày, **bot trợ giúp IT tự động hóa** này sẽ:
✅ **Trả lời chính xác** từ cơ sở tri thức hiện có của doanh nghiệp (không cần xây dựng vector store mới).
✅ **Tiết kiệm thời gian** cho đội ngũ hỗ trợ (giảm 80% công việc lặp lại).
✅ **Cải thiện trải nghiệm** với câu trả lời nhanh chóng và cá nhân hóa.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này chạy ổn định 24/7, các sếp nên cài **n8n trên VPS riêng (Self-hosted)** để đảm bảo bảo mật và tính liên tục.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Bot tự động trả lời 90% câu hỏi thường gặp, giảm tải cho đội ngũ hỗ trợ.
- **Chính xác cao**: Dựa trên cơ sở tri thức hiện có (không cần cập nhật thủ công).
- **Tiết kiệm chi phí**: Không cần xây dựng vector store tốn kém, chỉ sử dụng API search của cổng hỗ trợ.
- **Hoạt động liên tục**: Bot hoạt động 24/7, không cần nghỉ ngơi.
- **Dễ dàng mở rộng**: Thêm các công cụ hỗ trợ khác (Slack, Email, CRM...) chỉ với vài click.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản OpenAI** (để sử dụng mô hình AI GPT-4o-mini):
   - [Đăng ký API Key OpenAI](https://platform.openai.com/api-keys)
   - Thêm credentials `openAiApi` trong n8n (Settings → Credentials → Add Credential → OpenAI).

2. **API Key của cổng hỗ trợ hiện có**:
   - Nếu doanh nghiệp đang sử dụng **Acuity Scheduling** (hoặc hệ thống hỗ trợ khác), cần lấy **API Key** từ trang quản trị của cổng hỗ trợ.
   - Nếu không phải Acuity, cần **tùy chỉnh node `Acuity Support Search API`** để phù hợp với API của hệ thống hỗ trợ hiện có.

3. **Workflow phụ (KnowledgeBase Tool Subworkflow)**:
   - Workflow này sẽ xử lý logic tìm kiếm và trả về kết quả từ API. Các sếp có thể **sao chép và chỉnh sửa** để phù hợp với API của mình.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/3498) hoặc sao chép mã JSON từ trang này.
- Trong n8n Editor, nhấn **Import Workflow** → Chọn file JSON hoặc dán mã JSON vào ô **Import Workflow**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **A. Cấu hình OpenAI**
- Node **"OpenAI Chat Model"** cần **credentials `openAiApi`** đã thiết lập trước đó.
- Đảm bảo chọn mô hình `gpt-4o-mini` (hoặc mô hình khác nếu muốn thay đổi).

##### **B. Cấu hình API của cổng hỗ trợ**
- Node **"Acuity Support Search API"** là **node `httpRequest`** cần cấu hình:
  - **Method**: `GET` (hoặc `POST` nếu API yêu cầu).
  - **URL**: Thay thế bằng URL API của cổng hỗ trợ (ví dụ: `https://api.acutityscheduling.com/search`).
  - **Headers**:
    - `Authorization`: `Bearer {API_KEY}` (thay `{API_KEY}` bằng API Key thực tế).
    - `Content-Type`: `application/json`.
  - **Query Parameters** (nếu cần):
    - Thêm các tham số tìm kiếm như `q=$json["query"]` (để truyền câu hỏi từ người dùng).

##### **C. Tùy chỉnh Subworkflow (KnowledgeBase Tool)**
- Node **"KnowledgeBase Tool Subworkflow"** là một **workflow phụ** xử lý logic tìm kiếm và trả về kết quả.
- Các sếp cần **mở workflow phụ này** và chỉnh sửa:
  - **Node `httpRequest`**: Đảm bảo URL và headers phù hợp với API của cổng hỗ trợ.
  - **Node `Extract Relevant Fields`**: Chỉnh sửa logic để trích xuất dữ liệu cần thiết từ API (ví dụ: tiêu đề, nội dung, liên kết).
  - **Node `Aggregate Response`**: Đảm bảo kết quả được format đúng để gửi về AI.

##### **D. Test Run & Kích hoạt**
- **Test Run** với các câu hỏi mẫu:
  - *"Làm thế nào để kết nối iCloud với hệ thống?"*
  - *"Tôi không tìm thấy hóa đơn tháng trước ở đâu?"*
- Nếu kết quả không chính xác, kiểm tra lại:
  - API của cổng hỗ trợ có trả về dữ liệu đúng không?
  - Logic trích xuất và aggregate có đúng không?
- Sau khi test thành công, **bật Active workflow**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack Webhook** hoặc **Telegram Bot** để bot trả lời trên kênh chat công cộng.
   - Cách làm: Thêm node `httpRequest` để gửi tin nhắn từ n8n về Slack/Telegram.

2. **Lưu log hoạt động**:
   - Thêm node **Google Sheets** hoặc **Airtable** để ghi lại tất cả câu hỏi và câu trả lời của bot.
   - Cách làm: Sau node `agent`, thêm node `httpRequest` để gửi dữ liệu vào bảng tính.

3. **Gửi báo cáo định kỳ**:
   - Tạo một workflow phụ để gửi báo cáo hàng tuần về:
     - Số lượng câu hỏi được trả lời.
     - Các câu hỏi thường gặp nhất.
     - Thời gian phản hồi trung bình.
   - Cách làm: Sử dụng node `executeWorkflowTrigger` để kích hoạt workflow báo cáo.

4. **Thêm công cụ hỗ trợ khác**:
   - Nếu doanh nghiệp có **CRM (HubSpot, Salesforce)** hoặc **Email (Gmail, Outlook)**, có thể thêm node `toolWorkflow` để bot có thể truy cập dữ liệu từ các hệ thống này.

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa bot hỗ trợ IT **không cần code**, đồng thời tiết kiệm chi phí và thời gian. Bằng cách kết nối với **cổng hỗ trợ hiện có**, bot sẽ tự động trả lời câu hỏi một cách chính xác và hiệu quả.

**Hãy áp dụng ngay và giảm tải cho đội ngũ hỗ trợ của mình!**
👉 [Tải workflow từ n8n.io](https://n8n.io/workflows/3498)
👉 [Hỏi đáp trên Discord](https://discord.com/invite/XPKeKXeB7d) nếu gặp vấn đề.

---
**Happy Automating!** 🚀