---
title: "🚀 Tự động quét và làm giàu dữ liệu tên miền với Hunter.io và Google Sheets trong n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa việc lấy danh sách domain từ Google Sheets, quét email và thông tin liên hệ qua Hunter.io và lưu kết quả ngược lại Google Sheets."
slug: "tu-dong-lam-giay-du-lieu-ten-mien-hunter-io-google-sheets"
tags: [n8n, automation, lead-generation, hunter-io, google-sheets, no-code]
keywords: [n8n workflow, hunter.io n8n, google sheets automation, lam giay du lieu lead, tim email theo domain]
---

# 🚀 Tự động quét và làm giàu dữ liệu tên miền với Hunter.io và Google Sheets

Các sếp có đang tốn hàng giờ đồng hồ để copy từng tên miền website, tra cứu thủ công trên các công cụ tìm kiếm email để tìm kiếm khách hàng tiềm năng (leads)? Công việc lặp đi lặp lại này không chỉ tốn thời gian mà còn dễ gây nhàm chán cho đội ngũ sales và marketing.

Giải pháp là đây! Workflow n8n này sẽ tự động hóa 100% quy trình: Đọc danh sách tên miền từ Google Sheets -> Gửi sang Hunter.io để trích xuất email và thông tin liên lạc -> Tự động lưu toàn bộ dữ liệu đã "làm giàu" (enriched data) trở lại Google Sheets. Các sếp chỉ cần ngồi nhâm nhi ly cà phê và chờ danh sách khách hàng chất lượng đổ về!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Thay vì tra cứu thủ công từng domain, hệ thống xử lý hàng loạt trong tích tắc.
- **Dữ liệu chính xác:** Khai thác kho dữ liệu chất lượng cao từ Hunter.io giúp chiến dịch Email Outreach đạt tỷ lệ inbox cao hơn.
- **Tự động hóa liền mạch:** Đồng bộ dữ liệu 2 chiều trực tiếp lên Google Sheets mà không cần thao tác thủ công.
- **Dễ dàng mở rộng:** Có thể thay thế trigger thủ công bằng lịch trình chạy tự động hàng ngày.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Cloud hoặc Self-hosted).
- Tài khoản **Google Sheets** (chuẩn bị sẵn file nguồn chứa danh sách domain và file đích nhận dữ liệu).
- Tài khoản **Hunter.io** và lấy **API Key**.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng file JSON của workflow này, copy và paste trực tiếp vào màn hình n8n Editor của mình. Workflow gồm 4 nodes cơ bản nhưng cực kỳ mạnh mẽ.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru, các sếp cần cấu hình chính xác các node sau:

- **When Manually Triggered (`manualTrigger`):** Node kích hoạt thủ công. Các sếp có thể thay thế bằng *Schedule Trigger* nếu muốn chạy tự động theo lịch định kỳ.
- **Read Domains from Sheets (`googleSheets`):** 
  - Kết nối tài khoản thông qua `googleSheetsOAuth2Api`.
  - Trỏ tới file Google Sheets nguồn (Các sếp có thể tham khảo [Google Sheets Template mẫu tại đây](https://docs.google.com/spreadsheets/d/180ca70GWcm-BpM8U2ygS6jqhCTE_avx93Kd4d0USe5A)).
  - Chọn đúng Sheet Name chứa cột danh sách các tên miền (Domain URLs).
- **Find Emails via Hunter (`hunter`):**
  - Kết nối credentials bằng **Hunter API Key**.
  - Cấu hình kiểu tìm kiếm (Domain search hoặc Email finder) dựa trên dữ liệu đầu vào từ Google Sheets.
- **Append Exported Data to Sheets (`googleSheets`):**
  - Sử dụng chung hoặc kết nối tài khoản Google Sheets OAuth2.
  - Chọn file Google Sheets đích và tiến hành mapping các cột dữ liệu trả về từ Hunter.io (Email, First Name, Last Name, Position,...) vào đúng các cột tương ứng trên Sheet.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thử với một vài dòng dữ liệu mẫu xem hệ thống đã map đúng cột hay chưa.
- Sau khi kiểm tra dữ liệu trả về chính xác, gạt công tắc sang **Active** để đưa workflow vào trạng thái vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm Filter Node:** Đặt thêm một node `If` hoặc `Filter` ngay sau node Hunter.io để lọc ra các dòng tìm thấy email hợp lệ trước khi ghi vào Google Sheets, giúp tiết kiệm dung lượng bảng tính.
- **Tích hợp Slack/Telegram:** Thêm thông báo qua tin nhắn mỗi khi quá trình quét hoàn tất để đội ngũ sales nắm bắt tiến độ.
- **Kết nối CRM:** Thay vì ghi vào Google Sheets ở bước cuối, các sếp có thể đẩy thẳng thông tin liên hệ này vào HubSpot, Pipedrive hoặc Notion.

### 📌 Kết luận
Tự động hóa quy trình làm giàu dữ liệu (Data Enrichment) chưa bao giờ dễ dàng đến thế với n8n và Hunter.io. Hãy áp dụng ngay hôm nay để tối ưu hóa hiệu suất làm việc cho đội ngũ kinh doanh của các sếp!