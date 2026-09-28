---
title: "🚀 Xây dựng hộp thư phê duyệt email tự động bằng AI với OpenAI và CustomJS trong n8n"
description: "Tự động hóa quy trình trả lời email với AI, tích hợp giao diện duyệt (Human-in-the-loop) trực quan bằng Tailwind CSS và CustomJS trong n8n."
slug: "xay-dung-hop-thu-phe-duyet-email-tu-dong-ai-openai-customjs"
tags: [n8n, automation, ai, openai, gmail, customjs]
keywords: [n8n workflow, tự động hóa email, AI email reply, customjs, openai gpt, human-in-the-loop]
---

# 🚀 Xây dựng hộp thư phê duyệt email tự động bằng AI với OpenAI và CustomJS

Các sếp có đang cảm thấy quá tải mỗi khi mở hộp thư đến vì hàng đống email chờ phản hồi? Việc viết email thủ công ngốn rất nhiều thời gian, nhưng nếu giao phó hoàn toàn cho AI trả lời tự động thì lại tiềm ẩn rủi ro gửi đi những nội dung sai lệch hoặc kém chuyên nghiệp. 

Workflow n8n này chính là giải pháp hoàn hảo áp dụng mô hình **Human-in-the-loop** (Có con người kiểm duyệt). Hệ thống sẽ tự động quét email, dùng AI viết nháp câu trả lời, sau đó gom toàn bộ vào một giao diện web cực kỳ sang xịn mịn để các sếp duyệt, chỉnh sửa và bấm gửi chỉ với 1 cú click!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian:** Không cần tự gõ từng email từ đầu, AI đã lo phần soạn thảo ban đầu.
- **Kiểm soát tuyệt đối (Human-in-the-loop):** Email chỉ được gửi đi sau khi các sếp đã review, chỉnh sửa (nếu cần) và bấm nút phê duyệt trên giao diện web.
- **Giao diện hiện đại:** Web dashboard tích hợp Tailwind CSS và Alpine.js được host tự động qua CustomJS, truy cập dễ dàng mọi lúc mọi nơi.
- **Tự động hóa khép kín:** Sau khi duyệt, hệ thống tự động gửi phản hồi đúng luồng (threaded reply) qua Gmail và đánh dấu đã đọc email gốc.
:::

### 📦 Các thành phần trong Workflow
Workflow chia làm 2 luồng (Lane) chính hoạt động nhịp nhàng:
- **Lane 1 (Tạo bản nháp):** Lấy email chưa đọc $\rightarrow$ Lọc spam/no-reply $\rightarrow$ AI tạo nội dung trả lời $\rightarrow$ Đóng gói thành giao diện Dashboard bằng CustomJS.
- **Lane 2 (Xử lý phản hồi):** Nhận tín hiệu từ Webhook khi các sếp bấm duyệt $\rightarrow$ Gửi email qua Gmail $\rightarrow$ Đánh dấu email gốc là đã đọc.

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Gmail** (Kết nối qua OAuth2).
- **Tài khoản OpenAI** (Lấy OpenAI API Key).
- **Tài khoản CustomJS** (Lấy CustomJS API Credentials để host trang dashboard).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và dán trực tiếp vào n8n Editor của mình, hoặc import file JSON tải từ trang chủ n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node sau:
- **Get many messages, Reply to a message, Mark a message as read (Gmail Nodes):** Kết nối tài khoản Gmail của các sếp bằng **Gmail OAuth2**. Tại node `Get many messages`, có thể tùy chỉnh giới hạn số lượng email lấy về mỗi lần chạy (mặc định đang để là 3).
- **Generate AI Draft Reply (OpenAI Node):** Nhập **OpenAI API Key** và chọn mô hình (ví dụ: `gpt-4o` hoặc `gpt-5`). Các sếp có thể tinh chỉnh Prompt System bên trong node này để AI viết email chuẩn giọng văn (tone of voice) của cá nhân hoặc doanh nghiệp mình.
- **Upsert Approval Page (CustomJS Node):** Cấu hình **CustomJS API Credentials** để hệ thống có thể tạo và cập nhật trang Dashboard lên CDN.
- **Webhook - Receive Approval (Webhook Node):** Node này nhận dữ liệu khi các sếp bấm nút submit trên trang dashboard. *Lưu ý quan trọng:* Phải bật trạng thái **Active** cho workflow thì Webhook URL mới hoạt động và nhận được dữ liệu từ bên ngoài.

#### 3. Kích hoạt ⚡️
- Chạy thử thủ công (`Execute workflow`) bằng cách bấm nút `When clicking 'Execute workflow'` để test luồng tạo trang Dashboard.
- Sau khi kiểm tra mọi thứ trơn tru, hãy chuyển trạng thái workflow sang **Active** và thay thế trigger thủ công bằng *Gmail Trigger (On Email Received)* để hệ thống chạy hoàn toàn tự động khi có email mới đến.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo Telegram/Slack:** Thêm một node Telegram hoặc Slack ngay sau node `Upsert Approval Page` để bắn link dashboard trực tiếp về điện thoại mỗi khi có email mới cần duyệt.
- **Tùy biến giao diện Dashboard:** Tinh chỉnh code trong node `Build Approval Page` (chứa Tailwind CSS và Alpine.js) để thay đổi màu sắc, bố cục bảng điều khiển theo ý thích.
- **Lưu lịch sử:** Thêm node Google Sheets hoặc Airtable để lưu lại lịch sử các email đã được AI soạn thảo và được sếp phê duyệt nhằm phục vụ việc thống kê sau này.

### 📌 Kết luận
Với workflow n8n này, việc xử lý hàng chục hay hàng trăm email mỗi ngày không còn là ác mộng. Hãy cài đặt ngay hôm nay để tối ưu hóa năng suất làm việc và mang lại trải nghiệm chăm sóc khách hàng chuyên nghiệp nhất!