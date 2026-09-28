---
title: "🚀 Tự Động Tạo Sitemap Website và Cây Cấu Trúc Trực Quan Với Firecrawl & Google Sheets"
description: "Hướng dẫn chi tiết cách xây dựng workflow n8n tự động quét bản đồ website, xử lý dữ liệu và đồng bộ hóa vào Google Sheets bằng Firecrawl và Google Drive."
slug: "tao-sitemap-website-va-cay-cau-truc-voi-firecrawl-google-sheets"
tags: [n8n, automation, no-code, firecrawl, google-sheets, ai, market-research]
keywords: [n8n workflow, tự động hóa sitemap, firecrawl n8n, google sheets automation, phân tích website, market research]
keywords: [n8n workflow, tự động hóa, tạo sitemap website, firecrawl n8n, google sheets automation]
---

# 🚀 Tự Động Tạo Sitemap Website và Cây Cấu Trúc Trực Quan Với Firecrawl & Google Sheets

Việc phân tích cấu trúc website của đối thủ hoặc chính trang web của bạn thường tốn rất nhiều thời gian nếu làm thủ công. Các sếp thường phải dùng các công cụ trả phí đắt đỏ hoặc viết script phức tạp chỉ để lấy danh sách toàn bộ URL và sơ đồ trang web.

Đừng lo, workflow **"Generate Website Sitemaps & Visual Trees with Firecrawl and Google Sheets"** do *Growth AI* phát triển sẽ giải quyết triệt để bài toán này. Với nợn và sức mạnh từ **Firecrawl**, các sếp có thể quét toàn bộ website, lập bản đồ URL, sao lưu template Google Drive và tự động điền dữ liệu vào Google Sheets chỉ trong vòng một nốt nhạc!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Chỉ cần nhập URL qua chat hoặc webhook, hệ thống tự động quét và phân loại toàn bộ sitemap.
- **Lưu trữ thông minh:** Tự động copy Google Sheets template có sẵn và ghi dữ liệu URL đã phân loại vào bảng tính một cách ngăn nắp.
- **Tiết kiệm thời gian & chi phí:** Thay vì mất hàng giờ đồng hồ crawl dữ liệu thủ công, workflow xử lý gọn gàng chỉ trong vài giây.
- **Hỗ trợ nghiên cứu thị trường (Market Research):** Giúp các sếp dễ dàng phân tích cấu trúc website đối thủ cạnh tranh để tối ưu SEO hoặc xây dựng chiến lược nội dung.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **n8n instance** (Self-hosted hoặc Cloud).
- **Firecrawl API Key** (dùng cho node Map a website).
- **Tài khoản Google** (kết nối Google Drive OAuth2 và Google Sheets OAuth2).
- **Google Sheets Template mẫu** (dùng cho node Copy template).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể copy mã JSON của workflow từ nguồn cung cấp và dán trực tiếp vào n8n Editor, hoặc tải file JSON về và chọn **Import from File** trong giao diện n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 8 nodes hoạt động nhịp nhàng với nhau. Các sếp cần chú ý cấu hình kỹ các node sau:

- **When chat message received (`chatTrigger`):** Điểm khởi đầu nhận yêu cầu từ người dùng (URL website cần quét). Các sếp có thể thay đổi thành Webhook nếu muốn tích hợp lên web app riêng.
- **Map a website and get urls (`@mendable/n8n-nodes-firecrawl.firecrawl`):** 
  - Chọn Credentials: `firecrawlApi`.
  - Cấu hình operation là `map` để lấy toàn bộ danh sách URL từ website mục tiêu.
- **Firecrawl OK (`if`):** Kiểm tra xem quá trình crawl dữ liệu từ Firecrawl có thành công hay trả về lỗi.
- **Copy template (`googleDrive`):** 
  - Chọn Credentials: `googleDriveOAuth2Api`.
  - Thiết lập file ID gốc của Google Sheets template để hệ thống tự động nhân bản cho mỗi lần chạy mới.
- **Sorting URL into table (`code`):** Node Javascript giúp xử lý, phân loại và định dạng lại danh sách URL thành cấu trúc bảng gọn gàng.
- **Data mapping (`googleSheets`):** 
  - Chọn Credentials: `googleSheetsOAuth2Api`.
  - Điền Spreadsheet ID (lấy từ file vừa copy ở bước trên) và chọn Sheet Name để append dữ liệu URL vào bảng.
- **Final answer / Bad URL (`respondToWebhook`):** Phản hồi kết quả thành công kèm đường dẫn Google Sheets hoặc thông báo lỗi nếu URL không hợp lệ.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và thử nhập một URL bất kỳ để test xem dữ liệu có đổ về Google Sheets chuẩn chỉnh không.
- Sau khi test ngon lành, hãy gạt công tắc **Active** ở góc trên bên phải để workflow chính thức đi vào hoạt động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack / Telegram:** Thêm một node gửi thông báo về nhóm chat của công ty ngay khi workflow tạo xong sitemap và Google Sheets thành công.
- **Gửi báo cáo qua Email:** Sử dụng node Gmail hoặc SendGrid để tự động gửi link Google Sheets trực tiếp cho khách hàng hoặc sếp tổng.
- **Lưu log lỗi:** Kết nối nhánh `Bad URL` vào một bảng Google Sheets riêng để theo dõi các URL bị lỗi hoặc website không phản hồi.

### 📌 Kết luận
Workflow **Generate Website Sitemaps & Visual Trees** là một "vũ khí" cực kỳ lợi hại cho các chuyên gia SEO, Marketer và nhà phát triển web. Hãy cài đặt ngay hôm nay để tự động hóa toàn bộ quy trình nghiên cứu cấu trúc website của các sếp!