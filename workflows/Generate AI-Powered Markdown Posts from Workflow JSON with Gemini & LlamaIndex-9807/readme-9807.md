---
title: "🚀 Tự động hóa tạo bài viết Markdown từ Workflow JSON với Gemini & LlamaIndex"
description: "Hướng dẫn cấu hình workflow n8n sử dụng AI Gemini, LlamaIndex và Google Drive để tự động trích xuất, phân tích và tạo bài viết chuẩn Markdown chuyên nghiệp từ file JSON."
slug: "tao-bai-viet-markdown-tu-workflow-json-gemini-llamaindex"
tags: [n8n, automation, ai, gemini, llamaindex, google-drive, markdown]
keywords: [n8n workflow, tạo markdown tự động, gemini ai, llamaindex cloud, google drive trigger, AI agent n8n]
---

# 🚀 Tự động hóa tạo bài viết Markdown từ Workflow JSON với Gemini & LlamaIndex

Các sếp có bao giờ cảm thấy đuối sức khi phải ngồi thủ công viết tài liệu, hướng dẫn sử dụng hoặc bài viết blog phân tích từ các file cấu hình workflow n8n (JSON) dài dằng dặc? Việc này vừa tốn thời gian, vừa dễ bỏ sót các chi tiết kỹ thuật quan trọng.

Giải pháp cho các sếp đây: một workflow n8n hoàn chỉnh kết hợp sức mạnh của **Google Gemini**, **LlamaIndex Cloud**, và **Google Drive** để tự động hóa toàn bộ quy trình: nhận file JSON qua Form hoặc Google Drive, phân tích tài liệu tri thức (Knowledge Base), và sinh ra các bài viết định dạng Markdown vô cùng chuẩn chỉnh và chi tiết. Không cần viết code, chỉ cần "lắp ráp" và chạy!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và xử lý các file dữ liệu lớn không bị gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Biến các file JSON phức tạp thành tài liệu Markdown chỉ trong vài nốt nhạc.
- **Ứng dụng AI thông minh:** Sử dụng Google Gemini (GEmini 2.5 pro) kết hợp hệ thống RAG (Retrieval-Augmented Generation) thông qua LlamaIndex và Vector Store in-memory để đảm bảo nội dung chính xác, đúng ngữ cảnh kỹ thuật.
- **Đồng bộ qua Google Drive:** Tự động theo dõi và cập nhật cơ sở tri thức (Knowledge Base) trực tiếp từ Google Drive.
- **Tiết kiệm hàng giờ đồng hồ:** Thay vì viết thủ công, các sếp có thể dành thời gian đó để phát triển kinh doanh.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI CÀI ĐẶT]
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị sẵn các tài khoản và credentials sau:
1. **Google Gemini (Google Palm API Key):** Dành cho các node AI Agent, Embeddings và LLM Chat.
2. **LlamaIndex Cloud API Key:** Cấu hình qua chuẩn `HTTP Header Auth` cho các node tương tác với dịch vụ parse tài liệu của LlamaIndex.
3. **Google Drive OAuth2:** Dành cho các node theo dõi trigger và tải file tri thức từ Google Drive.
4. **Cohere API Key:** Dành cho node Reranker Cohere (tối ưu hóa kết quả tìm kiếm vector).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Copy đoạn mã JSON của workflow hoặc tải file JSON từ nguồn gốc.
- Mở giao diện n8n Editor của các sếp, chọn **Add workflow** -> **Import from File** (hoặc dán trực tiếp JSON vào canvas).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các thông số và kết nối credentials cho các node cốt lõi sau:

- **On form submission:** Node kích hoạt dạng form, các sếp có thể tùy chỉnh giao diện form nhận đầu vào file JSON từ người dùng.
- **Extract from File:** Đảm bảo key parameter `operation` được đặt là `fromJson` để trích xuất dữ liệu JSON chính xác.
- **Parse Document via LlamaIndex & Retrieve Parsed Content (HTTP Request nodes):**
  - Cần chọn credentials **HTTP Header Auth**.
  - Header Name: `Authorization`
  - Header Value: `Bearer <API_KEY_LLAMAINDEX_CUA_BAN>`
- **Google Drive Trigger & Download Knowledge Document:**
  - Kết nối với tài khoản **Google Drive OAuth2** của các sếp.
  - Chọn thư mục trên Google Drive để làm kho lưu trữ tri thức (Knowledge Base).
- **GEmini 2.5 pro & Embedd 004:**
  - Thêm credential **Google Palm API** (Google Gemini API Key).
- **Reranker Cohere:**
  - Thêm credential **Cohere API** để tinh chỉnh độ chính xác của các tài liệu truy xuất trong Vector Store.
- **n8ncreator (AI Agent):** Node trung tâm điều phối, đảm bảo liên kết với model Gemini và Vector Store (`vectorStoreInMemory`).

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và thử tải lên một file JSON mẫu để test run xem quá trình trích xuất và sinh Markdown có hoạt động mượt mà không.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để workflow sẵn sàng hoạt động tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
Để workflow trở nên "bá đạo" hơn nữa, các sếp có thể mở rộng theo các hướng sau:
- **Tích hợp Slack hoặc Telegram:** Thêm node gửi thông báo về kênh chat ngay khi bài viết Markdown được tạo xong kèm link tải.
- **Tự động lưu vào Notion / GitHub:** Thay vì chỉ hiển thị kết quả, hãy kết nối thêm node Notion hoặc GitHub để tự động push bài viết lên blog cá nhân hoặc kho lưu trữ tài liệu.
- **Báo cáo định kỳ:** Tạo thêm một nhánh chạy theo lịch (Schedule Trigger) để thống kê số lượng workflow đã được xử lý trong tuần.

### 📌 Kết luận
Workflow tạo bài viết Markdown từ JSON bằng Gemini & LlamaIndex là một "vũ khí" tuyệt vời giúp tự động hóa khâu làm tài liệu kỹ thuật, tiết kiệm hàng đống thời gian cho các lập trình viên và nhà quản lý tự động hóa. Hãy cài đặt ngay lên hệ thống n8n của các sếp và tận hưởng thành quả! Chúc các sếp thao tác thành công!