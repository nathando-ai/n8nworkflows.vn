---
title: "🚀 Tự động hóa quy trình phê duyệt yêu cầu chuyên nghiệp với SendGrid và Baserow trên n8n"
description: "Hướng dẫn xây dựng hệ thống quản lý và phê duyệt yêu cầu tự động từ A-Z bằng n8n, tích hợp Baserow để lưu trữ dữ liệu và SendGrid để gửi email thông báo, chờ phản hồi (Wait node) thông minh."
slug: "tu-dong-hoa-quy-trinh-phe-duyet-sendgrid-baserow-n8n"
tags: [n8n, automation, no-code, baserow, sendgrid, approval-workflow]
keywords: [n8n workflow, tự động hóa quy trình phê duyệt, baserow n8n, sendgrid email, wait node n8n]
---

# 🚀 Tự động hóa quy trình phê duyệt yêu cầu chuyên nghiệp với SendGrid và Baserow

Trong các doanh nghiệp, quy trình phê duyệt (nghỉ phép, mua sắm, tài chính,...) thường bị chậm trễ do xử lý thủ công qua lại bằng email hoặc chat. Việc này dễ dẫn đến thất lạc thông tin, quên duyệt và khó theo dõi trạng thái lịch sử. 

Bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n tự động hóa toàn bộ vòng đời phê duyệt: từ lúc tiếp nhận yêu cầu, kiểm tra tính hợp lệ, định tuyến người duyệt, gửi email thông minh có kèm link phê duyệt nhanh, cho đến việc tự động cập nhật trạng thái vào cơ sở dữ liệu Baserow. Tất cả diễn ra hoàn toàn tự động mà không cần tốn một dòng code phức tạp nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và xử lý các yêu cầu tức thì, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Loại bỏ hoàn toàn khâu giục duyệt thủ công qua lại giữa các phòng ban.
- **Xử lý thông minh với Wait Node:** Hệ thống tự động tạm dừng chờ phản hồi từ người duyệt qua một cú nhấp chuột và tự động chạy tiếp khi có quyết định.
- **Minh bạch dữ liệu:** Mọi yêu cầu và trạng thái (Pending, Approved, Rejected) được ghi nhận chính xác theo thời gian thực vào Baserow.
- **Cảnh báo lỗi tức thì:** Tự động phát hiện dữ liệu đầu vào không hợp lệ và phản hồi ngay lập tức cho người gửi.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản Baserow:** Đã tạo sẵn Database và Table quản lý yêu cầu.
- **Tài khoản SendGrid:** Đã cấu hình API Key và xác thực địa chỉ gửi email (Sender Verification).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Copy mã JSON của workflow hoặc tải file JSON từ nguồn cung cấp.
- Mở n8n Editor, chọn **Add workflow** -> **Import from File / Paste JSON** để nạp toàn bộ 16 nodes vào hệ thống.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các thông số quan trọng sau trong workflow:

- **Validate Request Data & Determine Approver (Nodes loại Code):** Kiểm tra cấu trúc dữ liệu đầu vào (`requestId`, `requesterName`, `department`, `amount`) và điều chỉnh logic phân quyền người duyệt tùy theo cơ cấu công ty.
- **Create Pending Record & Update Record Nodes (Nodes Baserow):** 
  - Chọn Credentials kết nối với Baserow.
  - Điền chính xác `Database ID` và `Table ID` của các sếp.
  - Map các trường dữ liệu tương ứng: *Request ID, Requester, Department, Amount, Status, SubmittedAt, DecisionAt*.
- **Send Invalid Input Alert, Notify Approver, Notify Requester (Nodes SendGrid):**
  - Cấu hình SendGrid API Key.
  - Điền email người gửi (Sender Email) đã được xác thực trên SendGrid.
  - Đảm bảo chèn đúng link resume của node **Wait for Approval Response** vào email gửi người duyệt để họ chỉ cần bấm nút là hệ thống tự cập nhật.
- **Wait for Approval Response (Node Wait):** Node này cực kỳ quan trọng, nó sẽ cấp một URL webhook riêng biệt để tạm dừng workflow cho đến khi người duyệt click vào liên kết chấp nhận/từ chối.

#### 3. Kích hoạt ⚡️
- Chạy thử (Test run) với dữ liệu mẫu bằng nút **Start Workflow** (`manualTrigger`).
- Kiểm tra các nhánh dữ liệu xem email đã gửi đi và Baserow đã tạo bản ghi `Pending` chưa.
- Bật công tắc **Active** để workflow chính thức hoạt động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống phê duyệt trở nên tối tân hơn, các sếp có thể mở rộng workflow với các ý tưởng sau:
- **Tích hợp Chatbot:** Gửi thông báo trực tiếp qua **Slack** hoặc **Telegram** bên cạnh email để người duyệt xử lý nhanh hơn trên điện thoại.
- **Báo cáo định kỳ:** Thêm một Cron Trigger chạy mỗi thứ Sáu hàng tuần để tổng hợp các yêu cầu đã duyệt gửi vào email ban giám đốc.
- **Quản lý hạn mức:** Thêm logic phân cấp duyệt (Dưới 10 triệu trưởng phòng duyệt, trên 10 triệu sếp lớn duyệt) bằng node IF nâng cao.

### 📌 Kết luận
Với workflow n8n kết hợp SendGrid và Baserow này, các sếp đã sở hữu ngay một hệ thống quản lý phê duyệt tự động chuyên nghiệp chẳng kém gì các phần mềm Enterprise đắt tiền. Triển khai ngay hôm nay để tối ưu hóa vận hành doanh nghiệp nào!