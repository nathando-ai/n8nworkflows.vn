---
title: "🚀 Tự động hóa trích xuất khách hàng tiềm năng và gửi email outbound bằng n8n & AI"
description: "Xây dựng hệ thống Domain Outbound tự động 100%: trích xuất data, quét website bằng Jina.ai, tạo nội dung cá nhân hóa bằng OpenAI và gửi email qua Gmail."
slug: "tu-dong-hoa-outbound-lead-extraction-ai"
tags: [n8n, automation, no-code, sales, ai, openai, gmail]
keywords: [n8n workflow, outbound sales, trích xuất lead, tự động hóa gửi email, ai sales automation]
---

# 🚀 Tự động hóa trích xuất khách hàng tiềm năng và gửi email outbound bằng n8n & AI

Việc thực hiện các chiến dịch Outbound Sales thủ công thường ngốn rất nhiều thời gian của các đội ngũ kinh doanh: từ việc tìm kiếm domain, cào dữ liệu website, lọc email cho đến việc viết từng nội dung email cá nhân hóa. Nếu làm bằng tay, các sếp chỉ tiếp cận được vài chục khách hàng mỗi ngày và rất dễ gặp tình trạng sai sót, thiếu chuyên nghiệp.

Giải pháp ở đây là gì? Workflow n8n mang tên **"Domain Outbound : Automate Lead Extraction, and Targeted Outreach"** do tác giả *Badr* phát triển sẽ giúp các sếp tự động hóa toàn bộ quy trình này từ A-Z mà không cần viết code phức tạp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100% phễu outbound:** Từ việc tạo từ khóa tìm kiếm, cào data website, lọc trùng cho đến gửi email.
- **Cá nhân hóa nội dung bằng AI:** Sử dụng OpenAI để phân tích website mục tiêu và soạn thảo email chào hàng sắc bén, trúng "nỗi đau" của khách hàng.
- **Tiết kiệm hàng chục giờ làm việc:** Xử lý hàng trăm lead tiềm năng chỉ trong vài phút.
- **Kiểm soát luồng gửi an toàn:** Tích hợp các khoảng chờ (`Wait`) thông minh giúp tránh bị Gmail đánh dấu spam.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (bản Cloud hoặc Self-hosted).
- **Google Sheets:** File chứa danh sách domain/từ khóa ban đầu hoặc dùng để lưu trữ kết quả.
- **OpenAI API Key:** Để chạy các node AI tạo query tìm kiếm và viết nội dung email.
- **Tài khoản Gmail:** Đã kết nối credentials với n8n để gửi email tự động.
- **Jina.ai API:** (Hoặc cấu hình HTTP Request tương ứng) để trích xuất nội dung website dưới dạng Markdown.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Các sếp tải file JSON của workflow hoặc copy trực tiếp mã nguồn từ [n8n Workflow #2821](https://n8n.io/workflows/2821).
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File / Paste JSON** và dán vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần cấu hình chính xác các node sau:
- **Google Sheets:** Kết nối tài khoản Google, trỏ tới file Sheet chứa danh sách nguồn khách hàng tiềm năng của các sếp.
- **Generate queries & Generate Email content (OpenAI):** Cung cấp OpenAI API Key và chọn model phù hợp (khuyên dùng `gpt-4o-mini` hoặc `gpt-4o` để nội dung email đạt chất lượng cao nhất).
- **get website with Jina.ai (HTTP Request1):** Kiểm tra lại Endpoint và cấu hình Header/API key của dịch vụ Jina.ai để đảm bảo việc cào nội dung website không bị gián đoạn.
- **Gmail1 & Gmail search:** Cấu hình tài khoản Gmail của doanh nghiệp để gửi email outreach và theo dõi phản hồi.
- **Các node Code & Filter:** Kiểm tra lại các logic xử lý dữ liệu (`Extract Urls`, `Extract Domain Name`, `Extract Emails`) để đảm bảo định dạng dữ liệu đầu ra khớp với yêu cầu của bước tiếp theo.

#### 3. Kích hoạt ⚡️
- Nhấn **Test workflow** trên node `When clicking ‘Test workflow’` để chạy thử với một vài dữ liệu mẫu.
- Kiểm tra kỹ nội dung email được tạo ra và quá trình gửi qua Gmail.
- Khi mọi thứ hoạt động trơn tru, hãy chuyển trạng thái workflow sang **Active**.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack/Telegram:** Thêm node thông báo qua Telegram hoặc Slack mỗi khi hệ thống gửi thành công một email outreach hoặc khi có khách hàng phản hồi.
- **Lưu lịch sử chi tiết:** Mở rộng node `Google Sheets` để ghi log toàn bộ thời gian, trạng thái gửi email và nội dung AI đã tạo để đội ngũ sales dễ dàng chăm sóc lại.
- **Tinh chỉnh khoảng nghỉ (Wait nodes):** Điều chỉnh thời gian ở các node `Wait1` và `Wait2` cho phù hợp với giới hạn (rate limit) gửi email hàng ngày của Gmail để tài khoản luôn an toàn.

### 📌 Kết luận
Workflow **Domain Outbound** này là thứ vũ khí cực kỳ mạnh mẽ giúp các đội ngũ sales, agency tối ưu hóa quy trình tiếp cận khách hàng lạnh (cold outreach). Hãy thiết lập ngay hôm nay để đưa hệ thống sales của doanh nghiệp lên một tầm cao mới tự động và thông minh hơn!