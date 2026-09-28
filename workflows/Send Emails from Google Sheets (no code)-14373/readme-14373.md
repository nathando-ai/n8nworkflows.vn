---
title: "🚀 Tự động hóa gửi email và theo dõi phản hồi từ Google Sheets với n8n"
description: "Hướng dẫn xây dựng hệ thống gửi email hàng loạt không cần code, tự động gửi qua Gmail và lưu vết phản hồi khách hàng trực tiếp vào Google Sheets."
slug: "tu-dong-hoa-gui-email-google-sheets-n8n"
tags: [n8n, automation, google-sheets, gmail, email-marketing]
keywords: [n8n workflow, tự động hóa gửi email, google sheets gmail n8n, email automation no code]
---

# 🚀 Tự động hóa gửi email và theo dõi phản hồi từ Google Sheets

Các sếp có đang tốn hàng giờ mỗi ngày để copy-paste thông tin từ Google Sheets vào Gmail để gửi email chăm sóc khách hàng, sau đó lại phải mỏi mắt kiểm tra xem khách có reply lại hay chưa? Công việc thủ công lặp đi lặp lại này vừa nhàm chán, vừa dễ sai sót lại tốn kém thời gian quý báu.

Với workflow n8n cực kỳ thông minh được phát triển bởi **Milan Vasarhelyi (SmoothWork)**, các sếp sẽ sở hữu ngay một hệ thống tự động hóa 100%: Tự động lấy danh sách từ Google Sheets, gửi email qua Gmail và tự động ghi nhận phản hồi của khách hàng vào bảng tính mà không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không còn phải thao tác thủ công từng email một.
- **Không bỏ sót khách hàng:** Tự động lọc các dòng có trạng thái "To send" và cập nhật thành "Sent" để tránh gửi trùng lặp.
- **Theo dõi phản hồi thông minh:** Hệ thống tự động theo dõi hộp thư Gmail, đối chiếu người gửi và lưu ngay nội dung phản hồi vào cột "Response" trên Google Sheets.
- **Hoạt động liên tục:** Vận hành mượt mà nhờ sự kết hợp hoàn hảo giữa Google Sheets và Gmail API.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Google / Google Sheets** chứa danh sách email cần gửi.
- **Tài khoản Gmail** để cấu hình gửi và nhận email.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn JSON của workflow (hoặc tải file từ nguồn gốc) và dán trực tiếp vào n8n Editor của mình. Workflow bao gồm 7 nodes chính được chia làm 2 luồng hoạt động song song rõ rệt.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống hoạt động trơn tru, các sếp cần chú ý cấu hình các node sau:

- **Google Sheets Nodes (`Get Pending Emails from Sheet`, `Mark Email as Sent`, `Find Original Email Row`, `Save Email Response`):**
  - Kết nối tài khoản bằng **Google Sheets OAuth2 API**.
  - Thay thế **Document ID** và **Sheet Name** bằng bảng tính quản lý email của riêng các sếp.
  - Đảm bảo Google Sheet của các sếp có các cột: `To`, `Subject`, `Message`, `Status`, và `Response`.
  - Bộ lọc mặc định tìm kiếm trạng thái `Status = "To send"`. Các sếp có thể thay đổi nhãn trạng thái này tùy theo ý thích.

- **Gmail Nodes (`Send Email via Gmail`, `On New Email Received`):**
  - Kết nối tài khoản bằng **Gmail OAuth2**.
  - Node `Send Email via Gmail` sẽ nhận dữ liệu từ Google Sheets để gửi đi.
  - Node `On New Email Received` hoạt động như một Trigger tự động kiểm tra hộp thư đến mỗi phút để bắt phản hồi từ khách hàng.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (`Manual Trigger - Start Email Campaign`) với một vài dòng dữ liệu mẫu để kiểm tra kết quả trên Gmail và Google Sheets.
- Sau khi test thành công, bật **Active workflow** để hệ thống tự động vận hành.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Thêm node Telegram hoặc Slack vào sau node `Save Email Response` để nhận thông báo ngay lập tức trên điện thoại mỗi khi có khách hàng reply email.
- **Độ trễ (Delay):** Thêm node Wait giữa các lần gửi email nếu danh sách của các sếp quá lớn, tránh việc bị Gmail giới hạn tốc độ gửi (Rate Limit).
- **Cá nhân hóa nội dung:** Sử dụng các biến từ Google Sheets (như tên khách hàng, công ty) để chèn vào tiêu đề và nội dung email thông qua biểu thức n8n (`{{ $json.To }}`).

### 📌 Kết luận
Workflow "Send Emails from Google Sheets" là một công cụ cực kỳ gọn nhẹ nhưng mang lại hiệu quả cao cho các chiến dịch outreach, CSKH hoặc Sales. Hãy thiết lập ngay hôm nay để giải phóng bản thân khỏi những tác vụ thủ công và tập trung vào việc chốt đơn!