---
title: "🚀 Tự Động Nghiên Cứu Từ Khóa YouTube & Google và Lưu Vào NocoDB với n8n"
description: "Khám phá cách tự động hóa quá trình tìm kiếm từ khóa tiềm năng trên Google và YouTube, phân tích lượng tìm kiếm (search volume) và lưu trữ trực tiếp vào NocoDB."
slug: "tu-dong-nghien-cuu-tu-khoa-youtube-google-nocodb"
tags: [n8n, automation, no-code, marketing, seo, nocodb, youtube]
keywords: [n8n workflow, tự động hóa seo, nghiên cứu từ khóa, nocodb, youtube keyword, google autocomplete]
---

# 🚀 Tự Động Nghiên Cứu Từ Khóa YouTube & Google và Lưu Vào NocoDB

Chào các sếp! Việc nghiên cứu từ khóa (Keyword Research) thủ công cho các chiến dịch SEO Google hay sáng tạo nội dung YouTube thường ngốn rất nhiều thời gian và công sức. Các sếp phải lọc từ khóa, check lượng tìm kiếm, CPC, rồi lại copy paste vào Excel vô cùng cực khổ. 

Đừng lo, bài toán đó sẽ được giải quyết triệt để với workflow n8n cực kỳ xịn sò này do tác giả **Shannon Atkinson** xây dựng. Workflow này sẽ tự động hóa từ A-Z: lấy danh sách từ khóa gốc, đào sâu các từ khóa gợi ý (second-order keywords) từ Google & YouTube, check lượng tìm kiếm, lọc các chỉ số quan trọng và đồng bộ thẳng vào cơ sở dữ liệu **NocoDB** một cách mượt mà!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Định kỳ quét và mở rộng danh sách từ khóa mà không cần đụng tay.
- **Dữ liệu chính xác:** Lấy thông tin search volume, CPC, độ cạnh tranh từ các API chuyên sâu.
- **Quản lý tập trung:** Toàn bộ từ khóa Google & YouTube được phân loại và lưu trữ gọn gàng trong NocoDB.
- **Tiết kiệm hàng chục giờ:** Giải phóng thời gian làm SEO thủ công để tập trung vào chiến lược nội dung.
:::

### Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **NocoDB Account:** Nơi lưu trữ dữ liệu từ khóa với các bảng được chuẩn bị sẵn.
- **DataforSEO Account:** Tài khoản API để lấy dữ liệu autocomplete và search volume ([Đăng ký tại đây](https://app.dataforseo.com/?aff=184401)).
- **Social Flood Docker Instance:** (Hoặc dịch vụ hỗ trợ tương đương theo yêu cầu hệ thống gốc).
- **Credentials cần thiết trong n8n:**
  - `nocoDbApiToken`: Token kết nối NocoDB.
  - `httpHeaderAuth` / `httpBasicAuth`: Xác thực API cho các dịch vụ bên thứ ba (DataforSEO, HTTP Requests).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Các sếp sao chép mã JSON của workflow hoặc tải file JSON từ nguồn.
- Mở n8n Editor, chọn **Add workflow** -> **Import from File / Paste JSON** để đưa toàn bộ 28 nodes lên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy trơn tru, các sếp cần cấu hình kỹ các phần sau:

- **NocoDB Nodes (`NocoDB`, `Add Second Tier YT Keyword Data`, v.v.):** 
  - Kết nối đúng `nocoDbApiToken` của các sếp.
  - Trỏ đúng Project ID, Table ID tương ứng với cấu trúc bảng trong NocoDB:
    - `Base Keyword Search` (Chứa từ khóa gốc).
    - `Second Order Google Keywords` (keyword, location_code, language_code, search_partners, competition, competition_index, search_volume, cpc...).
    - `Second Order YouTube Keywords` (Cấu trúc tương tự Google).
    - `Search Volume` (Lưu lượng tìm kiếm theo tháng/năm).

- **HTTP Request Nodes (`Second Order Google Autocomplete Keywords`, `Google Search Volume`, `YouTube Search Volume`,...):**
  - Đảm bảo các sếp đã điền đúng API Credentials của **DataforSEO** hoặc các endpoint API tương ứng mà workflow gọi tới để lấy dữ liệu autocomplete và chỉ số từ khóa.

- **Trigger Nodes (`Schedule Trigger` / `When clicking ‘Test workflow’`):**
  - Cấu hình lịch chạy tự động (ví dụ: chạy hàng tuần hoặc hàng tháng) bằng `Schedule Trigger` tùy theo nhu cầu thực tế của team SEO.

#### 3. Kích hoạt ⚡️
- Nhấn **Test workflow** trên một vài từ khóa mẫu để kiểm tra xem dữ liệu có đổ về NocoDB chính xác hay không.
- Sau khi test xanh mướt, hãy bật nút **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm một node **Telegram** hoặc **Slack** ở cuối workflow để thông báo ngay cho team mỗi khi quá trình quét và cập nhật từ khóa hoàn tất.
- **Mở rộng lọc dữ liệu:** Tận dụng các node `Google Filter` và `YT Filter` để đặt điều kiện chỉ lưu các từ khóa có lượng tìm kiếm lớn hơn một ngưỡng nhất định (ví dụ: `Search Volume > 500`), giúp loại bỏ từ khóa rác.
- **Báo cáo định kỳ:** Kết hợp thêm Google Looker Studio kết nối trực tiếp với NocoDB để vẽ biểu đồ trực quan về xu hướng từ khóa theo thời gian.

### 📌 Kết luận
Workflow này là một "vũ khí" cực mạnh cho các marketer và SEOer muốn tự động hóa hoàn toàn quy trình nghiên cứu từ khóa. Hãy cài đặt ngay lên VPS của mình và để hệ thống thay bạn làm những công việc lặp đi lặp lại nhé! Chúc các sếp thành công!