---
title: "🚀 Tự động hóa quy trình Lead Enrichment với Leadfeeder, Apollo và Google Sheets qua n8n"
description: "Hướng dẫn xây dựng hệ thống tự động quét khách hàng ghé thăm website từ Leadfeeder, làm giàu thông tin qua Apollo và lưu trữ trực tiếp vào Google Sheets hoàn toàn tự động."
slug: "tu-dong-hoa-lead-enrichment-leadfeeder-apollo-google-sheets"
tags: [n8n, automation, lead-generation, apollo, leadfeeder, google-sheets]
keywords: [n8n workflow, lead enrichment, leadfeeder, apollo io, google sheets automation, tự động hóa bán hàng]
---

# 🚀 Xây dựng hệ thống Lead Enrichment tự động: Leadfeeder kết hợp Apollo & Google Sheets

Các sếp có bao giờ cảm thấy mệt mỏi khi mỗi ngày phải thủ công tra cứu thông tin những công ty truy cập vào website của mình trên Leadfeeder, sau đó lại lọ mọ tìm kiếm thông tin người ra quyết định trên Apollo.io và copy-paste vào Google Sheets? Công việc lặp đi lặp lại này không chỉ tốn hàng giờ đồng hồ mà còn khiến đội ngũ sales bỏ lỡ "thời điểm vàng" để tiếp cận khách hàng tiềm năng.

Đừng lo, bài toán này sẽ được giải quyết triệt để với workflow n8n cực kỳ mạnh mẽ mang tên **Lead Enrichment Pipeline**. Hệ thống này sẽ tự động hóa từ A-Z: lấy danh sách công ty ghé thăm web, phân trang dữ liệu thông minh, làm giàu thông tin liên hệ (email, số điện thoại, chức vụ) qua Apollo và lưu trữ gọn gàng vào Google Sheets mỗi sáng!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 100% mỗi ngày:** Chạy tự động lúc 9 giờ sáng mà không cần sự can thiệp thủ công.
- **Làm giàu data chuyên sâu:** Kết hợp sức mạnh của Leadfeeder (nhận diện khách truy cập web) và Apollo.io (tìm kiếm thông tin contact chất lượng).
- **Quản lý tập trung:** Toàn bộ thông tin lead nóng hổi được đổ thẳng về Google Sheets, sẵn sàng cho đội sales gọi điện hoặc gửi email.
- **Giám sát lỗi thông minh:** Tích hợp Telegram Alert để báo cáo ngay lập tức nếu có sự cố xảy ra trong quá trình chạy.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản Leadfeeder (Visitors API):** Lấy API Key/Account ID.
- **Tài khoản Apollo.io:** Lấy API Key để thực hiện việc enrich dữ liệu.
- **Google Sheets:** Chuẩn bị sẵn một file Google Sheet để lưu trữ leads.
- **Telegram Bot:** (Tùy chọn) Để nhận thông báo lỗi qua Telegram.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow (hoặc tải file từ nguồn gốc) và dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node cốt lõi sau:

- **Daily Trigger (9 AM):** Node `scheduleTrigger` đặt lịch chạy định kỳ vào 9 giờ sáng mỗi ngày. Các sếp có thể thay đổi khung giờ tùy thuộc vào múi giờ của doanh nghiệp.
- **Fetch Leadfeeder Account ID & Retrieve Lead Data (Leadfeeder):** Node `httpRequest` yêu cầu cấu hình Header chứa API Key của Leadfeeder để lấy danh sách các công ty truy cập website.
- **Pagination Controller & Generate Pagination Sequence:** Các node `code` và `splitInBatches` giúp xử lý dữ liệu lớn bằng cách phân trang, tránh tình trạng quá tải hoặc vượt quá giới hạn API.
- **Enrich With Apollo (Last Page) & (Full Page):** Node `httpRequest` gọi đến API của Apollo.io. Các sếp cần điền Apollo API Key vào phần Header Authentication.
- **Save Leads to Google Sheets (Last Page) & (Full Page):** Node `googleSheets` kết nối với tài khoản Google của sếp, chọn đúng file Sheet và Sheet Name đã chuẩn bị sẵn để ghi dữ liệu.
- **Rate Limit Delay (40s):** Node `wait` cực kỳ quan trọng để "hãm phanh" giữa các request, giúp tránh việc bị Apollo hoặc Leadfeeder chặn do vượt quá giới hạn gọi API (Rate Limit).
- **Send Alert đến Telegram:** Node `telegram` kết nối với Bot Token và Chat ID của sếp để nhận thông báo khẩn cấp nếu có lỗi phát sinh (được kích hoạt bởi `errorTrigger` và `Format Error Report`).

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử với dữ liệu mẫu và kiểm tra xem dữ liệu đã đổ về Google Sheets chưa.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để workflow tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp CRM:** Thay vì chỉ lưu Google Sheets, các sếp có thể nối thêm node đẩy thẳng dữ liệu lead vào HubSpot, Salesforce hoặc ActiveCampaign.
- **Gửi thông báo Lead nóng:** Thêm node Telegram hoặc Slack để bắn thông báo ngay khi có một lead chất lượng cao được làm giàu xong, giúp đội sales tiếp cận khách hàng chỉ sau vài phút họ ghé web.
- **Mở rộng lọc dữ liệu:** Tận dụng node `if` để chỉ enrich những công ty đạt tiêu chuẩn về quy mô nhân sự hoặc ngành nghề cụ thể.

### 📌 Kết luận
Workflow **Lead Enrichment Pipeline** là một "vũ khí" hạng nặng giúp tối ưu hóa quy trình Sales Prospecting, tiết kiệm hàng chục giờ làm việc thủ công mỗi tuần. Hãy thiết lập ngay hôm nay để biến lượng traffic truy cập website thành danh sách khách hàng tiềm năng chất lượng cao!