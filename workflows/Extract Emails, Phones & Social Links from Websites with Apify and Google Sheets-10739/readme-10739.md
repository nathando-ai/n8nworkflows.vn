---
title: "🚀 Tự động trích xuất Email, Số điện thoại và Mạng xã hội từ Website với n8n, Apify và Google Sheets"
description: "Hướng dẫn xây dựng hệ thống Lead Generation tự động 100%: Quét danh sách website từ Google Sheets, cào thông tin liên hệ bằng Apify và lưu kết quả vào Google Sheet mới."
slug: "trich-xuat-email-dien-thoai-website-apify-google-sheets"
tags: [n8n, automation, no-code, apify, google-sheets, lead-generation]
keywords: [n8n workflow, cào email từ website, apify email extractor, tự động hóa lead generation, google sheets automation]
---

# 🚀 Tự động trích xuất Email, Số điện thoại và Mạng xã hội từ Website với n8n, Apify và Google Sheets

Các sếp làm sales, tuyển dụng hay marketing chắc chắn đã quá ngán ngẩm cảnh phải ngồi "đào bới" từng website thủ công để tìm địa chỉ email, số điện thoại hay link mạng xã hội của khách hàng tiềm năng. Việc này vừa tốn hàng giờ đồng hồ, vừa dễ bỏ sót dữ liệu quan trọng.

Đừng lo, bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ mạnh mẽ giúp tự động hóa toàn bộ quá trình trên: Đọc danh sách website từ **Google Sheets**, sử dụng sức mạnh cào dữ liệu của **Apify** để bóc tách thông tin liên hệ (Email, Phone, Social Links), và tự động tạo một Google Sheet mới chứa đầy đủ "mỏ vàng" data khách hàng cho các sếp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Thay vì mất hàng ngày trôi nổi trên web, hệ thống tự động cào hàng trăm website chỉ trong vài phút.
- **Dữ liệu sạch & có cấu trúc:** Tự động lọc và đồng bộ Email, SĐT, Facebook/LinkedIn/Twitter vào một Google Sheet mới một cách ngăn nắp.
- **Linh hoạt tùy biến:** Dễ dàng điều chỉnh độ sâu cào trang, giới hạn số lượng request hoặc chỉ định lấy riêng email theo ý muốn.
- **Hoạt động tự động 24/7:** Chạy mượt mà trên nền tảng n8n, sẵn sàng phục vụ các chiến dịch outreach bất cứ lúc nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** (Self-hosted hoặc n8n Cloud).
- **Tài khoản Google:** Để kết nối Google Sheets (cần quyền đọc/ghi).
- **Tài khoản Apify:** Đã đăng ký và lấy API Token, đồng thời kích hoạt Actor [Email & Phone Extractor](https://apify.com/anchor/email-phone-extractor).
- **File Google Sheet mẫu:** Chứa danh sách các domain hoặc URL website cần quét (mỗi dòng 1 URL).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và paste trực tiếp vào n8n Editor, hoặc import file JSON tải từ nguồn gốc. Workflow gồm 9 nodes phối hợp nhịp nhàng: từ Trigger thủ công, lấy dữ liệu Google Sheets, xử lý code JavaScript định dạng dữ liệu cho Apify, chạy Actor, lấy Dataset kết quả và tạo/ghi dữ liệu vào Sheet mới.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node `Set google sheet URL & original sheet name`:** Các sếp phải thay thế URL Google Sheet mẫu và tên sheet nguồn (ví dụ: `websites`) bằng thông tin thực tế của các sếp.
- **Node `Get website URLs from first sheet`, `Create new sheet for founded emails and phones`, `Add emails, phones, socials... into the new Sheet`:** Kết nối tài khoản Google Sheets của các sếp (OAuth2) để cấp quyền đọc và tạo file mới.
- **Node `Run Actor on Apify` & `Get Results from Apify`:** Cấu hình thông tin `apifyApi` credentials với API Key lấy từ tài khoản Apify.
- **Node `format data for Apify INPUT type` (Code node):** Tại đây các sếp có thể tùy chỉnh các tham số nâng cao:
  - `maxRequests`: Tổng số trang tối đa sẽ crawl trên toàn bộ các link (0 là không giới hạn).
  - `sameDomain`: Chỉ duyệt các liên kết trong cùng một domain (`true`/`false`).
  - `onlyEmails`: Chỉ lấy email, bỏ qua số điện thoại và mạng xã hội.
  - `onlyOneEmailPerDomain`: Dừng lại ngay khi tìm thấy 1 email đầu tiên trên trang (giúp tăng tốc độ crawl).
  - `maxDepth`: Độ sâu tối đa của link tính từ URL gốc.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thử với danh sách website mẫu.
- Kiểm tra kết quả trên Apify Run Log (nếu danh sách website lớn, việc crawl có thể mất chút thời gian).
- Sau khi test thành công, bật nút **Active** để đưa workflow vào trạng thái vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối thông báo:** Thêm node Telegram hoặc Slack vào cuối workflow để nhận thông báo ngay khi quá trình quét website hoàn tất.
- **Lưu log chạy:** Ghi lại thời gian và số lượng lead tìm được vào một Google Sheet quản lý chung.
- **Tích hợp CRM:** Thay vì ghi ra Google Sheet mới, các sếp có thể map dữ liệu trực tiếp vào HubSpot, Pipedrive hoặc Notion CRM để đội Sales chăm sóc ngay lập tức.

### 📌 Kết luận
Việc tìm kiếm khách hàng tiềm năng (Lead Generation) chưa bao giờ dễ dàng đến thế khi kết hợp sức mạnh tự động hóa của n8n và khả năng cào dữ liệu thông minh của Apify. Hãy áp dụng ngay workflow này để tối ưu hóa hiệu suất kinh doanh cho doanh nghiệp của các sếp ngay hôm nay!