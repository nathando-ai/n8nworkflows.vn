---
title: "🚀 Tự động tạo Infographic tức thì qua LINE với AI và Nano Banana Pro"
description: "Hướng dẫn xây dựng workflow n8n tích hợp LINE, Google Gemini và Nano Banana Pro để tự động chuyển đổi dữ liệu phức tạp thành Infographic trực quan 3:4."
slug: "tao-infographic-tu-dong-qua-line-voi-ai-va-nano-banana-pro"
tags: [n8n, automation, ai-infographic, line-bot, google-gemini, nano-banana-pro]
keywords: [n8n workflow, tạo infographic tự động, line webhook, google gemini, nano banana pro, aws s3]
---

# 🚀 Tự động tạo Infographic tức thì qua LINE với AI và Nano Banana Pro

Các sếp có bao giờ cảm thấy đau đầu khi phải biến những số liệu khô khan, dữ liệu phức tạp thành các hình ảnh Infographic bắt mắt để đăng mạng xã hội hay báo cáo chưa? Việc thuê Designer hoặc tự mày mò trên Canva tốn rất nhiều thời gian và chi phí. 

Giải pháp là đây! Workflow n8n này sẽ biến ứng dụng **LINE** thành một "Studio thiết kế AI" thu nhỏ. Các sếp chỉ cần gửi một đoạn text hoặc dữ liệu thô qua chat LINE, hệ thống sẽ tự động phân tích bằng AI và trả về một tấm hình Infographic chuẩn chỉnh (tỉ lệ 3:4) ngay lập tức.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Biến text thô thành hình ảnh đồ họa chỉ trong vài phút mà không cần mở phần mềm thiết kế.
- **AI thông minh:** Google Gemini tự động đóng vai trò Chuyên gia phân tích dữ liệu, lựa chọn biểu đồ (Pie, Bar, Flowchart...) phù hợp nhất.
- **Trải nghiệm liền tay:** Gửi tin nhắn qua LINE và nhận lại ngay Infographic chất lượng cao gửi thẳng vào đoạn chat.
- **Tối ưu chi phí:** Kết hợp các API mạnh mẽ giúp tiết kiệm hàng đống tiền thuê thiết kế định kỳ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **LINE Official Account / LINE Developer Account** (để lấy Webhook và Channel Access Token).
- **Google Gemini API Key** (dùng cho node phân tích dữ liệu).
- **Tài khoản Nano Banana Pro API** (dịch vụ render hình ảnh).
- **AWS S3 Bucket** (để lưu trữ và public hình ảnh Infographic sau khi render xong).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp hãy copy đoạn mã JSON của workflow này và paste trực tiếp vào n8n Editor, hoặc import file JSON thông qua menu giao diện của n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 12 nodes được chia thành 3 giai đoạn chính. Các sếp cần cấu hình kỹ các điểm sau:

- **LINE Webhook:** Cấu hình đường dẫn endpoint (`infographic-v7158`) và kết nối với LINE Bot của các sếp để nhận sự kiện `POST` từ người dùng gửi tin nhắn.
- **Optimize Prompt (Data Vis):** Thêm Google Gemini Credentials và kiểm tra câu lệnh prompt để AI hiểu đúng cách cấu trúc dữ liệu thành mô tả trực quan (Biểu đồ, Icon, Layout...).
- **Submit to Nano Banana Pro & Check Job Status:** Nhập API Key của Nano Banana Pro vào node `HTTP Request`. Chú ý cấu hình tỉ lệ khung hình (`Aspect Ratio 3:4`) theo đúng ghi chú trên canvas. Node `Wait` và `Is Ready?` sẽ làm nhiệm vụ thông minh: lặp lại việc kiểm tra trạng thái render mỗi 5 giây cho đến khi ảnh sẵn sàng.
- **Upload to S3:** Điền thông tin AWS S3 credentials (Access Key, Secret Key, Region, Bucket Name) để lưu trữ hình ảnh render và tạo link Public.
- **Send Image to LINE:** Cấu hình node `HTTP Request` gọi API của LINE để đẩy file ảnh từ S3 trả ngược về đoạn chat cho người dùng.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và gửi một tin nhắn mẫu qua LINE (ví dụ: *"Japan Energy Mix: 20% Solar, 30% Wind, 50% Nuclear"*) để test thử.
- Kiểm tra kết quả xem ảnh có trả về LINE suôn sẻ không.
- Nếu mọi thứ mượt mà, gạt công tắc **Active** lên màu xanh để chạy 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa kênh nhận tin:** Ngoài LINE, các sếp có thể thay thế node đầu vào bằng Telegram Bot hoặc Slack Webhook tùy theo thói quen sử dụng của team.
- **Lưu lịch sử:** Thêm một node Google Sheets hoặc Airtable ngay sau bước nhận data để lưu lại lịch sử các yêu cầu tạo infographic của khách hàng/nhân sự.
- **Báo cáo lỗi:** Kết hợp thêm node gửi thông báo qua Telegram cá nhân nếu quá trình render từ Nano Banana Pro gặp lỗi timeout hoặc API hết hạn mức.

### 📌 Kết luận
Instant Infographic Generator là một workflow mẫu mực cho việc ứng dụng Multimodal AI vào tự động hóa công việc hàng ngày. Hãy cài đặt ngay hôm nay để biến chiếc LINE Bot của các sếp thành một trợ lý thiết kế siêu đẳng!