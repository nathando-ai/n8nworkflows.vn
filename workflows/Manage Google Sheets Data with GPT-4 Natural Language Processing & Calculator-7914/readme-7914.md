---
title: "🚀 Quản lý Google Sheets bằng ngôn ngữ tự nhiên với GPT-4 và n8n AI Agent"
description: "Hướng dẫn xây dựng trợ lý AI kết nối Google Sheets và ChatGPT giúp bạn đọc, thêm, sửa, xóa dữ liệu và tính toán tự động chỉ bằng một câu lệnh chat."
slug: "quan-ly-google-sheets-bang-ai-gpt-4-n8n"
tags: [n8n, automation, ai-agent, google-sheets, openai, no-code]
keywords: [n8n workflow, ai agent google sheets, gpt-4 chat google sheets, tự động hóa google sheets, n8n langchain]
---

# 🚀 Quản lý Google Sheets bằng ngôn ngữ tự nhiên với GPT-4 và n8n AI Agent

Các sếp có bao giờ cảm thấy mệt mỏi khi phải mở hàng chục file Google Sheets, lọc dữ liệu thủ công, tính toán các cột tổng hay cập nhật trạng thái đơn hàng liên tiếp mỗi ngày? Việc này không chỉ tốn thời gian mà còn cực kỳ dễ nhầm lẫn.

Thay vì phải click chuột và gõ hàm phức tạp, giờ đây các sếp có thể trò chuyện trực tiếp với dữ liệu của mình! Workflow n8n này sẽ biến **GPT-4** thành một trợ lý ảo thông minh, giúp các sếp thực hiện mọi thao tác **Đọc (Read), Thêm mới (Create), Cập nhật (Update), Xóa (Delete)** dữ liệu trên Google Sheets, kèm theo khả năng tính toán chuẩn xác thông qua ngôn ngữ tự nhiên 100% không cần code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Thao tác bằng lời nói:** Chỉ cần chat "Thêm đơn hàng mới cho khách A", trợ lý AI sẽ tự động xử lý.
- **Tính toán thông minh:** AI tự động đọc dữ liệu từ bảng tính và kết hợp với công cụ Calculator để tính tổng doanh thu, trung bình, v.v. một cách chính xác.
- **Quản lý toàn diện:** Tích hợp trọn bộ công cụ CRUD (Create, Read, Update, Delete) trên Google Sheets trong một giao diện chat duy nhất.
- **Tiết kiệm 80% thời gian:** Không còn loay hoay với các hàm Excel hay Google Sheets phức tạp.
:::

### Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (phiên bản hỗ trợ LangChain và AI Agent).
- **OpenAI API Key:** Tài khoản OpenAI có quyền truy cập mô hình GPT-4 (hoặc GPT-4o-mini).
- **Google Account:** Tài khoản Google để kết nối Google Sheets.
- **File Google Sheets mẫu:** Copy file [Order Spreadsheet](https://docs.google.com/spreadsheets/d/1vbFb2dhys1VafAmX-hRtiyrEDgNKj_xaAA6ZmH09EL8/edit?usp=sharing) vào Google Drive cá nhân của các sếp.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy trực tiếp cấu trúc workflow từ n8n.
- Dán (Paste) vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để trợ lý AI hoạt động mượt mà, các sếp cần cấu hình chính xác các node sau:

- **Model (OpenAI Chat Model):** 
  - Chọn credential OpenAI của các sếp.
  - Đảm bảo model được chọn là `gpt-4o-mini` (hoặc các dòng GPT-4 tương đương) để AI hiểu ngữ cảnh và gọi công cụ (Tools) chính xác.
- **Các node Google Sheets Tools (Read, Create, Update, Delete):**
  - Kết nối tài khoản Google thông qua `Google Sheets OAuth2 API`.
  - Trỏ đường dẫn đến file Google Sheets đơn hàng mà các sếp đã copy vào Drive ở phần chuẩn bị.
  - Cấu hình tên Sheet (Tab Name) chính xác để các tool có thể tương tác đúng bảng dữ liệu.
- **Simple Memory (Buffer Window Memory):**
  - Giúp AI ghi nhớ lịch sử trò chuyện, cho phép các sếp ra lệnh tiếp nối (ví dụ: "Lọc ra các đơn của khách A" -> "Tính tổng tiền các đơn đó").

#### 3. Kích hoạt ⚡️
- Nhấp vào nút **Chat** ở node `When chat message received` để mở cửa sổ test.
- Gửi thử câu lệnh: *"Hãy tính tổng giá trị của cột amount trong bảng"* hoặc *"Thêm một đơn hàng mới..."*.
- Kiểm tra xem AI có gọi đúng công cụ Read/Calculator hay không.
- Khi đã chạy ổn định, gạt công tắc sang **Active** để đưa workflow vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh chat thực tế:** Thay vì dùng chat widget mặc định của n8n, các sếp có thể đổi trigger thành **Telegram Bot** hoặc **Slack** để quản lý đơn hàng ngay trên điện thoại.
- **Gửi thông báo tự động:** Kết hợp thêm node Email hoặc Zalo/Slack để thông báo cho sếp mỗi khi có lệnh "Thêm" hoặc "Cập nhật" đơn hàng quan trọng từ AI.
- **Lưu log lịch sử:** Thêm một bước ghi lại lịch sử các câu lệnh của người dùng vào một Google Sheet riêng để kiểm toán (audit trail) khi cần thiết.

### 📌 Kết luận
Workflow này là bước đệm tuyệt vời để các sếp ứng dụng AI Agent vào công việc vận hành hàng ngày mà không cần biết lập trình. Hãy cài đặt ngay hôm nay để trải nghiệm sức mạnh của việc quản lý dữ liệu bằng giọng nói/tin nhắn!