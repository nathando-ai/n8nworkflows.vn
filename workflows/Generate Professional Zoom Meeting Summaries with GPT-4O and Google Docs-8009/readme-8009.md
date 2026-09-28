---
title: "🚀 Tự động hóa tóm tắt cuộc họp Zoom chuyên nghiệp với GPT-4o và Google Docs"
description: "Biến bản ghi và tài liệu Zoom nhận qua Gmail thành bản tóm tắt chuyên nghiệp, tự động lưu trữ lên Google Docs và gửi email thông báo nhờ n8n và AI."
slug: "tu-dong-hoa-tom-tat-zoom-meeting-gpt-4o-google-docs"
tags: [n8n, automation, no-code, openai, googledocs, gmail, ai-summarization]
keywords: [n8n workflow, tóm tắt zoom tự động, gpt-4o google docs, automation email zoom, no-code workflow]
---

# 🚀 Tự động hóa tóm tắt cuộc họp Zoom chuyên nghiệp với GPT-4o và Google Docs

Các sếp có bao giờ cảm thấy ngợp trước hàng tá bản ghi, tài liệu (assets) từ các cuộc họp Zoom dài lê thê? Việc đọc lại toàn bộ, tự tay tổng hợp ý chính, tạo Google Docs rồi gửi email báo cáo cho team tốn không dưới 30-45 phút mỗi cuộc họp. 

Chưa kể, nếu quên hoặc làm trễ, tiến độ công việc sẽ bị chậm lại. Giải pháp gì để tự động hóa 100% quy trình này? Workflow n8n tích hợp **GPT-4o**, **Google Docs** và **Gmail** chính là "vũ khí tối thượng" giúp các sếp giải quyết triệt để bài toán này mà không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hoàn toàn:** Ngay khi Zoom gửi tài liệu/assets về Gmail, hệ thống sẽ tự kích hoạt xử lý.
- **AI thông minh:** Sử dụng GPT-4o để phân tích, chắt lọc nội dung thành các phần rõ ràng: Tiêu đề, Thành phần tham dự, Tổng quan, Các điểm thảo luận chính và Việc cần làm (Action Items).
- **Lưu trữ chuẩn chỉnh:** Tự động tạo và cập nhật tài liệu trên Google Docs đúng chuẩn tên, gọn gàng, dễ tra cứu.
- **Tương tác linh hoạt:** Tích hợp công cụ gửi email thông minh thông qua AI agent, giúp thông báo kết quả nhanh chóng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Gmail Account (OAuth2):** Để nhận email từ Zoom và gửi email báo cáo.
- **OpenAI API Key:** Sử dụng model `gpt-4o` để phân tích và định dạng nội dung.
- **Google Docs (OAuth2):** Để tạo và cập nhật tài liệu tự động.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow này, sau đó mở n8n Editor, chọn **New workflow** -> Nhấn `Ctrl + V` (hoặc `Cmd + V`) để dán trực tiếp vào màn hình làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình các credentials và tham số quan trọng sau tại các nodes:

- **Gmail Trigger:** 
  - Kết nối tài khoản Gmail cá nhân/doanh nghiệp của các sếp (`gmailOAuth2`).
  - Thiết lập bộ lọc (filter) để chỉ bắt email từ Zoom (ví dụ: tiêu đề chứa 'Meeting assets', 'Zoom', hoặc gửi từ `no-reply@zoom.us`).
- **Mark a message as read:** 
  - Đảm bảo kết nối đúng credentials Gmail để đánh dấu email đã xử lý, tránh lặp lại.
- **Markdown & Apply Formatting:** 
  - Các node này chuyển đổi nội dung email HTML sang dạng Markdown, giúp AI (GPT-4o) dễ dàng đọc hiểu và cấu trúc lại thông tin.
- **gpt-4O & Generate Summary (Agent):** 
  - Cần thêm OpenAI API Key (`openAiApi`).
  - Đảm bảo model được chọn chính xác là `gpt-4o`.
  - Cấu hình các công cụ (Tools) đính kèm như **Send Email** để Agent có quyền chủ động gửi báo cáo khi cần.
- **DocFormat & Google Docs (Create a document / Update a document):** 
  - Kết nối tài khoản Google Docs (`googleDocsOAuth2Api`).
  - Tại node **Create a document**, mặc định file sẽ được tạo ở thư mục gốc (Root). Các sếp có thể cấu hình lại ID thư mục cụ thể để lưu trữ gọn gàng hơn.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và gửi một email mẫu từ Zoom để test thử.
- Kiểm tra kết quả trên Google Docs và Gmail xem đã đúng ý chưa.
- Gạt công tắc sang **Active** để bật chế độ chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm ChatOps:** Kết nối thêm node Slack hoặc Telegram để bắn thông báo tóm tắt cuộc họp vào group chat chung ngay khi xử lý xong.
- **Lưu trữ Log:** Lưu thông tin tiêu đề meeting, link Google Docs vào Google Sheets để làm biên bản tổng hợp hàng tuần/tháng.
- **Tùy chỉnh Prompt cho AI:** Các sếp có thể tinh chỉnh prompt trong Agent để AI viết tóm tắt theo văn phong riêng của công ty (trang trọng, ngắn gọn hoặc theo dạng bullet points chi tiết).

### 📌 Kết luận
Việc tự động hóa tóm tắt cuộc họp Zoom với GPT-4o và Google Docs không chỉ giúp tiết kiệm hàng chục giờ làm việc mỗi tháng mà còn nâng cao tính chuyên nghiệp trong quy trình vận hành của doanh nghiệp. Hãy "lên đồ" và áp dụng ngay hôm nay các sếp nhé!