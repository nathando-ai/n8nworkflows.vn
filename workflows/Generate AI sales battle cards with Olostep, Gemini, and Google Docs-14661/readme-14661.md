---
title: "🚀 Tự động tạo Sales Battle Card bằng AI với Olostep, Gemini và Google Docs"
description: "Hướng dẫn xây dựng workflow n8n tự động nghiên cứu khách hàng, phân tích bằng Google Gemini và tạo bộ tài liệu sales battle card chuyên nghiệp lưu trực tiếp trên Google Docs."
slug: "tao-sales-battle-card-tu-dong-voi-ai-olostep-gemini-google-docs"
tags: [n8n, automation, ai, google-gemini, sales-automation, google-docs]
keywords: [n8n workflow, sales battle card, olostep scrape, google gemini ai, tu dong hoa ban hang]
---

# 🚀 Tự động tạo Sales Battle Card bằng AI với Olostep, Gemini và Google Docs

Các sếp có bao giờ cảm thấy mệt mỏi khi phải tốn hàng giờ đồng hồ nghiên cứu từng khách hàng tiềm năng, lướt website của họ, tìm kiếm tin tức, sau đó vắt óc suy nghĩ cách tiếp cận (cold email), câu hỏi khám phá (discovery questions) và cách xử lý từ chối? Việc làm thủ công này vừa tốn thời gian, vừa khó scale, dẫn đến các chiến dịch outbound kém hiệu quả.

Đừng lo, bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ mạnh mẽ do tác giả **Yasser Sami** thiết kế. Workflow này sẽ tự động hóa 100% quy trình: **Nghiên cứu đối thủ/khách hàng bằng Olostep -> Phân tích & Tạo chiến lược bằng Google Gemini AI -> Đóng gói thành tài liệu Google Docs chuyên nghiệp** chỉ với một vài cú click điền form.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Biến quá trình nghiên cứu và viết tài liệu sales từ 1 tiếng xuống còn chưa đầy 2 phút.
- **Cá nhân hóa sâu sắc:** Dữ liệu nghiên cứu lấy trực tiếp từ tin tức thời gian thực và nội dung website của khách hàng qua Olostep.
- **Vũ khí bán hàng toàn diện:** Tự động tạo hook tiếp cận, câu hỏi chốt sale, phương án xử lý từ chối (objection handling) và tóm tắt chiến lược.
- **Lưu trữ gọn gàng:** Tự động chuyển đổi Markdown thành file HTML, đẩy lên Google Drive và convert trực tiếp thành Google Docs sẵn sàng chia sẻ cho team.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Cloud hoặc Self-hosted.
- **Olostep API Key:** Dùng cho các node scrape và nghiên cứu công ty.
- **Google Gemini API Key (hoặc Google Palm API):** Để AI phân tích và viết nội dung pitch.
- **Google Drive / Google Docs OAuth2 Credentials:** Để tạo file, chia sẻ tài liệu và dọn dẹp file tạm.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow (hoặc tải template từ n8n.io), sau đó Paste trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà không lỗi, các sếp cần cấu hình kỹ các node sau:

- **On form submission:** Node dạng Form Trigger. Tại đây, các sếp có thể tùy chỉnh các trường đầu vào như Tên công ty, Website URL và Giá trị cốt lõi (Value Proposition) của sản phẩm bên mình để AI có dữ liệu khớp lệnh chính xác.
- **Company research & Scrape company website (Olostep nodes):** Cần kết nối `olostepScrapeApi` credentials để hệ thống bắt đầu quét tin tức, xu hướng tuyển dụng và nội dung trang web của mục tiêu.
- **Research Analyzer, Pitch Assets generator & Sales battle card generator (Google Gemini nodes):** Kết nối tài khoản Google AI (Gemini). Các sếp nhớ kiểm tra lại các prompt trong node để đảm bảo AI hiểu đúng văn phong và yêu cầu của sản phẩm bên mình.
- **Transfer HTML to Doc, Upload html file, Share link & email, Delete html file (Google Drive nodes):** Cần cấu hình OAuth2 cho Google Drive. Workflow sẽ thực hiện cơ chế thông minh: Chuyển dữ liệu từ Markdown sang HTML qua node **Generate HTML Binary File**, upload file HTML lên Google Drive để hệ thống Google tự động convert sang Google Docs, chia sẻ quyền truy cập và tự động **Delete html file** cũ để dọn rác bộ nhớ.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng cách điền form mẫu.
- Kiểm tra kết quả trên Google Drive và hộp thư đến xem tài liệu đã sẵn sàng chưa.
- Sau khi test ngon lành, hãy bật công tắc **Active** góc trên cùng bên phải để đưa workflow vào hoạt động chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp CRM:** Nối thêm node HubSpot hoặc Salesforce sau phần tạo Battle Card để tự động lưu thông tin nghiên cứu vào hồ sơ Deal/Company.
- **Đa dạng hóa kênh thông báo:** Thay vì chỉ gửi email, các sếp có thể cấu hình thêm node Slack hoặc Telegram để bắn thông báo ngay khi có Battle Card mới cho đội ngũ Sales nắm bắt "nóng".
- **Lưu trữ Notion:** Thêm node Notion để lưu trữ bộ sưu tập Sales Battle Card thành một cơ sở tri thức (Knowledge Base) cho toàn công ty.

### 📌 Kết luận
Với workflow n8n kết hợp giữa Olostep và Google Gemini này, việc chuẩn bị tài liệu bán hàng cho các cuộc họp cold outreach lớn sẽ trở nên tự động và chuyên nghiệp hơn bao giờ hết. Hãy setup ngay hôm nay để tối ưu hóa đội ngũ sales của các sếp!