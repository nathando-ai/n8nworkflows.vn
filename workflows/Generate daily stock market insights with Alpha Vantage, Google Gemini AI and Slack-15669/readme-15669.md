---
title: "🚀 Tự động hóa bản tin chứng khoán hàng ngày với Alpha Vantage, Google Gemini AI và Slack"
description: "Xây dựng hệ thống phân tích thị trường chứng khoán tự động 100% bằng n8n, lấy dữ liệu từ Alpha Vantage, phân tích bằng Google Gemini AI và gửi báo cáo trực quan lên Slack."
slug: "tu-dong-hoa-chung-khoan-alpha-vantage-gemini-slack"
tags: [n8n, automation, ai-summarization, crypto-trading, google-gemini, slack]
keywords: [n8n workflow, tự động hóa chứng khoán, alpha vantage, google gemini ai, slack integration, phân tích thị trường]
---

# 🚀 Tự động hóa bản tin chứng khoán hàng ngày với Alpha Vantage, Google Gemini AI và Slack

Các sếp có đang tốn hàng giờ mỗi ngày để theo dõi biểu đồ, lọc mã tăng/giảm mạnh (Top Gainers/Losers) và tìm đọc tin tức để hiểu lý do vì sao thị trường biến động? Việc làm thủ công này không chỉ tốn thời gian mà còn dễ bỏ lỡ các cơ hội đầu tư chớp nhoáng.

Đừng lo, workflow n8n này sẽ thay các sếp làm tất cả! Hệ thống sẽ tự động lấy dữ liệu thị trường, tính toán xu hướng tâm lý, phân tích tin tức mới nhất bằng **Google Gemini AI** và gửi ngay một báo cáo tài chính cực kỳ chi tiết, chuyên nghiệp thẳng vào kênh Slack của đội ngũ.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian:** Tự động hóa hoàn toàn quy trình thu thập dữ liệu và phân tích thị trường mỗi ngày.
- **Phân tích sâu sắc nhờ AI:** Google Gemini AI sẽ thay chuyên gia giải thích lý do "Tại sao" giá cổ phiếu lại biến động mạnh dựa trên tin tức thực tế.
- **Cập nhật tức thì:** Báo cáo được định dạng đẹp mắt và gửi thẳng vào kênh Slack cá nhân hoặc nhóm làm việc.
- **Vận hành liên tục:** Dễ dàng chuyển đổi từ chạy thủ công sang lịch trình tự động (Schedule) chạy vào cuối mỗi phiên giao dịch.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Đã sẵn sàng hoạt động (Self-hosted hoặc n8n Cloud).
- **Alpha Vantage API Key:** Dùng để gọi dữ liệu thị trường chứng khoán/crypto.
- **Google Gemini API Key:** Cung cấp trí tuệ nhân tạo để tổng hợp và phân tích thông tin.
- **Slack Workspace:** Tài khoản có quyền kết nối và gửi tin nhắn vào channel mong muốn.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Copy toàn bộ mã nguồn JSON của workflow hoặc import file JSON trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà không gặp lỗi, các sếp cần cấu hình chính xác các node sau:
- **Fetch Market Data (`httpRequest`) & Get Ticker News Context (`httpRequest`):** Thêm Alpha Vantage API Key vào phần Header hoặc Query Parameters theo tài liệu của Alpha Vantage.
- **Google Gemini Chat Model (`lmChatGoogleGemini`):** Kết nối thông tin xác thực (`credentials`) sử dụng Google Palm/Gemini API Key đã chuẩn bị.
- **Post to Portfolio Channel (`slack`):** Chọn kết nối tài khoản Slack (`slackApi`) và chọn chính xác Channel đích mà các sếp muốn nhận báo cáo.
- **Start Market Analysis (`manualTrigger`):** Node mặc định đang ở chế độ thủ công. Các sếp có thể đổi thành node **Schedule Trigger** để hệ thống tự động chạy vào cuối mỗi ngày giao dịch.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** để test run với dữ liệu mẫu và kiểm tra kết quả trên Slack.
- Nếu mọi thứ hiển thị đẹp đẽ, hãy bật nút **Active** ở góc trên cùng bên phải để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Ngoài Slack, các sếp có thể nối thêm node Telegram hoặc Email để nhận bản tin đa kênh.
- **Lưu trữ lịch sử:** Thêm node Google Sheets hoặc Notion ở cuối luồng để lưu lại toàn bộ các bản phân tích phục vụ việc backtest hoặc tra cứu sau này.
- **Tùy chỉnh Prompt:** Tinh chỉnh system prompt trong Agent AI (`Generate Financial Insight`) để đổi văn phong báo cáo (trang trọng, ngắn gọn, hoặc hài hước tùy ý thích).

### 📌 Kết luận
Workflow này là một "trợ lý tài chính ảo" cực kỳ đắc lực cho các nhà đầu tư hoặc các đội ngũ phân tích thị trường. Hãy cài đặt ngay hôm nay để tối ưu hóa quy trình làm việc và không bỏ lỡ bất kỳ biến động quan trọng nào của thị trường!