---
title: "🚀 Tạo Banner Quảng Cáo Đỉnh Cao Tự Động Bằng LINE, Gemini và Nano Banana Pro"
description: "Tự động hóa hoàn toàn quy trình thiết kế banner quảng cáo tiếp thị từ tin nhắn LINE, tối ưu prompt bằng Google Gemini và tạo ảnh chất lượng cao qua Nano Banana Pro."
slug: "tao-banner-quang-cao-tu-dong-line-gemini-nano-banana"
tags: [n8n, automation, ai, line-bot, google-gemini, content-creation]
keywords: [n8n workflow, tao banner quang cao tu dong, line bot ai, google gemini n8n, nano banana pro]
---

# 🚀 Tạo Banner Quảng Cáo Đỉnh Cao Tự Động Bằng LINE, Gemini và Nano Banana Pro

Việc thiết kế banner quảng cáo thủ công thường tốn rất nhiều thời gian từ khâu lên ý tưởng, viết prompt, tạo ảnh cho đến khi gửi lại cho khách hàng hoặc đội ngũ marketing. Các sếp có bao giờ nghĩ đến việc chỉ cần nhắn một câu lệnh đơn giản qua **LINE**, hệ thống sẽ tự động hô biến nó thành một banner quảng cáo sắc nét, chuyên nghiệp và gửi trả lại ngay lập tức chưa? 

Workflow n8n này do CEO Masaki Go (HumanoiD Inc.) xây dựng sẽ giúp các sếp giải quyết bài toán đó một cách mượt mà và tự động 100% mà không cần tốn một dòng code thủ công nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tốc độ chớp nhoáng:** Biến ý tưởng thô thành banner quảng cáo hoàn chỉnh chỉ trong vài phút.
- **AI tối ưu thông minh:** Google Gemini tự động biến mô tả ngắn gọn thành prompt chi tiết, chuyên nghiệp dành cho thiết kế marketing.
- **Tương tác liền mạch:** Nhận yêu cầu và trả kết quả trực tiếp qua ứng dụng chat LINE quen thuộc.
- **Tự động lưu trữ:** Tự động tải ảnh về, đẩy lên AWS S3 và trả link công khai cho người dùng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã kích hoạt và sẵn sàng sử dụng.
- **Tài khoản LINE Developers:** Để tạo Webhook nhận/gửi tin nhắn.
- **Google Gemini API Key:** Sử dụng cho node `Optimize Prompt (Marketing)1`.
- **Nano Banana Pro (Kie.ai) API & Header Auth:** Dùng cho dịch vụ tạo ảnh AI.
- **AWS S3 Bucket:** Cấu hình quyền Public Read để lưu trữ và hiển thị ảnh banner.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ n8n.io (ID: 11205) hoặc copy toàn bộ mã JSON và dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống hoạt động trơn tru, các sếp cần chú ý cấu hình các node cốt lõi sau:
- **LINE Webhook1 (`webhook`):** Lấy URL webhook được cung cấp sau khi Active và cấu hình vào bảng điều khiển LINE Developers (Messaging API). Path mặc định là `banner-v7158-2025`.
- **Optimize Prompt (Marketing)1 (`googleGemini`):** Kết nối tài khoản Google Gemini API (`googlePalmApi`) để làm nhiệm vụ phân tích ngôn ngữ và viết prompt thiết kế chuyên sâu.
- **Submit Nano Banana Pro1 & Check Job Status (`httpRequest`):** Thiết lập Header Auth kết nối với dịch vụ Nano Banana Pro (qua Kie.ai) để gửi yêu cầu tạo ảnh và kiểm tra trạng thái tiến trình (Async Generation).
- **Upload to S (`awsS3`):** Cấu hình credentials AWS S3 và đảm bảo Bucket được cấp quyền Public Read để ảnh sinh ra có thể hiển thị trực tiếp trên LINE.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và thử gửi một tin nhắn mô tả sản phẩm/concept qua ứng dụng LINE để test run.
- Sau khi kiểm tra dữ liệu trả về chính xác, gạt công tắc sang **Active** để đưa bot vào vận hành thực tế 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh chat:** Thay vì chỉ dùng LINE, các sếp có thể nhân bản node webhook và tích hợp thêm Telegram Bot hoặc Slack để đội ngũ marketing dễ dàng sử dụng.
- **Lưu lịch sử vào Google Sheets:** Thêm một node Google Sheets vào cuối luồng để lưu lại các prompt đã tạo và link ảnh S3, phục vụ cho việc tra cứu hoặc phân tích chiến dịch sau này.
- **Thông báo qua Email/Slack:** Gửi cảnh báo về Slack ngay khi có banner mới được tạo thành công để team duyệt trước khi tung ra các chiến dịch lớn.

### 📌 Kết luận
Workflow tự động hóa kết hợp giữa LINE, Gemini và Nano Banana Pro là một mảnh ghép tuyệt vời giúp tối ưu hóa quy trình sản xuất nội dung hình ảnh cho các doanh nghiệp thời đại số. Hãy cài đặt ngay hôm nay để tiết kiệm hàng giờ thiết kế thủ công cho đội ngũ của bạn!