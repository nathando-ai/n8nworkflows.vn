---
title: "🚀 Tự động trích xuất công việc từ Gmail bằng ChatGPT-4o và Supabase với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động đọc email chưa đọc trong Gmail, dùng ChatGPT-4o phân tích tác vụ và lưu trữ cấu trúc vào Supabase không sợ trùng lặp."
slug: "tu-dong-trich-xuat-cong-viec-tu-gmail-chatgpt-supbase-n8n"
tags: [n8n, automation, gmail, openai, supabase, ai-summarization]
keywords: [n8n workflow, tự động hóa gmail, chatgpt 4o trích xuất task, supabase lưu trữ email, n8n ai automation]
---

# 🚀 Tự động trích xuất công việc từ Gmail bằng ChatGPT-4o và Supabase

Các sếp có bao giờ cảm thấy ngợp thở mỗi khi mở hộp thư đến (Inbox) và phát hiện hàng chục email chứa các yêu cầu, task công việc nằm rải rác? Việc đọc thủ công, tổng hợp và đưa vào danh sách việc cần làm (To-do list) ngốn rất nhiều thời gian quý báu.

Đừng lo, bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ thông minh do tác giả **Paul Taylor** xây dựng. Workflow này sẽ tự động quét email chưa đọc, nhờ **ChatGPT-4o** phân tích và trích xuất task, sau đó lưu trữ gọn gàng vào **Supabase** — đồng thời thông minh nhận diện những email đã xử lý để không bao giờ bị lặp lại tốn kém credit API!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Hộp thư đến tự động "biến hình" thành cơ sở dữ liệu công việc có cấu trúc rõ ràng.
- **Tiết kiệm thời gian & Trí lực:** Không còn bỏ sót các yêu cầu quan trọng ẩn trong email dài dằng dặc nhờ AI tóm tắt.
- **Chống trùng lặp thông minh:** Cơ chế kiểm tra Supabase giúp hệ thống chỉ xử lý email mới, tiết kiệm tối đa chi phí OpenAI API.
- **Hoạt động liên tục 24/7:** Chạy ngầm theo lịch trình định sẵn, sẵn sàng mỗi khi sếp cần.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn:
- Một instance n8n (Cloud hoặc Self-hosted).
- Tài khoản **Gmail** có quyền kết nối OAuth với n8n.
- Một project **Supabase** đã tạo bảng `emails` kèm ràng buộc khóa duy nhất:
  ```sql
  ALTER TABLE emails ADD CONSTRAINT unique_email_id UNIQUE (email_id);
  ```
- **OpenAI API Key** (có quyền truy cập GPT-4o hoặc GPT-3.5-turbo).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON từ link gốc của workflow (`https://n8n.io/workflows/5496`), sau đó chọn **Import from File** hoặc copy toàn bộ mã JSON dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, workflow sẽ xuất hiện với 8 nodes chính. Các sếp cần cấu hình lần lượt:

- **Trigger Workflow (Schedule Trigger):** Cấu hình tần suất chạy mong muốn (ví dụ: chạy mỗi 30 phút hoặc 1 tiếng một lần).
- **Get Unread Emails from Inbox (Gmail):** Kết nối tài khoản Gmail qua OAuth. Đặt bộ lọc chỉ lấy các email chưa đọc (`operation: getAll`).
- **Loop Over Items (Split InBatches):** Giúp duyệt qua từng email một cách mượt mà, tránh quá tải request.
- **Get Email from Database & Check if Email in Database (Supabase & IF):** Kiểm tra xem `email_id` đã tồn tại trên Supabase hay chưa. Nếu có rồi thì bỏ qua, chưa có thì tiếp tục xử lý.
- **Prepare ChatGPT Prompt (Code):** Node code JavaScript chuẩn bị nội dung thô của email để đưa vào AI.
- **Extract Task Detail from Email (OpenAI):** Kết nối OpenAI API Key, sử dụng mô hình GPT-4o để trích xuất nội dung thông minh theo dạng cấu trúc (summary, requires_deep_work, v.v.).
- **Insert Email Detail to Supabase (HTTP Request):** Cấu hình biến môi trường kết nối Supabase (`Supabase_TaskManagement_URI` và `Supabase_TaskManagement_ANON_KEY`) để đẩy dữ liệu đã trích xuất vào bảng `emails`.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** với một vài email test để kiểm tra luồng dữ liệu chạy qua từng node có suôn sẻ hay không.
- Kiểm tra lại dữ liệu đã được đẩy chuẩn chỉnh lên bảng Supabase chưa.
- Nếu mọi thứ mượt mà, gạt công tắc sang **Active** để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống tối ưu và "ngầu" hơn nữa, các sếp có thể mở rộng:
- **Tích hợp thông báo:** Thêm node Telegram hoặc Slack ngay sau khi lưu Supabase thành công để bắn thông báo tóm tắt task nóng lên điện thoại.
- **Tự động tạo lịch:** Kết nối kết quả trả về từ GPT với Google Calendar để tự động đặt lịch hẹn hoặc deadline xử lý task.
- **Mở rộng nền tảng task:** Tự động đồng bộ các task quan trọng sang ClickUp, Notion hoặc Trello.

### 📌 Kết luận
Workflow trích xuất task từ Gmail qua ChatGPT-4o và Supabase là một trợ lý ảo đắc lực giúp tối ưu hóa quy trình làm việc cá nhân cũng như doanh nghiệp. Hãy cài đặt ngay hôm nay để giải phóng bản thân khỏi "nỗi sợ" mang tên hộp thư đến!