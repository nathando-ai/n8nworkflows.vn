---
title: "🚀 Tự Động Học & Trích Xuất Nội Dung Website → Lưu Trữ Vectorized Trên Supabase (Firecrawl + AI RAG)"
description: "Workflow tự động hóa trích xuất nội dung website bằng Firecrawl, chuyển đổi thành vector embeddings bằng OpenAI, lưu trữ trên Supabase pgVector, và xây dựng hệ thống RAG (Retrieval-Augmented Generation) để trả lời câu hỏi bằng AI. Giúp các sếp tiết kiệm 100+ giờ công sức so với phương pháp thủ công."
slug: "tieu-dong-hoc-trich-xuat-noi-dung-website-supabase"
tags: [n8n, automation, no-code, ai-rag, firecrawl, supabase, vector-database, openai, cohere]
keywords: [n8n workflow scrape website, tự động hóa trích xuất nội dung, supabase pgvector, firecrawl api, ai rag chatbot, embeddings openai, cohere rerank]
---

# 🚀 **Tự Động Học & Trích Xuất Nội Dung Website → Lưu Trữ Vectorized Trên Supabase (Firecrawl + AI RAG)**

### **🔍 Nỗi Đau Của Các Sếp Hiện Nay**
Hiện nay, các doanh nghiệp thường phải:
- **Thủ công** trích xuất nội dung từ hàng ngàn trang website (quá trình tốn thời gian, dễ sai sót).
- **Lưu trữ** dữ liệu một cách rời rạc (không thể tìm kiếm hiệu quả bằng AI).
- **Tạo chatbot** trả lời câu hỏi dựa trên nội dung website (phức tạp, đòi hỏi kỹ năng code cao).

Workflow này **giải quyết tất cả** bằng cách:
✅ **Tự động** trích xuất nội dung website bằng Firecrawl.
✅ **Chuyển đổi** thành vector embeddings (OpenAI) để lưu trữ trên Supabase pgVector.
✅ **Xây dựng hệ thống RAG** để trả lời câu hỏi bằng AI (Cohere + OpenRouter) với độ chính xác cao.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**).
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (ổn định, tốc độ cao).
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100+ giờ công sức** so với phương pháp thủ công.
- **Lưu trữ dữ liệu vectorized** trên Supabase (tìm kiếm siêu nhanh bằng AI).
- **Tạo chatbot RAG** trả lời câu hỏi bằng ngôn ngữ tự nhiên (không cần code).
- **Cập nhật tự động** khi website thay đổi (không cần can thiệp).
- **Cá nhân hóa** kết quả cho từng khách hàng (ví dụ: trích xuất thông tin từ website đối thủ).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Supabase** (để lưu trữ vector embeddings).
2. **API Key Firecrawl** (trích xuất nội dung website).
3. **API Key OpenAI** (tạo embeddings).
4. **API Key OpenRouter** (chatbot RAG).
5. **API Key Cohere** (rerank kết quả tìm kiếm).
6. **Cấu trúc bảng `documents` trên Supabase** (cần chạy SQL migration từ [đây](https://github.com/n8n-io/n8n/tree/main/packages/n8n-nodes-base/dist/nodes/supabase)).

---
:::info[CHUẨN BỊ]
**Cách tạo bảng `documents` trên Supabase:**
```sql
CREATE TABLE IF NOT EXISTS documents (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  url TEXT NOT NULL,
  content TEXT NOT NULL,
  embeddings vector(1536),
  metadata JSONB,
  created_at TIMESTAMPTZ NOT NULL DEFAULT NOW()
);
```
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/13911](https://n8n.io/workflows/13911).
- **Nhấn "Import"** trong n8n Editor (n8n.io).
- **Hoặc copy/paste JSON** vào tab "Import" của n8n.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **18 node**, nhưng các node **quan trọng nhất** cần cấu hình kỹ:

| **Node**                          | **Lưu Ý Cần Chỉnh**                                                                 | **Credentials Cần Thiết**          |
|-----------------------------------|------------------------------------------------------------------------------------|------------------------------------|
| **Receive company URL**           | Chọn **HTTP Method: POST**, giữ nguyên `path` là `dedaa64a-3dc9-43ea-82ac-7fac034af0b2`. | -                                  |
| **Check for duplicate in Supabase** | Chọn **Operation: get**, điền `tableName: documents`, `columnName: url`.         | `supabaseApi`                      |
| **Scrape company website**        | Điền **URL** vào `url` field, chọn `scrapeType: full`.                            | `firecrawlApi`                     |
| **Generate OpenAI embeddings**    | Chọn **Model: text-embedding-ada-002**, điền `input` từ node trước.               | `openAiApi`                        |
| **Answer query from enriched leads** | Cấu hình **Agent** với prompt tự định nghĩa (ví dụ: "Trả lời câu hỏi dựa trên nội dung website"). | -                                  |
| **OpenRouter LLM**                | Chọn **Model: anthropic/claude-sonnet-4.6**, điền `messages` từ node trước.         | `openRouterApi`                    |
| **Rerank results with Cohere**    | Chọn **Model: rerank-english-v3.0**, điền `query` và `documents` từ node trước.      | `cohereApi`                        |
| **Store embeddings in Supabase**  | Chọn **Operation: upsert**, điền `tableName: documents`, `embeddings` từ node trước. | `supabaseApi`                      |

#### **3. Kích Hoạt ⚡️**
1. **Test run** với URL mẫu (ví dụ: `https://example.com`).
   - Gửi **POST request** đến webhook với payload:
     ```json
     { "url": "https://example.com" }
     ```
2. **Bật Active** workflow.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** để thông báo kết quả trích xuất.
   - Ví dụ: Khi trích xuất thành công, gửi tin nhắn "Đã lưu trữ nội dung từ [URL]".

2. **Lưu log hoạt động**:
   - Thêm node **Code** để ghi log vào Supabase hoặc Google Sheets.

3. **Tự động cập nhật định kỳ**:
   - Sử dụng **n8n Cron Trigger** để chạy workflow hàng ngày để cập nhật nội dung mới.

4. **Tối ưu embeddings**:
   - Thử các model embeddings khác (ví dụ: `text-embedding-ada-002` vs `text-embedding-3-small`).

---
### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc trích xuất và lưu trữ dữ liệu thủ công, đồng thời **xây dựng hệ thống AI RAG** để trả lời câu hỏi một cách thông minh. **Hãy áp dụng ngay** và tự động hóa quy trình của mình!

👉 **[Tải workflow JSON](https://n8n.io/workflows/13911)** và bắt đầu "lên đồ" ngay!

---
**Chia sẻ ý kiến** của các sếp về workflow này ở phần **comment** dưới đây! 🚀