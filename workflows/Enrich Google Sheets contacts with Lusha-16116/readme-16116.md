---
title: "🚀 Tự động làm giàu dữ liệu khách hàng (Enrich Contacts) từ Google Sheets với Lusha qua n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động kết nối Google Sheets và Lusha API để bổ sung thông tin liên hệ, email, số điện thoại của khách hàng tiềm năng một cách nhanh chóng."
slug: "tu-dong-lam-giau-du-lieu-khach-hang-google-sheets-lusha-n8n"
tags: [n8n, automation, no-code, lead-generation, lusha, google-sheets]
keywords: [n8n workflow, làm giàu dữ liệu, enrich contacts, lusha api, google sheets automation, tự động hóa bán hàng]
---

# 🚀 Tự động làm giàu dữ liệu khách hàng (Enrich Contacts) từ Google Sheets với Lusha qua n8n

Các sếp có bao giờ rơi vào cảnh danh sách khách hàng tiềm năng (Leads) trong Google Sheets chỉ có mỗi tên và công ty, còn số điện thoại hay email chuẩn chỉnh thì... trống trơn? Ngồi copy từng tên đem đi search thủ công trên Lusha hay LinkedIn thì vừa mất thời gian, vừa nản chí anh em Sales, mà tỷ lệ sót đơn lại cao.

Đừng lo nữa các sếp ơi! Bài viết này sẽ hướng dẫn chi tiết cách thiết lập một workflow n8n tự động hóa 100% quy trình này: Đọc dữ liệu từ Google Sheets 👉 gọi Lusha API để "làm giàu" thông tin (Email, Phone, Chức vụ...) 👉 cập nhật ngược lại Google Sheets. Toàn bộ quy trình diễn ra mượt mà, không tốn một giọt mồ hôi thủ công!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không còn cảnh copy-paste thủ công từng dòng dữ liệu từ Google Sheets sang Lusha.
- **Tăng tỷ lệ chuyển đổi Sales:** Đội ngũ kinh doanh có ngay số điện thoại và email chính xác để chốt sale nhanh chóng.
- **Dữ liệu luôn sạch và chuẩn hóa:** Các contact được lọc, kiểm tra LinkedIn URL và tự động cập nhật trạng thái xử lý rõ ràng.
- **Vận hành tự động 24/7:** Chạy theo lịch trình hoặc kích hoạt thủ công tùy nhu cầu mà không tốn nhân lực giám sát.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Đã cài đặt sẵn (Self-hosted hoặc n8n Cloud).
- **Tài khoản Google Sheets:** Có file danh sách khách hàng chứa thông tin cơ bản (Tên, Công ty, LinkedIn URL...).
- **Tài khoản Lusha:** Cần có API Key để gọi dữ liệu từ nền tảng Lusha.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải mã nguồn JSON của workflow từ [n8n.io Workflow 16116](https://n8n.io/workflows/16116) hoặc sử dụng file JSON tương ứng. Sau đó copy và paste trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 11 nodes được thiết kế cực kỳ logic. Các sếp cần chú ý cấu hình các điểm mấu chốt sau:

- **When Executed Manually (manualTrigger):** Điểm khởi chạy thủ công. Các sếp có thể đổi sang *Schedule Trigger* nếu muốn n8n tự quét danh sách định kỳ mỗi ngày.
- **Read Contacts from Sheets (googleSheets):** Kết nối với tài khoản Google của sếp, chọn đúng file Spreadsheet và Sheet chứa danh sách contacts.
- **Filter Valid Contacts (filter):** Lọc bỏ các dòng dữ liệu rác hoặc thiếu thông tin cơ bản trước khi xử lý.
- **Loop Over Contacts (splitInBatches):** Chia nhỏ dữ liệu thành từng batch để tránh vượt quá giới hạn gọi API (Rate limit) của Lusha.
- **If LinkedIn URL Present (if):** Kiểm tra xem contact có sẵn link LinkedIn hay không để phân nhánh gọi API phù hợp.
- **Fetch Lusha by Name & Fetch Lusha by LinkedIn (httpRequest):** 
  - Cần cấu hình **Header Authentication** hoặc **Query Parameters** sử dụng Lusha API Key của các sếp.
  - Endpoint gọi API cần trỏ chính xác đến dịch vụ Contact Enrichment của Lusha.
- **Map Contact Fields (set):** Chuẩn hóa lại các trường dữ liệu trả về từ Lusha (như email, phone, job title) để khớp với cấu trúc cột trên Google Sheets.
- **If Contact Data Found (if):** Kiểm tra xem Lusha có tìm thấy dữ liệu hay không.
- **Update Enriched Contact & Update Contact Status (googleSheets):** Cập nhật dữ liệu mới (đã làm giàu) và đổi trạng thái (Status: Thành công/Thất bại) vào các cột tương ứng trên Google Sheets.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** với dữ liệu mẫu nhỏ để test thử xem Lusha trả về kết quả và ghi vào Google Sheets có đúng ý chưa.
- Sau khi test ngon lành, gạt công tắc sang **Active** để workflow chính thức đi vào hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node **Slack** hoặc **Telegram** sau bước cập nhật để bắn thông báo về group team Sales mỗi khi có một mẻ Leads mới được làm giàu thành công.
- **Lưu Log lỗi:** Thêm nhánh xử lý lỗi (Error Trigger) để ghi nhận những trường hợp Lusha không tìm thấy thông tin, giúp đội ngũ Marketing tối ưu lại nguồn data đầu vào.
- **Tự động hóa toàn diện:** Kết hợp với CRM như HubSpot hoặc Pipedrive để ngay sau khi Google Sheets được update thông tin từ Lusha, contact sẽ được đẩy thẳng vào CRM cho Sales chăm sóc.

### 📌 Kết luận
Việc tự động hóa quy trình làm giàu dữ liệu với n8n và Lusha không chỉ giúp đội ngũ tiết kiệm thời gian mà còn nâng cao hiệu suất kinh doanh đáng kể. Hãy áp dụng ngay hôm nay để tối ưu hóa quy trình vận hành của doanh nghiệp các sếp nhé!