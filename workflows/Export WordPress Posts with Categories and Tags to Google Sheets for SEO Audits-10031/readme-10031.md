---
title: "🚀 Tự động xuất bài viết WordPress kèm Categories và Tags sang Google Sheets phục vụ Audit SEO"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa việc trích xuất toàn bộ bài viết, chuyên mục và thẻ từ WordPress đẩy thẳng lên Google Sheets để làm SEO Audit cực nhanh chóng."
slug: "xuat-wordpress-posts-sang-google-sheets-cho-seo-audit"
tags: [n8n, automation, wordpress, google-sheets, seo-audit, no-code]
keywords: [n8n workflow, export wordpress to google sheets, seo audit wordpress, tự động hóa n8n, api wordpress]
---

# 🚀 Tự động xuất bài viết WordPress kèm Categories và Tags sang Google Sheets phục vụ Audit SEO

Các sếp làm SEO hoặc quản trị website WordPress chắc chắn đã từng trải qua cảm giác "đau đầu" khi phải thủ công copy/paste từng URL bài viết, kiểm tra lại danh mục (categories), thẻ (tags) để làm báo cáo nội dung hay thực hiện On-page SEO Audit. Việc này không những mất hàng giờ đồng hồ mà còn rất dễ sót bài, sai sót dữ liệu.

Đừng lo, bài viết này sẽ hướng dẫn các sếp cách thiết lập một workflow n8n cực kỳ xịn sò giúp tự động hóa toàn bộ quy trình: Lấy danh sách toàn bộ bài viết, gom nhóm chuyên mục, thẻ từ WordPress REST API và đồng bộ thẳng lên Google Sheets chỉ bằng một cú click thông qua giao diện Form tiện lợi!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và xử lý các trang web WordPress lớn mà không lo timeout, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 99% thời gian:** Thay vì thao tác thủ công, toàn bộ dữ liệu bài viết được trích xuất trong vài giây.
- **Dữ liệu chuẩn xác 100%:** Tự động map chính xác tên Categories và Tags tương ứng với từng URL bài viết thông qua custom code thông minh.
- **Sẵn sàng cho SEO Audit:** Dữ liệu được cấu trúc sạch sẽ trên Google Sheets, sẵn sàng cho việc phân tích mồ côi (orphan pages), thiếu từ khóa, hay tối ưu nội dung.
- **Kích hoạt linh hoạt:** Sử dụng Form Trigger giúp bất kỳ thành viên nào trong đội ngũ cũng có thể tự chạy báo cáo mà không cần can thiệp vào hệ thống n8n.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Trang web WordPress:** Đã bật REST API (mặc định WordPress đều có sẵn).
- **Google Account:** Tài khoản Google Sheets để lưu trữ dữ liệu xuất ra.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow từ nguồn cung cấp (hoặc tải file JSON) và paste trực tiếp vào giao diện n8n Editor của mình. Workflow bao gồm 10 nodes chính làm việc nhịp nhàng với nhau.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động mượt mà với website của các sếp, hãy cấu hình kỹ các node sau:

- **Node `Config` (Set):** Cấu hình các thông số cơ bản như đường dẫn trang web WordPress của các sếp (ví dụ: `https://yourwebsite.com`) và giới hạn số lượng bài viết lấy về mỗi lần (`per_page` mặc định là 100, các sếp có thể điều chỉnh tùy theo quy mô blog).
- **Nodes `Get Posts`, `Get Categories`, `Get Tags` (HTTP Request):** Các node này gọi trực tiếp đến WordPress REST API tương ứng (`/wp-json/wp/v2/posts`, `/wp-json/wp/v2/categories`, `/wp-json/wp/v2/tags`). Hãy đảm bảo URL trang web của các sếp chính xác.
- **Node `Assign tags and categories names to posts` (Code):** Node này sử dụng JavaScript để đọc dữ liệu từ 3 API trên, xây dựng bảng tra cứu (lookup maps) nhanh và gán trực tiếp tên `categoryNames` và `tagNames` vào từng bài viết. Không cần sửa gì ở đây trừ khi các sếp muốn custom thêm trường dữ liệu.
- **Node `Add posts, with tags, categories to Google Sheet` (Google Sheets):** 
  - Kết nối tài khoản Google qua `GoogleSheetsOAuth2Api`.
  - Chọn file Google Sheet và Sheet Name chuẩn bị sẵn.
  - **LƯU Ý QUAN TRỌNG:** Cần tạo sẵn một Google Sheet với đúng các cột tiêu đề (Columns) sau để khớp với dữ liệu xuất ra:
    - **URL**
    - **Title**
    - **Categories**
    - **Tags**
- **Nodes `WP API Error` & `Form` (Form Completion):** Các node xử lý giao diện thông báo khi quá trình hoàn tất hoặc nếu có lỗi xảy ra từ phía API WordPress.

#### 3. Kích hoạt ⚡️
- Nhấn **Test step** hoặc **Execute Workflow** để chạy thử qua giao diện `On form submission` (Form Trigger).
- Điền thử thông tin và kiểm tra xem Google Sheet đã nhận được dữ liệu bài viết chưa.
- Nếu mọi thứ mượt mà, hãy gạt công tắc sang **Active** để đưa workflow vào trạng thái vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack/Telegram:** Thêm một node thông báo qua Chat app ngay sau khi quá trình trích xuất hoàn tất kèm theo đường link Google Sheet để đội ngũ SEO nắm bắt ngay.
- **Tự động hóa định kỳ (Scheduled):** Thay vì dùng `formTrigger`, các sếp có thể thay thế bằng `Schedule Trigger` để hệ thống tự động quét và cập nhật báo cáo SEO hàng tuần/hàng tháng mà không cần ai bấm nút.
- **Mở rộng trường dữ liệu:** Các sếp có thể chỉnh sửa HTTP Request gọi bài viết để lấy thêm ngày xuất bản (`date`), trạng thái (`status`), hoặc số lượng từ để làm giàu báo cáo audit.

### 📌 Kết luận
Việc tối ưu hóa quy trình làm việc chưa bao giờ dễ dàng đến thế với n8n. Chỉ với vài phút cài đặt workflow này, các sếp đã giải phóng bản thân khỏi những tác vụ thủ công nhàm chán và tập trung hoàn toàn vào chiến lược SEO cốt lõi. Áp dụng ngay thôi nào các sếp ơi!