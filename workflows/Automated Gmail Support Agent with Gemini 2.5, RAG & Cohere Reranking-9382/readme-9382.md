---
title: "🤖 **Công cụ hỗ trợ email tự động hóa với Gemini 2.5, RAG & Cohere Reranking - Giải pháp AI cho doanh nghiệp không cần code**"
description: "Workflow tự động hóa hoàn toàn phản hồi email khách hàng bằng AI Gemini 2.5, kết hợp RAG (Retrieval-Augmented Generation) và Cohere Reranking để đảm bảo tính chính xác và cá nhân hóa cao. Giúp doanh nghiệp tiết kiệm thời gian, cải thiện trải nghiệm khách hàng và mở rộng khả năng hỗ trợ 24/7."
slug: "automated-gmail-support-agent-gemini-rag-cohere"
tags: [n8n, automation, no-code, ai-automation, gmail-bot, langchain, gemini-2-5, cohere-reranking]
keywords: [n8n workflow tự động hóa email, AI hỗ trợ khách hàng, Gemini 2.5 cho doanh nghiệp, RAG với Pinecone, Cohere Reranking, tự động trả lời email, giải pháp AI không code]
---

# 🚀 **Công cụ hỗ trợ email tự động hóa với Gemini 2.5, RAG & Cohere Reranking**

## **📌 Nỗi đau thực tế của doanh nghiệp khi hỗ trợ email thủ công**
Hàng ngày, các sếp và đội ngũ hỗ trợ phải mất **giờ đồng hồ** để:
- **Trả lời email lặp đi lặp lại** như câu hỏi về dịch vụ, chính sách, hoặc FAQ.
- **Tìm kiếm thông tin** trong tài liệu nội bộ để trả lời chính xác, dẫn đến **sai sót** và mất thời gian.
- **Phản hồi không đồng nhất**, khiến khách hàng cảm thấy không được quan tâm.
- **Không hoạt động 24/7**, khiến khách hàng phải chờ đợi trong giờ làm việc.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động hóa phản hồi email** trong giây lát, không cần can thiệp thủ công.
✅ **Sử dụng AI Gemini 2.5** để trả lời **cá nhân hóa**, giống như một chuyên viên hỗ trợ thực sự.
✅ **Kết hợp RAG (Retrieval-Augmented Generation)** với **Pinecone** để tra cứu thông tin chính xác từ cơ sở tri thức của doanh nghiệp.
✅ **Cohere Reranking** để **sắp xếp lại kết quả tìm kiếm** theo độ phù hợp cao nhất, tránh trả lời sai lệch.
✅ **Ghi nhớ lịch sử trò chuyện** bằng **PostgreSQL**, giúp AI học hỏi và cải thiện dần.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo **tính bảo mật và hiệu suất cao**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa **90% phản hồi email lặp lại**, giúp đội ngũ tập trung vào vấn đề phức tạp.
- **Chính xác cao**: Sử dụng **RAG + Cohere Reranking** để trả lời dựa trên **thông tin chính xác** từ cơ sở tri thức của doanh nghiệp.
- **Cá nhân hóa**: Gemini 2.5 tạo ra **phản hồi tự nhiên**, giống như một chuyên viên hỗ trợ thực sự.
- **Hoạt động 24/7**: Khách hàng được hỗ trợ **mọi lúc**, không phụ thuộc vào giờ làm việc.
- **Cải thiện trải nghiệm khách hàng**: Trả lời nhanh chóng và chính xác **tăng độ hài lòng** và **tỷ lệ chuyển đổi**.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản và API Keys**:
   - **Gmail**: OAuth2 (để đọc và gửi email).
   - **OpenAI**: API Key (để tạo embedding).
   - **Cohere**: API Key (để reranking kết quả).
   - **Google Gemini API**: API Key (để sử dụng Gemini 2.5).
   - **Pinecone**: API Key và **index "agency-info"** (dimension 1024).
   - **PostgreSQL**: Database để lưu trữ lịch sử trò chuyện (có thể dùng **Neon/Supabase** miễn phí).

