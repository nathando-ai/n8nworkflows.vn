---
title: "🚀 Xây dựng Hệ thống Phê duyệt & Gửi dữ liệu tương tác qua Slack với n8n Webhooks"
description: "Tự động hóa quy trình phê duyệt và thu thập dữ liệu từ Slack trực tiếp vào n8n qua hệ thống Webhook thông minh, giúp tiết kiệm thời gian và tối ưu hóa vận hành."
slug: "he-thong-phe-duyet-va-gui-du-lieu-slack-voi-n8n"
tags: [n8n, automation, no-code, slack, webhook, approval-workflow]
keywords: [n8n workflow, tự động hóa slack, phê duyệt slack tự động, n8n webhook, slack integration]
---

# 🚀 Xây dựng Hệ thống Phê duyệt & Gửi dữ liệu tương tác qua Slack với n8n Webhooks

Các sếp có bao giờ cảm thấy mệt mỏi khi phải xử lý thủ công các yêu cầu phê duyệt từ nhân viên, thu thập dữ liệu qua lại giữa các phòng ban rồi mới bấm nút đồng ý? Việc quản lý rời rạc này không chỉ làm chậm tiến độ công việc mà còn dễ xảy ra sai sót, quên duyệt hoặc thất lạc thông tin.

Giải pháp là đây! Workflow **Interactive Slack Approval & Data Submission System with Webhooks** do tác giả *Niranjan G* thiết kế sẽ giúp các sếp tự động hóa hoàn toàn quy trình nhận dữ liệu, gửi thông báo tương tác và xử lý hành động phê duyệt trực tiếp ngay trên Slack. Không cần code phức tạp, tích hợp mượt mà và chạy 24/7!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và nhận webhook real-time từ Slack, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100% quy trình:** Nhận dữ liệu đầu vào và gửi yêu cầu phê duyệt đến kênh Slack ngay lập tức.
- **Tương tác trực tiếp:** Người quản lý có thể bấm nút duyệt (Approve/Reject) ngay trên giao diện Slack mà không cần truy cập vào hệ thống khác.
- **Phản hồi tức thì:** Hệ thống tự động gửi thông báo xác nhận (Acknowledgment) cho cả người gửi yêu cầu và người phê duyệt.
- **Bảo mật cao:** Hỗ trợ xác thực Basic Auth bảo vệ các endpoint webhook khỏi truy cập trái phép.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn:
- **Tài khoản n8n:** (Self-hosted hoặc n8n Cloud).
- **Slack Workspace:** Quyền cấu hình Slack App / Bot để thiết lập Webhook và Slash Commands.
- **Credentials cần có:** 
  - `httpBasicAuth` (Dùng để bảo mật các Webhook nodes).
  - `slackApi` (Token kết nối với Slack Bot để gửi tin nhắn và tương tác).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Copy mã JSON của workflow hoặc import trực tiếp file JSON vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 5 nodes chính xử lý hai luồng nhiệm vụ (Nhận dữ liệu & Xử lý nút bấm):

- **n8n Data Webhook (`webhook`):** 
  - Đóng vai trò nhận dữ liệu gửi vào hệ thống. 
  - *Cấu hình:* Thiết lập đường dẫn `path` (`874768ff-6631-42a8-8c49-25b63ead3fec`), HTTP Method là `POST` và cấu hình `httpBasicAuth` để bảo mật.
- **Slack - Data Acknowledgment (`slack`):**
  - Nhận dữ liệu từ webhook trên và gửi thông báo xác nhận/yêu cầu phê duyệt vào kênh Slack chỉ định.
  - *Cấu hình:* Chọn `slackApi` credentials, điền Channel ID nhận thông báo.
- **n8n Button Webhook (`webhook`):**
  - Lắng nghe sự kiện khi người dùng bấm nút tương tác trên Slack (ví dụ: nút Duyệt/Từ chối).
  - *Cấu hình:* Thiết lập `path` (`fa872cfc-abe3-481d-ab7c-74f78d83a070`), HTTP Method là `POST` và gắn `httpBasicAuth`.
- **Process Button Action (`function`):**
  - Xử lý logic dữ liệu trả về từ hành động bấm nút của người dùng trên Slack (chuyển đổi trạng thái dữ liệu).
- **Slack - Button Acknowledgment (`slack`):**
  - Gửi tin nhắn cập nhật trạng thái cuối cùng (Đã duyệt / Đã từ chối) về lại Slack để các bên cùng nắm thông tin.
  - *Cấu hình:* Chọn `slackApi` credentials và chọn channel tương ứng.

#### 3. Kích hoạt ⚡️
- Thực hiện `Test step` hoặc `Execute Workflow` để kiểm tra dữ liệu mẫu bắn vào Webhook URL.
- Sau khi test thành công, gạt công tắc sang **Active** để đưa workflow vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống hoàn thiện hơn, các sếp có thể mở rộng workflow này bằng cách:
- **Lưu trữ dữ liệu:** Kết nối thêm node Google Sheets hoặc Airtable để lưu lại lịch sử các yêu cầu và kết quả phê duyệt.
- **Định tuyến thông minh:** Sử dụng thêm node `If` hoặc `Switch` để phân loại yêu cầu gửi đến các kênh Slack của từng phòng ban tương ứng.
- **Gửi Email tự động:** Kết hợp gửi thông báo qua Gmail/SMTP cho người yêu cầu ngay sau khi có kết quả phê duyệt từ Slack.

### 📌 Kết luận
Workflow tích hợp Slack và n8n Webhook này là một "vũ khí" cực kỳ lợi hại giúp doanh nghiệp chuẩn hóa quy trình ra quyết định, tiết kiệm hàng giờ thao tác thủ công mỗi tuần. Hãy cài đặt ngay hôm nay để tối ưu hóa đội ngũ của các sếp nhé!