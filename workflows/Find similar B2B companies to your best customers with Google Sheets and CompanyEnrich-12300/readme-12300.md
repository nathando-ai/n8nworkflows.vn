---
title: "🚀 Tự động tìm kiếm công ty B2B tương tự khách hàng tốt nhất bằng n8n và CompanyEnrich"
description: "Hướng dẫn xây dựng workflow n8n tự động đọc danh sách domain từ Google Sheets, gọi API CompanyEnrich tìm kiếm các công ty lookalike và lưu kết quả ngược lại Google Sheets."
slug: "tim-kiem-cong-ty-b2b-tu-tuong-tu-google-sheets-companyenrich"
tags: [n8n, automation, no-code, lead-generation, google-sheets, companyenrich, b2b-sales]
keywords: [n8n workflow, tự động hóa lead gen, tìm kiếm công ty B2B, CompanyEnrich API, Google Sheets automation]
---

# 🚀 Tự động tìm kiếm công ty B2B tương tự khách hàng tốt nhất với n8n và CompanyEnrich

Các sếp làm sales B2B chắc chắn hiểu cảm giác mệt mỏi khi phải thủ công đi tìm các khách hàng tiềm năng mới có đặc điểm giống với những khách hàng hiện tại đang mang lại doanh thu cao. Việc này vừa tốn hàng giờ đồng hồ lướt LinkedIn, tra cứu Google, vừa dễ bỏ sót các "mỏ vàng" tiềm năng. 

Workflow n8n này sinh ra để giải quyết triệt để vấn đề đó! Bằng cách kết hợp **Google Sheets** và **CompanyEnrich API**, hệ thống sẽ tự động phân tích danh sách domain khách hàng mẫu của các sếp, tìm ra hàng loạt các công ty tương tự (lookalike companies) và gom toàn bộ thông tin chi tiết (Tên công ty, Domain, Điểm số tương đồng) lưu thẳng về Google Sheets hoàn toàn tự động.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Mở rộng tệp khách hàng tự động:** Tự động tìm hàng loạt công ty B2B có chung ADN với khách hàng tốt nhất hiện tại.
- **Tiết kiệm 90% thời gian:** Thay vì tìm kiếm thủ công từng nhà, workflow xử lý hàng loạt domain trong vài phút.
- **Dữ liệu sạch và có cấu trúc:** Mọi kết quả gồm Tên công ty, Domain và Điểm tương đồng (Similarity Score) được cập nhật thẳng vào Google Sheets.
- **Vận hành không gián đoạn:** Kích hoạt thủ công khi cần hoặc dễ dàng chuyển sang chạy lịch trình định kỳ (Cron/Schedule).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Google Account:** Tài khoản Google Sheets để lưu danh sách nguồn và bảng kết quả.
- **CompanyEnrich API Key:** Tài khoản và API Key từ [CompanyEnrich](https://companyenrich.com) để truy xuất dữ liệu doanh nghiệp độc quyền.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trong n8n, sau đó copy toàn bộ mã nguồn JSON của workflow này và paste trực tiếp vào giao diện n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà không lỗi, các sếp nhớ cấu hình kỹ các node sau:

- **Read Source List (Google Sheets):** 
  - Kết nối tài khoản Google thông qua `googleSheetsOAuth2Api`.
  - Chọn đúng File Google Sheet và Tab chứa danh sách website mục tiêu. Đảm bảo có cột tên là `Domain`.
- **Fetch Similar Companies (HTTP Request):** 
  - Mở phần cấu hình Headers, tìm trường `Authorization`.
  - Thay thế đoạn chữ mẫu bằng API Key thực tế của các sếp theo định dạng Bearer Token (`Bearer YOUR_API_KEY`).
- **Write Results (Google Sheets):** 
  - Kết nối tài khoản Google Sheets.
  - Chọn File Google Sheet và Tab thứ hai (dành riêng để chứa kết quả trả về, thao tác `Append`).

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** để chạy thử nghiệm (Test run) với dữ liệu mẫu từ Google Sheets.
- Kiểm tra lại Google Sheet kết quả xem dữ liệu đã đổ về chuẩn chỉnh chưa.
- Gạt công tắc sang **Active** để chính thức đưa workflow vào vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh thông báo:** Nối thêm node Telegram hoặc Slack vào cuối workflow để nhận thông báo ngay khi hệ thống tìm xong danh sách công ty mới.
- **Lọc điểm số tương đồng:** Thêm node `If` sau bước xử lý dữ liệu để chỉ lưu lại những công ty có điểm Similarity Score vượt mức kỳ vọng (ví dụ > 80%).
- **Tự động hóa định kỳ:** Thay thế node `Manual Trigger` bằng `Schedule Trigger` để n8n tự động quét và làm giàu dữ liệu hàng tuần hoặc hàng tháng.

### 📌 Kết luận
Việc tìm kiếm khách hàng B2B tiềm năng chưa bao giờ dễ dàng đến thế khi áp dụng sức mạnh tự động hóa của n8n kết hợp dữ liệu doanh nghiệp từ CompanyEnrich. Hãy thiết lập ngay hôm nay để đội ngũ sales của các sếp luôn có nguồn lead chất lượng cao mỗi ngày!