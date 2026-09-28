---
title: "🚀 Tự động trích xuất biên lai chuyển tiền qua Line Chatbot và Gemini AI vào Google Sheets"
description: "Hướng dẫn xây dựng workflow n8n tích hợp Line Chatbot với Google Gemini AI để tự động đọc biên lai (pay slip), phân tích thông tin và lưu trữ trực tiếp vào Google Sheets."
slug: "trich-xuat-bien-lai-line-chatbot-gemini-google-sheets"
tags: [n8n, automation, line-bot, google-gemini, google-sheets, ai]
keywords: [n8n workflow, line chatbot ai, trích xuất biên lai gemini, google sheets automation, tự động hóa tài chính]
use_ai_translation: true
---

# 🚀 Tự động trích xuất biên lai chuyển tiền qua Line Chatbot và Gemini AI vào Google Sheets

Các doanh nghiệp nhỏ, đội ngũ bán hàng hay bộ phận kế toán thường xuyên phải đối mặt với việc kiểm tra hàng trăm hình ảnh biên lai chuyển tiền (pay slip) mỗi ngày. Việc kiểm tra thủ công, đối chiếu số tiền, thời gian và người gửi/nhận vừa tốn thời gian, dễ nhầm lẫn lại vừa gây chậm trễ trong quy trình xác nhận đơn hàng.

Giải pháp ở đây là gì? Workflow n8n này sẽ giúp các sếp tự động hóa 100% quy trình trên! Khách hàng hoặc nhân viên chỉ cần gửi ảnh biên lai qua **Line Chatbot**, AI **Google Gemini** sẽ thông minh đọc hiểu, trích xuất toàn bộ dữ liệu quan trọng và tự động lưu thẳng vào **Google Sheets**, đồng thời phản hồi kết quả ngay lập tức cho người gửi. Không cần code phức tạp, không cần dùng dịch vụ OCR đắt đỏ!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Biến Line Chatbot thành trợ lý tài chính thông minh, xử lý cả tin nhắn văn bản lẫn hình ảnh biên lai.
- **Trích xuất chính xác bằng AI**: Sử dụng sức mạnh của Google Gemini để phân tích hình ảnh biên lai và trả về dữ liệu dưới định dạng JSON chuẩn mực (Trạng thái, Người gửi, Người nhận, Ngày tháng, Số tiền).
- **Đồng bộ thời gian thực**: Tự động ghi nhận toàn bộ thông tin bóc tách được vào Google Sheets để dễ dàng kiểm toán, đối soát.
- **Hoạt động 24/7 không nghỉ**: Phản hồi người dùng ngay lập tức mà không cần sự can thiệp thủ công của con người.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI BẮT ĐẦU]
- Một tài khoản **n8n** (Cloud hoặc Self-hosted).
- **Line Developer Account** để tạo Channel và lấy Messaging API Token / Webhook.
- **Google Gemini API Key** (Google AI Studio) để cấu hình cho các node AI.
- **Google Sheets** đã chuẩn bị sẵn một file Google Sheet với các cột tương ứng (Status, From, To, Date, Amount).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ nguồn gốc hoặc tạo mới, sau đó copy toàn bộ cấu trúc JSON và dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống vận hành trơn tru, các sếp cần cấu hình chính xác các thành phần sau:

- **Line Messaging API (Webhook)**: 
  - Lấy URL webhook từ node này và dán vào phần cấu hình Webhook URL trên Line Developer Console của các sếp.
  - Cấu hình Credentials loại `httpHeaderAuth` cho các node **Line: Get Image**, **Line: Response to User**, và **Line: Text Response to User** bằng Channel Access Token của Line Bot.
- **Phân loại tin nhắn (Message Type & Message Classification)**:
  - Workflow sử dụng node `Set` và `Switch` để nhận diện xem người dùng gửi văn bản (text) hay hình ảnh biên lai (image), từ đó điều hướng luồng xử lý thông minh.
- **Google Gemini AI (Text & Image Processing)**:
  - Cấu hình Credentials `googlePalmApi` bằng Gemini API Key của các sếp cho hai node **Google Gemini for Text** và **Google Gemini for Image**.
  - Tại node **Image Message Processing** (Chain LLM), hãy sử dụng prompt yêu cầu Gemini phân tích hình ảnh biên lai và trả về định dạng JSON thuần túy gồm các trường: `Status`, `From`, `To`, `Date`, `Amount`.
- **Lưu trữ dữ liệu (Text from Slip Result)**:
  - Kết nối tài khoản Google thông qua `googleSheetsOAuth2Api`.
  - Chọn đúng file Google Sheet và Sheet Name dùng để lưu dữ liệu biên lai với thao tác `append` (thêm dòng mới).

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và gửi thử một ảnh biên lai hoặc tin nhắn văn bản qua Line Bot để kiểm tra dữ liệu trả về.
- Nếu mọi thứ hoạt động chính xác, hãy bật nút **Active** để đưa workflow vào vận hành chính thức 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm thông báo**: Nối thêm node Telegram hoặc Slack sau bước lưu Google Sheets để gửi thông báo tức thời cho quản lý mỗi khi có khách hàng chuyển khoản thành công.
- **Xử lý trùng lặp**: Thêm một bước kiểm tra (Filter/Code node) để đối chiếu mã giao dịch (nếu có) nhằm tránh việc một biên lai bị ghi nhận nhiều lần vào Google Sheets.
- **Mở rộng AI Assistant**: Tận dụng node **Window Buffer Memory** sẵn có trong workflow để cho phép bot ghi nhớ lịch sử trò chuyện, hỗ trợ khách hàng tra cứu trạng thái đơn hàng thông minh hơn.

### 📌 Kết luận
Với workflow n8n kết hợp Line Chatbot và Google Gemini AI này, việc quản lý và trích xuất biên lai chuyển tiền không còn là gánh nặng thủ công nữa. Hãy "lên đồ" ngay cho hệ thống của các sếp để tối ưu hóa vận hành và mang lại trải nghiệm tự động hóa chuyên nghiệp cho khách hàng!