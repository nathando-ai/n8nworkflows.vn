---
title: "🚀 Tự động tạo bản nháp trả lời Gmail thông minh với GPT-4o-mini trong n8n"
description: "Xây dựng hệ thống tự động đọc email đến, phân tích nội dung bằng AI và tạo bản nháp phản hồi chuẩn xác, tiết kiệm thời gian xử lý hòm thư."
slug: "tu-dong-tra-loi-gmail-gpt-4o-mini-n8n"
tags: [n8n, automation, gmail, openai, ai-agent, productivity]
keywords: [n8n workflow, tự động hóa gmail, openai gpt-4o-mini, ai agent trả lời email, n8n viet nam]
---

# 🚀 Tự động tạo bản nháp trả lời Gmail thông minh với GPT-4o-mini

Các sếp có bao giờ cảm thấy ngộp thở vì hàng tá email đến mỗi ngày? Việc phải đọc, phân loại và ngồi gõ từng email trả lời khách hàng, đối tác chiếm rất nhiều thời gian quý báu mà lẽ ra các sếp nên dùng để phát triển kinh doanh.

Đừng lo, bài toán này sẽ được giải quyết triệt để với **Gmail Auto-Reply Generator with GPT-4o-mini**. Workflow n8n này sẽ hoạt động như một trợ lý ảo 24/7: tự động quét email mới, phân tích xem email đó có thực sự cần phản hồi hay chỉ là rác/thông báo vớ vẩn, và tự động soạn sẵn một bản nháp (draft) cực kỳ chuyên nghiệp để các sếp chỉ cần bấm nút "Gửi". Tất cả hoàn toàn tự động, không cần tốn một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 không lo mất kết nối, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian xử lý email:** Không còn cảnh trầy trật viết email phản hồi lặp đi lặp lại.
- **An toàn tuyệt đối:** AI chỉ tạo *bản nháp (Draft)* chứ không tự động gửi đi, các sếp hoàn toàn kiểm soát được nội dung trước khi xuất xưởng.
- **Lọc bỏ rác thông minh:** AI tự động nhận diện tin nhắn rác, thông báo hệ thống và bỏ qua, chỉ tập trung vào email thực sự cần xử lý.
- **Phân loại tự động:** Gắn nhãn (Label) "Action" cho những luồng email cần chú ý đặc biệt.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn:
- Tài khoản n8n (Cloud hoặc Self-hosted).
- Tài khoản **Google / Gmail** (để cấp quyền đọc và tạo nháp email).
- **OpenAI API Key** (để sử dụng model `gpt-4o-mini`).
- Tạo sẵn một Label trong Gmail của các sếp có tên chính xác là: `Action`.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow hoặc copy trực tiếp và dán vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 9 nodes chính hoạt động mượt mà với nhau. Các sếp cần cấu hình các điểm sau:
- **Trigger on New Email (`gmailTrigger`):** Kết nối tài khoản Gmail của các sếp để hệ thống lắng nghe sự kiện có email mới đến.
- **Get Unread Email (`gmail`):** Node này dùng để lấy chi tiết nội dung email dựa trên ID từ trigger. Hãy đảm bảo chọn đúng Credentials Gmail.
- **OpenAI (`lmChatOpenAi`):** Chọn model `gpt-4o-mini` và điền OpenAI API Key của các sếp vào credential.
- **AI Agent (`agent`) & Structured Output (`outputParserStructured`):** Nơi định hình nhân cách và giọng văn (brand voice) của trợ lý ảo. Các sếp có thể tùy chỉnh Prompt trong Agent để AI viết email theo phong cách trang trọng, thân thiện hoặc chuyên nghiệp tùy ý.
- **Can AI Agent Respond? (`if`):** Node logic kiểm tra xem AI quyết định có nên phản hồi email này hay không (bỏ qua spam, thông báo...).
- **Create a draft (`gmail`) & Label Email As "Action" (`gmail`):** Cấu hình để tạo bản nháp phản hồi vào đúng thread và gắn nhãn `Action` vào chuỗi email đó trên Gmail.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và gửi một email test vào hòm thư của các sếp để kiểm tra kết quả.
- Kiểm tra mục **Drafts** trong Gmail xem bản nháp đã được sinh ra chuẩn chỉnh chưa.
- Nếu mọi thứ mượt mà, gạt công tắc sang **Active** để workflow chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm một node Telegram hoặc Slack sau bước tạo bản nháp để bot bắn tin nhắn báo về điện thoại: *"Sếp ơi, vừa có email mới từ khách hàng X và em đã soạn nháp sẵn rồi nhé!"*
- **Tùy chỉnh Prompt AI:** Tinh chỉnh system prompt trong **AI Agent** để dạy AI hiểu sâu hơn về sản phẩm, dịch vụ của công ty các sếp, giúp bản nháp tạo ra sát với thực tế nhất có thể.

### 📌 Kết luận
Một trợ lý email thông minh, làm việc không lương, túc trực 24/7 giờ đây nằm gọn trong tầm tay các sếp chỉ với vài cú click setup n8n. Triển khai ngay để giải phóng thời gian và tối ưu hóa quy trình chăm sóc khách hàng thôi nào các sếp!