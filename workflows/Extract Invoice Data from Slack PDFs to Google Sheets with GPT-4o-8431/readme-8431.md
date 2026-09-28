---
title: "🚀 Tự động trích xuất hóa đơn từ Slack PDF vào Google Sheets bằng GPT-4o"
description: "Hướng dẫn xây dựng workflow n8n tự động bắt file PDF hóa đơn trên Slack, dùng AI GPT-4o phân tích dữ liệu và lưu thẳng vào Google Sheets một cách chính xác."
slug: "tu-dong-trich-xuat-hoa-don-tu-slack-vao-google-sheets-gpt-4o"
tags: [n8n, automation, no-code, openai, google-sheets, slack, ai]
keywords: [n8n workflow, trích xuất hóa đơn tự động, gpt-4o pdf extraction, slack to google sheets, n8n ai agent]
---

# 🚀 Tự động trích xuất hóa đơn từ Slack PDF vào Google Sheets bằng GPT-4o

Việc quản lý hóa đơn thủ công từ các file PDF gửi qua nhóm chat thường tốn rất nhiều thời gian, dễ bỏ sót hoặc nhập sai số liệu tài chính. Khi đội ngũ gửi file hóa đơn lên Slack, kế toán hoặc người quản lý thường phải mở xem, đọc từng con số và gõ lại vào Google Sheets. 

Workflow n8n này sẽ giải quyết triệt để nỗi đau đó bằng cách tự động hóa 100%: bắt file PDF trên Slack, sử dụng sức mạnh của AI (GPT-4o) để bóc tách thông tin chuẩn xác (tên công ty, số hóa đơn, tổng tiền, hạn thanh toán...), lưu dữ liệu vào Google Sheets và gửi thông báo xác nhận ngược lại vào Slack mà không cần một thao tác thủ công nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [An tâm chạy ngầm với VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Không còn cảnh copy-paste dữ liệu từ hóa đơn PDF sang Excel/Google Sheets.
- **Độ chính xác cao:** Ứng dụng GPT-4o giúp đọc hiểu cấu trúc hóa đơn đa dạng, trích xuất đúng các trường thông tin cốt lõi.
- **Lưu trữ khoa học:** Mọi dữ liệu tài chính được tổng hợp gọn gàng vào Google Sheets để dễ dàng làm báo cáo.
- **Phản hồi tức thì:** Bot Slack sẽ gửi tin nhắn thông báo ngay khi hóa đơn được xử lý và lưu thành công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động.
- Tài khoản **Slack** có quyền đọc file tải lên và gửi tin nhắn (Bot Token/OAuth).
- Tài khoản **Google** có quyền truy cập Google Drive và Google Sheets để tạo/ghi dữ liệu vào file tổng hợp.
- **OpenAI API Key** (có hạn mức sử dụng model `gpt-4o`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này hoặc tải file từ nguồn gốc, sau đó vào giao diện n8n chọn **Add workflow** -> **Import from File / Clipboard** để dán vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình chính xác các node sau:
- **Receive invoice pdf (`slackTrigger`):** Kết nối với tài khoản Slack của tổ chức, chọn channel chỉ định (ví dụ: `#invoices` hoặc `#ketoan`) để lắng nghe sự kiện có file PDF được gửi lên.
- **Fetch the pdf (`httpRequest`):** Đảm bảo đã chọn đúng credential Slack để n8n có quyền tải nội dung file PDF về xử lý.
- **AI model (`lmChatOpenAi`):** Chọn model `gpt-4o` và điền OpenAI API Key của các sếp vào phần credentials.
- **Structure Output (`outputParserStructured`):** Kiểm tra lại định dạng dữ liệu đầu ra mà các sếp muốn AI trả về (như tên nhà cung cấp, mã hóa đơn, tổng tiền, ngày hóa đơn, hạn thanh toán...).
- **Append row in sheet (`googleSheets`):** Kết nối tài khoản Google Sheets OAuth2, chọn file Google Spreadsheet và Sheet Name đích mà các sếp muốn lưu dữ liệu hóa đơn. Map các trường dữ liệu từ AI trả về vào các cột tương ứng trong sheet.
- **Send a message (`slack`):** Cấu hình gửi tin nhắn xác nhận về lại kênh Slack với các thông tin tóm tắt hóa đơn vừa xử lý xong.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và thử upload một file PDF hóa đơn mẫu lên kênh Slack đã chọn để test xem dữ liệu có bay vào Google Sheets chuẩn chỉnh chưa.
- Nếu mọi thứ mượt mà, gạt công tắc sang **Active** để workflow chính thức trực chiến 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm thông báo khẩn:** Nếu hóa đơn có tổng tiền vượt quá một hạn mức nhất định (ví dụ: > 10 triệu VND), cấu hình thêm điều kiện để gửi ping riêng đến sếp lớn qua Telegram hoặc Slack Direct Message.
- **Lưu trữ file PDF:** Kết hợp thêm node Google Drive để lưu bản scan/PDF hóa đơn vào một thư mục năm/tháng nhằm phục vụ việc kiểm toán sau này.
- **Báo cáo định kỳ:** Tạo thêm một workflow phụ để tổng hợp dữ liệu từ Google Sheets và gửi báo cáo chi tiêu tự động vào mỗi thứ Sáu hàng tuần.

### 📌 Kết luận
Với workflow n8n kết hợp GPT-4o này, việc xử lý hóa đơn không còn là cơn ác mộng tốn thời gian của bộ phận kế toán hay vận hành. Hãy cài đặt ngay hôm nay để tối ưu hóa năng suất cho doanh nghiệp của các sếp!