---
title: "🚀 Tự động tra cứu thông tin liên hệ và địa chỉ từ tên với ScraperCity trên n8n"
description: "Hướng dẫn tự động hóa quy trình tìm kiếm thông tin lead (email, SĐT, địa chỉ) từ họ tên sử dụng ScraperCity API và lưu trữ trực tiếp vào Google Sheets."
slug: "tu-dong-tra-cuu-thong-tin-lien-he-scrapercity-n8n"
tags: [n8n, automation, lead-generation, scrapercity, google-sheets]
keywords: [n8n workflow, tra cứu thông tin liên hệ, scrapercity, tìm kiếm lead b2b, tự động hóa n8n]
---

# 🚀 Tự Động Tra Cứu Thông Tin Liên Hệ & Địa Chỉ Từ Tên Với ScraperCity

Chào các sếp! Trong các chiến dịch Cold Email hay Sales Outreach, việc tốn hàng giờ để tìm kiếm thủ công email, số điện thoại hay địa chỉ của khách hàng tiềm năng dựa trên tên của họ là một nỗi đau cực kỳ lớn. Công việc này vừa nhàm chán, vừa dễ sai sót lại tốn kém nhân lực.

Hôm nay, em xin giới thiệu một workflow n8n cực kỳ xịn sò được thiết kế bởi **Alex Berman** (chuyên gia hàng đầu về Sales và Cold Email, tác giả cuốn *The Cold Email Manifesto*). Workflow này giúp tự động hóa 100% quy trình gửi yêu cầu tìm kiếm đến **ScraperCity**, xử lý cơ chế đợi kết quả (polling async), lọc dữ liệu trùng lặp và lưu trữ gọn gàng vào Google Sheets mà không cần đụng đến một dòng code phức tạp nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện**: Chỉ cần nhập tên, hệ thống sẽ lo phần còn lại từ quét dữ liệu, kiểm tra trạng thái đến lưu trữ.
- **Tiết kiệm 90% thời gian**: Xử lý hàng loạt thay vì tra cứu thủ công từng người một.
- **Dữ liệu sạch sẽ**: Tự động lọc bỏ các liên hệ trùng lặp (`Remove Duplicate Contacts`) trước khi đẩy vào Google Sheets.
- **Thông minh & Bền bỉ**: Sử dụng cơ chế vòng lặp thông minh (`Poll Loop` và `Wait`) để chờ kết quả từ API mà không làm sập tiến trình.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Đã cài đặt sẵn (Cloud hoặc Self-hosted).
- **Tài khoản ScraperCity**: Để lấy API Key (truy cập [ScraperCity](https://scrapercity.com) của Alex Berman).
- **Google Sheets**: Một file Google Sheet sẵn sàng để lưu kết quả lead.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể copy mã JSON của workflow từ nguồn chính thức hoặc paste trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node sau:

- **Tạo Credentials cho ScraperCity**:
  - Tại các node HTTP (`Start People Finder Scrape`, `Check Scrape Status`, `Download Results`), tạo mới một Credential kiểu **Header Auth** đặt tên là **ScraperCity API Key**.
  - Thiết lập Header Name: `Authorization`
  - Thiết lập Value: `Bearer YOUR_API_KEY` (thay `YOUR_API_KEY` bằng key thực tế của các sếp).

- **Configure Search Inputs (Node kiểu Set)**:
  - Điền thông tin mục tiêu cần tìm kiếm (Tên, Số điện thoại, hoặc Email) vào node này để khởi chạy quá trình quét.

- **Save Results to Google Sheets (Node kiểu Google Sheets)**:
  - Chọn tài khoản kết nối Google Sheets (`googleSheetsOAuth2Api`).
  - Chọn Document và Sheet Name chính xác nơi các sếp muốn lưu trữ danh sách lead.
  - Thiết lập operation là `append`.

#### 3. Kích hoạt ⚡️
- Bấm nút **"Execute Workflow"** để test chạy thử với dữ liệu mẫu trong `Configure Search Inputs`.
- Kiểm tra lại Google Sheets xem dữ liệu đã đổ về chuẩn chỉnh chưa.
- Gạt công tắc sang **Active** để workflow sẵn sàng hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Webhook / Chatbot**: Kết hợp thêm node Telegram hoặc Slack ở cuối workflow để bắn thông báo ngay về máy mỗi khi quét xong một batch lead mới.
- **Mở rộng nguồn đầu vào**: Thay vì dùng node `Configure Search Inputs` thủ công, các sếp có thể thay thế bằng node **Webhook** hoặc **Google Sheets Trigger** để đọc danh sách tên cần tìm từ một file Google Sheet đầu vào.
- **Làm giàu dữ liệu (Data Enrichment)**: Sau khi lấy được thông tin cơ bản từ ScraperCity, có thể nối thêm các bước gửi email tự động qua Lemlist, Instantly hoặc Hubspot CRM.

### 📌 Kết luận
Workflow này là một "vũ khí bí mật" giúp tối ưu hóa quy trình tìm kiếm khách hàng tiềm năng cho đội ngũ sales và marketing. Hãy cài đặt ngay lên hệ thống n8n của các sếp để giải phóng sức lao động thủ công và bứt phá doanh số ngay hôm nay!