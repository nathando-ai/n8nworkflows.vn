---
title: "🚀 Tự động giám sát AppSumo Lifetime Deals với ScrapeOps và Google Sheets"
description: "Hướng dẫn xây dựng workflow n8n tự động cào dữ liệu deal phần mềm trọn đời từ AppSumo, lọc theo danh mục và đồng bộ hóa thông minh vào Google Sheets mỗi ngày."
slug: "tu-dong-giam-sat-appsumo-lifetime-deals-voi-scrapeops-va-google-sheets"
tags: [n8n, automation, scrapeops, google-sheets, web-scraping, lifetime-deals]
keywords: [n8n workflow, appsumo monitor, scrapeops n8n, tu dong hoa google sheets, web scraping appsumo]
---

# 🚀 Tự động giám sát AppSumo Lifetime Deals với Google Sheets & ScrapeOps

Các sếp làm trong ngành phần mềm, Agency hay thích săn deal hời chắc chắn không lạ gì **AppSumo** – nền tảng săn deal phần mềm trọn đời (Lifetime Deals - LTD) nổi tiếng nhất thế giới. Tuy nhiên, việc phải vào check website mỗi ngày để tìm các deal ngon, đúng nhu cầu thực sự tốn rất nhiều thời gian và dễ bỏ lỡ.

Đừng lo, bài toán này sẽ được giải quyết triệt để với workflow n8n cực xịn sò được thiết kế bởi *Ian Kerins*. Workflow này sẽ tự động cào dữ liệu từ AppSumo, lọc ra các danh mục các sếp quan tâm, check trùng lặp và lưu trữ gọn gàng vào Google Sheets hoàn toàn tự động!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không sợ sập, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian:** Không cần phải lướt AppSumo thủ công mỗi ngày.
- **Lọc thông minh:** Chỉ nhận thông tin các deal thuộc danh mục phần mềm sếp thực sự quan tâm (Marketing, SEO, AI, Productivity...).
- **Chống trùng lặp hoàn hảo (Deduplication):** Tự động nhận diện deal mới để thêm dòng mới, hoặc cập nhật lại giá tiền/trạng thái nếu deal đã tồn tại trên Google Sheets.
- **Hoạt động 24/7:** Chạy tự động đều đặn mỗi sáng lúc 09:00 mà không cần can thiệp thủ công.
:::

### Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Đã hoạt động (Self-hosted hoặc Cloud).
- **Tài khoản ScrapeOps:** Lấy API Key miễn phí tại [ScrapeOps Register](https://scrapeops.io/app/register/n8n).
- **Google Sheets:** Tạo sẵn một file Google Sheet để lưu trữ dữ liệu (có thể dùng template mẫu từ tác giả).
- **Credentials:** Kết nối Google Sheets OAuth2 API và ScrapeOps API trong n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy đoạn mã JSON của workflow hoặc import file trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình chính xác các node sau để workflow chạy mượt mà:

- **Fetch AppSumo Deals via ScrapeOps (JS Render):** Thêm ScrapeOps API Key vào phần Credentials của node này để kích hoạt tính năng render JavaScript khi cào dữ liệu.
- **Lookup Deal in Google Sheet (by URL), Append New Deal to Sheet, Update Existing Deal Row in Sheet:** 
  - Chọn tài khoản Google Sheets OAuth2 đã kết nối.
  - Trỏ đường dẫn đến file Google Sheet quản lý deal của các sếp.
- **Filter Relevant Deal Categories (Code Node):** Mở node này ra và chỉnh sửa danh sách từ khóa/danh mục (categories) sao cho khớp với sở thích hoặc nhu cầu kinh doanh của các sếp.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** chạy thủ công lần đầu để test dữ liệu đổ về Google Sheets.
- Nếu mọi thứ xanh mướt, hãy gạt nút **Active** ở góc trên bên phải để hệ thống tự chạy mỗi ngày theo lịch trình.

### ✍️ Mẹo & gợi ý nâng cao
Để workflow "trâu bò" và tiện ích hơn nữa, các sếp có thể mở rộng:
- **Thêm thông báo (Notifications):** Nối thêm node **Telegram** hoặc **Slack** ngay sau nhánh *New Deal* để nhận thông báo ngay lập tức trên điện thoại mỗi khi có deal hot xuất hiện.
- **Lọc theo giá tiền:** Bổ sung điều kiện chỉ lấy các deal có giá dưới mức ngân sách cho phép.
- **Báo cáo tuần:** Tạo thêm một nhánh tổng hợp các deal mới trong tuần gửi vào email cá nhân vào tối Chủ Nhật.

### 📌 Kết luận
Với workflow tự động hóa này, việc săn sale phần mềm trên AppSumo giờ đây trở nên chuyên nghiệp và nhàn hạ hơn bao giờ hết. Hãy setup ngay hôm nay để không bỏ lỡ bất kỳ phần mềm trọn đời giá hời nào các sếp nhé!