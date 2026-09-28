---
title: "🚀 Tự động cập nhật bảng giá cổ phiếu thời gian thực với OpenAI, Octagon Agent và Google Sheets"
description: "Hướng dẫn xây dựng workflow n8n tự động đọc mã cổ phiếu từ Google Sheets, sử dụng AI và Octagon Agent để phân tích, sau đó cập nhật dữ liệu real-time."
slug: "tu-dong-cap-nhat-gia-co-phieu-openai-octagon-agent-google-sheets"
tags: [n8n, automation, ai, openai, google-sheets, crypto-trading]
keywords: [n8n workflow, tu dong hoa co phieu, openai n8n, octagon agent, google sheets automation]
keywords: [n8n workflow, tự động hóa cổ phiếu, openai n8n, octagon agent, google sheets automation]
---

# 🚀 Tự động cập nhật bảng giá cổ phiếu thời gian thực với OpenAI, Octagon Agent và Google Sheets

Các sếp có đang đau đầu vì mỗi ngày phải tốn hàng giờ đồng hồ vào các trang web tài chính để tra cứu giá cổ phiếu, sau đó copy-paste thủ công vào Google Sheets để theo dõi danh mục đầu tư? Việc làm thủ công này không chỉ tốn thời gian, dễ gây nhầm lẫn mà còn bỏ lỡ những biến động thị trường chớp nhoáng.

Giải pháp ở đây là gì? Một hệ thống tự động hóa 100% không cần code (No-Code) được xây dựng trên n8n! Workflow này sẽ tự động đọc danh sách mã cổ phiếu của các sếp, kết hợp sức mạnh của **OpenAI** và **Octagon Agent** để lấy dữ liệu thời gian thực từ internet, đọc kỹ năng (skills) từ **GitHub**, và tự động ghi đè kết quả phân tích ngược lại vào **Google Sheets**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn cảnh tra cứu thủ công từng mã cổ phiếu.
- **Dữ liệu cập nhật liên tục:** Lấy giá thời gian thực thông qua hệ thống AI Agent thông minh.
- **Đồng bộ trực quan:** Mọi thông tin phân tích, giá cả tự động đổ về Google Sheets chuẩn xác.
- **Hoạt động mượt mà, kiểm soát tải tốt:** Tích hợp bộ đệm (Throttle/Wait) giúp tránh việc gửi quá nhiều request cùng lúc gây lỗi API.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
1. **n8n Instance:** Đã cài đặt sẵn sàng (Self-hosted hoặc n8n Cloud).
2. **Google Sheets:** Một file Google Sheet chứa danh sách các mã cổ phiếu (Tickers) cần theo dõi.
3. **OpenAI API Key:** Để tạo các câu lệnh prompt thông minh cho AI.
4. **Octagon API Key:** Tài khoản và API từ dịch vụ Octagon Agents.
5. **GitHub:** Đường dẫn (URL) tới file chứa kỹ năng (skills) stock quote.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn JSON của workflow (hoặc tải file từ nguồn) và dán trực tiếp vào n8n Editor của mình. Workflow gồm tổng cộng 11 nodes được thiết kế mạch lạc, trực quan.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy trơn tru, các sếp cần chú ý cấu hình kỹ các node sau:

- **Set Task and Skills URL (Node `set` & `httpRequest` - *Fetch Skill from GitHub URL*):** 
  - Cần trỏ đường dẫn GitHub URL đến đúng file chứa bộ kỹ năng (skill) thu thập giá cổ phiếu.
- **Read Tickers in Sheets & Update Tickers in Sheets (Node `googleSheets`):**
  - Kết nối tài khoản Google thông qua **Credentials OAuth2**.
  - Trỏ đúng ID của Google Sheet và tên Sheet (Tab name) mà các sếp đang sử dụng để lưu danh sách mã cổ phiếu.
- **Create Octagon API Prompt (Node `openAi`):**
  - Chọn **Credentials OpenAI API**.
  - Tinh chỉnh Prompt của AI nếu các sếp muốn phân tích thêm các chỉ số chuyên sâu khác ngoài giá cơ bản.
- **Execute Octagon Agent (Node `n8n-nodes-octagon.octagonAgents`):**
  - Cấu hình **Octagon API Credentials** để agent có thể thực thi các tác vụ tài chính.
- **Wait 1 Second (Node `wait`):**
  - Node này cực kỳ quan trọng giúp "ghìm cương" tốc độ gọi API, tránh việc bị giới hạn (Rate Limit) từ phía các nhà cung cấp dữ liệu hoặc Google Sheets.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** thủ công (thông qua node *Manual Workflow Trigger*) để test thử với 1-2 dòng dữ liệu mẫu xem hệ thống chạy có mượt không.
- Sau khi test thành công, bật công tắc **Active** góc trên bên phải để hoàn tất.

### ✍️ Mẹo & gợi ý nâng cao
- **Tự động hóa theo lịch trình:** Thay vì dùng *Manual Workflow Trigger*, các sếp có thể thay thế bằng node **Schedule Trigger** để hệ thống tự động quét giá cổ phiếu vào mỗi 9h sáng hoặc mỗi giờ một lần.
- **Cảnh báo qua Telegram/Slack:** Kết hợp thêm node Telegram hoặc Slack ở cuối luồng để nhận thông báo ngay lập tức nếu có mã cổ phiếu biến động mạnh.
- **Lưu lịch sử (Log):** Tạo thêm một bảng Google Sheets phụ để ghi lại lịch sử biến động giá theo từng mốc thời gian phục vụ cho việc vẽ biểu đồ trực quan sau này.

### 📌 Kết luận
Việc tự động hóa cập nhật dữ liệu tài chính chưa bao giờ dễ dàng đến thế với sự trợ giúp của n8n, OpenAI và Octagon Agent. Hãy áp dụng ngay workflow này để giải phóng sức lao động và tối ưu hóa quy trình đầu tư của các sếp ngay hôm nay!