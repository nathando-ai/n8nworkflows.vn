---
title: "🚀 Tự động hóa cá nhân hóa Lead LinkedIn với Google Drive, Apify và AI"
description: "Hướng dẫn xây dựng workflow n8n tự động cào dữ liệu profile và bài viết LinkedIn gần nhất của khách hàng tiềm năng, sau đó sử dụng Claude AI để tạo nội dung tiếp cận (outreach) cực kỳ cá nhân hóa."
slug: "tu-dong-hoa-ca-nhan-hoa-lead-linkedin-voi-google-drive-apify-va-ai"
tags: [n8n, automation, no-code, linkedin, ai-agent, apify, claude]
keywords: [n8n workflow, tu dong hoa linkedin, apify linkedin scraper, claude ai outreach, ca nhan hoa lead, google drive trigger]
---

# 🚀 Tự động hóa cá nhân hóa Lead LinkedIn với Google Drive, Apify & AI

Các sếp có bao giờ cảm thấy mệt mỏi khi phải thủ công truy cập vào từng profile LinkedIn của khách hàng tiềm năng, đọc bài viết của họ, rồi vắt óc nghĩ ra câu mở đầu thật tự nhiên để nhắn tin (outreach) không? Công việc này cực kỳ tốn thời gian nhưng lại quyết định tỷ lệ phản hồi (response rate).

Đừng lo, workflow n8n được thiết kế bởi chuyên gia *Mariela Slavenova* này sẽ giải quyết triệt để nỗi đau đó! Workflow này sẽ tự động hóa toàn bộ quy trình: từ việc phát hiện file danh sách lead mới trên **Google Drive**, cào dữ liệu profile và bài viết LinkedIn bằng **Apify**, cho đến việc dùng **Claude AI (Anthropic)** để phân tích và viết thông điệp cá nhân hóa sâu sắc, sau đó cập nhật lại vào **Google Sheets** và bắn thông báo qua **Telegram**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không còn phải lướt profile thủ công từng lead một.
- **Cá nhân hóa cực cao:** AI sẽ dựa vào bài đăng gần nhất trong 30 ngày qua của khách hàng để tạo ra lời mở đầu cực kỳ trúng "tử huyệt".
- **Thông minh đa nhánh:** Nếu khách hàng không có bài đăng gần đây, AI sẽ tự động chuyển sang phân tích thông tin tổng quan trên profile để tạo nội dung thay thế.
- **Hoạt động tự động 24/7:** Kích hoạt ngay khi có file danh sách lead mới được tải lên Google Drive và nhận thông báo qua Telegram khi hoàn thành.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để vận hành trơn tru, các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **n8n Instance** (Khuyên dùng bản Self-hosted trên VPS).
- **Google Drive & Google Sheets Account** (Để nhận file trigger và lưu kết quả).
- **Apify Account** (Dùng để cào dữ liệu profile và bài viết LinkedIn).
- **Anthropic API Key** (Dùng cho mô hình Claude Sonnet 4 cực mạnh về ngữ nghĩa).
- **OpenAI API Key** (Hỗ trợ phụ trợ nếu cần).
- **Telegram Bot Token** (Để nhận thông báo tiến độ).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này, vào giao diện n8n Editor, chọn **Add workflow** -> Nhấn tổ hợp `Ctrl + V` (hoặc `Cmd + V`) để dán toàn bộ các nodes lên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà không bị lỗi xác thực, các sếp cần cấu hình kỹ các node sau:

- **Google Drive Trigger1 & Google Drive_DownLoad1:** Kết nối tài khoản Google Drive qua `googleDriveOAuth2Api`. Chọn thư mục (Folder) chuyên dụng để chứa file danh sách lead định dạng Excel/CSV.
- **Google Sheet Parse & Google Sheets Update with Personalization:** Cấu hình credentials Google Sheets. Đảm bảo file Excel/CSV đầu vào có cột chứa đường dẫn LinkedIn Profile (LinkedIn URL) để các node cào dữ liệu hoạt động chính xác.
- **Colect LinkedIn Data & Scrape LinkedIn Profile Post:** Cấu hình kết nối tới dịch vụ Apify thông qua HTTP Request để gọi Actor cào thông tin profile và bài viết LinkedIn.
- **Anthropic Chat Model1 & Anthropic Chat Model3 (Claude Sonnet 4):** Cấu hình `anthropicApi`. Model được chỉ định là `claude-sonnet-4-20250514`. Đảm bảo tài khoản Anthropic của các sếp có đủ số dư (credits).
- **If the LN post is in the last 30 days:** Node điều kiện sử dụng `Date & Time` để kiểm tra xem bài viết gần nhất của lead có nằm trong vòng 30 ngày qua hay không.
- **AI Agent1 & AI Agent_Personalization_no LN post:** Hai AI Agent này sẽ xử lý hai kịch bản: Có bài viết gần đây (tập trung vào nội dung họ vừa chia sẻ) và Không có bài viết gần đây (tập trung vào tiểu sử, kinh nghiệm làm việc).
- **Lead Enrichment is ready:** Kết nối Telegram Bot Token và Chat ID của các sếp để nhận thông báo ngay khi hệ thống hoàn tất việc xử lý toàn bộ danh sách lead.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (Test workflow) với một file Google Drive chứa từ 1-2 dòng dữ liệu mẫu để kiểm tra xem dữ liệu có được trả về Google Sheets đầy đủ không.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải màn hình n8n để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp CRM:** Thay vì chỉ cập nhật lại Google Sheets, các sếp có thể thay thế node Google Sheets bằng node **HubSpot**, **Notion** hoặc **Pipedrive** để đẩy thẳng lead đã cá nhân hóa vào phễu bán hàng.
- **Gửi Email tự động:** Kết nối thêm node Gmail hoặc Resend ở cuối workflow để tự động gửi luôn email outreach ngay sau khi AI tạo xong nội dung.
- **Xử lý lỗi (Error Handling):** Thêm Error Trigger workflow để nếu Apify lỗi hoặc API Anthropic quá tải, hệ thống sẽ gửi cảnh báo về Telegram ngay lập tức.

### 📌 Kết luận
Việc cá nhân hóa outreach trên LinkedIn chưa bao giờ dễ dàng và thông minh đến thế nhờ sự kết hợp giữa n8n, Apify và Claude AI. Hãy triển khai ngay hôm nay để tối ưu hóa tỷ lệ chuyển đổi cho đội ngũ Sales của các sếp nhé!