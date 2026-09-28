---
title: "🚀 Tự động soạn bản nháp Email với AI, OpenAI và OpenRouter (Inbox Zero)"
description: "Hướng dẫn cài đặt workflow n8n tự động phân loại email đến qua Gmail, sử dụng AI LangChain để soạn sẵn bản nháp phản hồi chuẩn phong cách cá nhân và gửi thông báo qua Telegram."
slug: "tu-dong-soan-nhap-email-voi-ai-openai-openrouter-n8n"
tags: [n8n, automation, ai, openai, gmail, telegram, openrouter]
keywords: [n8n workflow, tự động hóa gmail, ai soạn email, inbox zero, openrouter, langchain n8n]
---

# 🚀 Tự động soạn bản nháp Email với AI, OpenAI và OpenRouter (Inbox Zero)

Các sếp có bao giờ cảm thấy ngợp thở mỗi sáng khi mở hộp thư đến với hàng chục, hàng trăm email chờ xử lý? Việc đọc hiểu, tra cứu tài liệu rồi ngồi gõ từng email phản hồi ngốn rất nhiều thời gian quý báu, khiến các sếp phân tâm khỏi các chiến lược cốt lõi của doanh nghiệp.

Giải pháp ở đây là gì? Workflow n8n này sẽ thay các sếp làm sạch hộp thư đến (đạt trạng thái **Inbox Zero**) bằng cách tự động hóa 100%: Lắng nghe email mới -> Phân loại thông minh bằng AI -> Tra cứu kiến thức (RAG) nếu cần -> Tự động tạo bản nháp (Draft) trong Gmail chuẩn phong cách cá nhân -> Báo cáo ngay qua Telegram. Không cần code phức tạp, chỉ cần kéo thả và kết nối!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian xử lý email**: AI tự động viết nháp 90% nội dung trả lời, các sếp chỉ cần review lại và bấm "Gửi".
- **Lọc sạch email rác/tự động**: Hệ thống tự động bỏ qua các bản tin (newsletter), hóa đơn, thông báo hệ thống và chỉ tập trung vào khách hàng thực sự.
- **Cá nhân hóa cao**: AI được huấn luyện theo văn phong của riêng sếp và có thể tra cứu kho tài liệu (FAQ, chính sách) qua Vector Store.
- **Cập nhật tức thì**: Nhận thông báo qua Telegram ngay khi có bản nháp email mới được tạo hoặc có email cần chú ý.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị sẵn các tài khoản sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Gmail** (để cấu hình OAuth2 credentials và quyền tạo draft).
- **OpenAI API Key** (dùng cho Chat Model và Embeddings).
- **OpenRouter API Key** (dùng cho mô hình phân loại email).
- **Telegram Bot Token & Chat ID** (để nhận thông báo).
- **Supabase Account** (Tùy chọn: Kho lưu trữ Vector cho cơ sở kiến thức/FAQ của doanh nghiệp).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này từ n8n templates (ID: 13203) hoặc copy đoạn mã JSON tương ứng, sau đó dán trực tiếp vào n8n Editor của các sếp bằng cách chọn **New workflow** -> Dán (Ctrl+V / Cmd+V).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 15 nodes thông minh kết hợp giữa AI Agent và Gmail automation. Các sếp cần cấu hình kỹ các điểm sau:

- **Gmail Trigger & createDraft**: Kết nối tài khoản Gmail của các sếp thông qua `gmailOAuth2` để node có quyền đọc email đến và tạo bản nháp (`draft`) tự động.
- **OpenAI Chat Model & Embeddings OpenAI**: Điền thông tin `openAiApi` credentials để cấp quyền cho AI xử lý ngôn ngữ và tạo vector embeddings.
- **OpenRouter Chat Model**: Cấu hình `openRouterApi` credentials dùng cho node `Client/Prospect Related?` nhằm phân loại email nhanh chóng và tiết kiệm chi phí.
- **Email Draft Agent**: Đây là "trái tim" của workflow. Các sếp cần cập nhật System Prompt, nhồi thông tin chi tiết về doanh nghiệp, phong cách viết email của sếp, kèm theo 5-10 ví dụ email mẫu để AI học theo đúng văn phong.
- **Customer Support? (Switch node)** & **Response / Response Not Customer Support (Telegram nodes)**: Cấu hình Telegram Bot Token và Chat ID để nhận tin nhắn cảnh báo hoặc thông báo bản nháp mới tạo thành công.
- **Vector Storage (Supabase)**: *(Tùy chọn)* Nếu doanh nghiệp có kho tài liệu FAQ, hãy kết nối với Supabase Vector Store để AI tra cứu thông tin chính xác khi trả lời câu hỏi khó từ khách hàng.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và gửi một email thử nghiệm vào hòm thư Gmail để test luồng chạy.
- Kiểm tra kết quả hiển thị trên Telegram và hòm thư Gmail (phần Nháp/Draft).
- Nếu mọi thứ chạy mượt mà, hãy gạt công tắc **Active** ở góc trên cùng bên phải để workflow tự động chiến đấu 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack/Microsoft Teams**: Thay thế hoặc bổ sung node Telegram bằng Slack/Teams để đội ngũ chăm sóc khách hàng cùng nhận được thông báo bản nháp.
- **Lưu log vào Google Sheets**: Thêm node Google Sheets để ghi lại lịch sử các email đã được AI soạn nháp, giúp dễ dàng thống kê hiệu suất.
- **Mở rộng RAG**: Kết nối thêm Notion hoặc Google Drive làm nguồn dữ liệu (Knowledge Base) để AI cập nhật thông tin sản phẩm mới nhất tự động.

### 📌 Kết luận
Với workflow n8n cực kỳ thông minh này, việc quản lý hộp thư email không còn là gánh nặng mỗi ngày. Hãy thiết lập ngay hôm nay để tối ưu hóa thời gian và mang lại trải nghiệm phản hồi khách hàng cực kỳ chuyên nghiệp và tức thì!