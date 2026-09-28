---
title: "🤖 **Tự Động Hóa Trợ Lý Hỗ Trợ Khách Hàng AI (Voice + Chat) Với RAG, Supabase & Gemini - Không Cần Code!**"
description: "Workflow này tự động hóa hệ thống hỗ trợ khách hàng AI đa modal (text + voice) bằng công nghệ RAG (Retrieval-Augmented Generation), kết hợp Supabase (database), Gemini AI (Google Vertex) và ElevenLabs (synthesis voice). Giúp doanh nghiệp giảm 90% thời gian phản hồi, cải thiện trải nghiệm khách hàng và tự động hóa 24/7."
slug: "tieu-dong-hoa-tro-ly-ho-tro-khach-hang-ai-rag-supabase-gemini"
tags: [n8n, automation, no-code, ai-chatbot, supabase, google-gemini, elevenlabs, rag, voice-ai]
keywords: [n8n workflow hỗ trợ khách hàng AI, tự động hóa chatbot voice, RAG với Supabase và Gemini, tự động hóa hỗ trợ khách hàng 24/7, AI đa modal, Google Vertex AI, ElevenLabs voice synthesis]
---

# 🚀 **Tự Động Hóa Trợ Lý Hỗ Trợ Khách Hàng AI (Voice + Chat) Với RAG, Supabase & Gemini**

## **🔥 Bạn đã bao giờ mệt mỏi vì phải trả lời cùng một câu hỏi hàng trăm lần mỗi ngày?**
Hệ thống hỗ trợ khách hàng truyền thống không chỉ tốn thời gian mà còn dễ gây chán nản cho khách hàng khi phải chờ đợi lâu. **Workflow này giải quyết vấn đề đó bằng cách xây dựng một trợ lý AI thông minh, hỗ trợ cả văn bản và giọng nói, tự động tra cứu và trả lời khách hàng dựa trên kiến thức doanh nghiệp.**

Với công nghệ **RAG (Retrieval-Augmented Generation)**, trợ lý này không chỉ trả lời dựa trên kiến thức chung mà còn **tự động tra cứu từ cơ sở dữ liệu nội bộ** của bạn (được lưu trên **Supabase**), đảm bảo thông tin chính xác và cá nhân hóa. Khi khách hàng gửi tin nhắn hoặc gọi điện, hệ thống sẽ **synthesize giọng nói tự nhiên** (thông qua **ElevenLabs**) để trả lời, tạo trải nghiệm gần như với một nhân viên hỗ trợ thực sự.

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[**LỢI ÍCH CỐT LÕI**]
✅ **Tiết kiệm thời gian**: Giảm 90% thời gian phản hồi so với hỗ trợ thủ công.
✅ **Trải nghiệm khách hàng cao cấp**: Trả lời nhanh chóng, chính xác và tự động hóa 24/7.
✅ **Cá nhân hóa hỗ trợ**: AI tự động tra cứu từ cơ sở dữ liệu nội bộ (Supabase) để trả lời chính xác.
✅ **Hỗ trợ đa modal**: Khách hàng có thể gửi tin nhắn **văn bản hoặc giọng nói**, hệ thống trả lời bằng cả hai định dạng.
✅ **Không cần code**: Sử dụng **n8n Self-hosted** để chạy 24/7 mà không lo chi phí cloud.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
- **Tài khoản Supabase** (để lưu trữ embeddings và dữ liệu cơ sở).
- **API Key của Google Vertex AI** (để sử dụng mô hình Gemini).
- **API Key của ElevenLabs** (để synthesize giọng nói).
- **Google Docs** (để lưu trữ tài liệu huấn luyện cho AI).
- **n8n Self-hosted** (để chạy workflow 24/7).

:::info[**Gợi ý hạ tầng cho n8n**]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## **🚀 Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/7188](https://n8n.io/workflows/7188) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON và dán vào **Create Workflow** trong n8n.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **12 node**, mỗi node đều cần cấu hình kỹ lưỡng. Dưới đây là hướng dẫn chi tiết:

#### **🔹 Node "Webhook" (Bắt đầu workflow)**
- **Lưu ý**: Cần cấu hình **URL Webhook** để khách hàng có thể gửi yêu cầu hỗ trợ.
- **Credentials**: Chọn **Default** hoặc tạo mới nếu cần.

#### **🔹 Node "Respond to Webhook" (Trả lời yêu cầu)**
- **Lưu ý**: Nếu khách hàng gửi yêu cầu qua **giọng nói**, dữ liệu sẽ được chuyển sang định dạng text trước khi xử lý.

#### **🔹 Node "Content for the Training" (Google Docs)**
- **Lưu ý**:
  - Cần **chỉ định file Google Docs** chứa tài liệu huấn luyện (ví dụ: FAQ, hướng dẫn sản phẩm).
  - **Cấu hình**:
    - **File ID**: Lấy từ liên kết Google Docs (ví dụ: `https://docs.google.com/document/d/[FILE_ID]/edit`).
    - **Sheet Name**: Nếu là file Excel/Sheet, chỉ định tên sheet.

#### **🔹 Node "Splitting into Chunks" (Code - Chia tài liệu thành mảnh)**
- **Lưu ý**:
  - Node này sử dụng **JavaScript** để chia tài liệu thành các đoạn nhỏ (chunk) để dễ dàng embed.
  - **Mã mặc định** đã được cung cấp, **không cần chỉnh sửa** trừ khi cần thay đổi logic chia mảnh.

