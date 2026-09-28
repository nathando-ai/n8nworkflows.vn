---
title: "🚀 Tự động hóa chuỗi chăm sóc khách hàng LinkedIn với Linked API và Google Sheets"
description: "Xây dựng hệ thống outreach LinkedIn tự động 100% không cần code: gửi lời mời kết nối, theo dõi trạng thái, gửi tin nhắn follow-up và đồng bộ dữ liệu vào Google Sheets."
slug: "tu-dong-hoa-linkedin-outreach-linked-api-google-sheets"
tags: [n8n, automation, no-code, linkedin, lead-nurturing, google-sheets]
keywords: [n8n workflow, tự động hóa linkedin, linked api, google sheets automation, lead nurturing b2b]
---

# 🚀 Tự động hóa chuỗi chăm sóc khách hàng LinkedIn với Linked API và Google Sheets

Các sếp có đang tốn hàng giờ mỗi ngày để copy-paste thủ công trên LinkedIn: gửi lời mời kết nối, kiểm tra xem khách hàng đã đồng ý chưa, rồi lại nhớ nhớ quên quên để gửi tin nhắn chào hàng và tin nhắn follow-up (nhắn lại)? Việc làm thủ công này không chỉ cực kỳ tốn thời gian mà còn dễ bỏ sót khách hàng tiềm năng (leads) béo bở.

Workflow n8n chuyên nghiệp này sẽ giải quyết triệt để nỗi đau đó! Hệ thống tự động hóa toàn bộ quy trình chăm sóc khách hàng (Outreach & Lead Nurturing) trên LinkedIn dựa trên dữ liệu từ Google Sheets, giúp các sếp scale-up chiến dịch Sales B2B mà không cần tốn tiền thuê thêm nhân sự vận hành thủ công.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 100% quy trình phễu LinkedIn:** Từ gửi lời mời kết nối (`NEW`), kiểm tra trạng thái (`PENDING`), gửi tin nhắn đầu tiên (`CONNECTED`) đến gửi chuỗi tin nhắn chăm sóc (`AWAITING_REPLY`).
- **Đồng bộ hóa dữ liệu thời gian thực:** Mọi thay đổi trạng thái của lead đều được cập nhật tự động vào Google Sheets.
- **Kiểm soát giới hạn an toàn (Daily Limit):** Tích hợp tính năng giới hạn số lượng lời mời kết nối mỗi ngày, giúp tài khoản LinkedIn tránh bị quét/spam.
- **Vận hành liên tục 24/7:** Chạy ngầm định kỳ mỗi 2 hours, các sếp chỉ việc ngồi chờ khách phản hồi (REPLIED) hoặc từ chối (DECLINED).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Google Drive / Google Sheets** để lưu trữ danh sách leads.
- **Tài khoản Linked API** (Lấy API Key tại [app.linkedapi.io](https://app.linkedapi.io)).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy toàn bộ JSON từ n8n.
- Mở n8n Editor, chọn **Add workflow** -> Click vào menu dấu ba chấm ở góc trên bên phải -> Chọn **Import from File** hoặc **Import from Clipboard** và dán mã JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình các thành phần quan trọng sau:

- **Google Sheets Credentials & Template:** 
  - Kết nối node `📥 Get All Leads` và các node `💾 Update Sheet (...)` với tài khoản Google Sheets OAuth2 của bạn.
  - Hãy copy [Google Sheet template mẫu tại đây](https://docs.google.com/spreadsheets/d/141fJskisAQ7H8AxtojQ7LZrnd14EOyB26RdDq5aczEU/copy) để đảm bảo cấu trúc cột đồng bộ với workflow.
- **Linked API Credentials:** 
  - Cấu hình API Key cho các node thao tác với LinkedIn (`Send connection request`, `Check connection status`, `Send message`, `Poll conversations`,...).
- **Cấu hình thông số trong node `⚙️ Config`:**
  - `DOCUMENT_LINK`: URL của file Google Sheet chứa danh sách leads của bạn.
  - `SHEET_NAME`: Tên tab chứa leads (mặc định là `Leads`).
  - `DAILY_CONNECTION_LIMIT`: Số lượng kết nối tối đa mỗi ngày (mặc định: `25`).
  - Các thông số về thời gian chờ (`HOURS_TO_CHECK_IF_CONNECTION_ACCEPTED`, `HOURS_DELAY_AFTER_CONNECTION_ACCEPTED`, `DAYS_DELAY_BETWEEN_MESSAGES`,...). Tùy chỉnh theo chiến lược chăm sóc của team.

#### 3. Kích hoạt ⚡️
- Thêm một vài dòng dữ liệu mẫu vào Google Sheet với `Status = NEW` và điền nội dung vào các cột `Message 1/2/3`.
- Bấm nút **Execute Workflow** để test thử nghiệm vòng lặp đầu tiên.
- Nếu mọi thứ hoạt động trơn tru, hãy bật công tắc **Active** ở góc trên bên phải để workflow tự động chạy ngầm mỗi 2 tiếng.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo Telegram/Slack:** Thêm node Telegram ngay sau nhánh `💾 Update Sheet (REPLIED)` để nhận thông báo tức thì khi có khách hàng đồng ý trò chuyện.
- **Lưu log lỗi chi tiết:** Sử dụng Error Trigger để bắt các lỗi kết nối API LinkedIn và gửi cảnh báo về email hoặc kênh chat nội bộ.
- **Mở rộng kịch bản:** Tích hợp thêm AI (OpenAI/Claude Node) để tự động cá nhân hóa nội dung tin nhắn dựa trên profile LinkedIn của lead trước khi gửi.

### 📌 Kết luận
Tự động hóa LinkedIn Outreach chưa bao giờ dễ dàng và tối ưu đến thế. Hãy triển khai ngay template này để giải phóng thời gian cho đội ngũ Sales, tập trung vào việc chốt hợp đồng thay vì làm tay chân!