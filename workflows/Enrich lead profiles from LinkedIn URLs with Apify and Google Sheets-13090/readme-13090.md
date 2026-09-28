---
title: "🚀 Tự động làm giàu dữ liệu Lead từ LinkedIn bằng Apify và Google Sheets"
description: "Hướng dẫn xây dựng workflow n8n tự động trích xuất thông tin chi tiết từ URL LinkedIn, làm sạch và cập nhật trực tiếp vào Google Sheets."
slug: "tu-dong-lam-giau-du-lieu-lead-tu-linkedin-apify-google-sheets"
tags: [n8n, automation, lead-generation, apify, google-sheets, linkedin]
keywords: [n8n workflow, apify linkedin scraper, làm giàu lead linkedin, google sheets automation, crm enrichment]
---

# 🚀 Tự động làm giàu dữ liệu Lead từ LinkedIn bằng Apify và Google Sheets

Các sếp có đang tốn hàng giờ đồng hồ mỗi ngày chỉ để copy thủ công từng URL LinkedIn, dán vào bảng tính, rồi mày mò ghi chép lại chức vụ, công ty, lịch sử làm việc hay bài đăng gần nhất của khách hàng tiềm năng? Công việc lặp đi lặp lại này vừa ngốn thời gian, vừa dễ gây mỏi mắt và sai sót.

Đừng lo, giải pháp ở đây rồi! Workflow n8n này sẽ tự động hóa 100% quy trình "Enrich" (làm giàu) dữ liệu lead từ LinkedIn. Các sếp chỉ việc ném danh sách link LinkedIn vào Google Sheets, phần việc còn lại cứ để hệ thống lo: từ cào dữ liệu, xử lý thông tin thông minh cho đến ghi ngược lại kết quả gọn gàng vào bảng tính.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không sợ sập nguồn hay mất kết nối, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 20+ giờ mỗi tuần:** Thay vì làm thủ công, hàng trăm profile LinkedIn được xử lý tự động hàng loạt.
- **Dữ liệu cực kỳ chi tiết:** Lấy sạch sành sanh từ tên, chức vụ, tiểu sử, thông tin công ty, cho đến 2 bài đăng gần nhất trên LinkedIn.
- **Thông minh & Bền bỉ:** Tích hợp logic chờ (polling) và kiểm tra trạng thái cào dữ liệu từ Apify, xử lý lỗi mượt mà không làm gián đoạn luồng.
- **Cá nhân hóa sâu:** Dữ liệu trích xuất sẵn sàng để phục vụ cho các chiến dịch AI cold email hoặc nhắn tin chăm sóc khách hàng cực kỳ trúng đích.
:::

### Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản **n8n** (Cloud hoặc Self-hosted).
- Tài khoản **Apify** kèm API Token (sử dụng Actor `dev_fusion~linkedin-profile-scraper`).
- Tài khoản **Google** có quyền kết nối **Google Sheets OAuth2**.
- Một file Google Sheet chuẩn bị sẵn với các cột: `LinkedIn`, `First Name`, `Last Name`, `Job Position`, `Location`, `Industry`, `Company Name`, `Company URL`, `Company Size`, `LI Other Profile Information`, `Status`, `Apify ID`, `Add date`, `row_number`.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này và import trực tiếp vào giao diện n8n Editor của các sếp, hoặc sử dụng tính năng Copy/Paste JSON thông thường.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp chú ý cấu hình các node cốt lõi sau:
- **Node `Get Rows - Not Enriched Yet` & Các node Google Sheets khác:** Kết nối tài khoản Google Sheets OAuth2 của các sếp và trỏ đến file Google Sheet chứa danh sách lead.
- **Node `Start Apify Scrape`, `Check Status`, & `Fetch LinkedIn Data` (HTTP Request):** Thay thế chuỗi `YOUR_APIFY_API_KEY` bằng Apify API Token thực tế của các sếp.
- **Node `Process One Row at a Time` (Split In Batches):** Giúp hệ thống xử lý từng URL một cách tuần tự, tránh việc gửi quá nhiều request cùng lúc gây quá tải hoặc dính rate limit.

#### 3. Kích hoạt ⚡️
- Nhập thử 1-2 dòng URL LinkedIn vào file Google Sheet (để trống cột *First Name* để hệ thống nhận diện là lead chưa chạy).
- Nhấn **Test Workflow** để kiểm tra dữ liệu trả về.
- Sau khi kiểm tra mọi thứ hoàn hảo, bật nút **Active** để workflow chạy tự động theo ý muốn.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối thông báo:** Thêm node **Slack** hoặc **Telegram** vào cuối luồng để nhận thông báo mỗi khi hệ thống quét xong một danh sách lead lớn.
- **Tích hợp AI:** Sử dụng cột `LI Other Profile Information` (chứa chuỗi thông tin tóm tắt profile) truyền trực tiếp vào OpenAI Node để AI tự động viết kịch bản nhắn tin (icebreaker) chào hàng siêu cá nhân hóa.
- **Chia mẻ nhỏ:** Khi mới bắt đầu, các sếp nên chạy thử các mẻ nhỏ (5-10 profiles) để kiểm tra cấu trúc dữ liệu và mức tiêu thụ credit trên Apify.

### 📌 Kết luận
Việc tự động hóa khâu thu thập và làm giàu dữ liệu lead chưa bao giờ dễ dàng đến thế với sự kết hợp hoàn hảo giữa n8n và Apify. Hãy áp dụng ngay hôm nay để giải phóng sức lao động cho đội ngũ sales và marketing của các sếp!