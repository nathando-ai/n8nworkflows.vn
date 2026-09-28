---
title: "🚀 Tự động hóa gửi email bán hàng cá nhân hóa siêu đỉnh với LinkedIn và Claude 3.7 qua OpenRouter"
description: "Hướng dẫn xây dựng workflow n8n tự động cào dữ liệu LinkedIn cá nhân/công ty, kết hợp Claude 3.7 Sonnet qua OpenRouter để viết email sales cực kỳ cá nhân hóa và tự động gửi qua Gmail."
slug: "tu-dong-hoa-email-sales-linkedin-claude-37-n8n"
tags: [n8n, automation, no-code, ai, lead-generation, claude, sales]
keywords: [n8n workflow, tự động hóa email sales, linkedin scraping, claude 3.7 openrouter, ai lead nurturing]
---

# 🚀 Tự động hóa gửi email bán hàng cá nhân hóa siêu đỉnh với LinkedIn và Claude 3.7 qua OpenRouter

Các sếp có đang mệt mỏi vì phải ngồi thủ công tra cứu từng khách hàng tiềm năng trên LinkedIn, nghiên cứu công ty của họ, rồi vắt óc viết từng chiếc email cá nhân hóa để rồi nhận lại tỷ lệ phản hồi thấp lẹt đẹt? Công việc thủ công này ngốn hàng giờ đồng hồ mỗi ngày mà hiệu quả lại không cao.

Đừng lo, giải pháp ở đây rồi! Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ mạnh mẽ do tác giả **Adam Janes** sáng tạo. Workflow này sẽ tự động hóa toàn bộ quy trình: từ việc lấy danh sách lead từ Google Sheets, tìm kiếm thông tin LinkedIn của cá nhân và công ty, sử dụng siêu AI **Claude 3.7 Sonnet** (qua OpenRouter) để viết email bán hàng siêu cá nhân hóa, và cuối cùng tự động gửi đi qua **Gmail**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không cần tra cứu thủ công profile LinkedIn hay tự soạn từng email chào hàng.
- **Cá nhân hóa sâu sắc:** AI phân tích sâu dữ liệu từ LinkedIn của cả cá nhân lẫn công ty để tạo ra nội dung email trúng "nỗi đau" và đúng trọng tâm.
- **Tự động hóa toàn diện:** Tích hợp liền mạch từ Google Sheets -> AI -> Gmail mà không cần can thiệp thủ công.
- **Tỷ lệ chuyển đổi cao:** Email viết cực kỳ tự nhiên, chuyên nghiệp nhờ sức mạnh của mô hình Claude 3.7 Sonnet mới nhất.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị sẵn các tài khoản và API sau:
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **Google Sheets:** File chứa danh sách leads (Họ tên, Công ty, Email...).
- **OpenRouter API Key:** Để kết nối với mô hình Claude 3.7 Sonnet.
- **Apify (hoặc HTTP API tương đương):** Dùng để thực hiện Google Search và cào dữ liệu LinkedIn (được cấu hình qua các node `Google Search for Person LinkedIn`, `Get LinkedIn Person`,...).
- **Gmail Account:** Đã cấp quyền OAuth2 để n8n gửi email thay mặt các sếp.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow, sau đó vào giao diện n8n, chọn **Add workflow** -> Click vào menu ba chấm (...) ở góc trên bên phải -> Chọn **Import from File / Clipboard** và dán đoạn JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import thành công, các sếp cần cấu hình các node quan trọng sau:

- **Get Leads (Google Sheets):** Kết nối với tài khoản Google Drive/Sheets của các sếp, chọn đúng file Google Sheet chứa danh sách khách hàng tiềm năng (`First Name`, `Last Name`, `Company`, `Email`).
- **Set Data (Node `Set Data`):** Đây là nơi các sếp định nghĩa thông tin về sản phẩm/dịch vụ của công ty mình để AI dựa vào đó mà viết email chào hàng phù hợp với từng lead.
- **Google Search & LinkedIn Nodes (HTTP Request):** Kiểm tra lại các kết nối API (Credential `httpHeaderAuth`) dùng cho việc tìm kiếm link LinkedIn và lấy thông tin profile qua Apify hoặc dịch vụ bên thứ ba tương tự.
- **OpenRouter Chat Model:** Chọn credential OpenRouter và đảm bảo model được trỏ chính xác là `anthropic/claude-3.7-sonnet`.
- **Generate Personalized Email (Chain LLM) & Structured Output Parser:** Tinh chỉnh prompt nếu cần thiết để AI định dạng tiêu đề và nội dung email trả về đúng cấu trúc JSON mà node Gmail yêu cầu.
- **Gmail Node:** Kết nối tài khoản Gmail cá nhân hoặc doanh nghiệp qua OAuth2 để node này có quyền gửi email tự động.

#### 3. Kích hoạt ⚡️
- Click vào node **When clicking ‘Execute workflow’** hoặc dùng `Manual Trigger` để test với 1-2 dòng dữ liệu mẫu đầu tiên.
- Kiểm tra kết quả trả về ở các node AI và hòm thư nháp/thư đã gửi của Gmail xem email đã được soạn chuẩn chỉnh chưa.
- Nếu mọi thứ mượt mà, gạt công tắc **Active** ở góc trên bên phải để workflow sẵn sàng chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm bước Phê duyệt (Human-in-the-loop):** Thay vì gửi thẳng qua Gmail, các sếp có thể đổi node Gmail thành gửi tin nhắn qua **Slack** hoặc **Telegram** kèm theo nút duyệt, để kiểm tra lại nội dung email trước khi gửi đi.
- **Lưu lịch sử:** Thêm một node Google Sheets ở cuối luồng để ghi log lại trạng thái "Đã gửi email" kèm thời gian vào bảng quản lý leads.
- **Chia batch thông minh:** Sử dụng node `Loop Over Items` (`Split In Batches`) với số lượng vừa phải (ví dụ 10-20 lead/lần) để tránh vượt quá giới hạn gọi API (Rate limit) của LinkedIn/Google/OpenRouter.

### 📌 Kết luận
Tự động hóa quy trình Sales Outreach chưa bao giờ dễ dàng đến thế với sự kết hợp của n8n và Claude 3.7. Hãy áp dụng ngay workflow này để tối ưu hóa đội ngũ sales, tiếp cận hàng trăm khách hàng mỗi ngày mà vẫn giữ được độ cá nhân hóa đỉnh cao. Chúc các sếp "chốt đơn" mỏi tay!