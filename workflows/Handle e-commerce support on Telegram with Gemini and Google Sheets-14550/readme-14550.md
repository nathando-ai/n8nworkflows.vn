---
title: "🚀 Xây dựng Bot hỗ trợ khách hàng Thương mại điện tử trên Telegram với Google Gemini và Google Sheets"
description: "Tự động hóa hoàn toàn quy trình chăm sóc khách hàng trên Telegram: tra cứu đơn hàng, hủy đơn và tạo ticket hỗ trợ bằng AI Agent tích hợp Google Sheets."
slug: "bot-ho-tro-khach-hang-telegram-gemini-google-sheets"
tags: [n8n, automation, no-code, telegram, ai-chatbot, google-sheets, google-gemini]
keywords: [n8n workflow, telegram bot ai, chatbot thương mại điện tử, google gemini n8n, tự động hóa chăm sóc khách hàng]
keywords: [n8n workflow, telegram bot ai, chatbot thương mại điện tử, google gemini n8n, tự động hóa chăm sóc khách hàng]
---

# 🚀 Tự động hóa Chăm sóc Khách hàng Thương mại điện tử trên Telegram với AI

Các sếp đang gặp khó khăn khi số lượng tin nhắn hỏi về đơn hàng, chính sách đổi trả, hoặc yêu cầu hủy đơn trên Telegram tăng vọt mỗi ngày? Việc trả lời thủ công khiến đội ngũ quá tải, phản hồi chậm và dễ dẫn đến bỏ lỡ khách hàng tiềm năng? 

Giải pháp chính là đây: Workflow n8n tích hợp **Google Gemini AI Agent** kết hợp cùng **Google Sheets**. Bot này sẽ trực tiếp tiếp nhận tin nhắn từ Telegram, thông minh hiểu ý định của khách hàng, tự động truy vấn dữ liệu đơn hàng, cập nhật trạng thái (như hủy đơn) hoặc tạo ticket hỗ trợ 24/7 mà không cần sự can thiệp thủ công.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phản hồi tức thì 24/7:** Khách hàng hỏi là có bot trả lời ngay lập tức, không phải chờ đợi.
- **Tự động hóa nghiệp vụ kho/đơn hàng:** AI tự động tra cứu, cập nhật trạng thái đơn hàng (ví dụ: hủy đơn) trực tiếp trên Google Sheets.
- **Ghi nhận khiếu nại thông minh:** Tự động tạo ticket hỗ trợ khi phát sinh vấn đề phức tạp để nhân viên xử lý sau.
- **Cá nhân hóa trải nghiệm:** Bot nhớ ngữ cảnh trò chuyện nhờ bộ nhớ thông minh (Memory Buffer Window), giúp cuộc trò chuyện tự nhiên như người thật.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Telegram Bot Token** (tạo qua [@BotFather](https://t.me/BotFather)).
- **Google Gemini API Key** (tạo qua Google AI Studio).
- **Tài khoản Google Sheets** và một file Google Sheets chứa sẵn thông tin đơn hàng, trạng thái đơn và bảng ghi nhận ticket hỗ trợ.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy đoạn mã JSON của workflow này và paste trực tiếp vào n8n Editor, hoặc tải file JSON về và chọn **Import from File** trong giao diện n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, hệ thống sẽ hiển thị 12 nodes. Các sếp cần cấu hình chính xác các thành phần sau:

- **Telegram Trigger** & **Send Welcome Menu** & **Send Telegram Reply**: 
  - Tạo hoặc chọn **Telegram Bot Credentials** bằng cách điền Bot Token lấy từ BotFather.
- **Google Gemini Chat Model**: 
  - Tạo **Google Gemini API Credentials** và dán API Key của các sếp vào.
- **Tool: Read Orders Sheet**, **Tool: Update Order Status**, **Tool: Create Support Ticket**:
  - Cấu hình **Google Sheets OAuth2 API** hoặc Service Account.
  - Trỏ đúng đến **Sheet ID** và tên Sheet (Tab Name) tương ứng với bảng quản lý đơn hàng và bảng ticket của doanh nghiệp.
- **Extract Message** & **Prepare Reply** (Nodes dạng `code`):
  - Các đoạn code JavaScript có sẵn đã được tối ưu để lọc Chat ID, tên và xử lý dữ liệu đầu ra. Các sếp giữ nguyên hoặc tinh chỉnh lại định dạng thông điệp nếu muốn bot nói chuyện theo phong cách riêng của thương hiệu.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và gửi thử một tin nhắn `/start` hoặc một câu hỏi tra cứu đơn hàng mẫu tới Bot Telegram của các sếp để kiểm tra.
- Nếu mọi thứ hoạt động mượt mà, hãy bật nút **Active** ở góc trên cùng bên phải để bot chính thức "nhận việc" 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm kênh thông báo:** Kết nối thêm node Telegram cá nhân hoặc Slack để bắn thông báo cho quản lý kho mỗi khi có yêu cầu hủy đơn hoặc ticket hỗ trợ mới được tạo.
- **Lưu log chi tiết:** Lưu toàn bộ lịch sử hội thoại của khách hàng vào một Sheet riêng biệt để phân tích hành vi mua sắm và cải thiện chất lượng dịch vụ.
- **Mở rộng kho tri thức (RAG):** Kết hợp thêm Vector Store để AI có thể đọc hiểu toàn bộ chính sách đổi trả, bảo hành của cửa hàng và trả lời khách hàng chính xác 100%.

### 📌 Kết luận
Việc tự động hóa chăm sóc khách hàng thương mại điện tử chưa bao giờ dễ dàng đến thế với sức mạnh kết hợp giữa n8n, Google Gemini và Google Sheets. Hãy triển khai ngay hôm nay để tiết kiệm thời gian vận hành và gia tăng sự hài lòng cho khách hàng của các sếp!