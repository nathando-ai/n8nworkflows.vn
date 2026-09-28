---
title: "🚀 Tự động phân tích biến động giá nguyên liệu và đưa ra khuyến nghị mua hàng thông minh với n8n"
description: "Xây dựng hệ thống tự động kiểm tra giá nguyên liệu hàng ngày từ API, lưu trữ vào PostgreSQL, tính toán xu hướng, tạo báo cáo HTML và gửi cảnh báo qua Email/Slack."
slug: "phan-tich-bien-dong-gia-nguyen-lieu-n8n"
tags: [n8n, automation, postgresql, slack, email, ai-summarization, market-research]
keywords: [n8n workflow, tự động hóa giá nguyên liệu, postgresql n8n, phân tích xu hướng giá, slack alert n8n]
---

# 🚀 Tự động phân tích biến động giá nguyên liệu và đưa ra khuyến nghị mua hàng thông minh với n8n

Các doanh nghiệp sản xuất, nhà hàng hoặc kinh doanh F&B thường xuyên phải đối mặt với bài toán đau đầu: Giá nguyên liệu đầu vào biến động liên tục từng ngày. Việc theo dõi thủ công bằng Excel vừa mất thời gian, dễ sai sót, lại bỏ lỡ thời điểm vàng để mua trữ hàng với giá hời.

Được phát triển bởi **Oneclick AI Squad**, workflow n8n này sẽ thay thế hoàn toàn quy trình thủ công đó. Hệ thống sẽ tự động gọi API lấy giá mới nhất mỗi ngày, lưu trữ vào cơ sở dữ liệu PostgreSQL, phân tích xu hướng, đưa ra quyết định mua hàng thông minh và gửi báo cáo trực quan qua Email cùng cảnh báo tức thì qua Slack!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Định kỳ kiểm tra giá mỗi ngày mà không cần con người can thiệp.
- **Phân tích xu hướng thông minh:** Tự động tính toán biến động lịch sử giá để đưa ra lời khuyên nên mua hay chờ đợi.
- **Báo cáo trực quan:** Tổng hợp dữ liệu thành bảng HTML chuyên nghiệp gửi trực tiếp vào hộp thư email.
- **Cảnh báo tức thời:** Nhận thông báo nhanh chóng qua Slack để kịp thời ra quyết định thu mua.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **PostgreSQL Database:** Cần có thông tin kết nối (Host, Port, User, Password, Database Name) để lưu trữ lịch sử giá và khuyến nghị.
- **External Price API:** Endpoint API cung cấp dữ liệu giá nguyên liệu đầu vào.
- **SMTP Credentials:** Tài khoản gửi email (Gmail, SendGrid, Amazon SES, v.v.) để gửi báo cáo.
- **Slack Webhook URL:** Để đẩy thông báo cảnh báo giá vào kênh Slack của đội ngũ thu mua.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow hoặc copy trực tiếp mã nguồn JSON, sau đó dán vào giao diện n8n Editor của các sếp bằng cách chọn **Add workflow** -> Dán (Ctrl+V).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 11 nodes liên kết chặt chẽ với nhau. Các sếp cần chú ý cấu hình các điểm sau:

- **Daily Price Check (cron):** Thiết lập lịch chạy mong muốn (mặc định chạy hàng ngày vào một khung giờ cố định).
- **Fetch API Prices (httpRequest):** Điền Endpoint API thực tế của các sếp vào để hệ thống quét dữ liệu giá nguyên liệu.
- **Setup Database, Store Price Data, Calculate Trends, Store Recommendations, Get Dashboard Data (postgres):** 
  - Chọn `Credentials` là kết nối PostgreSQL của các sếp.
  - Node `Setup Database` sẽ tự động tạo bảng (nếu chưa có) để lưu trữ dữ liệu giá và lịch sử.
- **Generate Recommendations & Generate Dashboard HTML (code):** Các node JavaScript xử lý logic tính toán xu hướng, tạo ra lời khuyên mua sắm (Buy/Wait) và dựng giao diện HTML cho báo cáo. Các sếp có thể tùy chỉnh lại câu chữ thông điệp tại đây nếu muốn.
- **Send Email Report (emailSend):** Chọn SMTP Credentials, cấu hình địa chỉ Email nhận báo cáo (bộ phận kế toán/mua hàng).
- **Send Slack Alert (httpRequest):** Cấu hình Slack Webhook URL để đẩy tin nhắn cảnh báo biến động giá mạnh vào channel Slack nội bộ.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** chạy thử lần đầu với dữ liệu thủ công để kiểm tra kết nối Database, API, Email và Slack hoạt động trơn tru.
- Sau khi test thành công, bật công tắc **Active** ở góc trên cùng bên phải để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Telegram:** Ngoài Slack, các sếp có thể bổ sung thêm Telegram Bot node để gửi tin nhắn trực tiếp vào nhóm chat Zalo/Telegram của sếp hoặc nhân viên.
- **Lưu file Excel/Google Sheets dự phòng:** Kết nối thêm node Google Sheets để lưu bản sao lưu (backup) dữ liệu giá hàng ngày phục vụ việc đối soát tài chính.
- **Nâng cấp AI Agent:** Tích hợp OpenAI hoặc Claude node vào bước `Generate Recommendations` để AI đóng vai trò chuyên gia thu mua, tự động phân tích sâu hơn về chuỗi cung ứng dựa trên dữ liệu giá lịch sử.

### 📌 Kết luận
Workflow **Ingredient Price Trend Analysis & Buying Recommendations** là một giải pháp tự động hóa cực kỳ mạnh mẽ giúp tối ưu chi phí nguyên liệu đầu vào cho doanh nghiệp. Hãy triển khai ngay hôm nay để quản lý dòng tiền và chi phí mua hàng một cách thông minh, khoa học nhất!