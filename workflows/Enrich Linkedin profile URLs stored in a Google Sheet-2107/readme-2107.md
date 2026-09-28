---
title: "🚀 Tự Động Làm Giàu Dữ Liệu LinkedIn (LinkedIn Data Enrichment) Vào Google Sheets Bằng n8n"
description: "Hướng dẫn tự động lấy thông tin email và dữ liệu chuyên sâu từ URL LinkedIn bằng Prospeo.io API và cập nhật trực tiếp vào Google Sheets với n8n."
slug: "tu-dong-lam-giau-du-lieu-linkedin-google-sheets-n8n"
tags: [n8n, automation, no-code, sales, marketing, linkedin, google-sheets]
keywords: [n8n workflow, linkedin email finder, prospeo api, google sheets automation, data enrichment, tự động hóa sales]
---

# 🚀 Tự Động Làm Giàu Dữ Liệu LinkedIn Vào Google Sheets Bằng n8n

Các sếp làm sales hoặc marketing chắc chắn đã từng trải qua cảm giác mệt mỏi khi phải copy từng đường link profile LinkedIn, mò mẫm tìm email cá nhân/công việc rồi paste thủ công vào Google Sheets để chạy chiến dịch outreach. Việc này vừa tốn hàng giờ đồng hồ, vừa dễ xảy ra sai sót.

Giải pháp ở đây là gì? Workflow n8n này sẽ tự động hóa 100% quy trình: Quét danh sách URL LinkedIn từ Google Sheets -> Gọi API của Prospeo.io để tìm kiếm email/thông tin liên hệ -> Tự động cập nhật ngược lại vào file Google Sheets của các sếp một cách mượt mà!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn phải thủ công tìm email từng khách hàng tiềm năng.
- **Dữ liệu luôn sạch và chuẩn:** Tự động enrich (làm giàu) thông tin từ profile LinkedIn vào CRM hoặc file quản lý.
- **Tự động hóa theo lịch trình:** Thiết lập chạy định kỳ mỗi ngày hoặc mỗi giờ mà không cần bận tâm can thiệp thủ công.
- **Tăng tỷ lệ chuyển đổi sales:** Có sẵn email chính xác để triển khai các chiến dịch cold email nhanh chóng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Cloud hoặc Self-hosted).
- Tài khoản Google Workspace để kết nối Google Sheets (`googleSheetsOAuth2Api`).
- Tài khoản tại [Prospeo.io](https://prospeo.io/) và lấy **API Key** để sử dụng dịch vụ tìm kiếm email LinkedIn.
- Một file Google Sheets chuẩn bị sẵn cột chứa các URL LinkedIn cần enrich.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này, vào giao diện n8n, chọn **Add workflow** -> **Import from JSON** và dán vào là xong.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy trơn tru, các sếp cần cấu hình chính xác các node sau:

- **Schedule Trigger:** Cấu hình mốc thời gian chạy tự động (theo phút, giờ hoặc ngày) tùy thuộc vào nhu cầu quét dữ liệu của các sếp.
- **Get links from Google Sheet:** 
  - Kết nối tài khoản Google Sheets của các sếp.
  - Điền chính xác **Document ID** và **Sheet Name** chứa danh sách URL LinkedIn.
- **Conditional Check (If):** Kiểm tra xem dòng dữ liệu đó đã có URL LinkedIn hợp lệ hay chưa trước khi gửi request lên API.
- **HTTP Request - Utilize Prospeo.io LinkedIn Email Finder API1:**
  - Cấu hình endpoint API của Prospeo (`https://prospeo.io/api/linkedin-email-finder`).
  - Thêm API Key của các sếp vào phần Header để xác thực.
  - Truyền tham số là URL LinkedIn lấy từ Google Sheets vào body của request.
- **Field Editing (Set) & Data Merge:** Xử lý, lọc và ghép nối dữ liệu trả về từ API sao cho khớp với cấu trúc cột trên Google Sheets.
- **Update the sheet with information (Google Sheets):**
  - Chọn đúng file Google Sheets và cấu hình chế độ **Update**.
  - Map các trường dữ liệu email/thông tin mới tìm được vào đúng dòng tương ứng.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** chạy thử với 1-2 dòng dữ liệu mẫu để kiểm tra kết quả trả về.
- Sau khi test thành công, bật nút **Active** ở góc trên bên phải để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Thêm node Telegram hoặc Slack vào cuối workflow để nhận thông báo ngay mỗi khi hoàn tất quá trình enrich một batch dữ liệu.
- **Xử lý lỗi (Error Handling):** Thêm Error Trigger để bắt các lỗi liên quan đến hếtCredits của Prospeo API hoặc lỗi kết nối Google Sheets.
- **Gửi tự động:** Kết nối tiếp dữ liệu sau khi enrich vào các công cụ gửi Cold Email (như Lemlist, Instantly) để tối ưu hóa phễu bán hàng.

### 📌 Kết luận
Việc tự động hóa quy trình làm giàu dữ liệu LinkedIn chưa bao giờ dễ dàng đến thế với n8n và Prospeo API. Hãy áp dụng ngay hôm nay để giải phóng sức lao động cho đội ngũ sales và tăng tốc doanh số cho doanh nghiệp các sếp nhé!