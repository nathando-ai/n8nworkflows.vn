---
title: "🚀 Tự động phân loại và gắn nhãn email Gmail thông minh bằng AI OpenAI"
description: "Hướng dẫn xây dựng hệ thống tự động hóa quản lý hòm thư Gmail, dùng AI phân tích nội dung email và tự động tạo/gắn nhãn thông minh 24/7."
slug: "tu-dong-phan-loai-gan-nhan-email-gmail-ai-openai"
tags: [n8n, automation, gmail, openai, ai-agent, productivity]
keywords: [n8n workflow, tự động hóa gmail, openai phân loại email, gắn nhãn email tự động, quản lý email thông minh]
---

# 🚀 Tự động phân loại và gắn nhãn email Gmail thông minh bằng AI OpenAI

Các sếp có bao giờ cảm thấy ngợp thở mỗi sáng mở hòm thư Gmail lên với hàng trăm email chưa đọc: từ email công việc quan trọng, thông báo hệ thống, newsletter rác cho tới các hóa đơn tài chính? Việc ngồi lọc, đọc và gắn nhãn thủ công cho từng email tốn rất nhiều thời gian và dễ bỏ lỡ thông tin quan trọng.

Giải pháp ư? Workflow n8n này sẽ giúp các sếp tự động hóa 100% quy trình đọc, phân tích nội dung bằng AI (OpenAI), kiểm tra nhãn hiện có, thậm chí tự động tạo nhãn mới và gắn vào email cực kỳ chuyên nghiệp. Không cần tốn một giọt mồ hôi thủ công nào nữa!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tuyệt đối:** Tự động quét và xử lý hòm thư định kỳ mà không cần đụng tay.
- **Phân loại thông minh bằng AI:** Sử dụng sức mạnh của OpenAI để hiểu ngữ cảnh email sâu sắc thay vì chỉ dùng từ khóa thô sơ.
- **Tự động quản lý nhãn (Labels):** Tự động nhận diện nhãn có sẵn trong Gmail hoặc tạo nhãn mới hoàn toàn tự động nếu email thuộc một chủ đề hoàn toàn mới.
- **Hệ thống chạy ngầm 24/7:** Hoạt động trơn tru theo lịch trình được thiết lập sẵn (Schedule Trigger).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Google/Gmail** để cấp quyền kết nối (Gmail OAuth2 credentials).
- **OpenAI API Key** để AI xử lý và phân loại nội dung email.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn JSON của workflow (hoặc tải file từ n8n.io/workflows/4557), sau đó paste trực tiếp vào màn hình n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 17 nodes hoạt động nhịp nhàng với nhau. Các sếp cần chú ý cấu hình kỹ các điểm sau:
- **Schedule Trigger:** Cấu hình tần suất chạy workflow (ví dụ: mỗi 15 phút, 1 tiếng/lần hoặc chạy vào giờ hành chính).
- **Gmail - Get All Messages & Gmail - Single Message:** Kết nối tài khoản Gmail của các sếp thông qua `gmailOAuth2` credentials để bot có quyền đọc danh sách email và nội dung chi tiết.
- **Filter Emails Without Excluded Labels (Code node):** Tùy chỉnh đoạn code lọc này nếu các sếp muốn bỏ qua một số email đã có nhãn cụ thể hoặc email từ các thể loại không cần xử lý.
- **OpenAI Chat Model:** Điền `openAiApi` credentials và chọn model mong muốn (mặc định cấu hình sẵn `gpt-4.1-nano` hoặc các model GPT-4o-mini, GPT-4o tùy nhu cầu).
- **Categorize Email with AI (Agent node):** Node này chịu trách nhiệm định hướng AI cách đọc tiêu đề, nội dung email và đưa ra nhãn phù hợp nhất. Các sếp có thể tinh chỉnh System Prompt bên trong để AI phân loại đúng ý đồ doanh nghiệp (VD: *Hỗ trợ, Kinh doanh, Hóa đơn, Spam...*).
- **Check if Label Exists & Apply/Create Label nodes:** Các node Gmail resource label sẽ tự động đối chiếu xem nhãn do AI đề xuất đã có trong Gmail chưa. Nếu có rồi thì gắn vào (`Apply Label to Email`), nếu chưa thì tự động tạo mới (`Apply New Label` và `Create New Label`).

#### 3. Kích hoạt ⚡️
- Nhấn **Test Step** hoặc **Execute Workflow** với một vài email mẫu để kiểm tra xem AI phân loại và gắn nhãn có chính xác không.
- Sau khi test mượt mà, gạt công tắc sang **Active** để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm một node Telegram hoặc Slack sau bước gắn nhãn để nhận thông báo ngay lập tức khi có email cực kỳ quan trọng (VD: Email phàn nàn từ khách hàng VIP).
- **Lưu log Google Sheets:** Thêm một node Google Sheets để ghi lại lịch sử các email đã được AI phân loại nhằm dễ dàng thống kê báo cáo cuối tuần.
- **Mở rộng bộ lọc:** Tinh chỉnh prompt của AI để phân cấp mức độ ưu tiên (Khẩn cấp, Bình thường, Thấp) kết hợp gắn màu sắc cho nhãn Gmail nếu API hỗ trợ.

### 📌 Kết luận
Việc tự động hóa hòm thư chưa bao giờ dễ dàng đến thế với sự kết hợp hoàn hảo giữa n8n và AI OpenAI. Hãy cài đặt ngay workflow này để giải phóng thời gian cho các công việc chiến lược hơn, đừng để bản thân bị ngập chìm trong núi email mỗi ngày nữa nhé các sếp!