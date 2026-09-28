---
title: "🚀 Tự động giám sát hạn SSL Certificate và cảnh báo qua Slack với n8n"
description: "Hướng dẫn cài đặt workflow n8n giúp kiểm tra hạn sử dụng chứng chỉ SSL tự động từ Google Sheets, cập nhật trạng thái và gửi thông báo cảnh báo qua Slack."
slug: "giam-sat-ssl-certificate-tu-dong-voi-google-sheets-va-slack"
tags: [n8n, automation, secops, ssl-checker, google-sheets, slack]
keywords: [n8n workflow, giám sát ssl, kiểm tra hạn ssl, tự động hóa secops, cảnh báo slack ssl]
keywords: [n8n workflow, giám sát ssl, kiểm tra hạn ssl, tự động hóa secops, cảnh báo slack ssl]
---

# 🚀 Tự động giám sát hạn SSL Certificate và cảnh báo qua Slack với n8n

Việc để chứng chỉ SSL (SSL Certificate) hết hạn bất ngờ là một cơn ác mộng đối với đội ngũ vận hành website và hệ thống IT. Nó không chỉ làm gián đoạn trải nghiệm người dùng, mất uy tín doanh nghiệp mà còn ảnh hưởng nghiêm trọng đến SEO. Kiểm tra thủ công từng domain trong một danh sách dài vừa tốn thời gian, vừa dễ bỏ sót.

Giải pháp? Workflow n8n tự động hóa 100% giúp các sếp gom toàn bộ danh sách domain vào Google Sheets, hệ thống sẽ tự động quét hạn SSL định kỳ, cập nhật kết quả và chủ động bắn cảnh báo qua Slack trước khi quá muộn!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hoàn toàn**: Không cần ai phải nhớ ngày hết hạn hay kiểm tra thủ công hàng tuần.
- **Cảnh báo sớm**: Phát hiện và thông báo qua Slack ngay khi SSL sắp đến hạn ngưỡng cấu hình (ví dụ: dưới 30 ngày).
- **Đồng bộ tập trung**: Quản lý toàn bộ danh sách domain và trạng thái SSL trực tiếp trên Google Sheets một cách trực quan.
- **Hoạt động 24/7**: Lên lịch chạy tự động ngầm, đảm bảo hệ thống luôn trong tầm kiểm soát an bảo mật (SecOps).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Self-hosted hoặc Cloud).
- Google Sheets chứa danh sách các domain cần kiểm tra.
- Slack Workspace và quyền tạo/gửi tin nhắn qua Webhook/Bot.
- Node mở rộng `@custom-js/n8n-nodes-pdf-toolkit.sslChecker` để thực hiện việc kiểm tra chứng chỉ SSL.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn JSON của workflow hoặc import file trực tiếp vào n8n Editor để bắt đầu.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 6 nodes chính, các sếp cần chú ý cấu hình kỹ các điểm sau:

- **Schedule Trigger**: Thiết lập lịch chạy tự động (ví dụ: Chạy mỗi ngày một lần vào 8 giờ sáng).
- **Get row(s) in sheet (Google Sheets)**: 
  - Kết nối tài khoản `googleSheetsOAuth2Api`.
  - Chọn đúng file Google Sheets và Sheet Name chứa danh sách các URL/domain cần kiểm tra.
- **SSL Checker (`@custom-js/n8n-nodes-pdf-toolkit.sslChecker`)**:
  - Nhập thông tin credentials `customJsApi` (nếu có yêu cầu).
  - Trỏ biến domain lấy từ Google Sheets vào node này để hệ thống thực hiện quét hạn SSL.
- **Check Days Left Threshold (If Node)**: Cấu hình điều kiện lọc số ngày còn lại (ví dụ: `Days Left < 30`) để tách nhánh domain nào cần cảnh báo và domain nào vẫn an toàn.
- **Update row in sheet (Google Sheets)**: Cập nhật lại ngày hết hạn và trạng thái SSL mới nhất vừa quét được vào đúng dòng tương ứng trong Google Sheets.
- **Send a message (Slack)**: 
  - Kết nối tài khoản `slackApi`.
  - Chọn Channel nhận thông báo và soạn nội dung cảnh báo kèm tên domain, số ngày còn lại trước khi SSL hết hạn.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** chạy thủ công lần đầu để test xem dữ liệu từ Google Sheets đổ về và bắn tin nhắn Slack có chuẩn xác hay không.
- Sau khi test xanh mướt, bật công tắc **Active** để workflow tự động chạy ngầm theo lịch đã định.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa kênh thông báo**: Ngoài Slack, các sếp có thể gắn thêm node Telegram hoặc gửi Email cảnh báo cho đội ngũ kỹ thuật.
- **Phân loại mức độ ưu cảnh báo**: Tạo nhiều nhánh `If` khác nhau (Ví dụ: Dưới 7 ngày cảnh báo mức độ Khẩn cấp - Urgent, dưới 30 ngày cảnh báo mức độ Cảnh báo - Warning).
- **Log lịch sử**: Lưu lại lịch sử kiểm tra SSL vào một sheet riêng để phục vụ việc kiểm tra và báo cáo bảo mật hàng tháng.

### 📌 Kết luận
Với một workflow n8n cực kỳ gọn nhẹ gồm 6 nodes này, các sếp đã có thể tự động hóa hoàn toàn bài toán giám sát chứng chỉ SSL, loại bỏ hoàn toàn rủi ro sập web do quên gia hạn. Triển khai ngay thôi nào!