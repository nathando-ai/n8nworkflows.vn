---
title: "🚀 Tự động hóa báo cáo chiến dịch Brevo hàng tuần với Groq AI và Google Sheets"
description: "Xây dựng hệ thống tự động lấy dữ liệu chiến dịch từ Brevo, phân tích xu hướng 7 ngày qua bằng Groq AI (Llama 3.3) và gửi báo cáo HTML chuyên nghiệp qua Gmail."
slug: "tu-dong-hoa-bao-cao-brevo-hang-tuan-groq-ai-google-sheets"
tags: [n8n, automation, groq, brevo, google-sheets, ai-summarization]
keywords: [n8n workflow, brevo reporting, groq ai, google sheets automation, tu dong hoa marketing]
---

# 🚀 Tự động hóa báo cáo chiến dịch Brevo hàng tuần với Groq AI và Google Sheets

Các sếp làm marketing chắc hẳn đều thấm thía cảnh tượng mỗi đầu tuần: Hì hục đăng nhập vào Brevo, xuất file Excel, lọc số liệu Open rate, Click rate, Bounce rate, rồi viết báo cáo gửi sếp lớn. Công việc lặp đi lặp lại này vừa tốn thời gian, vừa dễ xảy ra sai sót thủ công.

Đừng để những việc tay chân làm chậm tốc độ tăng trưởng của doanh nghiệp! Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực xịn sò được thiết kế bởi chuyên gia Avkash Kakdiya. Workflow này sẽ tự động hóa toàn bộ quy trình: lấy dữ liệu từ Brevo, lưu trữ lịch sử vào Google Sheets, sử dụng **Groq AI (Llama 3.3)** để phân tích xu hướng và gửi một bản báo cáo HTML cực kỳ chuyên nghiệp qua **Gmail** vào mỗi tuần.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian:** Không còn phải thủ công copy-paste số liệu hay tính toán tỷ lệ mở/click mỗi tuần.
- **Lưu trữ dữ liệu dài hạn:** Tự động ghi nhận toàn bộ thông số chiến dịch vào Google Sheets để phục vụ việc tracking theo thời gian.
- **Góc nhìn thông minh từ AI:** Groq AI (Llama 3.3 70B) sẽ tự động phân tích và tóm tắt xu hướng hoạt động trong 7 ngày qua thành những nhận định cốt lõi.
- **Báo cáo chuyên nghiệp:** Gửi trực tiếp bản báo cáo định dạng HTML đẹp mắt đến hòm thư của ban lãnh đạo hoặc team marketing đúng giờ hẹn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và thông tin sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Brevo Account**: Lấy API Key để kết nối với node `HTTP Request`.
- **Google Sheets**: Tạo sẵn một Google Sheet với các cột tương ứng (Ví dụ: Campaign Name, Open Rate, Click Rate, Bounce Rate...).
- **Groq API Key**: Để sử dụng mô hình `llama-3.3-70b-versatile` tại node `Groq Chat Model`.
- **Gmail Account**: Kết nối credentials để gửi email báo cáo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow (hoặc tải file JSON từ nguồn gốc) và dán trực tiếp vào n8n Editor của mình. Workflow bao gồm **12 nodes** được bố trí mạch lạc qua 5 bước chính:

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Schedule Trigger**: Thiết lập lịch chạy định kỳ (Ví dụ: Sứ giả tự động chạy vào Thứ Hai hàng tuần lúc 08:00 sáng).
- **HTTP Request**: Cấu hình chuẩn xác Brevo API Key và endpoint lấy danh sách chiến dịch đã gửi ("Sent" campaigns).
- **Data Cleaning1 & Filtered 7 days data (Code nodes)**: Kiểm tra các key trả về từ Brevo để đảm bảo code JavaScript map đúng với các trường dữ liệu (Campaign Name, Open, Click, Bounce).
- **Append row in sheet & Get row(s) in sheet (Google Sheets)**: Chọn đúng file Google Sheet và Sheet Name đã chuẩn bị từ trước.
- **Groq Chat Model & AI Agent**: Chọn model `llama-3.3-70b-versatile` và cấu hình Prompt yêu cầu AI tóm tắt ngắn gọn các số liệu trong 7 ngày qua thành dạng bảng Markdown kèm nhận định súc tích.
- **Send a message (Gmail)**: Điền email người nhận (Stakeholders) và đảm bảo nội dung email nhận HTML template từ node phía trước.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** chạy thử thủ công để kiểm tra luồng dữ liệu từ Brevo -> Google Sheets -> Groq AI -> Gmail có hoạt động trơn tru hay không.
- Nếu mọi thứ xanh mướt, gạt công tắc sang **Active** để hệ thống tự động cày cuốc thay cho các sếp.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo**: Thêm node Slack hoặc Telegram ngay sau bước AI Agent để team nhận được thông báo nhanh chóng trên nhóm chat công việc.
- **Cảnh báo thông minh (Alerts)**: Tùy chỉnh đoạn code HTML để tự động tô đỏ hoặc gửi cảnh báo khẩn cấp nếu tỷ lệ Bounce Rate vượt ngưỡng 2% (0.02).
- **Báo cáo tháng**: Nhân bản workflow này, điều chỉnh node Filter thành 30 ngày để tạo báo cáo tổng kết hiệu suất mỗi tháng một lần.

### 📌 Kết luận
Tự động hóa báo cáo email marketing chưa bao giờ dễ dàng đến thế với sức mạnh kết hợp giữa n8n, Brevo, Google Sheets và Groq AI. Hãy cài đặt ngay hôm nay để giải phóng bản thân khỏi các báo cáo thủ công và tập trung vào các chiến lược tăng trưởng đột phá!