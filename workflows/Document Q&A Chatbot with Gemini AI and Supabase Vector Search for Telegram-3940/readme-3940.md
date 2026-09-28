---
title: "🚀 Xây dựng Chatbot Telegram AI Đọc Tài Liệu Cá Nhân với n8n, Gemini và Supabase"
description: "Hướng dẫn chi tiết cách tự động hóa chatbot Telegram tích hợp AI Google Gemini và Supabase Vector Search để trò chuyện, hỏi đáp trực tiếp với tài liệu PDF của bạn trên n8n."
slug: "chatbot-telegram-ai-tai-lieu-gemini-supabase-n8n"
tags: [n8n, automation, ai, telegram, gemini, supabase, vector-search]
keywords: [n8n workflow, chatbot telegram ai, gemini ai, supabase vector search, rag n8n, tự động hóa tài liệu]
---

# 🚀 Xây dựng Chatbot Telegram AI Đọc Tài Liệu Cá Nhân với n8n, Gemini và Supabase

Các sếp có bao giờ cảm thấy mệt mỏi khi phải đọc lướt hàng chục trang tài liệu PDF chỉ để tìm một thông tin nhỏ? Hay việc quản lý kiến thức cá nhân trở nên quá tải vì tài liệu nằm rải rác khắp nơi? Thay vì tốn hàng giờ tra cứu thủ công, tại sao không tự xây dựng một **Trợ lý AI thông minh trên Telegram** có khả năng đọc hiểu toàn bộ tài liệu và trả lời mọi câu hỏi của các sếp chỉ trong vài giây?

Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ mạnh mẽ, kết hợp giữa **Google Gemini LLM**, **Supabase Vector Database** và **Telegram Bot** để tạo ra một hệ thống RAG (Retrieval-Augmented Generation) hoàn chỉnh mà không cần viết một dòng code phức tạp nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, xử lý các file tài liệu lớn và phản hồi tin nhắn Telegram mượt mà, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tương tác trực tiếp qua Telegram**: Gửi câu hỏi và nhận câu trả lời ngay lập tức từ bot giống như đang chat với trợ lý riêng.
- **Biến PDF thành tri thức sống**: Chỉ cần upload file PDF lên chat, bot sẽ tự động đọc, bóc tách văn bản, tạo vector embeddings và lưu trữ an toàn.
- **Bảo mật tuyệt đối & Tốc độ cao**: Tài liệu gốc lưu trữ an toàn trên Supabase của sếp, chỉ các đoạn nội dung liên quan mới được gửi đến LLM để xử lý.
- **Mở rộng linh hoạt**: Tích hợp sẵn công cụ tra cứu thời tiết (OpenWeatherMap) và khả năng suy luận mở rộng.
:::

### 📦 Tổng quan về Workflow (25 Nodes)
Workflow này được chia thành 2 kịch bản (scenarios) chính xử lý song song:
1. **Scenario 1 – Chatbot Interaction**: Tiếp nhận tin nhắn từ người dùng, xử lý câu hỏi, tra cứu vector trên cơ sở dữ liệu Supabase, kết hợp với Google Gemini Chat Model để đưa ra câu trả lời chính xác nhất.
2. **Scenario 2 – Document Upload and Embedding**: Tự động tải file PDF từ Telegram, bóc tách nội dung văn bản, cắt nhỏ chuỗi text, tạo embeddings và lưu vào bảng vector của Supabase.

Các nodes chủ chốt trong hệ thống bao gồm: `Telegram Trigger`, `AI Agent`, `Google Gemini Chat Model`, `Supabase Vector Store`, `Extract from File`, `Recursive Character Text Splitter`,...

---

