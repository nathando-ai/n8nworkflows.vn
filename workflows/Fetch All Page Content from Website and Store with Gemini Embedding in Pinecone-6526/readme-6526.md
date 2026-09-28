---
title: "🚀 Tự động quét toàn bộ website và lưu trữ Vector Embedding vào Pinecone bằng Gemini"
description: "Hướng dẫn xây dựng hệ thống RAG tự động cào dữ liệu toàn bộ website (qua sitemap hoặc URL) kết hợp Gemini Embeddings và Pinecone Vector Store trong n8n."
slug: "quet-website-gemini-embedding-pinecone-n8n"
tags: [n8n, automation, ai-rag, pinecone, google-gemini, web-scraping]
keywords: [n8n workflow, rir, ai rag, pinecone vector store, gemini embeddings, cào dữ liệu website, sitemap parser]
---

# 🚀 Tự động quét toàn bộ website và lưu trữ Vector Embedding vào Pinecone bằng Gemini

Các sếp có bao giờ gặp khó khăn khi muốn xây dựng một trợ lý AI (Chatbot RAG) dựa trên toàn bộ dữ liệu từ website của công ty, nhưng việc copy-paste hoặc cấu hình các công cụ cào dữ liệu thủ công quá tốn thời gian và dễ lỗi? Việc tổng hợp hàng trăm, hàng ngàn bài viết từ website để đưa vào cơ sở dữ liệu vector đòi hỏi một quy trình tự động hóa bài bản.

Workflow n8n này do chuyên gia **Zain Khan** thiết kế chính là giải pháp "tất cả trong một" giúp các sếp tự động cào toàn bộ nội dung website (thông qua Sitemap XML hoặc danh sách URL tùy chỉnh), chuyển hóa chúng thành các vector embedding bằng **Google Gemini** và lưu trữ an toàn vào **Pinecone Vector Database** hoàn toàn tự động!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và xử lý các trang web lớn mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Chỉ cần nhập Sitemap hoặc danh sách URL vào Form, hệ thống sẽ tự lo phần còn lại.
- **Xử lý thông minh:** Tự động lọc trùng lặp URL, phân đoạn nội dung và thêm thời gian nghỉ (`Wait`) để tránh bị website đích chặn (rate-limit).
- **AI-Powered RAG:** Sử dụng mô hình `models/gemini-embedding-001` mạnh mẽ của Google để tạo vector embedding chất lượng cao.
- **Sẵn sàng cho Chatbot:** Lưu trữ trực tiếp vào Pinecone Index (`supportbot`), giúp các sếp xây dựng AI Chatbot tư vấn khách hàng hoặc tra cứu tài liệu nội bộ cực nhanh.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và thông tin sau:
1. **n8n Instance:** Đã chạy ổn định (khuyến nghị bản mới nhất).
2. **Google Gemini API Key:** Dùng cho node Gemini Embeddings.
3. **Pinecone API Key & Index Name:** Tài khoản Pinecone và đã tạo sẵn một Index (ví dụ: `supportbot`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow từ nguồn gốc hoặc tải file về, sau đó chọn **Add workflow** -> **Import from File / Paste JSON** trong giao diện n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 15 nodes được chia làm 3 giai đoạn chính, các sếp cần chú ý cấu hình các điểm sau:

- **Input Sitemap or page urls (`formTrigger`):** Điểm khởi đầu dưới dạng Form. Khi chạy, hệ thống sẽ yêu cầu các sếp nhập Sitemap URL hoặc danh sách URL cần quét.
- **Fetch Sitemap (`httpRequest`) & XML Conversion (`xml`):** Xử lý việc tải và chuyển đổi cấu trúc XML của sitemap thành JSON để lấy danh sách URL bài viết.
- **Fetch Page HTML For content (`httpRequest`) & Extract Content (`html`):** Node HTML sẽ lọc bỏ hình ảnh, rác và chỉ lấy phần nội dung text chính của trang web. Node **Wait 5 sec** đóng vai trò quan trọng giúp giãn cách thời gian gọi request, bảo vệ IP của sếp không bị ban.
- **Gemini Embeddings (`embeddingsGoogleGemini`):** Kết nối với tài khoản Google AI Studio của sếp, chọn model embedding phù hợp (mặc định: `models/gemini-embedding-001`).
- **Pinecone KnowledgeBase (`vectorStorePinecone`):** Điền thông tin API Key của Pinecone, trỏ tới Index (ví dụ: `supportbot`) để đẩy dữ liệu vector lên đám mây.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử với một Sitemap nhỏ hoặc 1-2 URL cụ thể qua Form Trigger.
- Sau khi kiểm tra dữ liệu đã vào Pinecone thành công, gạt công tắc sang **Active** để hệ thống sẵn sàng hoạt động bất cứ lúc nào.

---

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa workflow này cho doanh nghiệp, các sếp có thể mở rộng thêm:
1. **Gửi thông báo Telegram/Slack:** Thêm một node thông báo kết quả (số lượng trang đã quét thành công) về nhóm chat nội bộ khi hoàn thành.
2. **Lịch trình tự động (Schedule Trigger):** Thay thế Form Trigger bằng Schedule Trigger để tự động quét và cập nhật lại Knowledge Base hàng tuần/hàng tháng.
3. **Xử lý lỗi (Error Handling):** Thêm Error Trigger để bắt các URL bị lỗi 404 hoặc timeout và ghi log lại.

### 📌 Kết luận
Việc tự động hóa xây dựng cơ sở tri thức RAG từ website chưa bao giờ dễ dàng đến thế với sự kết hợp giữa n8n, Google Gemini và Pinecone. Hãy áp dụng ngay vào dự án của các sếp để tối ưu hóa thời gian và nâng cấp hệ thống AI của doanh nghiệp lên một tầm cao mới!