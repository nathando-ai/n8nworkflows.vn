---
title: "🛒 Tự động gửi Email báo giá giảm hàng ngày từ Amazon, Walmart và Google Shopping qua ScraperAPI"
description: "Hướng dẫn cài đặt workflow n8n tự động cào dữ liệu giá sản phẩm từ Amazon, Walmart và Google, phân tích biến động và gửi email cảnh báo giá giảm mỗi ngày."
slug: "tu-dong-gui-email-bao-gia-giam-amazon-walmart-google-scraperapi"
tags: [n8n, automation, scraperapi, ecommerce, email-digest]
keywords: [n8n workflow, scraperapi, amazon price tracker, walmart scraper, google shopping, tự động hóa email giá giảm]
---

# 🛒 Tự động gửi Email báo giá giảm hàng ngày từ Amazon, Walmart và Google Shopping qua ScraperAPI

Việc theo dõi thủ công giá của hàng loạt sản phẩm trên các sàn thương mại điện tử lớn như Amazon, Walmart hay Google Shopping để "sợ hãi" bỏ lỡ các đợt giảm giá là một cực hình đối với người mua sắm thông thái lẫn các nhà kinh doanh Dropshipping. 

Giải pháp? Workflow n8n tự động hóa toàn bộ quy trình này: định kỳ cào dữ liệu giá mới nhất, so sánh với lịch sử giá, ghi nhận biến động và tổng hợp thành một bản tin (digest email) gửi thẳng vào hộp thư của các sếp mỗi sáng! Không cần code, không lo CAPTCHA nhờ sự trợ giúp mạnh mẽ từ ScraperAPI.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 100%:** Hệ thống tự chạy vào 8 giờ sáng mỗi ngày nhờ lịch trình thiết lập sẵn mà không cần đụng tay.
- **Dữ liệu chính xác:** Sử dụng ScraperAPI vượt qua mọi tường lửa, chặn bot hay CAPTCHA của Amazon, Walmart, Google.
- **Cảnh báo kịp thời:** Phát hiện ngay các mặt hàng giảm giá sâu và tổng hợp vào một email digest gọn gàng.
- **Lưu trữ lịch sử:** Tự động ghi nhận biến động giá vào Data Table để dễ dàng phân tích xu hướng.
:::

### Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **ScraperAPI Account:** Tài khoản và API Key để truy xuất dữ liệu sản phẩm từ Amazon, Walmart và Google Shopping.
- **Email Service/Gmail Account:** Cấu hình tài khoản Gmail hoặc SMTP provider để gửi email thông báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ n8n template hoặc copy trực tiếp và paste vào không gian làm việc (n8n Editor) của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các node sau để hệ thống chạy mượt mà:
- **Morning Schedule Trigger / Manual Trigger Setup:** Kiểm tra thời gian chạy định kỳ (mặc định 8h sáng mỗi ngày) hoặc dùng trigger thủ công để test hệ thống lần đầu.
- **Initialize Products Table & Initialize History Table:** Khởi tạo cấu trúc Data Table trong n8n để lưu danh sách sản phẩm và lịch sử giá.
- **Scrape Amazon Data, Scrape Walmart Data, Scrape Google Shopping Data:** Điền ScraperAPI Credentials (API Key) để các node này có thể gọi dữ liệu thành công từ 3 nền tảng thương mại lớn.
- **Email Price Drop Notice / Send Digest via Gmail:** Kết nối tài khoản Gmail hoặc cấu hình thông số SMTP để hệ thống gửi email bản tin tổng hợp giá giảm.

#### 3. Kích hoạt ⚡️
- Chạy thử công (Test run) bằng nút **Manual Trigger Setup** và khởi tạo các bảng dữ liệu mẫu (`Generate Sample Products`, `Add Samples to Products Table`).
- Kiểm tra kết quả trả về ở các node trung gian và hộp thư đến xem email đã được định dạng đẹp mắt chưa.
- Bật công tắc **Active** để workflow tự động vận hành hàng ngày.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh Chat:** Thay vì chỉ nhận email, các sếp có thể nối thêm node Telegram hoặc Slack để nhận thông báo giá giảm ngay lập tức trên điện thoại.
- **Mở rộng danh mục:** Thêm các sản phẩm mới vào Data Table bằng cách tùy chỉnh node `Generate Sample Products` hoặc tạo Google Sheet đồng bộ trực tiếp.
- **Báo cáo hàng tuần:** Tạo thêm nhánh tổng hợp báo cáo biến động giá hàng tuần để có cái nhìn toàn diện hơn về thị trường.

### 📌 Kết luận
Workflow này là trợ thủ đắc lực giúp các tín đồ săn sale hoặc các nhà kinh doanh e-commerce nắm bắt mọi biến động giá trên thị trường mà không tốn một phút sức lực thủ công nào. Hãy áp dụng ngay vào hệ thống n8n của các sếp nhé!