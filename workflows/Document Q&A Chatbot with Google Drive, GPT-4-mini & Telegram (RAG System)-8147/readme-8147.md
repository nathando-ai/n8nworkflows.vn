---
title: "🚀 Xây dựng Chatbot Q&A Tài liệu thông minh với Google Drive, GPT-4-mini & Telegram (Hệ thống RAG)"
description: "Hướng dẫn xây dựng hệ thống RAG tự động hóa bằng n8n, cho phép hỏi đáp trực tiếp với tài liệu trên Google Drive qua Telegram sử dụng OpenAI GPT-4-mini."
slug: "chatbot-qa-tai-lieu-google-drive-gpt4-mini-telegram-rag"
tags: [n8n, automation, ai-rag, openai, telegram, google-drive]
keywords: [n8n workflow, chatbot q&a, rAG system, google drive ai, telegram bot openai, gpt-4-mini]
---

# 🚀 Xây dựng Chatbot Q&A Tài liệu thông minh với Google Drive, GPT-4-mini & Telegram (Hệ thống RAG)

Các sếp có bao giờ cảm thấy mệt mỏi khi phải mò mẫm tìm kiếm thông tin trong hàng đống tài liệu PDF, Word lưu trên Google Drive mỗi khi khách hàng hoặc sếp lớn hỏi đến? Việc đọc thủ công vừa tốn thời gian, lại dễ bỏ sót ý. 

Đừng lo, bài toán này sẽ được giải quyết triệt để với workflow n8n tích hợp **Hệ thống RAG (Retrieval-Augmented Generation)**. Workflow này sẽ tự động hóa toàn bộ quy trình: khi các sếp ném tài liệu lên Google Drive, AI sẽ tự động đọc hiểu, đưa vào cơ sở dữ liệu vector và sẵn sàng trả lời mọi câu hỏi của các sếp (hoặc khách hàng) ngay qua chat Telegram một cách nhanh chóng và chính xác 100%!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn việc nạp tri thức:** Chỉ cần upload file lên thư mục Google Drive chỉ định, hệ thống tự động cập nhật kiến thức cho AI mà không cần thao tác thủ công.
- **Hỏi đáp thông minh 24/7 qua Telegram:** Tương tác với kho tài liệu của doanh nghiệp mọi lúc, mọi nơi ngay trên ứng dụng chat quen thuộc.
- **Độ chính xác cao nhờ RAG:** AI trả lời dựa trên chính xác nội dung tài liệu gốc, hạn chế tối đa việc bịa đặt thông tin (hallucination).
- **Tiết kiệm hàng chục giờ làm việc:** Không còn phải "lật tung" Google Drive để tìm kiếm thông tin cũ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản OpenAI API Key** (Dùng cho Embedding và Model GPT-4-mini).
- **Tài khoản Google Drive** (Đã tạo sẵn một thư mục riêng biệt để chứa tài liệu).
- **Telegram Bot Token** (Tạo qua `@BotFather` trên Telegram).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và paste trực tiếp vào n8n Editor của mình, hoặc import file JSON tải từ nguồn gốc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống hoạt động mượt mà, các sếp cần cấu hình chính xác các node sau:

- **Node `File uploaded` (Google Drive Trigger) & `Download file`:** 
  - Kết nối tài khoản Google Drive (Credentials: `googleDriveOAuth2Api`).
  - Chọn chính xác thư mục (Folder) trên Google Drive mà các sếp muốn dùng làm "kho tri thức". Mọi file mới đưa vào đây sẽ kích hoạt quá trình nạp dữ liệu.
- **Node `Model` (OpenAI Chat Model):**
  - Cấu hình Credentials OpenAI (`openAiApi`).
  - Đảm bảo model được chọn là `gpt-4.1-mini` (hoặc `gpt-4o-mini` tùy theo cập nhật của OpenAI) để tối ưu chi phí và tốc độ.
- **Node `Embedding model`:**
  - Sử dụng chung Credentials OpenAI để tạo vector embedding cho tài liệu. Lưu ý quan trọng từ tác giả: *Node nạp dữ liệu (`Insert documents`) và truy xuất (`Retrieve documents`) phải dùng chung một loại Embedding model để tránh lỗi không khớp dữ liệu.*
- **Node `Listen for incoming events` (Telegram Trigger) & `Telegram`:**
  - Cấu hình Telegram API Credentials bằng cách điền Bot Token lấy từ `@BotFather`.

#### 3. Kích hoạt ⚡️
- **Test nạp dữ liệu:** Upload thử một file PDF/Word vào thư mục Google Drive đã chọn, quay lại n8n và bấm **"Execute workflow"** để kiểm tra node `Insert documents` chạy thành công.
- **Test Chat:** Mở con bot Telegram vừa tạo, gửi câu hỏi liên quan đến nội dung tài liệu và nhận câu trả lời từ AI.
- Sau khi test ngon lành, các sếp bật công tắc **Active** góc trên cùng bên phải để workflow chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh chat:** Ngoài Telegram, các sếp có thể thay thế bằng node Slack, Messenger hoặc Webhook để tích hợp trực tiếp lên website công ty.
- **Lưu lịch sử chat:** Kết nối thêm một node Google Sheets hoặc Database để lưu lại lịch sử câu hỏi của người dùng nhằm phục vụ việc cải thiện chất lượng tài liệu sau này.
- **Báo cáo định kỳ:** Thêm nhánh gửi báo cáo tổng hợp các câu hỏi phổ biến về Telegram cá nhân của quản lý vào cuối ngày.

### 📌 Kết luận
Một hệ thống RAG thu nhỏ ngay trong tầm tay với chi phí gần như bằng 0 và không cần một dòng code nào. Hãy áp dụng ngay vào doanh nghiệp của các sếp để tối ưu hóa việc quản lý và tra cứu tri thức ngay hôm nay!