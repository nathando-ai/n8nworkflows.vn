---
title: "🚀 Tự động hóa SecOps: Tích hợp Qualys và Slack Shortcut Bot với n8n"
description: "Xây dựng bot Slack tương tác trực tiếp với Qualys để kích hoạt quét lỗ hổng bảo mật và tạo báo cáo tự động mà không cần rời khỏi Slack."
slug: "tu-dong-hoa-secops-qualys-slack-shortcut-bot-n8n"
tags: [n8n, automation, no-code, security, secops, slack, qualys]
keywords: [n8n workflow, tự động hóa secops, qualys slack bot, quét lỗ hổng bảo mật n8n, slack shortcut bot]
---

# 🚀 Tự động hóa SecOps: Tích hợp Qualys và Slack Shortcut Bot với n8n

Các kỹ sư bảo mật và quản trị hệ thống thường xuyên đối mặt với việc phải chuyển đổi qua lại giữa nhiều nền tảng để kích hoạt quét lỗ hổng (vulnerability scan) và tạo báo cáo bảo mật. Việc này không chỉ tốn thời gian mà còn làm chậm trễ quá trình phản ứng với các sự cố.

Được thiết kế bởi chuyên gia Angel Menendez, workflow n8n này mang đến giải pháp **Qualys Slack Shortcut Bot** tự động hóa toàn diện. Giờ đây, các sếp có thể kích hoạt quét bảo mật, cấu hình tham số qua Modal trên Slack và nhận báo cáo PDF chi tiết ngay lập tức ngay trong kênh Slack của đội ngũ.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tương tác trực tiếp:** Quản lý bảo mật ngay trong Slack thông qua các Shortcut, Modal giao diện trực quan và thân thiện trên thiết bị di động lẫn máy tính.
- **Tự động hóa toàn trình:** Tự động kết nối với Qualys để thực thi quét lỗ hổng và tổng hợp báo cáo dạng PDF gửi thẳng vào kênh Slack chỉ định.
- **Phản hồi tức thì:** Cập nhật trạng thái thời gian thực cho người dùng, đóng các popup modal tự động sau khi submit thành công.
- **Tiết kiệm thời gian:** Loại bỏ thao tác thủ công trên giao diện quản trị Qualys phức tạp, giúp đội ngũ SecOps tập trung vào việc xử lý rủi ro.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Slack Workspace:** Quyền cấu hình Slack App, tạo Event Subscriptions và kết nối Bot Token.
- **Qualys Account:** Thông tin API/Integration để thực hiện quét và tạo báo cáo (thông qua các sub-workflow liên quan).
- **Credentials trong n8n:** Slack API Credentials (`slackApi`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc sao chép toàn bộ mã JSON từ kho lưu trữ n8n.
- Mở giao diện n8n Editor của các sếp, chọn **Add workflow** -> **Import from File / Paste JSON**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node `Webhook`**: Cấu hình đường dẫn Webhook để nhận sự kiện từ Slack API (Event Subscriptions). Tham khảo cấu hình Slack Events API [tại đây](https://api.slack.com/apis/connections/events-api).
- **Các node HTTP Request (`Scan Report Task Modal`, `Vuln Scan Modal`)**: Chọn và cấu hình chính xác `slackApi` credentials để n8n có thể tương tác với Slack UI (mở modal, gửi tin nhắn).
- **Node `Route Message` & `Route Submission` (Switch)**: Đảm bảo các điều kiện định tuyến khớp với `callback_id` và tiêu đề modal của Slack mà các sếp thiết lập.
- **Các sub-workflow (`Qualys Create Report`, `Qualys Start Vulnerability Scan`)**: Nhớ cập nhật lại ID kênh Slack đích (Slack Channels) trong các node thuộc sub-workflow để bot gửi kết quả đúng nơi quy định.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (Test workflow) bằng cách kích hoạt lệnh trên Slack để kiểm tra việc mở modal, xử lý dữ liệu qua các node `Parse Webhook` và `Set` (Required Report/Scan Variables).
- Sau khi kiểm tra mọi thứ hoạt động trơn tru, bật công tắc **Active** để đưa workflow vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm kênh thông báo:** Kết hợp thêm node Telegram hoặc Microsoft Teams để cảnh báo song song khi có kết quả quét quan trọng.
- **Lưu trữ lịch sử:** Thêm node Google Sheets hoặc Airtable để lưu lại log mỗi khi có người dùng trigger quét bảo mật.
- **Báo cáo định kỳ:** Sử dụng thêm Schedule Trigger để tự động tạo và gửi báo cáo tóm tắt hàng tuần vào kênh Slack bảo mật chung.

### 📌 Kết luận
Workflow **Qualys Slack Shortcut Bot** là mảnh ghép hoàn hảo giúp tối ưu hóa quy trình SecOps, đưa các công cụ bảo mật phức tạp đến gần hơn với không gian làm việc hàng ngày của đội ngũ qua Slack. Hãy cài đặt ngay để nâng tầm tự động hóa bảo mật cho tổ chức của các sếp!