### 🔧 Yêu cầu cần thiết
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API Keys sau:
:::info[CHUẨN BỊ]
- **n8n Instance**: Đã cài đặt sẵn (Self-hosted hoặc Cloud).
- **Telegram Bot Token**: Tạo qua `@BotFather` trên Telegram.
- **Google Gemini API Key**: Lấy từ Google AI Studio để dùng cho LLM và Embeddings.
- **Supabase Account**: Tạo một project miễn phí để làm Vector Database.
- **OpenWeatherMap API Key** (Tùy chọn): Nếu muốn bot có thêm tính năng tra cứu thời tiết.
:::

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ nguồn cung cấp hoặc copy trực tiếp mã JSON.
- Trong giao diện n8n Editor, chọn **Add workflow** -> Nhấp vào biểu tượng menu (3 chấm) -> **Import from File / Clipboard** và dán dữ liệu vào.

#### 2. Cấu hình cơ sở dữ liệu Supabase (BẮT BUỘC) 📌
Trước khi chạy workflow, các sếp cần thiết lập bảng vector trong Supabase. Truy cập vào **Supabase SQL Editor** và chạy đoạn lệnh sau:

```sql
-- Kích hoạt extension pgvector
create extension vector;

-- Tạo bảng lưu trữ kiến thức và embeddings
create table user_knowledge_base (
  id bigserial primary key,
  content text, -- Lưu đoạn text từ tài liệu
  metadata jsonb, -- Lưu thông tin file (tên, số trang...)
  embedding vector(768) -- Vector embedding từ Gemini (768 chiều)
);

-- Tạo hàm tìm kiếm tương đồng vector
create function match_documents (
  query_embedding vector(768),
  match_count int default null,
  filter jsonb DEFAULT '{}'
) returns table (
  id bigint,
  content text,
  metadata jsonb,
  similarity float
)
language plpgsql
as $$
#variable_conflict use_column
begin
  return query
  select
    id,
    content,
    metadata,
    1 - (user_knowledge_base.embedding <=> query_embedding) as similarity
  from user_knowledge_base
  where metadata @> filter
  order by user_knowledge_base.embedding <=> query_embedding
  limit match_count;
end;
$$;
```

#### 3. Kết nối Credentials trong n8n 📌
Các sếp cần thiết lập các credentials tương ứng cho các node sau:
- **Telegram Trigger** & Các node **Telegram**: Nhập `Telegram API Token`.
- **Google Gemini Chat Model** & **Embeddings Google Gemini**: Nhập `Google Gemini API Key`.
- **Supabase Vector Store** & **Supabase - Save Embeddings**: Nhập URL và Service Role Key của dự án Supabase.
- **OpenWeatherMap**: Nhập API key nếu sử dụng tính năng thời tiết.

#### 4. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và thử gửi một file PDF bất kỳ vào bot Telegram của các sếp để kiểm tra quá trình embedding.
- Sau khi báo thành công, hãy thử đặt câu hỏi liên quan đến nội dung file vừa gửi.
- Nếu mọi thứ hoạt động trơn tru, hãy bật công tắc **Active** ở góc trên cùng bên phải để bot hoạt động 24/7.

---

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống hoàn thiện và chuyên nghiệp hơn, các sếp có thể mở rộng thêm:
- **Lưu lịch sử chat**: Kết hợp thêm node lưu log hội thoại vào Google Sheets hoặc Airtable để phân tích nhu cầu người dùng.
- **Đa kênh thông báo**: Mở rộng workflow để nhận tài liệu không chỉ từ Telegram mà còn qua Email (IMAP node) hoặc Slack.
- **Bộ lọc đa người dùng**: Bổ sung thêm xử lý Session/User ID nếu muốn triển khai bot công khai cho nhiều người dùng cùng lúc (lưu ý phiên bản hiện tại tối ưu cho cá nhân/single-user).

---

### 📌 Kết luận
Chỉ với vài bước cấu hình cùng n8n, Supabase và Gemini AI, các sếp đã sở hữu ngay một trợ lý AI đọc tài liệu cực kỳ xịn sò chạy trên Telegram. Không còn cảnh tìm kiếm thủ công mệt mỏi, tri thức giờ đây nằm trong tầm tay. Chúc các sếp cài đặt thành công và hẹn gặp lại ở các bài hướng dẫn tự động hóa tiếp theo!