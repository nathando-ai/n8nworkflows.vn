---
title: "🚀 Tự động tạo câu mở đầu Cold Email cá nhân hóa bằng Website Scraping, Claude & GPT-4"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa việc cào dữ liệu website khách hàng tiềm năng, kết hợp AI thông minh để viết email cá nhân hóa và cập nhật Google Sheets."
slug: "tu-dong-tao-cold-email-ca-nhan-hoa-voi-claude-gpt4-n8n"
tags: [n8n, automation, ai-agent, claude, gpt4, cold-email, lead-generation]
keywords: [n8n workflow, cold email automation, website scraping, AI agent claude gpt4, google sheets automation]
---

# 🚀 Tự động tạo câu mở đầu Cold Email cá nhân hóa với Claude & GPT-4

Các sếp làm sales, marketing chắc chắn đều hiểu cảm giác "nản" thế nào khi phải ngồi thủ công lướt qua hàng trăm website của khách hàng tiềm năng, đọc bài viết gần nhất hoặc tìm hiểu về dịch vụ của họ chỉ để viết ra một câu mở đầu (opener) thật hay, thật trúng tâm lý nhằm tăng tỷ lệ phản hồi (response rate) cho chiến dịch Cold Email. Việc này vừa tốn thời gian, vừa khó scale (mở rộng quy mô) đội ngũ.

Đừng lo, workflow n8n được thiết kế bởi chuyên gia Mariela Slavenova sẽ giải quyết triệt để bài toán này cho các sếp. Hệ thống sẽ tự động theo dõi file danh sách lead trên Google Drive, cào dữ liệu (scraping) từ website của từng khách hàng, giao cho AI Agent phân tích và viết câu mở đầu cực kỳ cá nhân hóa, sau đó tự động lưu kết quả vào Google Sheets và bắn thông báo qua Telegram khi hoàn thành!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không sợ gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Chỉ cần thả file danh sách lead vào Google Drive, phần việc còn lại để AI lo.
- **Cá nhân hóa sâu sắc:** AI tự động đọc website doanh nghiệp mục tiêu (qua Jina AI & AI Agent) để tìm ra "nỗi đau" hoặc điểm nhấn độc đáo, giúp câu mở đầu cold email cực kỳ tự nhiên và thuyết phục.
- **Linh hoạt xử lý:** Tự động nhận biết lead nào có website hay không có website để chia nhánh xử lý thông minh (qua node `If`).
- **Báo cáo tức thì:** Nhận thông báo trực tiếp qua Telegram ngay khi toàn bộ quá trình xử lý lead hoàn tất.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI "LÊN ĐỒ"]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google Drive & Google Sheets** (Để lưu trữ và cập nhật danh sách lead).
- **Anthropic API Key** (Dùng cho mô hình Claude Sonnet 4).
- **OpenAI API Key** (Dùng cho node OpenAI).
- **Telegram Bot Token** (Để nhận thông báo hoàn thành).
- **Jina AI API** (Hoặc API key tương ứng cho HTTP Header Auth dùng ở node cào dữ liệu).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này, vào giao diện n8n Editor chọn **Add workflow** -> Click vào dấu ba chấm (...) ở góc trên bên phải -> Chọn **Import from Clipboard** và dán vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà không lỗi, các sếp nhớ cấu hình kỹ các node sau:

- **Google Drive Trigger & Google Drive_DownLoad**: Kết nối tài khoản Google Drive của sếp và chỉ định thư mục/file chứa danh sách lead đầu vào (dạng file Excel/CSV).
- **Google Sheet Parse & Google Sheets**: Thiết lập kết nối tài khoản Google Sheets. Đảm bảo cấu trúc cột trong file khớp với cấu hình cập nhật ở node `Google Sheets` (đặc biệt là cột lưu kết quả câu mở đầu email).
- **Anthropic Chat Model (1, 2, 3)**: Điền *Anthropic API Credentials* và xác nhận model đang chọn là `claude-sonnet-4-20250514`.
- **OpenAI1**: Điền *OpenAI API Credentials* cho node OpenAI.
- **Fetch Markdown via Jina AI1**: Cấu hình HTTP Header Auth cho dịch vụ cào nội dung website dưới dạng markdown.
- **Lead Enrichment is ready**: Kết nối *Telegram API Credentials* và điền Chat ID của sếp để nhận tin nhắn báo cáo.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (**Execute Workflow**) với một vài dòng dữ liệu mẫu trong file Google Drive để kiểm tra kết quả trả về.
- Sau khi thấy mọi thứ chạy trơn tru, hãy bật công tắc **Active** ở góc trên bên phải để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm CRM:** Thay vì chỉ lưu vào Google Sheets, các sếp có thể đổi node ghi dữ liệu thành HubSpot, Salesforce hoặc Close CRM để đồng bộ lead thẳng vào hệ thống sales.
- **Thêm bước duyệt qua Slack/Telegram:** Thay vì tự động gửi email ngay, hãy thêm bước gửi đoạn opener vừa tạo vào một kênh chat nhóm để nhân viên sales review nhanh trước khi chiến dịch bắt đầu.
- **Mở rộng nguồn Lead:** Kết hợp thêm các node trigger từ LinkedIn Automation hoặc Webhook để tự động thêm lead mới vào hệ thống mà không cần dùng Google Drive.

### 📌 Kết luận
Workflow tạo Cold Email cá nhân hóa bằng AI này là vũ khí cực kỳ mạnh mẽ giúp đội ngũ sales của các sếp tối ưu hóa thời gian, tăng tỷ lệ chuyển đổi mà không cần tốn nhiều nhân lực nghiên cứu thủ công. Hãy cài đặt ngay hôm nay để bứt phá doanh thu cho các chiến dịch Outbound Sales!