---
title: "🚀 Tự động hóa tóm tắt danh mục đầu tư chứng khoán với Google Sheets, NewsAPI, Gemini và Gmail"
description: "Hướng dẫn xây dựng workflow n8n tự động cập nhật giá cổ phiếu, tổng hợp tin tức, dùng AI Gemini viết báo cáo danh mục đầu tư và gửi email tự động."
slug: "tu-dong-hoa-tom-tat-danh-muc-dau-tu-chung-khoan-n8n"
tags: [n8n, automation, ai-summarization, google-sheets, gemini, gmail]
keywords: [n8n workflow, tóm tắt danh mục đầu tư, tự động hóa chứng khoán, google sheets, newsapi, google gemini, gmail automation]
---

# 🚀 Tự động hóa tóm tắt danh mục đầu tư chứng khoán với Google Sheets, NewsAPI, Gemini và Gmail

Các nhà đầu tư và quản lý tài chính thường mất rất nhiều thời gian để theo dõi giá cổ phiếu thời gian thực, cập nhật tin tức thị trường mới nhất và soạn báo cáo gửi cho khách hàng. Việc làm thủ công này không chỉ tẻ nhạt mà còn dễ bỏ lỡ các biến động quan trọng của thị trường.

Workflow n8n này sẽ giải quyết triệt để vấn đề đó bằng cách tự động hóa 100% quy trình: lắng nghe dữ liệu từ Google Sheets, lấy giá cổ phiếu trực tiếp, quét tin tức mới nhất, phân tích qua AI Gemini và gửi báo cáo chuyên nghiệp qua Gmail mà không cần can thiệp thủ công.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Tự động hóa toàn bộ từ khâu tính toán lãi/lỗ đến soạn báo cáo.
- **Cập nhật thời gian thực:** Lấy giá live của cổ phiếu và tin tức mới nhất liên quan ngay khi có dữ liệu mới.
- **AI phân tích chuyên sâu:** Sử dụng Google Gemini để tạo bản tóm tắt trực quan, dễ hiểu cho khách hàng.
- **Hoạt động 24/7 không gián đoạn:** Chạy ngầm trên n8n và gửi email tự động qua Gmail đúng thời điểm yêu cầu.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- Tài khoản n8n (Self-hosted hoặc Cloud).
- Tài khoản Google (Google Sheets & Gmail Credentials).
- Tài khoản NewsAPI (hoặc API nhà cung cấp giá chứng khoán tương tự).
- Google Gemini API Key (để sử dụng node `Generate Portfolio Summary`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow, sau đó dán trực tiếp vào giao diện n8n Editor (hoặc sử dụng tính năng Import từ file JSON).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node trọng điểm sau:
- **Google Sheet New Row Add Trigger:** Kết nối tài khoản Google Sheets của các sếp, chọn đúng file Google Sheet quản lý danh mục đầu tư (với các cột cơ bản như Tên cổ phiếu, Số lượng, Giá mua).
- **Cleans & standardizes & Calculate Portfolio Metrics (Code Nodes):** Đảm bảo cấu trúc dữ liệu đầu vào khớp với code xử lý Javascript bên trong các node này.
- **Fetch Live Stock Prices & Fetch Stock News (HTTP Request Nodes):** Điền API Key hợp lệ của nhà cung cấp giá cổ phiếu và NewsAPI vào phần Header hoặc Query Parameters.
- **Wait For 5 Seconds (Cooling Period) & Iterate Stocks for News (Split In Batches):** Giúp vòng lặp duyệt qua từng mã cổ phiếu không bị dính lỗi vượt quá giới hạn gọi API (Rate Limit).
- **Generate Portfolio Summary (Google Gemini):** Chọn credentials của Google Gemini và kiểm tra lại System Prompt để AI định dạng nội dung báo cáo gửi khách hàng theo đúng ý muốn.
- **Send Email Report (Gmail):** Kết nối tài khoản Gmail cá nhân hoặc doanh nghiệp để gửi email báo cáo tự động.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) bằng một dòng dữ liệu mẫu trong Google Sheets để kiểm tra log từng node.
- Khi mọi thứ hoạt động trơn tru, hãy bật nút **Active** để workflow chính thức tự động vận hành.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Kết hợp thêm node Telegram hoặc Slack để gửi cảnh báo tức thời khi danh mục có biến động mạnh.
- **Lưu lịch sử báo cáo:** Thêm một bước ghi lại kết quả tóm tắt của AI vào một bảng Google Sheets riêng biệt để làm nhật ký theo dõi theo ngày/tuần.
- **Lên lịch định kỳ:** Thay vì dùng Trigger theo dòng mới, các sếp có thể đổi sang Schedule Trigger để hệ thống tự động tổng hợp báo cáo vào mỗi thứ Hai hàng tuần.

### 📌 Kết luận
Workflow tự động hóa danh mục đầu tư kết hợp AI Gemini và Google Sheets là trợ đắc lực giúp các nhà đầu tư tối ưu hóa quy trình quản trị tài sản và chăm sóc khách hàng chuyên nghiệp hơn. Hãy triển khai ngay hôm nay để trải nghiệm sức mạnh của tự động hóa!