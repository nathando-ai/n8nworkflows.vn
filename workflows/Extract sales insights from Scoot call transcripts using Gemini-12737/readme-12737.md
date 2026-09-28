---
title: "🚀 Tự động trích xuất insights cuộc gọi bán hàng từ Scoot với Google Gemini trong n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động lấy bản ghi cuộc gọi từ Scoot, dùng AI Gemini phân tích insights và cập nhật CRM, gửi email báo cáo cho sales rep."
slug: "trich-xuat-sales-insights-scoot-gemini-n8n"
tags: [n8n, automation, no-code, ai-agent, gemini, crm, sales-automation]
keywords: [n8n workflow, trich xuat sales insights, scoot call transcription, google gemini ai, tu dong hoa crm, ai agent n8n]
---

# 🚀 Tự động trích xuất insights cuộc gọi bán hàng từ Scoot với Google Gemini

Các sếp làm sales chắc hẳn đều ngán ngẩm cảnh phải ngồi nghe lại hàng chục đoạn ghi âm cuộc gọi mỗi ngày, sau đó thủ công ghi chú lại ngân sách, đối thủ cạnh tranh, ý kiến phản đối (objections) hay bước tiếp theo vào CRM. Vừa mất thời gian, vừa dễ bỏ sót thông tin quan trọng của khách hàng!

Workflow n8n này sinh ra để giải quyết triệt để nỗi đau đó. Hệ thống sẽ tự động hóa từ A-Z: nhận bản ghi cuộc gọi (transcript) từ **Scoot**, dùng sức mạnh AI của **Google Gemini** để bóc tách dữ liệu thông minh, tự động cập nhật vào CRM và gửi email tổng hợp tóm tắt trực tiếp cho sale rep chỉ trong tích tắc. 100% tự động, không tốn một phút nhập liệu thủ công nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Sales rep không cần tóm tắt cuộc gọi thủ công, tập trung 100% vào chốt deal.
- **Dữ liệu CRM chuẩn xác:** AI tự động bóc tách ngân sách, đối thủ, pain points, timeline và đưa thẳng vào hệ thống.
- **Cơ chế xử lý thông minh (Retry Logic):** Tự động kiểm tra trạng thái transcript, nếu chưa xong sẽ chờ và thử lại, đảm bảo không bỏ sót dữ liệu.
- **Thông báo tức thì:** Gửi email tóm tắt cuộc gọi sắc bén đến từng sales rep ngay sau khi cuộc gọi kết thúc.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Scoot API Key**: Dùng để lấy bản ghi cuộc gọi thông qua Webhook và API.
- **Google AI API Key**: Lấy từ [Google AI Studio](https://aistudio.google.com) để kết nối với Gemini.
- **Tài khoản Gmail**: Kết nối OAuth2 để gửi email tổng hợp cho nhân viên sales.
- **Hệ thống CRM**: HubSpot, Salesforce, Pipedrive hoặc bất kỳ CRM nào các sếp đang dùng (có thể thay thế node mock CRM).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ n8n.io (Link gốc: ID 12737) hoặc copy trực tiếp mã JSON và dán vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 17 nodes được sắp xếp logic. Các sếp cần cấu hình chính xác các điểm sau:

- **Node `Receive Scoot webhook` & `Fetch transcript from Scoot`**: 
  - Copy Webhook URL dán vào phần cài đặt Webhook trên bảng điều khiển Scoot.
  - Tạo Credentials loại **Header Auth** với API Key của Scoot để node `Fetch transcript from Scoot` gọi dữ liệu thành công.
- **Node `Gemini 1.5 Flash` (AI Model) & `Extract data with Gemini`**: 
  - Kết nối Google AI API Key (`googlePalmApi`). Model Gemini sẽ đóng vai trò AI Agent bóc tách các trường dữ liệu như: ngân sách, đối thủ cạnh tranh, objections, timeline, quyết định mua hàng...
- **Node `Update CRM (mock)`**: 
  - Workflow mặc định dùng node code dạng mock. Các sếp nhớ thay thế node này bằng các node CRM chính thức (như HubSpot, Salesforce, Pipedrive, hoặc HTTP Request kết nối API nội bộ).
- **Node `Email summary to rep`**: 
  - Cấu hình Credentials **Gmail OAuth2** để hệ thống có quyền gửi email báo cáo trực tiếp đến hộp thư của sales rep.
- **Node `Wait 1 hour` & Retry Logic**: 
  - Workflow có sẵn logic xử lý khi transcript chưa sẵn sàng: chờ 1 tiếng và retry tối đa 6 lần (`Count retry attempts`, `Retries remaining?`, `Prepare retry request`). Các sếp có thể điều chỉnh thời gian chờ tại node `Wait 1 hour` tùy theo tốc độ xử lý của Scoot.

#### 3. Kích hoạt ⚡️
- Bấm nút **"Test with sample data"** (`Test with sample data` node kết nối với `Load sample transcript`) để chạy thử nghiệm xem AI trích xuất chuẩn chỉnh chưa.
- Sau khi test mượt mà, gạt công tắc **Active** ở góc trên bên phải để workflow chính thức trực chiến 24/7!

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Slack/Telegram**: Thay vì chỉ gửi email, các sếp có thể cắm thêm node Slack hoặc Telegram để bắn thông báo nóng vào group sales ngay khi có cuộc gọi VIP.
- **Lưu trữ Log thất bại**: Nếu sau 6 lần retry mà transcript vẫn lỗi, hãy cấu hình thêm một nhánh gửi cảnh báo vào kênh DevOps/Admin để kiểm tra.
- **Tùy biến Prompt AI**: Tinh chỉnh system prompt trong AI Agent để Gemini tập trung sâu hơn vào các câu hỏi đặc thù của sản phẩm bên mình (ví dụ: câu hỏi về tính năng bảo mật, giá cước Enterprise...).

### 📌 Kết luận
Với workflow n8n kết hợp giữa Scoot và Google Gemini này, quy trình quản lý thông tin cuộc gọi bán hàng của công ty sẽ được nâng lên một tầm cao mới: chuyên nghiệp, tự động và cực kỳ nhanh chóng. Triển khai ngay thôi các sếp ơi!