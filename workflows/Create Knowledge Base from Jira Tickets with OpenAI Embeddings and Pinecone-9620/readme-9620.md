---
title: "🚀 Tự động tạo Knowledge Base từ Jira tickets bằng OpenAI & Pinecone"
description: "Workflow n8n tự động lấy các ticket đã hoàn thành trên Jira, chuyển nội dung thành vector embeddings bằng OpenAI và lưu trữ trong Pinecone, tạo nên Knowledge Base thông minh chỉ trong vài phút."
slug: "tu-dong-tao-knowledge-base-tu-jira-bang-openai-pinecone"
tags: [n8n, automation, no-code, jira, openai, pinecone]
keywords: [n8n workflow, tự động hóa, knowledge base, jira, openai embeddings, pinecone vector store]
---

# 🚀 Tự động tạo Knowledge Base từ Jira tickets bằng OpenAI & Pinecone

Trong môi trường SaaS, các dự án luôn tích luỹ hàng trăm, thậm chí hàng nghìn ticket trên Jira. Khi cần tra cứu nhanh các vấn đề đã giải quyết, các sếp thường phải **đọc lại từng ticket**, sao chép nội dung, rồi tìm kiếm thủ công – tốn thời gian, dễ sai sót và không thể mở rộng.  

Workflow này sẽ **tự động thu thập ticket đã hoàn thành**, trích xuất tiêu đề, mô tả và comment, chuyển chúng thành vector embeddings bằng OpenAI, rồi lưu trữ trong Pinecone. Kết quả là một Knowledge Base có khả năng trả lời câu hỏi bằng ngôn ngữ tự nhiên, luôn cập nhật mỗi lần chạy.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không còn phải mở từng ticket để tìm thông tin.  
- **Tìm kiếm chính xác**: Vector search trên Pinecone cho kết quả gần đúng 99% so với nội dung gốc.  
- **Cập nhật liên tục**: Workflow chạy định kỳ, Knowledge Base luôn đồng bộ với Jira.  
- **Mở rộng dễ dàng**: Có thể tích hợp ngay vào chatbot nội bộ, Slack, hoặc công cụ tìm kiếm.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Jira** (Cloud hoặc Server) với quyền **Read** các issue và comment.  
- **API Key OpenAI** (có quyền `text-embedding-ada-002` hoặc tương đương).  
- **API Key Pinecone** và **Index** đã tạo (kích thước phù hợp với khối lượng dữ liệu).  
- **n8n** đã cài đặt (Self‑hosted hoặc n8n.cloud) và có quyền **Import workflow**.  
- (Tùy chọn) **Node “Code”** cần bật `Execute Once` để chạy JavaScript ES6.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.  
2. Nhấn **Import** → **Upload JSON** → Chọn file JSON của workflow (hoặc copy toàn bộ JSON và dán vào ô **Paste JSON**).  
3. Nhấn **Import**, workflow sẽ xuất hiện trên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌  

| Node | Mục đích | Cấu hình cần chỉnh |
|------|----------|--------------------|
| **Schedule Trigger** | Đặt lịch chạy định kỳ (ví dụ: mỗi ngày 02:00). | - `Cron` → `0 2 * * *` (hoặc tùy nhu cầu). |
| **Jira Issue List** | Lấy danh sách ticket đã hoàn thành. | - **Credentials**: chọn Jira credential.<br>- **JQL**: `project = YOUR_PROJECT AND status = Done AND updated >= -7d` (lấy ticket trong 7 ngày qua). |
| **Jira Issue Detail** | Lấy chi tiết (summary, description, comment) cho mỗi ticket. | - **Credentials**: cùng credential Jira.<br>- **Resource**: `issueComment`.<br>- **Issue Key**: `{{$json["key"]}}` (được truyền từ node trước). |
| **Loop Over Items (splitInBatches)** | Duyệt từng ticket để xử lý song song. | - **Batch Size**: `5` (tùy tài nguyên). |
| **Code1** | Chuẩn hoá dữ liệu, loại bỏ HTML/markdown không cần. | - **Code**: (đã có sẵn trong workflow). Kiểm tra biến `item` và trả về `{ text: cleanedText, metadata: {...} }`. |
| **Code2** | Định dạng lại dữ liệu cho **Default Data Loader**. | - Đảm bảo output có trường `content` và `metadata`. |
| **Default Data Loader** | Đóng gói dữ liệu thành **Document** chuẩn cho LangChain. | - **Field Mapping**: `content` → `text`, `metadata` → `metadata`. |
| **Embeddings OpenAI** | Tạo vector embeddings từ nội dung ticket. | - **Credentials**: OpenAI API Key.<br>- **Model**: `text-embedding-ada-002`. |
| **Pinecone Vector Store** | Lưu vector vào Pinecone Index. | - **Credentials**: Pinecone API Key.<br>- **Index Name**: `jira-knowledge-base` (hoặc tên bạn tạo).<br>- **Namespace**: `tickets`. |

> **Lưu ý:** Các node **Code1** và **Code2** chứa script JavaScript. Nếu bạn muốn tùy chỉnh cách lọc dữ liệu (ví dụ: bỏ qua các ticket không có comment), hãy chỉnh sửa biến `item` trong script.

#### 3. Kích hoạt ⚡️
1. **Test run**: Chọn **Execute Workflow** → **Run Once** → Kiểm tra log của mỗi node, đặc biệt là **Embeddings OpenAI** và **Pinecone Vector Store** để chắc chắn vector được tạo và lưu thành công.  
2. Khi mọi thứ ổn, bật **Active** (nút chuyển đổi ở góc trên bên phải). Workflow sẽ tự động chạy theo lịch đã định.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp Slack/Telegram**: Thêm node **Slack** hoặc **Telegram** để gửi thông báo mỗi khi có ticket mới được đưa vào Knowledge Base.  
- **Log chi tiết**: Dùng node **Write Binary File** hoặc **Google Sheets** để lưu log số ticket đã xử lý, thời gian chạy, và lỗi (nếu có).  
- **Tự động tạo câu hỏi FAQ**: Thêm một node **LLM (ChatGPT)** sau **Embeddings OpenAI** để sinh câu hỏi/đáp cho mỗi ticket, rồi lưu vào một sheet để tạo FAQ nhanh.  
- **Rà soát định kỳ**: Sử dụng node **Schedule Trigger** để chạy một workflow “clean‑up” xóa các vector cũ hơn 90 ngày, giữ cho index gọn gàng.  

### 📌 Kết luận
Với workflow này, các sếp có thể **biến kho ticket Jira thành một Knowledge Base thông minh**, hỗ trợ tìm kiếm nhanh, giảm tải công việc hỗ trợ kỹ thuật và nâng cao hiệu suất làm việc của toàn đội. Hãy import ngay, cấu hình các credentials, và để n8n tự động làm việc cho bạn! 🚀