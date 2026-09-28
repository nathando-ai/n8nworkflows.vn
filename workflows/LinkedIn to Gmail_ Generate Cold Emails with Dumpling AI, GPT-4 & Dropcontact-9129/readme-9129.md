---
title: "🚀 Tự động hóa chiến dịch Cold Email từ LinkedIn Profile với Dumpling AI, GPT-4 và Dropcontact"
description: "Biến một URL LinkedIn thành chuỗi Cold Email cá nhân hóa siêu tốc bằng AI, tự động tìm email, soạn nội dung và gửi qua Gmail."
slug: "tu-dong-hoa-cold-email-tu-linkedin-profile-ai"
tags: [n8n, automation, no-code, linkedin, ai, open-ai, cold-email]
keywords: [n8n workflow, tự động hóa cold email, linkedin to email, gpt-4 cold email, dropcontact, dumpling ai]
---

# 🚀 Tự động hóa chiến dịch Cold Email từ LinkedIn Profile với Dumpling AI, GPT-4 và Dropcontact

Các sếp có đang tốn hàng giờ mỗi ngày để "soi" profile LinkedIn của khách hàng tiềm năng, tìm kiếm email của họ, sau đó vắt óc viết từng email chào hàng (Cold Email) mang tính cá nhân hóa? Công việc thủ công này cực kỳ tốn thời gian mà tỷ lệ phản hồi lại không cao.

Đừng lo, bài toán này sẽ được giải quyết triệt để với workflow n8n tự động hóa 100%. Chỉ cần nhập URL LinkedIn, hệ thống sẽ tự động phân tích công ty, tìm email chính xác, dùng GPT-4 viết email chuẩn "thôi miên" khách hàng, gửi đi qua Gmail và lưu toàn bộ log vào Airtable!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%**: Biến thao tác nghiên cứu lead thủ công thành một cú click form đơn giản.
- **Cá nhân hóa đỉnh cao**: GPT-4 kết hợp dữ liệu từ Dumpling AI tạo ra nội dung email cực kỳ sát với ngữ cảnh của khách hàng mục tiêu.
- **Tìm kiếm lead thông minh**: Dropcontact tự động khai thác thông tin liên hệ và email chính xác.
- **Quản lý chuyên nghiệp**: Tự động đồng bộ và lưu trữ toàn bộ dữ liệu lead, nội dung email vào Airtable để theo dõi chuyển đổi.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị sẵn các tài khoản và API Keys sau:
- Tài khoản **n8n** (Cloud hoặc Self-hosted).
- Tài khoản **Dumpling AI** (lấy API Key cho node HTTP Request).
- Tài khoản **Dropcontact** (lấy API Key).
- Tài khoản **OpenAI** (có sẵn số dư để dùng GPT-4).
- Tài khoản **Gmail** (cấp quyền OAuth2 để gửi email).
- Tài khoản **Airtable** (tạo sẵn Base/Table để lưu log lead).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và paste trực tiếp vào n8n Editor của mình, hoặc tải file JSON về và chọn **Import from File** trong giao diện n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 6 nodes chính, các sếp cần cấu hình kỹ các điểm sau để chạy không lỗi:

- **Trigger on LinkedIn Profile Submission (`formTrigger`)**: 
  - Đây là điểm bắt đầu dưới dạng một Web Form. Các sếp có thể mở node này để lấy link Form công khai, nơi khách hàng hoặc đội ngũ sales sẽ điền URL LinkedIn của lead.
- **Extract Company Info (Dumpling AI) (`httpRequest`)**: 
  - Cấu hình Authentication kiểu `Header Auth` với API Key của Dumpling AI để hệ thống cào dữ liệu từ profile và công ty của lead.
- **Enrich Contact (Dropcontact) (`dropcontact`)**: 
  - Kết nối credentials của Dropcontact để hệ thống tự động bóc tách tên, domain và tìm email chính xác của nhân sự mục tiêu.
- **Generate Cold Email (GPT-4) (`openAi`)**: 
  - Chọn credentials `OpenAI API`. Tại đây, các sếp có thể tinh chỉnh Prompt trong node để GPT-4 viết email theo văn phong (Tone of voice) phù hợp nhất với sản phẩm/dịch vụ của công ty mình.
- **Send Cold Email via Gmail (`gmail`)**: 
  - Kết nối tài khoản Gmail cá nhân hoặc Workspace qua `Gmail OAuth2`. Đảm bảo mapping đúng trường email nhận được từ Dropcontact và nội dung tiêu đề/thân bài từ GPT-4.
- **Log Lead to Airtable (`airtable`)**: 
  - Chọn credentials `Airtable Token API`, trỏ tới Base và Table tương ứng để lưu lại thông tin: URL LinkedIn, Email, Nội dung email đã gửi và Trạng thái.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và test thử bằng một URL LinkedIn thật trên Form.
- Kiểm tra kết quả ở Gmail xem email đã được gửi đi chưa và check lại Airtable xem dữ liệu đã được ghi nhận đầy đủ chưa.
- Nếu mọi thứ mượt mà, gạt công tắc sang **Active** để hệ thống tự động hóa 24/7!

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh thông báo**: Thêm một node Slack hoặc Telegram ngay sau node gửi Gmail để báo cáo về team sales ngay khi có một Cold Email được gửi đi thành công.
- **Thêm bước kiểm duyệt (Human-in-the-loop)**: Thay vì tự động gửi thẳng qua Gmail, các sếp có thể dùng node `Wait` hoặc tạo một Approval Flow để duyệt nội dung AI viết trước khi gửi.
- **Mở rộng lưu trữ**: Thay vì Airtable, các sếp có thể đồng bộ lead thẳng về Google Sheets, HubSpot hoặc Notion tùy thuộc vào CRM đang sử dụng.

### 📌 Kết luận
Với workflow n8n này, việc tiếp cận khách hàng tiềm năng qua LinkedIn và Cold Email chưa bao giờ dễ dàng và chuyên nghiệp đến thế. Hãy áp dụng ngay để tối ưu hóa năng suất đội ngũ Sales của các sếp ngay hôm nay!