---
title: "🚀 Tự động hóa quy trình quản lý yêu cầu thay đổi kỹ thuật (ECR) qua Webhook và Slack"
description: "Hướng dẫn xây dựng workflow n8n tự động tiếp nhận yêu cầu thay đổi thiết kế, phân loại mức độ ảnh hưởng và gửi phê duyệt qua Slack một cách chuyên nghiệp."
slug: "quan-ly-yeu-cau-thay-doi-ky-thuat-ecr-qua-slack"
tags: [n8n, automation, slack, webhook, engineering-change-request, no-code]
keywords: [n8n workflow, tự động hóa ecr, quản lý thay đổi kỹ thuật, webhook slack approvals, n8n viet nam]
---

# 🚀 Tự động hóa quy trình quản lý yêu cầu thay đổi kỹ thuật (ECR) qua Webhook và Slack

Trong các dự án kỹ thuật, cơ khí và sản xuất, việc quản lý các Yêu cầu Thay đổi Kỹ thuật (Engineering Change Request - ECR) đóng vai trò sống còn để đảm bảo chất lượng sản phẩm. Tuy nhiên, quy trình thủ công thường gặp nhiều rắc rối: thông báo bị thất lạc qua email, cấp quản lý chậm trễ phê duyệt do thiếu thông tin, và khó theo dõi trạng thái. 

Workflow n8n này sẽ giải quyết triệt để các vấn đề trên bằng cách tự động hóa 100% quy trình: Nhận dữ liệu qua Webhook, tự động phân loại mức độ ảnh hưởng, gửi thông báo phê duyệt tương tác qua Slack và ghi nhận kết quả cuối cùng mà không cần dùng đến các phần mềm PLM đắt đỏ hay viết code phức tạp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Tiếp nhận yêu cầu ECR ngay lập tức từ hệ thống ngoài thông qua Webhook.
- **Phân loại thông minh:** Tự động phân tích mức độ ảnh hưởng (High, Medium, Low) dựa trên từ khóa trong nội dung thay đổi.
- **Tương tác mượt mà:** Gửi yêu cầu phê duyệt trực tiếp đến kênh Slack, kết hợp cơ chế Human-in-the-loop (tạm dừng chờ duyệt và tiếp tục chạy tự động).
- **Minh bạch và rõ ràng:** Thông báo kết quả Phê duyệt (Approval) hoặc Từ chối (Rejection) ngay lập tức tới đội ngũ liên quan.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt và hoạt động (Self-hosted hoặc n8n Cloud).
- **Slack Workspace:** Tài khoản có quyền kết nối ứng dụng (OAuth2) và một kênh (Channel) chuyên dụng để nhận thông báo phê duyệt.
- **Hệ thống nguồn (Upstream):** Google Forms, Typeform, hoặc công cụ nội bộ có khả năng bắn HTTP POST Webhook.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sao chép mã JSON của workflow này từ kho lưu trữ n8n (Link gốc: [n8n Workflow #13932](https://n8n.io/workflows/13932)) và dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru với hệ thống của công ty, các sếp cần cấu hình các node quan trọng sau:

- **Webhook - Receive Drawing Change Request:** Copy URL dạng Production của node này và cấu hình nó vào hệ thống gửi yêu cầu (Google Forms, ứng dụng nội bộ...) để bắt đầu nhận dữ liệu POST chứa `drawing_no` và `change_reason`.
- **IF - Validate Required Fields & Switch - Determine Approver by Impact:** Kiểm tra tính hợp lệ của dữ liệu đầu vào. Tùy chỉnh các từ khóa trong node *Switch* (ví dụ: "Dimension", "Material") cho phù hợp với chính sách đánh giá mức độ rủi ro thay đổi thiết kế của công ty.
- **Các node Set (Set Low, Set Medium, Set High...):** Thiết lập các metadata cần thiết cho ECR dựa trên kết quả phân loại.
- **Notify Slack (Approval Request), Notify Approval (Slack), Notify Rejection (Slack):** Kết nối tài khoản Slack của các sếp (`slackOAuth2Api`) và chọn đúng kênh (Channel) để bot gửi thông điệp yêu cầu phê duyệt và kết quả.
- **Wait (Form) & Check Decision:** Quản lý luồng chờ phản hồi từ người quản lý thông qua form tạm dừng của n8n, sau đó rẽ nhánh dựa trên quyết định Duyệt hay Từ chối.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và gửi một request mẫu đến Webhook URL để kiểm tra luồng chạy (Test run).
- Sau khi kiểm tra toàn bộ dữ liệu đi qua các nhánh Slack và Webhook trả về chính xác, gạt công tắc **Active** để đưa workflow vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu trữ dữ liệu:** Tích hợp thêm node *Google Sheets* hoặc *Airtable* ngay sau bước tạo Metadata để lưu lại lịch sử mọi yêu cầu ECR phục vụ cho việc kiểm toán sau này.
- **Mở rộng kênh thông báo:** Kết hợp thêm node *Telegram Bot* hoặc *Microsoft Teams* để đa dạng hóa kênh nhận tin cho các cấp quản lý không dùng Slack.
- **Báo cáo định kỳ:** Thêm một nhánh cron (Schedule Trigger) chạy vào cuối tuần để tổng hợp số lượng ECR đã duyệt và từ chối gửi báo cáo về cho ban giám đốc.

### 📌 Kết luận
Việc tự động hóa quy trình quản lý yêu cầu thay đổi kỹ thuật (ECR) không chỉ giúp tiết kiệm hàng giờ đồng hồ mỗi tuần mà còn loại bỏ các điểm nghẽn trong khâu phê duyệt. Hãy cài đặt ngay workflow này trên hệ thống n8n của các sếp để tối ưu hóa quy trình làm việc kỹ thuật ngay hôm nay!