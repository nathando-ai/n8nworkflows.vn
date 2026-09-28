---
title: "🤖 **Hệ Thống RAG Tiến Tiến với Supabase & GPT-5: Tự Động Trả Lời Câu Hỏi Phức Tạp Không Cần Code**"
description: "Workflow tự động hóa AI RAG tiên tiến giúp các sếp xây dựng một hệ thống trả lời câu hỏi thông minh, phân tích đa chiều và kết hợp vector store Supabase với GPT-5 để tối ưu hóa chất lượng trả lời. Giảm thiểu 90% thời gian tra cứu thủ công và nâng cao độ chính xác 300% so với phương pháp truyền thống."
slug: "huong-dan-rag-supabase-gpt5-n8n"
tags: [n8n, automation, AI RAG, Supabase, OpenAI, GPT-5, LangChain, no-code, vector-database]
keywords: [n8n workflow RAG, tự động hóa AI, Supabase vector store, GPT-5 tự động trả lời, LangChain n8n, giải pháp tra cứu thông minh]
---

# 🚀 **Hệ Thống RAG Tiến Tiến với Supabase & GPT-5: Trả Lời Câu Hỏi Phức Tạp Như Người Chuyên Gia**

## **💡 Nỗi Đau Của Các Sếp: Tra Cứu Thông Tin Chậm Chạp & Không Chính Xác**
Hiện nay, khi các sếp hoặc nhân viên phải tra cứu thông tin từ lượng dữ liệu lớn (ví dụ: tài liệu nội bộ, báo cáo, hay dữ liệu khách hàng), họ thường phải:
- **Tìm kiếm thủ công** trên nhiều nguồn khác nhau (Google Sheets, Notion, hoặc cơ sở dữ liệu).
- **Phân tích nhiều trang** để tìm ra thông tin chính xác, dẫn đến **tốn thời gian và dễ mắc sai sót**.
- **Không thể xử lý câu hỏi phức tạp** (ví dụ: "So sánh hiệu suất của sản phẩm A và B trong 3 quý gần đây, đồng thời dự đoán xu hướng thị trường năm 2025").

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động hóa tra cứu thông tin** từ vector store Supabase với độ chính xác cao.
✅ **Phân tích đa chiều** câu hỏi phức tạp thành nhiều sub-query nhỏ, sau đó tổng hợp kết quả.
✅ **Lọc thông tin không liên quan** bằng hệ thống điểm số (score > 0.4) để đảm bảo chất lượng.
✅ **Trả lời tự động** với GPT-5, giống như một chuyên gia nội bộ.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**3 Lợi Ích Cốt Lõi**]
- **Tiết kiệm 90% thời gian tra cứu** so với phương pháp thủ công.
- **Độ chính xác cao** (300% so với tra cứu truyền thống) nhờ hệ thống lọc thông tin thông minh.
- **Hoạt động 24/7** mà không cần can thiệp của con người.
- **Cập nhật động** khi dữ liệu trong Supabase thay đổi.
- **Cá nhân hóa** trả lời dựa trên kiến thức cơ sở của doanh nghiệp.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI SỬ DỤNG**]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản OpenAI** (để sử dụng GPT-5 và Embeddings):
   - API Key từ [OpenAI](https://platform.openai.com/account/api-keys).
   - Chọn model: `gpt-5-mini` (hoặc `gpt-4o` nếu muốn chất lượng cao hơn).
2. **Tài khoản Supabase** (để lưu trữ vector store):
   - URL của cơ sở dữ liệu Supabase.
   - API Key và Secret Key từ **Project Settings > API**.
   - Bảng (`table`) đã chứa dữ liệu cần tra cứu (cần đã được **embedding** trước bằng OpenAI).
3. **Workflow con "RAG sub-workflow"** (được tạo sẵn trong workflow chính):
   - Các sếp cần **import workflow này** và kết nối với Supabase & OpenAI tương tự như workflow chính.
   - **Không cần code**, chỉ cần cấu hình các credentials.

**📌 Lưu ý quan trọng:**
- Dữ liệu trong Supabase **phải đã được embedding** (chuyển thành vector) trước khi sử dụng.
- Nếu chưa có dữ liệu, các sếp có thể tham khảo [hướng dẫn embedding dữ liệu với LangChain](https://python.langchain.com/docs/modules/data_connection/retrievers/vectorstores/supabase).
:::

---

## **🚀 Cách Import & Cấu Hình Workflow**

### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow này:

#### **Cách 1: Import từ file JSON**
1. Tải file JSON của workflow từ [đây](https://n8n.io/workflows/7779) (hoặc copy JSON từ trang gốc).
2. Trên n8n Editor, nhấn **Import** (icon "↑" ở góc trên bên trái).
3. Dán JSON và nhấn **Import**.

#### **Cách 2: Copy/Paste JSON vào Editor**
1. Mở n8n Editor và tạo một workflow mới.
2. Nhấn **Import** → **Paste JSON** và dán toàn bộ nội dung JSON từ workflow gốc.
3. Nhấn **Import**.

---

### **2. Các Bước Cấu Hình BẮT BUỘC 📌**
Sau khi import, các sếp cần **cấu hình các node quan trọng** như sau:

#### **🔹 Node "When chat message received" (chatTrigger)**
- **Chức năng:** Nhận câu hỏi từ người dùng (có thể kết nối với Slack, Telegram, hoặc Webhook).
- **Cấu hình:**
  - Chọn **credentials** (nếu sử dụng Slack/Telegram).
  - Hoặc cấu hình **Webhook URL** để nhận câu hỏi từ bên ngoài.

#### **🔹 Node "OpenAI Chat Model" (lmChatOpenAi)**
- **Chức năng:** Sử dụng GPT-5 để trả lời cuối cùng.
- **Cấu hình:**
  - **Credentials:** Chọn `openAiApi` (đã cấu hình trước).
  - **Model:** Đặt `gpt-5-mini` (hoặc `gpt-4o`).
  - **Prompt:** Sẽ tự động được truyền từ workflow.

#### **🔹 Node "Supabase Vector Store" (vectorStoreSupabase)**
- **Chức năng:** Tra cứu dữ liệu trong Supabase dựa trên vector.
- **Cấu hình:**
  - **Credentials:** Chọn `supabaseApi` (đã cấu hình trước).
  - **Table Name:** Tên bảng chứa dữ liệu (ví dụ: `documents`).
  - **Prompt:** Sẽ tự động được truyền từ node `Embeddings OpenAI`.

#### **🔹 Node "Embeddings OpenAI" (embeddingsOpenAi)**
- **Chức năng:** Chuyển câu hỏi thành vector để so sánh với dữ liệu trong Supabase.
- **Cấu hình:**
  - **Credentials:** Chọn `openAiApi`.
  - **Model:** Sử dụng `text-embedding-ada-002` (mặc định).

#### **🔹 Node "Filter" (Keep score over 0.4)**
- **Chức năng:** Lọc bỏ thông tin không liên quan (score < 0.4).
- **Cấu hình:**
  - Đặt **score > 0.4** (có thể điều chỉnh từ 0.3 đến 0.7 tùy chất lượng dữ liệu).

#### **🔹 Node "AI Agent" (agent)**
- **Chức năng:** Quản lý toàn bộ quá trình RAG (decompose, retrieve, filter, synthesize).
- **Cấu hình:**
  - **System Prompt:** Cần **tùy chỉnh** để phù hợp với kiến thức cơ sở của doanh nghiệp.
    **Ví dụ:**
    ```json
    "You are a helpful assistant that answers questions based on our company's internal documents. Only use information from the retrieved context."
    ```
  - **Tools:** Đảm bảo các tool như `toolThink`, `toolWorkflow` và `lmChatOpenAi` được kết nối đúng.

#### **🔹 Node "RAG sub-workflow" (executeWorkflowTrigger)**
- **Chức năng:** Gọi workflow con để tra cứu và lọc thông tin.
- **Cấu hình:**
  - Chọn **credentials** của workflow con (nếu khác với workflow chính).
  - Đảm bảo workflow con đã được **import và cấu hình** trước.

---

### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run với dữ liệu mẫu:**
   - Gửi một câu hỏi đơn giản (ví dụ: *"Giải thích về sản phẩm X"*).
   - Kiểm tra nếu workflow trả lời chính xác và không có lỗi.
2. **Bật Active:**
   - Nhấn **Active** ở góc trên bên phải.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **1. Tùy Chỉnh Hệ Thống Lọc (Filter)**
- Nếu dữ liệu trong Supabase **ít liên quan**, giảm **score** từ 0.4 xuống 0.3.
- Nếu dữ liệu **rất chính xác**, tăng **score** lên 0.6-0.7.

### **2. Kết Nối với Slack/Telegram**
- Sử dụng **node `n8n-nodes-base.webhook`** để nhận câu hỏi từ Slack/Telegram.
- Cấu hình **Webhook URL** trong Slack/Telegram và kết nối với node `When chat message received`.

### **3. Lưu Log Tra Cứu**
- Thêm **node `n8n-nodes-base.set`** sau node `Supabase Vector Store` để lưu log.
- Sử dụng **node `n8n-nodes-base.executeWorkflowTrigger`** để gửi log đến Google Sheets hoặc Notion.

### **4. Cập Nhật Dữ liệu Tự Động**
- Sử dụng **node `n8n-nodes-base.schedule`** để chạy workflow định kỳ (ví dụ: mỗi ngày) để cập nhật vector store.

### **5. Tối Ưu Hóa Prompt cho AI Agent**
- **Ví dụ prompt hiệu quả:**
  ```json
  "You are a senior analyst for {Company Name}. Your task is to answer complex questions based on internal documents. Only use information from the retrieved context. If the answer is not found, say 'I don't have enough information to answer this question.'"
  ```

---

## **📌 Kết Luận: Áp Dụng Ngay để Trở Thành "Chuyên Gia Nội Bộ"**
Workflow này không chỉ **giải phóng thời gian** cho các sếp mà còn **nâng cao chất lượng trả lời** đến mức gần như một chuyên gia. Với **Supabase + GPT-5**, hệ thống có thể:
✔ **Tra cứu nhanh chóng** trên hàng ngàn tài liệu.
✔ **Phân tích câu hỏi phức tạp** thành nhiều sub-query.
✔ **Lọc bỏ thông tin không liên quan** để đảm bảo độ chính xác.
✔ **Hoạt động 24/7** mà không cần can thiệp của con người.

**👉 Hành động ngay:**
1. **Cài đặt n8n trên VPS** (để workflow chạy 24/7).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
2. **Import workflow** và cấu hình Supabase + OpenAI.
3. **Test với câu hỏi thực tế** và tối ưu hóa!

**🚀 Hãy bắt đầu tự động hóa tra cứu thông minh ngay hôm nay!**