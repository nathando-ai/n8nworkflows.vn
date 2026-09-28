---
title: "🚀 Tự động hóa Scrape Website với Airtop & Google Sheets - Không cần code"
description: "Hướng dẫn chi tiết cách tự động scrape website theo độ sâu (depth) với Airtop và lưu kết quả vào Google Sheets, Google Docs - giải pháp hoàn hảo cho SEO, nghiên cứu thị trường và thu thập dữ liệu"
slug: "tu-dong-hoa-scrape-website-voi-airtop-google-sheets"
tags: [n8n, automation, no-code, web-scraping, google-sheets, google-docs]
keywords: [n8n workflow, tự động hóa scrape website, Airtop, Google Sheets, Google Docs, thu thập dữ liệu]
---

# 🚀 Tự động hóa Scrape Website với Airtop & Google Sheets - Không cần code

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp có bao giờ phải thu thập dữ liệu từ nhiều trang web liên kết nhau? Việc này thường tốn thời gian và dễ gây lỗi khi làm thủ công. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình từ scrape website đến lưu trữ dữ liệu vào Google Sheets và Google Docs, với khả năng điều chỉnh độ sâu (depth) để thu thập dữ liệu từ nhiều trang liên kết.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa toàn bộ quy trình scrape website từ 30-50% thời gian làm thủ công.
- Chính xác: Giảm thiểu lỗi do làm thủ công, đảm bảo dữ liệu được thu thập đầy đủ và chính xác.
- Cá nhân hóa: Điều chỉnh độ sâu (depth) để thu thập dữ liệu từ nhiều trang liên kết khác nhau.
- Hoạt động liên tục: Chạy tự động theo lịch hoặc kích hoạt bằng form, không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google và quyền truy cập vào Google Sheets, Google Docs.
- API Key từ [Airtop](https://portal.airtop.ai/api-keys) (miễn phí).
- Credentials cho Google Sheets và Google Docs đã được cấu hình trong n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập trang [Workflow gốc](https://n8n.io/workflows/4252).
2. Nhấn nút "Copy JSON" để sao chép nội dung workflow.
3. Trong n8n Editor, nhấn vào "Import from Clipboard" và dán nội dung đã sao chép.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node "On form submission" (formTrigger)**:
   - Cấu hình form để nhận các tham số đầu vào: Seed URL, Links must contain, Depth.

2. **Node "Load info to spreadsheet" (googleSheets)**:
   - Chọn credentials Google Sheets đã cấu hình.
   - Điền Spreadsheet ID và Sheet Name để lưu trữ dữ liệu.

3. **Node "Scrape webpage" (airtop)**:
   - Chọn credentials Airtop đã cấu hình.
   - Điền URL cần scrape và cấu hình các tham số khác như prompt, extractor, v.v.

4. **Node "Create Google Docs" (googleDocs)**:
   - Chọn credentials Google Docs đã cấu hình.
   - Điền tên tài liệu và cấu hình các tham số khác như title, content, v.v.

5. **Node "Read scraped webpages" (googleSheets)**:
   - Chọn credentials Google Sheets đã cấu hình.
   - Điền Spreadsheet ID và Sheet Name để đọc dữ liệu.

6. **Node "Retrieve links to scrape" (airtop)**:
   - Chọn credentials Airtop đã cấu hình.
   - Điền URL cần scrape và cấu hình các tham số khác như prompt, extractor, v.v.

7. **Node "Insert new links" (googleSheets)**:
   - Chọn credentials Google Sheets đã cấu hình.
   - Điền Spreadsheet ID và Sheet Name để lưu trữ dữ liệu.

8. **Node "Scrape webpage1" (airtop)**:
   - Chọn credentials Airtop đã cấu hình.
   - Điền URL cần scrape và cấu hình các tham số khác như prompt, extractor, v.v.

9. **Node "Update with new scraped content" (googleDocs)**:
   - Chọn credentials Google Docs đã cấu hình.
   - Điền tên tài liệu và cấu hình các tham số khác như title, content, v.v.

10. **Node "Insert flag" (googleSheets)**:
    - Chọn credentials Google Sheets đã cấu hình.
    - Điền Spreadsheet ID và Sheet Name để lưu trữ dữ liệu.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm bộ lọc**: Lọc các liên kết cần theo dõi dựa trên domain, path hoặc loại nội dung.
- **Kết hợp với Scheduler**: Chạy workflow theo lịch để liên tục khám phá các trang mới được phát hiện.
- **Xuất dữ liệu có cấu trúc**: Mở rộng quy trình để lưu trữ dữ liệu đã trích xuất vào CSV hoặc cơ sở dữ liệu để phân tích.
- **Kết hợp với Slack/Telegram**: Nhận thông báo khi quá trình scrape hoàn thành hoặc gặp lỗi.

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc tự động hóa scrape website với độ sâu tùy chỉnh, giúp tiết kiệm thời gian và đảm bảo dữ liệu được thu thập đầy đủ và chính xác. Các sếp có thể dễ dàng áp dụng và tùy chỉnh workflow này để phù hợp với nhu cầu cụ thể của mình.