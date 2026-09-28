---
title: "🚀 Tự động hóa tìm kiếm, làm giàu dữ liệu LinkedIn và gửi chuỗi Email chăm sóc khách hàng với n8n, Apify, Gemini & Google Sheets"
description: "Hướng dẫn chi tiết workflow n8n tự động cào profile LinkedIn bằng Apify, làm giàu thông tin, viết nội dung cá nhân hóa bằng Google Gemini và gửi chuỗi email outreach tự động qua Gmail."
slug: "tu-dong-hoa-linkedin-lead-gen-apify-gemini-gmail"
tags: [n8n, automation, no-code, lead-generation, apify, google-gemini, gmail]
keywords: [n8n workflow, cào dữ liệu linkedin, apify linkedin, google gemini n8n, tự động gửi email outreach, google sheets automation]
---

# 🚀 Tự động hóa tìm kiếm, làm giàu dữ liệu LinkedIn và gửi chuỗi Email chăm sóc khách hàng với n8n, Apify, Gemini & Google Sheets

Việc tìm kiếm khách hàng tiềm năng (Lead Generation) và outreach thủ công trên LinkedIn tốn rất nhiều thời gian của các đội ngũ Sales và Marketing: từ việc tìm profile, cào thông tin liên lạc, viết email chào hàng cá nhân hóa cho đến việc theo dõi lịch sử gửi email và chờ phản hồi. 

Workflow n8n mạnh mẽ này sẽ giải quyết triệt để bài toán trên bằng cách tự động hóa 100% quy trình: Tìm kiếm và cào profile LinkedIn qua **Apify**, làm giàu dữ liệu, sử dụng AI **Google Gemini** để viết email chăm sóc cực kỳ cá nhân hóa, và kích hoạt chuỗi **Gmail outreach** đa tầng có kiểm tra phản hồi thông minh.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không còn phải thủ công copy/paste profile hay gõ từng email outreach.
- **Dữ liệu luôn sạch & đồng bộ:** Mọi thông tin profile và trạng thái gửi email được quản lý chặt chẽ trong Google Sheets.
- **Cá nhân hóa bằng AI:** Google Gemini phân tích sâu thông tin profile để soạn nội dung email follow-up chuẩn sales, tỷ lệ chuyển đổi cao.
- **Hệ thống outreach tự động:** Gửi chuỗi 3 email theo lịch trình có kèm độ trễ (`Wait` nodes) và tự động ghi nhận phản hồi.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Apify Account:** Tài khoản và API Key để cào dữ liệu LinkedIn.
- **Google Account:** Kết nối Google Sheets API và Gmail API (OAuth2).
- **Google Gemini API Key:** Dành cho node AI Follow-Up Message Generator.
- **Template Google Sheets:** Chuẩn bị sẵn file Google Sheets (Tham khảo cấu trúc từ [Template mẫu](https://docs.google.com/spreadsheets/d/1JlFjEo7yhuHprDwa41kxogXsLTe02K3uUjFgjtumrzQ/edit?usp=sharing)).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Copy toàn bộ mã JSON của workflow này.
- Trong giao diện n8n Editor, chọn **Add workflow** -> Nhấn tổ hợp phím `Ctrl + V` (hoặc `Cmd + V`) để dán toàn bộ các node lên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình lần lượt các nhóm node sau trong workflow:
- **Nhóm Apify & HTTP Request (`Post Apify Search Request`, `Post LinkedIn Profile Enrichment`, `Post LinkedIn to Email API`):** Nhập Apify API Token hợp lệ vào phần Credentials hoặc Header của các HTTP Request nodes để gọi API cào dữ liệu LinkedIn.
- **Nhóm Google Sheets (`Read Input Leads`, `Append Profiles to Raw Sheet`, `Update Input Sheet Status`, v.v.):** Kết nối tài khoản Google Sheets OAuth2, sau đó trỏ chính xác đến file Google Sheet quản lý Leads của các sếp (đảm bảo đúng tên các cột như yêu cầu của template).
- **Node AI (`AI Follow-Up Message Generator`):** Chọn credentials cho Google Gemini và kiểm tra lại System Prompt để câu lệnh phù hợp với sản phẩm/dịch vụ của công ty các sếp.
- **Nhóm Gmail Outreach (`Send Initial Email via Gmail`, `Send Follow-Up Email 2`, `Send Final Follow-Up Email 3`):** Cấu hình tài khoản Gmail gửi đi (OAuth2) và thiết lập nội dung email, điều kiện kiểm tra phản hồi ở các node `If` liền kề.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (`Manual Outreach Starting Point`) với 1-2 dòng dữ liệu mẫu trong Google Sheets để kiểm tra luồng chạy từ cào dữ liệu đến gửi email.
- Sau khi test thành công không báo lỗi, bật công tắc **Active** góc trên cùng bên phải để workflow sẵn sàng vận hành.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo Real-time:** Thêm node Telegram hoặc Slack sau các bước gửi email thành công để đội ngũ sales nhận thông báo ngay khi có khách hàng tiềm năng phản hồi.
- **Quản lý Rate Limit:** Điều chỉnh thông số ở các node `Split In Batches` và `Wait` (ví dụ: giãn cách thời gian giữa các email) để tránh bị Gmail hoặc Apify quét spam/giới hạn request.
- **Mở rộng phễu lọc:** Thêm các điều kiện `If` thông minh để lọc ra các lead chất lượng cao nhất trước khi đưa vào tiến trình AI Gemini sinh nội dung.

### 📌 Kết luận
Workflow tự động hóa kết hợp giữa Apify, Google Gemini và Gmail này là vũ khí bí mật giúp các đội ngũ sales scale-up hoạt động outreach trên LinkedIn một cách chuyên nghiệp và hiệu quả nhất. Hãy áp dụng ngay để tối ưu hóa phễu kiếm khách hàng của doanh nghiệp các sếp!