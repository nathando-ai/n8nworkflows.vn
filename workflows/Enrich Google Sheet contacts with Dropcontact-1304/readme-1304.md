---
title: "🚀 Tự động làm giàu dữ liệu danh bạ Google Sheet với Dropcontact và Lemlist trên n8n"
description: "Hướng dẫn tự động hóa quy trình Sales & Marketing: lấy danh bạ từ Google Sheet, làm sạch và bổ sung thông tin qua Dropcontact, sau đó đẩy trực tiếp vào chiến dịch Lemlist."
slug: "tu-dong-lam-giau-du-lieu-google-sheet-voi-dropcontact-va-lemlist"
tags: [n8n, automation, no-code, sales, marketing, dropcontact, lemlist, google-sheets]
keywords: [n8n workflow, làm giàu dữ liệu, dropcontact lemlist, tự động hóa sales, google sheets automation]
---

# 🚀 Tự động làm giàu dữ liệu danh bạ Google Sheet với Dropcontact và Lemlist

Các sếp làm trong ngành Sales và Marketing chắc chắn đã quá quen thuộc với việc tốn hàng giờ đồng hồ để tìm kiếm, lọc và cập nhật thông tin liên hệ của khách hàng tiềm năng. Dữ liệu thô từ các file Google Sheet thường thiếu email doanh nghiệp, số điện thoại hoặc chức danh chính xác, khiến việc outreach mất hiệu quả.

Giải pháp là gì? Hãy để n8n lo! Workflow tuyệt vời này sẽ giúp các sếp tự động hóa 100% quy trình: lấy danh bạ từ **Google Sheets**, gửi sang **Dropcontact** để làm giàu và làm sạch dữ liệu, rồi đồng bộ thẳng vào chiến dịch cold email trên **Lemlist** mà không cần đụng tay vào một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không còn phải tra cứu thủ công từng dòng thông tin khách hàng.
- **Dữ liệu siêu chuẩn:** Dropcontact tự động tìm kiếm email chuyên nghiệp, tên, họ, website công ty một cách hợp pháp (chuẩn GDPR).
- **Chiến dịch liền mạch:** Đẩy thẳng lead đã được "làm giàu" vào Lemlist để bắt đầu chiến dịch nuôi dưỡng ngay lập tức.
- **Hoạt động linh hoạt:** Dễ dàng trigger bằng tay hoặc lên lịch chạy tự động định kỳ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API sau:
- Tài khoản **n8n** (Cloud hoặc Self-hosted).
- Tài khoản **Google Sheets** có sẵn một bảng tính chứa danh sách thông tin khách hàng thô (Tên, Họ, Tên công ty hoặc Website).
- Tài khoản **Dropcontact** (kèm API Key) để làm giàu dữ liệu.
- Tài khoản **Lemlist** (kèm API Key/Credentials) để quản lý chiến dịch lead.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Các sếp tải file JSON của workflow này hoặc copy mã nguồn JSON.
- Trong giao diện n8n Editor, nhấn vào dấu **`+`** (Add workflow) -> Chọn **Import from File** hoặc dán trực tiếp vào màn hình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node sau:

- **Node `On clicking 'execute'` (manualTrigger):** 
  - Đây là node kích hoạt thủ công. Các sếp có thể thay thế bằng node *Schedule Trigger* nếu muốn workflow tự động chạy vào một khung giờ cố định mỗi ngày.
- **Node `Google Sheets`:** 
  - Kết nối tài khoản Google thông qua **Google Sheets OAuth2 API**.
  - Chọn đúng file Spreadsheet và Sheet Name chứa danh sách lead thô của các sếp.
  - Đảm bảo các cột dữ liệu (Ví dụ: First Name, Last Name, Company Website) được map chính xác vào tham số đầu vào.
- **Node `Dropcontact`:** 
  - Kết nối với tài khoản Dropcontact sử dụng `dropcontactApi`.
  - Node này sẽ nhận dữ liệu từ Google Sheets, tự động tìm kiếm và trả về thông tin email công ty, số điện thoại, và các thông tin pháp lý của doanh nghiệp đó.
- **Node `Lemlist`:** 
  - Cấu hình Lemlist credentials (`lemlistApi`).
  - Tại phần `keyParameters` (resource: `lead`), các sếp chọn chiến dịch (Campaign) cụ thể trong Lemlist để hệ thống tự động thêm các lead đã được enrich vào chiến dịch đó.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thử với 1-2 dòng dữ liệu mẫu xem hệ thống có trả về kết quả đúng ý không.
- Sau khi test thành công, gạt công tắc sang **Active** để bật chế độ tự động hóa hoàn toàn.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm bước lọc dữ liệu (Filter Node):** Thêm một node Filter ngay sau Dropcontact để chỉ đẩy những lead tìm được email hợp lệ vào Lemlist, tránh lãng phí email quota.
- **Ghi log kết quả:** Thêm một bước cập nhật ngược lại Google Sheets (hoặc gửi thông báo qua Slack/Telegram) để đánh dấu những dòng nào đã được enrich thành công.
- **Tích hợp CRM:** Có thể bổ sung thêm node HubSpot hoặc Pipedrive để đồng bộ dữ liệu khách hàng tiềm năng về hệ thống CRM của công ty.

### 📌 Kết luận
Việc làm giàu dữ liệu khách hàng chưa bao giờ dễ dàng đến thế với sự kết hợp giữa n8n, Dropcontact và Lemlist. Hãy thiết lập ngay hôm nay để giải phóng thời gian cho đội ngũ Sales và tối ưu hóa tỷ lệ chuyển đổi chiến dịch outreach của các sếp nhé!