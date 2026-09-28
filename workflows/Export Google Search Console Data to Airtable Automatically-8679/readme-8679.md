---
title: "🚀 Tự động hóa xuất dữ liệu Google Search Console sang Airtable với n8n"
description: "Hướng dẫn chi tiết cách thiết lập workflow n8n để tự động kéo dữ liệu từ Google Search Console (Query, Page, Date) và lưu vào Airtable mà không cần làm thủ công."
slug: "tu-dong-hoa-google-search-console-sang-airtable-voi-n8n"
tags: [n8n, automation, google-search-console, airtable, seo, no-code]
keywords: [n8n workflow, google search console airtable, tu dong hoa seo, export gsc data, n8n viet nam]
---

# 🚀 Tự động hóa xuất dữ liệu Google Search Console sang Airtable

Đã bao giờ các sếp cảm thấy mệt mỏi mỗi khi phải tải file CSV thủ công từ Google Search Console, mở Excel định dạng lại mớ dữ liệu lộn xộn, rồi lại copy paste vào Google Sheets chỉ để làm một báo cáo SEO đơn giản? Nếu câu trả lời là "Có", thì workflow n8n này sinh ra là dành riêng cho các sếp.

Workflow này giúp tự động hóa 100% quy trình lấy dữ liệu từ GSC và đẩy thẳng vào Airtable theo định kỳ, giúp tiết kiệm hàng giờ đồng hồ mỗi tuần.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tạm biệt file CSV thủ công:** Không còn cảnh tải xuống, chỉnh sửa format rườm rà.
- **Dữ liệu luôn tươi mới:** Tự động cập nhật báo cáo theo ngày, tuần hoặc tháng một cách trơn tru.
- **Kho lưu trữ SEO chuyên nghiệp:** Dữ liệu được phân loại rõ ràng theo từ khóa (Query), trang (Page) và thời gian (Date) trong Airtable.
- **Tiết kiệm thời gian:** Tập trung vào việc tối ưu SEO thay vì làm công việc chân tay.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Cloud hoặc Self-hosted).
- Truy cập vào **Google Search Console** và một **Google Cloud Project** đã bật Search Console API.
- Tài khoản **Airtable** để lưu trữ cơ sở dữ liệu.
- Credentials: `Google OAuth2 API` và `Airtable Token API`.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể copy mã JSON của workflow từ nguồn cung cấp và dán trực tiếp vào n8n Editor của mình, sau đó tiến hành kết nối các tài khoản.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần chú ý cấu hình các node sau:
- **Schedule Trigger:** Cấu hình thời gian chạy tự động (ví dụ: chạy mỗi ngày lúc 8 giờ sáng).
- **Set your domain (Node Set):** Điền chính xác domain website của các sếp vào biến `domain` (ví dụ: `https://websitecua-ban.com/`) và khoảng thời gian lấy dữ liệu `days` (mặc định là 30 ngày).
- **Get Query Report, Get Page Report, Get Date Report (Nodes HTTP Request):** Kết nối với tài khoản `Google OAuth2 API` đã cấp quyền truy cập Search Console.
- **Create a record, Create a record1, Create a record2 (Nodes Airtable):** Kết nối với `Airtable Token API`, chọn Base và Table tương ứng đã tạo sẵn trên Airtable (Queries, Pages, Dates) để mapping các trường dữ liệu (`Keyword`, `clicks`, `impressions`, `ctr`, `position`).

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thử nghiệm dữ liệu lần đầu.
- Sau khi kiểm tra thấy dữ liệu đã đồng bộ sang Airtable chuẩn chỉnh, hãy gạt công tắc sang **Active** để chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node Telegram hoặc Slack vào cuối workflow để nhận thông báo mỗi khi dữ liệu được đồng bộ thành công.
- **Mở rộng dải thời gian:** Có thể điều chỉnh biến `days` trong node Set để lấy báo cáo theo tuần (7 ngày) hoặc quý (90 ngày) tùy nhu cầu phân tích.
- **Xây dựng Dashboard:** Sử dụng Airtable Interface để vẽ biểu đồ trực quan hóa traffic, từ khóa SEO ngay trên nền tảng này.

### 📌 Kết luận
Tự động hóa quy trình báo cáo SEO với Google Search Console và Airtable không chỉ giúp các sếp quản lý dữ liệu tốt hơn mà còn giải phóng sức lao động khỏi những bảng tính thủ công. Hãy thiết lập ngay hôm nay để nâng cấp hệ thống vận hành marketing của doanh nghiệp!