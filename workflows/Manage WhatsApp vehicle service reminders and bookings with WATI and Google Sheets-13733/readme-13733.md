---
title: "🚀 Tự động hóa lịch hẹn và nhắc nhở bảo dưỡng xe qua WhatsApp với WATI và Google Sheets"
description: "Hướng dẫn cài đặt workflow n8n giúp tự động hóa quy trình quản lý lịch hẹn bảo dưỡng xe, gửi tin nhắn nhắc nhở qua WhatsApp bằng WATI tích hợp Google Sheets."
slug: "quan-ly-lich-hen-bao-duong-xe-whatsapp-wati-google-sheets"
tags: [n8n, automation, wati, google-sheets, whatsapp, chatbot, ai-automation]
keywords: [n8n workflow, wati whatsapp, google sheets booking, tự động hóa nhắc nhở bảo dưỡng, chatbot dịch vụ xe]
keywords: [n8n workflow, wati whatsapp, google sheets booking, tự động hóa nhắc nhở bảo dưỡng, chatbot dịch vụ xe]
---

# 🚀 Tự động hóa lịch hẹn và nhắc nhở bảo dưỡng xe qua WhatsApp với WATI và Google Sheets

Việc quản lý lịch hẹn bảo dưỡng xe và gửi tin nhắn nhắc nhở thủ công thường tốn rất nhiều thời gian, dễ xảy ra sai sót, bỏ quên khách hàng và làm giảm trải nghiệm dịch vụ. Khách hàng ngày nay mong đợi sự phản hồi nhanh chóng và chuyên nghiệp qua các kênh nhắn tin trực tuyến như WhatsApp.

Workflow n8n này được thiết kế bởi chuyên gia *Jitesh Dugar* nhằm giải quyết triệt để bài toán trên. Hệ thống sẽ tự động hóa toàn bộ quy trình tiếp nhận tin nhắn từ WATI, xử lý logic, cập nhật dữ liệu lên Google Sheets và tự động gửi thông báo nhắc nhở lịch hẹn bảo dưỡng xe cho khách hàng 100% không cần can thiệp thủ công.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 24/7:** Hệ thống tự động kích hoạt lịch trình nhắc nhở hoặc phản hồi tin nhắn khách hàng gửi tới qua WhatsApp bất kể ngày đêm.
- **Đồng bộ dữ liệu tập trung:** Mọi thông tin đặt lịch, thông tin xe và lịch sử bảo dưỡng được lưu trữ và cập nhật trực tiếp trên Google Sheets.
- **Nâng cao trải nghiệm khách hàng:** Gửi tin nhắn chăm sóc, nhắc lịch đúng giờ giúp tăng tỷ lệ khách hàng quay lại bảo dưỡng định kỳ.
- **Tiết kiệm nhân sự:** Giảm tải công việc cho đội ngũ chăm sóc khách hàng, loại bỏ hoàn toàn sai sót do ghi chép thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Hạ tầng n8n:** Đã cài đặt và truy cập được vào n8n editor.
- **Tài khoản WATI:** Cần có tài khoản WATI (WhatsApp Business API) kèm theo API Endpoint và Access Token.
- **Google Sheets:** Một trang tính (Google Sheet) được thiết kế sẵn các cột lưu thông tin khách hàng, số điện thoại, ngày hẹn bảo dưỡng và trạng thái dịch vụ.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc sao chép toàn bộ mã JSON.
- Trong giao diện n8n, chọn **Add workflow** -> Nhấp vào biểu tượng ba chấm góc trên bên phải -> Chọn **Import from File** hoặc **Import from Clipboard** và dán mã JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các node cốt lõi sau đây để workflow hoạt động mượt mà:

- **Schedule Trigger:** Cấu hình thời gian chạy định kỳ (ví dụ: chạy mỗi ngày vào lúc 8:00 sáng) để quét và gửi tin nhắn nhắc nhở bảo dưỡng xe.
- **WATI Trigger:** Lắng nghe các tin nhắn hoặc sự kiện đến từ khách hàng nhắn qua WhatsApp. Cần cấu hình Webhook URL từ n8n dán vào dashboard của WATI.
- **Google Sheets Node:** 
  - Kết nối tài khoản Google thông qua OAuth2.
  - Chọn đúng file Google Sheet và Sheet Name chứa dữ liệu đặt lịch bảo dưỡng.
  - Map các trường dữ liệu như Số điện thoại, Tên khách hàng, Ngày hẹn, Loại dịch vụ.
- **WATI Node:** Cấu hình thông tin API của WATI để gửi tin nhắn văn bản (Template Message hoặc Session Message) trực tiếp cho khách hàng qua số WhatsApp.
- **Switch Node & Code Node:** Xử lý logic phân loại yêu cầu của khách hàng (đặt lịch mới, thay đổi lịch, hoặc hủy lịch) dựa trên từ khóa tin nhắn hoặc dữ liệu thời gian.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử nghiệm với dữ liệu giả lập (Test Run) nhằm kiểm tra kết nối Google Sheets và WATI.
- Sau khi test thành công không báo lỗi, chuyển công tắc sang **Active** để hệ thống tự động vận hành 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp AI Chatbot:** Kết hợp thêm OpenAI Node để chatbot WATI có thể trả lời các câu hỏi phức tạp về chi phí phụ tùng, lịch làm việc của gara một cách thông minh.
- **Báo cáo qua Telegram/Slack:** Thêm node gửi thông báo về kênh Telegram nội bộ mỗi khi có khách hàng đặt lịch thành công để nhân viên kỹ thuật kịp thời chuẩn bị.
- **Lưu log chi tiết:** Ghi lại lịch sử gửi tin nhắn thất bại/thành công vào một tab riêng trên Google Sheets để dễ dàng theo dõi và xử lý sự cố.

### 📌 Kết luận
Việc tự động hóa quy trình quản lý lịch hẹn bảo dưỡng xe với WATI và Google Sheets không chỉ giúp doanh nghiệp tiết kiệm hàng giờ làm việc thủ công mà còn tạo ấn tượng chuyên nghiệp tuyệt đối trong mắt khách hàng. Hãy áp dụng ngay workflow này vào hệ thống của các sếp để tối ưu hóa vận hành ngay hôm nay!