2. **Cơ sở tri thức (Knowledge Base)**:
   - **Điền dữ liệu vào Pinecone** trước khi chạy workflow (cần một workflow riêng để upsert dữ liệu).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/9382](https://n8n.io/workflows/9382) hoặc copy/paste JSON vào **n8n Editor**.
- **Nhấn "Import"** và chọn **Create new workflow**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này bao gồm **8 node chính**, các sếp cần cấu hình kỹ lưỡng như sau:

##### **🔹 Node 1: Gmail Trigger (n8n-nodes-base.gmailTrigger)**
- **Chọn credential**: `gmailOAuth2` (đã cấu hình trước).
- **Lưu ý**:
  - **Scopes phải đầy đủ**:
    - `https://www.googleapis.com/auth/gmail.readonly` (đọc email).
    - `https://www.googleapis.com/auth/gmail.send` (gửi phản hồi).
  - **Polling interval**: Đặt **5-10 phút** để không quá tải Gmail API.

##### **🔹 Node 2: Pinecone Retriever (n8n-nodes-langchain.vectorStorePinecone)**
- **Chọn credential**: `pineconeApi`.
- **Cấu hình chính**:
  - **Mode**: `retrieve-as-tool` (để AI sử dụng kết quả tìm kiếm như công cụ).
  - **Embeddings**: `OpenAI text-embedding-3-large` (1024 dimensions).
  - **Reranker**: **Bật Cohere** (để cải thiện độ phù hợp).
- **Lưu ý**:
  - **Index "agency-info" phải được tạo trước** và **điền dữ liệu** (tài liệu FAQ, chính sách, hướng dẫn).
  - Nếu không có dữ liệu, AI sẽ trả lời **không chính xác**.

##### **🔹 Node 3: Cohere Reranker (n8n-nodes-langchain.rerankerCohere)**
- **Chọn credential**: `cohereApi`.
- **Lưu ý**:
  - **Monitor token usage**: Cohere có giới hạn token, nếu quá tải, API sẽ trả về lỗi.
  - **Đảm bảo API Key đúng** và có đủ quyền truy cập.

##### **🔹 Node 4: OpenAI Embeddings (n8n-nodes-langchain.embeddingsOpenAi)**
- **Chọn credential**: `openAiApi`.
- **Model**: `text-embedding-3-large` (không thay đổi).
- **Lưu ý**:
  - **API Key phải hoạt động** và có đủ credit.
  - Nếu không có credit, **OpenAI sẽ từ chối yêu cầu**.

##### **🔹 Node 5: Email Support Agent (n8n-nodes-langchain.agent)**
- **User Prompt**: Sử dụng **nội dung email** từ node Gmail Trigger.
- **LLM**: `Gemini 2.5` (đã chọn trong credential `googlePalmApi`).
- **Memory**: `Postgres Memory` (để AI ghi nhớ lịch sử trò chuyện).
- **Lưu ý**:
  - **Prompt phải rõ ràng**: Nếu không, AI sẽ trả lời **không logic**.
  - **Bật "Tools"** để AI có thể sử dụng kết quả từ Pinecone.

##### **🔹 Node 6: Postgres Memory (n8n-nodes-langchain.memoryPostgresChat)**
- **Chọn credential**: `postgres`.
- **Lưu ý**:
  - **Table Name**: Đặt tên phù hợp (ví dụ: `email_support_memory`).
  - **Session Key**: Có thể sử dụng `emailId` để phân biệt từng cuộc trò chuyện.

##### **🔹 Node 7: Gmail Reply (n8n-nodes-base.gmail)**
- **Chọn credential**: `gmailOAuth2`.
- **Operation**: `reply`.
- **Lưu ý**:
  - **Nội dung reply** sẽ tự động lấy từ **Email Support Agent**.
  - **Kiểm tra email mẫu** trước khi bật workflow.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** với **email mẫu** để kiểm tra:
   - AI có trả lời chính xác không?
   - Có ghi nhớ lịch sử không?
   - Email reply có gửi được không?
2. **Bật Active workflow** khi mọi thứ hoạt động ổn.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tối ưu hóa cơ sở tri thức (Knowledge Base)**:
   - **Điền càng nhiều tài liệu càng tốt** (FAQ, hướng dẫn, chính sách).
   - **Cập nhật thường xuyên** để AI luôn có thông tin mới nhất.

2. **Kết hợp với Slack/Telegram**:
   - Sử dụng **node Webhook** để gửi thông báo khi có email mới vào Slack/Telegram.
   - Ví dụ:
     ```json
     {
       "operation": "create",
       "url": "https://hooks.slack.com/services/XXX",
       "text": "🚨 New email from {{$node["Gmail Trigger"].json["$jsonpath"].emailAddress}}: {{$node["Gmail Trigger"].json["$jsonpath"].subject}}"
     }
     ```

3. **Lưu log và báo cáo**:
   - Sử dụng **node StickyNote** để ghi lại **lịch sử phản hồi** và **thống kê**.
   - Ví dụ:
     ```json
     {
       "key": "email_support_log",
       "value": {
         "emailId": "{{$node["Gmail Trigger"].json["$jsonpath"].id}}",
         "timestamp": "{{$node["Gmail Trigger"].json["$jsonpath"].date}}",
         "status": "replied"
       }
     }
     ```

4. **Cập nhật thường xuyên AI**:
   - **Gemini 2.5** và **Cohere** thường cập nhật mô hình, nên **check thường xuyên** để nâng cấp.

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho doanh nghiệp muốn:
✔ **Tự động hóa phản hồi email** mà không cần code.
✔ **Tăng tốc độ hỗ trợ** và giảm tải cho đội ngũ.
✔ **Cải thiện chất lượng phản hồi** bằng AI Gemini 2.5 + RAG + Cohere Reranking.
✔ **Hoạt động 24/7** mà không cần can thiệp thủ công.

**Hãy áp dụng ngay để:**
✅ **Tiết kiệm thời gian** cho đội ngũ.
✅ **Tăng trải nghiệm khách hàng**.
✅ **Mở rộng khả năng hỗ trợ** mà không tăng chi phí.

**Bắt đầu với n8n Self-hosted trên VPS để đảm bảo an toàn và hiệu suất tối ưu!** 🚀

---
**🔗 [Tải workflow nguyên bản tại n8n.io](https://n8n.io/workflows/9382)**
**💡 Cần hỗ trợ thêm? Đăng ký VPS n8n tại [TinoHost](https://tino.vn/vps-n8n?affid=388) và chat với chuyên gia!**