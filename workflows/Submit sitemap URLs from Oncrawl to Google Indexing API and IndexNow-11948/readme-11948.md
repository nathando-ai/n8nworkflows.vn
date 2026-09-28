---
title: "🚀 Tự động gửi sitemap URLs từ Oncrawl lên Google Indexing API và IndexNow"
description: "Hướng dẫn tự động hóa gửi sitemap URLs từ Oncrawl lên Google Indexing API và IndexNow để tăng tốc độ lập chỉ mục và cải thiện SEO"
slug: "tu-dong-gui-sitemap-urls-tu-oncrawl-len-google-indexing-api-va-indexnow"
tags: [n8n, automation, no-code, SEO, Google Indexing API, IndexNow]
keywords: [n8n workflow, tự động hóa, SEO, Google Indexing API, IndexNow, Oncrawl]
---

# 🚀 Tự động gửi sitemap URLs từ Oncrawl lên Google Indexing API và IndexNow

[Các sếp đang gặp khó khăn khi phải thủ công gửi sitemap URLs lên Google Indexing API và IndexNow để tăng tốc độ lập chỉ mục. Workflow này giúp tự động hóa toàn bộ quá trình này một cách hoàn toàn không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động gửi hàng nghìn URLs lên Google và IndexNow mà không cần can thiệp thủ công.
- Tăng tốc độ lập chỉ mục: Giảm thời gian chờ đợi cho các trang web được lập chỉ mục.
- Cải thiện SEO: Đảm bảo nội dung mới nhất của các sếp luôn được tìm thấy trên các công cụ tìm kiếm.
- Hoạt động liên tục: Workflow chạy tự động 24/7, không cần giám sát.
- Cá nhân hóa: Lọc và gửi chỉ những URLs quan trọng nhất trong khoảng thời gian được chỉ định.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Oncrawl với API access đã kích hoạt.
- API Key từ Oncrawl (có thể tạo trong User Account profile > tokens > + Add API access token).
- IndexNow Key từ Bing Webmaster tools (có thể tạo [tại đây](https://www.bing.com/indexnow/getstarted)).
- Google Indexing API đã được kích hoạt trong Google Search Console.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/11948).
2. Click vào nút "Download" để tải file JSON.
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Config"**:
   - Cập nhật các biến sau trong node "Config":
     - `SITE_URL`: URL của trang web của các sếp.
     - `SITEMAP_URL`: URL của sitemap.xml. Nếu có nhiều sitemap, các sếp có thể sao chép và sửa đổi trường này.
     - `INDEXNOW_KEY`: Key được tạo từ Bing Webmaster tools.
     - `INDEXNOW_KEY_URL`: Thường là domain của các sếp kết hợp với INDEXNOW_KEY (ví dụ: `wwww.example.com/<INDEXNOW_KEY>`).
     - `DAYS_BACK`: Số ngày để lọc URLs mới (mặc định là 7).
     - `BATCH_SIZE`: Kích thước batch cho IndexNow (mặc định là 500).
     - `USE_GOOGLE`, `USE_INDEXNOW`: Đặt thành `true` để chạy cho cả Google và IndexNow.

2. **Node "Webhook"**:
   - Cập nhật `path` trong node "Webhook" để tránh xung đột với các workflow khác.

3. **Node "Get Orphan Pages" và "Get Crawl over crawl"**:
   - Đảm bảo các node này được cấu hình đúng với API Key của Oncrawl.

4. **Node "IndexNow Submit"**:
   - Đảm bảo `INDEXNOW_KEY` và `INDEXNOW_KEY_URL` đã được cấu hình chính xác.

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
2. Bật Active workflow để bắt đầu tự động hóa.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi workflow hoàn thành.
- Lưu log các URLs đã gửi để theo dõi hiệu suất.
- Gửi báo cáo định kỳ về số lượng URLs đã được lập chỉ mục.
- Tích hợp với các công cụ phân tích SEO khác để theo dõi hiệu quả của workflow.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quá trình gửi sitemap URLs lên Google Indexing API và IndexNow, tiết kiệm thời gian và tăng tốc độ lập chỉ mục. Hãy áp dụng ngay để cải thiện SEO và tăng khả năng hiển thị của nội dung trên các công cụ tìm kiếm.