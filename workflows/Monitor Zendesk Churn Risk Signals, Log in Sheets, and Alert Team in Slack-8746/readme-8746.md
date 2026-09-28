---
title: "🚀 Tự Động Giám Sát Rủi Ro Khách Hàng Rời Bỏ (Churn Risk) từ Zendesk, Lưu Google Sheets và Cảnh Báo Slack"
description: "Xây dựng hệ thống tự động phát hiện khách hàng có nguy cơ rời bỏ (churn) qua phản hồi tiêu cực trên Zendesk, tự động lưu log vào Google Sheets và gửi thông báo tức thì lên Slack cho đội ngũ CS."
slug: "tu-dong-giam-sat-rui-ro-khach-hang-zendesk-slack-google-sheets"
tags: [n8n, automation, zendesk, slack, google-sheets, customer-success, ai]
keywords: [n8n workflow, zendesk churn risk, tự động hóa zendesk slack, giam sat khach hang roi bo, google sheets automation]
---

# 🚀 Tự Động Giám Sát Rủi Ro Khách Hàng Rời Bỏ (Churn Risk) từ Zendesk, Lưu Google Sheets và Cảnh Báo Slack

Các sếp có bao giờ gặp tình trạng khách hàng phàn nàn, đánh giá tiêu cực trên hệ thống hỗ trợ (Zendesk) nhưng đội ngũ Chăm sóc khách hàng (CS) lại phát hiện quá muộn, dẫn đến việc khách hàng âm thầm rời bỏ dịch vụ (Churn)? Việc kiểm tra thủ công các ticket khiếu nại mỗi ngày ngốn rất nhiều thời gian và cực kỳ dễ bỏ sót.

Giải pháp ở đây là gì? Workflow n8n này sẽ tự động hóa 100% quy trình: tự động quét ticket Zendesk định kỳ, lọc ra các phản hồi tiêu cực, lưu vết chi tiết vào Google Sheets để làm báo cáo, đồng thời bắn cảnh báo ngay lập tức lên kênh Slack của đội ngũ để xử lý nóng!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phản ứng tức thì:** Cảnh báo ngay lập tức lên Slack khi có khách hàng đánh giá "bad" (tiêu cực), giúp CSKH can thiệp kịp thời giữ chân khách hàng.
- **Minh bạch dữ liệu:** Tự động ghi nhận mọi sự cố rủi ro vào Google Sheets để phân tích xu hướng và tính điểm sức khỏe khách hàng (Customer Health Score).
- **Tiết kiệm 100% thời gian thủ công:** Thay vì nhân sự phải ngồi lọc hàng trăm ticket mỗi ngày, hệ thống tự động chạy ngầm 24/7 theo lịch trình.
- **Vận hành chuyên nghiệp:** Chuẩn hóa quy trình xử lý khủng hoảng nhỏ trước khi biến thành sự cố lớn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động mượt mà, các sếp cần chuẩn bị sẵn các tài khoản sau:
- **n8n Instance** (Self-hosted hoặc n8n Cloud).
- **Tài khoản Zendesk** (Có quyền truy cập API/Admin để lấy thông tin tickets).
- **Google Account** (Để kết nối Google Sheets lưu trữ dữ liệu).
- **Slack Workspace** (Tạo sẵn Webhook hoặc Bot để gửi tin nhắn thông báo vào kênh chỉ định).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn JSON của workflow (hoặc tải file JSON từ n8n template #8746) và dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 6 nodes chính được thiết kế tối ưu. Các sếp cần cấu hình các điểm sau:

- **Schedule Trigger:** Mặc định đang đặt chạy hàng ngày lúc 20:00 (Biểu thức Cron: `0 20 * * *`). Các sếp có thể điều chỉnh lại múi giờ và tần suất chạy cho phù hợp với giờ làm việc của công ty.
- **Fetch Zendesk Tickets:** Kết nối tài khoản Zendesk của doanh nghiệp (`zendeskApi`). Node này sẽ lấy toàn bộ danh sách ticket (`operation: getAll`). Các sếp có thể tùy chỉnh thêm bộ lọc theo thời gian (ví dụ: chỉ lấy ticket trong 24h qua) nếu lượng ticket quá lớn.
- **Format Ticket Data (Code Node):** Node này dùng để làm sạch dữ liệu thô từ Zendesk, tính toán tuổi của ticket, phân loại mức độ ưu tiên và xử lý giá trị trống trước khi chuyển sang bước tiếp theo.
- **Check Negative Feedback (If Node):** Thiết lập logic lọc các ticket có điểm đánh giá sự hài lòng là tiêu cực (`satisfaction_score = "bad"`). Các sếp có thể mở rộng logic này để lọc thêm các ticket VIP hoặc ticket quá hạn chưa xử lý.
- **Log Churn Risk to Sheet (Google Sheets Node):** Kết nối tài khoản Google Sheets (`googleSheetsOAuth2Api`), chọn file Google Sheet quản lý và chỉ định bảng tính để hệ thống tự động append (`operation: append`) thông tin chi tiết ticket rủi ro, thời gian và thông tin khách hàng.
- **Send Slack Alert (Slack Node):** Kết nối tài khoản Slack (`slackApi`), trỏ tới kênh (channel) chuyên trách của đội CSKH. Tùy chỉnh nội dung tin nhắn đính kèm ID ticket, link trực tiếp, mức độ đánh giá và mô tả để đội ngũ dễ dàng bấm vào xử lý ngay.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thử với dữ liệu mẫu xem luồng chạy có mượt mà hay không.
- Sau khi test thành công, bật nút **Active** ở góc trên cùng bên phải để hệ thống tự động hóa chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp AI phân tích cảm xúc:** Thay vì chỉ dựa vào `satisfaction_score`, các sếp có thể chèn thêm một AI Agent node để đọc nội dung đoạn chat/email trong ticket và đánh giá mức độ tức giận của khách hàng một cách thông minh hơn.
- **Gửi thêm cảnh báo qua Telegram/Zalo OA:** Ngoài Slack, nếu đội ngũ dùng Telegram, các sếp có thể duplicate nhánh cảnh báo để bắn tin đồng thời vào nhóm Telegram.
- **Báo cáo định kỳ hàng tuần:** Kết hợp thêm Google Sheets trigger hoặc Schedule node cuối tuần để tổng hợp số lượng churn risk trong tuần gửi bản tóm tắt cho Ban Giám Đốc.

### 📌 Kết luận
Việc giữ chân khách hàng cũ luôn tiết kiệm chi phí hơn rất nhiều so với việc đi tìm khách hàng mới. Với workflow tự động hóa giám sát rủi ro Zendesk này, đội ngũ của các sếp sẽ luôn ở thế chủ động trong việc chăm sóc và xử lý khủng hoảng khách hàng. Lên đồ và áp dụng ngay vào hệ thống thôi nào các sếp!