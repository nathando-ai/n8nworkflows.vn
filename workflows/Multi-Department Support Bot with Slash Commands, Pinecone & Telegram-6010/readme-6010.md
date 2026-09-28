---
title: "🚀 Xây dựng Bot Telegram Hỗ Trợ Đa Phòng Ban Thông Minh với AI RAG, Pinecone & PostgreSQL trên n8n"
description: "Hướng dẫn xây dựng hệ thống Support Bot đa phòng ban trên Telegram tích hợp AI RAG (Pinecone, Cohere, OpenRouter) và PostgreSQL để tự động hóa chăm sóc khách hàng 24/7."
slug: "bot-telegram-ho-tro-da-phong-ban-ai-rag-pinecone-n8n"
tags: [n8n, automation, ai-agent, telegram, pinecone, postgres, rag]
keywords: [n8n workflow, telegram bot ai, rag pinecone n8n, ai agent support bot, tu dong hoa telegram]
---

# 🚀 Xây dựng Bot Telegram Hỗ Trợ Đa Phòng Ban Thông Minh với AI RAG, Pinecone & PostgreSQL

Các sếp có đang đau đầu vì đội ngũ hỗ trợ khách hàng quá tải, phải trả lời đi trả lời lại các câu hỏi lặp đi lặp lại về chính sách đổi trả, kỹ thuật hay thanh toán? Việc phân loại thủ công các yêu cầu từ khách hàng lên Telegram thường xuyên gây chậm trễ và nhầm lẫn giữa các phòng ban.

Giải pháp ở đây chính là workflow **Multi-Department Support Bot with Slash Commands, Pinecone & Telegram**. Đây là một hệ thống tự động hóa 100% không cần code, kết hợp giữa AI Agent thông minh, cơ sở dữ liệu Vector (Pinecone), quản lý trạng thái qua PostgreSQL và giao diện Telegram quen thuộc. Bot sẽ tự động cập nhật tài liệu từ Google Drive, phân loại yêu cầu và trả lời khách hàng chính xác như một nhân viên support thực thụ!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, xử lý các tác vụ AI và webhook liên tục từ Telegram, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phân loại phòng ban tự động:** Khách hàng có thể chọn chuyên khoa hỗ trợ (Chính sách, Kỹ thuật, Thanh toán) thông qua câu lệnh `/start`, `/end` hoặc các nút điều hướng.
- **Hệ thống RAG thông minh:** Tự động đồng bộ tài liệu PDF từ Google Drive vào Pinecone Vector Store, giúp AI trả lời dựa trên tài liệu thực tế của doanh nghiệp mà không bịa đặt (hallucination).
- **Lưu trữ ngữ cảnh lịch sử:** Sử dụng PostgreSQL để quản lý tiến trình hội thoại và lịch sử chat của từng người dùng qua `Simple Memory3`.
- **Hoạt động 24/7:** Phản hồi tức thì mọi lúc mọi nơi qua Telegram, tiết kiệm tối đa thời gian và nhân lực cho đội ngũ Support.
:::

### 📦 Các thành phần chính trong hệ thống
Workflow gồm **46 nodes** được chia thành các phân khu rõ ràng trên canvas n8n:
- **Main Bot & Telegram Trigger:** Lắng nghe tin nhắn, xử lý lệnh slash (`/start`, `/end`) và điều hướng người dùng bằng `Switch`.
- **Google Drive & Pinecone Sync:** Tự động bắt sự kiện file PDF mới (`Google Drive Trigger`), tải file xuống (`Download file`), bẻ nhỏ văn bản (`Character Text Splitter`), tạo vector nhúng qua `Embeddings Cohere` và lưu trữ tại `Pinecone Vector Store` cho từng phòng ban (Billing, Technical, Return Policy).
- **AI Agent & Database:** Sử dụng `OpenRouter Chat Model3` (chạy model DeepSeek Chat v3 miễn phí/tiết kiệm) kết hợp với `Execute a SQL query` (PostgreSQL) để tra cứu và ghi nhớ trạng thái hội thoại.

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI "LÊN ĐỒ"]
- **n8n instance** (phiên bản Cloud hoặc Self-hosted).
- **Telegram Bot Token** (tạo qua `@BotFather`).
- **Pinecone Account & Index** (để lưu trữ vector tài liệu).
- **Cohere API Key** (để tạo vector embeddings).
- **OpenRouter API Key** (để gọi LLM DeepSeek/OpenAI).
- **Google Drive API Credentials** (để quản lý tài liệu PDF các phòng ban).
- **PostgreSQL Database** (để lưu trạng thái và phiên làm việc của user).
:::

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy toàn bộ mã nguồn JSON.
- Trong giao diện n8n, chọn **Add workflow** -> Nhấp vào biểu tượng menu (3 chấm) ở góc trên bên phải -> Chọn **Import from JSON** và dán dữ liệu vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình các credentials quan trọng cho các nhóm node sau:

- **Telegram Nodes (`Telegram Trigger`, `Send a text message`,...):** Kết nối với tài khoản Telegram Bot của doanh nghiệp bằng Telegram API Token.
- **Google Drive Nodes (`Google Drive Trigger`, `Download file`,...):** Xác thực tài khoản Google OAuth2 để bot có thể theo dõi thư mục tài liệu phòng ban.
- **AI & Vector Nodes (`OpenRouter Chat Model3`, `Embeddings Cohere3`, `Pinecone Vector Store3`):** 
  - Điền OpenRouter API Key và chọn model mong muốn (mặc định cấu hình `deepseek/deepseek-chat-v3-0324:free`).
  - Điền Cohere API Key cho các node Embeddings.
  - Cấu hình thông số Index Name chính xác trên Pinecone tương ứng với các phòng ban (Billing, Tech, Return Policy).
- **PostgreSQL Nodes (`Execute a SQL query`, `Select rows from a table`):** Điền thông tin kết nối Database Postgres của các sếp để bot lưu trữ phiên làm việc (`just to create table`, `billing1`, `tech questions`, `return policy1`).

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** và test thử bằng cách gửi lệnh `/start` tới bot Telegram của bạn.
- Kiểm tra luồng dữ liệu chạy qua node `Switch` và `AI Agent3`.
- Nếu mọi thứ hoạt động trơn tru, hãy bật công tắc **Active** ở góc trên cùng bên phải để bot chạy tự động 24/7.

---

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh giao tiếp:** Ngoài Telegram, các sếp có thể nhân bản luồng xử lý AI sang **Slack** hoặc **Facebook Messenger** bằng cách thay thế các node Telegram Trigger/Sender tương ứng.
- **Lưu log hội thoại:** Thêm một node Postgres hoặc Google Sheets vào cuối luồng để ghi lại toàn bộ câu hỏi của khách hàng, giúp đội ngũ quản lý phân tích insight cải thiện sản phẩm/dịch vụ.
- **Tự động hóa cập nhật tài liệu:** Chỉ cần ném file PDF mới vào thư mục Google Drive tương ứng, hệ thống sẽ tự động cập nhật tri thức cho AI mà không cần can thiệp thủ công.

---

### 📌 Kết luận
Workflow **Multi-Department Support Bot** là một mô hình AI RAG cực kỳ mạnh mẽ, giúp tự động hóa khâu chăm sóc khách hàng đa phòng ban với chi phí tối ưu nhất. Hãy triển khai ngay hôm nay để nâng cấp hệ thống CSKH của doanh nghiệp lên một tầm cao mới!