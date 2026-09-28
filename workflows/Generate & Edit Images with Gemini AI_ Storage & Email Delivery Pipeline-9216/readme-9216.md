---
title: "🚀 Tự động Tạo và Chỉnh sửa Ảnh với Gemini AI kết hợp Google Drive & Email"
description: "Hướng dẫn xây dựng pipeline tự động hóa n8n giúp tạo ảnh, chỉnh sửa ảnh bằng Gemini AI, lưu trữ tự động lên Google Drive và gửi kết quả qua Email hoàn toàn tự động."
slug: "tu-dong-tao-va-chinh-sua-anh-voi-gemini-ai-google-drive-email"
tags: [n8n, automation, gemini-ai, google-drive, ai-image-generation, no-code]
keywords: [n8n workflow, tạo ảnh ai, gemini ai, google drive automation, tự động hóa gửi email]
---

# 🚀 Tự động Tạo và Chỉnh sửa Ảnh với Gemini AI kết hợp Google Drive & Email

Các sếp có bao giờ cảm thấy mệt mỏi khi phải thủ công tạo prompt, chạy tool AI để tạo ảnh, sau đó tải về máy, upload lên Google Drive rồi lại mất công soạn email gửi cho khách hàng hoặc đội ngũ? Quy trình lặp đi lặp lại này ngốn rất nhiều thời gian và dễ xảy ra sai sót.

Đừng lo, trong bài viết này, tôi sẽ hướng dẫn các sếp triển khai một siêu phẩm n8n workflow do chuyên gia **Gerald Denor (DominixAI)** thiết kế: **Generate & Edit Images with Gemini AI: Storage & Email Delivery Pipeline**. Workflow này sẽ tự động hóa từ A-Z quy trình nhận yêu cầu, xử lý hình ảnh bằng AI, lưu trữ đám mây và trả kết quả qua email cực kỳ chuyên nghiệp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Biến mọi ý tưởng thành hình ảnh chất lượng cao thông qua Gemini AI chỉ bằng một cú nhấp chuột hoặc một Webhook request.
- **Lưu trữ thông minh:** Tự động đẩy file ảnh kết quả lên Google Drive và cấu hình quyền chia sẻ linh hoạt.
- **Giao tiếp liền mạch:** Tự động soạn và gửi email kèm hình ảnh trực tiếp đến người nhận ngay khi hoàn thành.
- **Linh hoạt đầu vào:** Hỗ trợ cả việc tạo ảnh hoàn toàn từ văn bản (Prompt Only) lẫn việc nhận file ảnh tải lên để chỉnh sửa.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống **n8n** đang hoạt động (Self-hosted hoặc n8n Cloud).
- Tài khoản và API Key của **Gemini AI / Nano** (hoặc dịch vụ AI tích hợp qua HTTP Request).
- Tài khoản **Google Drive** (đã cấu hình Google OAuth2 Credentials trong n8n để upload và share file).
- Cấu hình **SMTP / Email Account** để node `Send email` có thể hoạt động gửi thư.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này (hoặc tải file từ n8n.io/workflows/9216) và paste trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần chú ý cấu hình kỹ các node trọng điểm sau:
- **Webhook:** Điểm tiếp nhận request đầu vào (chứa prompt hoặc file ảnh cần xử lý). Hãy copy URL webhook để tích hợp vào ứng dụng của các sếp.
- **If Image File Was Uploaded & Code / Edit Fields:** Node phân loại luồng xử lý (nếu có file ảnh tải lên thì đi hướng chỉnh sửa, nếu không sẽ đi hướng tạo ảnh từ prompt thuần túy).
- **Nano 🍌 & Nano 🍌: Prompt Only (HTTP Request Nodes):** Nơi cấu hình API gọi tới Gemini AI. Các sếp cần điền chính xác API Key, Header và Body theo tài liệu API của nhà cung cấp.
- **Upload file & Share file (Google Drive Nodes):** Kết nối tài khoản Google Drive của sếp, chọn thư mục đích (Folder ID) để lưu ảnh và thiết lập quyền chia sẻ công khai hoặc nội bộ nếu cần.
- **Send email (Email Send Node):** Cấu hình tài khoản gửi email (SMTP/Gmail), điền tiêu đề và nội dung template kèm đường dẫn Google Drive hoặc tệp đính kèm.
- **Respond to Webhook:** Đảm bảo node này trả về phản hồi JSON thành công (status 200) cho phía gọi API ban đầu.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và bắn một request thử nghiệm qua Webhook để kiểm tra toàn bộ dữ liệu chạy qua các nhánh.
- Nếu mọi thứ mượt mà, hãy gạt công tắc sang **Active** để hệ thống tự động vận hành 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm thông báo:** Nối thêm node Telegram hoặc Slack sau node `Send email` để đội ngũ nhận được thông báo ngay khi có ảnh mới được tạo thành công.
- **Lưu log vào Google Sheets:** Thêm một node Google Sheets trước khi kết thúc để lưu lại lịch sử prompt, thời gian tạo và link ảnh phục vụ việc thống kê, tra cứu sau này.
- **Tối ưu Prompt AI:** Tùy biến các node `Edit Fields` để làm giàu prompt tự động trước khi gửi cho Gemini AI giúp chất lượng ảnh đầu ra nghệ thuật và sát với thực tế hơn.

### 📌 Kết luận
Workflow **Generate & Edit Images with Gemini AI: Storage & Email Delivery Pipeline** là một giải pháp cực kỳ mạnh mẽ giúp tự động hóa khâu sáng tạo nội dung hình ảnh cho các Agency, nhà sáng tạo nội dung hoặc đội ngũ marketing. Hãy thiết lập ngay hôm nay để tiết kiệm hàng giờ đồng hồ làm việc thủ công mỗi ngày nhé các sếp!