---
title: "🚀 Tự động làm giàu dữ liệu doanh nghiệp bằng Perplexity AI và Google Sheets trên n8n"
description: "Hướng dẫn xây dựng hệ thống tự động quét, nghiên cứu thông tin doanh nghiệp qua Perplexity AI và cập nhật trực tiếp vào Google Sheets với n8n."
slug: "tu-dong-lam-giau-du-lieu-doanh-nghiep-perplexity-ai-google-sheets"
tags: [n8n, automation, no-code, perplexity-ai, lead-generation, google-sheets]
keywords: [n8n workflow, làm giàu dữ liệu, company data enrichment, perplexity ai n8n, google sheets automation]
---

# 🚀 Tự động làm giàu dữ liệu doanh nghiệp (Company Data Enrichment) với Perplexity AI & Google Sheets

Các sếp có đang đau đầu mỗi khi nhận được một danh sách dài dằng dặc các tên miền (domain) công ty và phải mất hàng giờ đồng hồ để tìm kiếm thủ công các thông tin như: quy mô nhân sự, doanh thu, địa chỉ trụ sở, số điện thoại hay trang LinkedIn? Việc làm thủ công này không chỉ cực kỳ tốn thời gian, dễ sai sót mà còn làm giảm năng suất của đội ngũ Sales và Marketing.

Giải pháp là đây! Workflow n8n này sẽ tự động hóa 100% quy trình nghiên cứu doanh nghiệp. Hệ thống sẽ đọc danh sách domain từ Google Sheets, nhờ Perplexity AI "đào bới" thông tin chi tiết trên internet, sau đó tự động điền ngược lại bảng tính và đánh dấu trạng thái hoàn thành. Các sếp chỉ việc ngồi nhâm nhi ly cà phê và nhận dữ liệu sạch.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không sợ sập nguồn hay mất kết nối, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Tự động hóa hoàn toàn việc research thông tin công ty với tốc độ ~2-3 phút cho mỗi batch (10 domain).
- **Dữ liệu chính xác, trung thực:** Perplexity AI trả về nguồn (source URL) minh bạch; nếu thiếu dữ liệu, AI sẽ để trống thay vìa bịa đặt thông tin (no fake data).
- **Tối ưu chi phí:** Chỉ tốn khoảng ~$0.005 cho mỗi 10 domain nhờ cơ chế gom nhóm (batching).
- **Vận hành thông minh:** Tự động lọc các domain chưa xử lý (`processed = ""`) để tránh lặp lại công việc khi chạy nhiều lần.
:::

### Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google Sheets Template:** [Copy bản mẫu tại đây](https://docs.google.com/spreadsheets/d/1bdK8xskt-qfLlDwdzolM0zFyo9KxZ-HHpTVxcEw3ZMY/edit?usp=sharing) (Bao gồm các cột: `domain`, `processed` và tab tên `Data`).
- **Perplexity AI API Key** (Đăng ký tại trang chủ Perplexity).
- **Google Sheets OAuth2 Credentials** kết nối trực tiếp với tài khoản Google của các sếp.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này, dán thẳng vào trình soạn thảo n8n (n8n Editor) hoặc import file JSON trực tiếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà không lỗi, các sếp cần chú ý cấu hình các node sau:
- **Fetch Unproved Domains & Save Enriched Data (Google Sheets Nodes):** 
  - Chọn đúng Credentials Google Sheets OAuth2.
  - Thay thế `Spreadsheet ID` mặc định trong template bằng `Spreadsheet ID` của bảng tính mà các sếp vừa copy.
  - Đảm bảo tên Tab chính xác là `Data` và cấu hình bộ lọc lấy các dòng có cột `processed` đang trống.
- **Perplexity AI Research (HTTP Request Node):** 
  - Chọn Credentials loại `perplexityApi` và điền API Key của các sếp vào.
- **Batch Process Domains (Split in Batches Node):** 
  - Mặc định chia batch 10 domain/lần để tối ưu tốc độ và chi phí. Các sếp có thể điều chỉnh con số này tùy theo nhu cầu.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** để chạy thử nghiệm với vài dòng dữ liệu mẫu đầu tiên.
- Kiểm tra kết quả trả về trong Google Sheets. Nếu mọi thứ xanh mướt và dữ liệu đổ về đầy đủ, hãy bật công tắc **Active** để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống xịn sò hơn nữa, các sếp có thể tùy biến thêm:
- **Tích hợp Slack / Telegram:** Thêm node thông báo về kênh chat ngay khi workflow hoàn thành việc quét một batch domain.
- **Mở rộng trường dữ liệu:** Tùy chỉnh câu lệnh prompt trong HTTP Request để lấy thêm các thông tin chuyên sâu như công nghệ sử dụng, tên CEO, hoặc email liên hệ.
- **Tự động hóa định kỳ:** Kết hợp thêm node **Schedule Trigger** để hệ thống tự động quét danh sách domain mới mỗi ngày hoặc mỗi tuần mà không cần bấm tay.

### 📌 Kết luận
Việc làm giàu dữ liệu khách hàng (Lead Enrichment) chưa bao giờ dễ dàng đến thế với sự trợ giúp của n8n và AI. Hãy áp dụng ngay workflow này để tối ưu hóa quy trình sales của doanh nghiệp ngay hôm nay các sếp nhé!