#### **🔹 Node "Embedding Uploaded document" (HTTP Request - Tạo embedding)**
- **Lưu ý**:
  - Cần **API Key của Google Vertex AI** để gọi mô hình **Gemini**.
  - **Cấu hình**:
    - **URL**: `https://generativelanguage.googleapis.com/v1beta/models/gemini-pro:generateContent`
    - **Headers**:
      ```json
      {
        "Content-Type": "application/json",
        "Authorization": "Bearer YOUR_GOOGLE_VERTEX_API_KEY"
      }
      ```
    - **Body**: Dữ liệu JSON chứa prompt và nội dung cần embed.

#### **🔹 Node "Save the embedding in DB" (Supabase - Lưu embeddings)**
- **Lưu ý**:
  - Cần **API Key và URL của Supabase**.
  - **Cấu hình**:
    - **Database URL**: `https://[PROJECT_REF].supabase.co`
    - **API Key**: `your-supabase-anon-key`
    - **Table Name**: `embeddings` (hoặc tên bảng tùy chỉnh).

#### **🔹 Node "Search Embeddings" (HTTP Request - Tìm kiếm embeddings)**
- **Lưu ý**:
  - Sử dụng **Supabase Vector Search** để tìm kiếm embeddings gần nhất với câu hỏi của khách hàng.
  - **Cấu hình**:
    - **URL**: `https://[PROJECT_REF].supabase.co/rest/v1/embeddings`
    - **Headers**: Chứa `Authorization` và `apikey` của Supabase.

#### **🔹 Node "Embend User Message" (HTTP Request - Embed câu hỏi khách hàng)**
- **Lưu ý**:
  - Tương tự như node "Embedding Uploaded document", nhưng với **câu hỏi của khách hàng** thay vì tài liệu huấn luyện.

#### **🔹 Node "Basic LLM Chain" (Chain LLM - Xây dựng chuỗi LLM)**
- **Lưu ý**:
  - Sử dụng **Google Vertex AI (Gemini)** để tạo phản hồi dựa trên kết quả tra cứu embeddings.
  - **Cấu hình**:
    - **Model**: `gemini-pro`
    - **Prompt**: Cần tùy chỉnh để phù hợp với doanh nghiệp (ví dụ: "Trả lời khách hàng dựa trên kiến thức từ [tên doanh nghiệp]").

#### **🔹 Node "Google Vertex Chat Model" (LM Chat Google Vertex)**
- **Lưu ý**:
  - Node này **synthesize giọng nói** cho phản hồi AI (nếu khách hàng muốn nghe thay vì đọc).
  - **Cần API Key ElevenLabs** để synthesize voice.
  - **Cấu hình**:
    - **Voice ID**: Chọn giọng nói phù hợp (ví dụ: `Eliot`).
    - **Text**: Nội dung phản hồi từ AI.

#### **🔹 Node "Aggregate" (Kết hợp kết quả)**
- **Lưu ý**:
  - Node này **gộp kết quả** từ các bước trước để trả lời cuối cùng.
  - **Cấu hình mặc định** đã đủ, **không cần chỉnh sửa**.

#### **🔹 Node "Manual Trigger" (Bắt đầu workflow thủ công)**
- **Lưu ý**:
  - Dùng để **test workflow** trước khi kích hoạt Webhook.

---

### **3. Kích hoạt ⚡️**
1. **Test run dữ liệu mẫu**:
   - Gửi một **câu hỏi mẫu** qua Webhook (ví dụ: "Làm thế nào để hủy đơn hàng?").
   - Kiểm tra phản hồi của AI có logic không.
2. **Bật Active workflow**:
   - Sau khi test thành công, **bật chế độ Active** để workflow hoạt động 24/7.

---

## **✍️ Mẹo & gợi ý nâng cao**
:::tip[**CÁCH TIẾP CẬN HƠN**]
🔹 **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack Webhook** hoặc **Telegram Bot** để khách hàng có thể gửi yêu cầu hỗ trợ qua chat.

🔹 **Lưu log hoạt động**:
   - Thêm node **Google Sheets** hoặc **Supabase** để ghi lại tất cả các yêu cầu và phản hồi của AI.

🔹 **Gửi báo cáo định kỳ**:
   - Sử dụng **n8n Schedule Node** để gửi báo cáo tổng hợp về số lượng yêu cầu, thời gian phản hồi trung bình.

🔹 **Cập nhật kiến thức tự động**:
   - Thêm một **Webhook từ Google Drive** để tự động cập nhật tài liệu huấn luyện khi có thay đổi.
:::

---

## **📌 Kết luận**
Workflow này **không chỉ tự động hóa hỗ trợ khách hàng mà còn nâng cao chất lượng dịch vụ** bằng cách kết hợp **AI RAG, Supabase và voice synthesis**. Với **n8n Self-hosted**, các sếp có thể chạy hệ thống 24/7 **không lo chi phí cloud** và không cần viết một dòng code nào.

**Hãy áp dụng ngay và giảm thiểu 90% thời gian phản hồi cho đội ngũ hỗ trợ của mình!** 🚀

---
**💡 Bạn có câu hỏi về cách cấu hình chi tiết? Hãy để lại comment dưới đây!**