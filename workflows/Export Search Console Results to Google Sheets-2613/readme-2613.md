---
title: "🚀 Tự động đồng bộ Google Search Console vào Google Sheets với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động lấy báo cáo từ Google Search Console (từ khóa, trang, ngày) và lưu trữ trực tiếp vào Google Sheets theo lịch trình."
slug: "tu-dong-sync-google-search-console-vao-google-sheets"
tags: [n8n, automation, seo, google-search-console, google-sheets, marketing]
keywords: [n8n workflow, export search console to google sheets, tự động hóa seo, google search console api, n8n marketing automation]
---

# 🚀 Tự động đồng bộ Google Search Console vào Google Sheets với n8n

Các sếp làm SEO hay Digital Marketing chắc chắn đã quá quen thuộc với việc mỗi tuần hoặc mỗi tháng phải vào Google Search Console, thủ công xuất (export) dữ liệu từ khóa, trang đích (pages), hiệu suất theo ngày rồi gom lại vào Google Sheets để báo cáo. Công việc lặp đi lặp lại này vừa tốn thời gian, vừa dễ thiếu sót dữ liệu lịch sử.

Với workflow n8n này, các sếp sẽ tự động hóa 100% quy trình trên. Hệ thống sẽ tự động gọi API của Google Search Console theo lịch trình định sẵn, xử lý dữ liệu và cập nhật trực tiếp vào Google Sheets mà không cần động tay chân!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm hàng giờ mỗi tuần:** Không còn cảnh copy/paste dữ liệu Search Console thủ công.
- **Lưu trữ dữ liệu lịch sử chuẩn xác:** Theo dõi sát sao biến động từ khóa, clicks, impressions, CTR và vị trí trung bình (position).
- **Tự động hóa hoàn toàn:** Chạy ngầm theo lịch (Schedule Trigger) hàng ngày, hàng tuần tùy ý.
- **Báo cáo sẵn sàng:** Dữ liệu được đẩy thẳng vào Google Sheets, sẵn sàng để vẽ biểu đồ báo cáo cho sếp lớn hoặc khách hàng.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động.
- Tài khoản Google có quyền truy cập vào Google Search Console và Google Sheets.
- Google OAuth 2.0 Credentials cấu hình sẵn trong n8n với các scope truy cập: `https://www.googleapis.com/auth/webmasters`, `https://www.googleapis.com/auth/webmasters.readonly`.
- Bản sao Google Sheet mẫu để nhận dữ liệu: [Google Sheets Template](https://docs.google.com/spreadsheets/d/10hSuGOOf14YvVY2Bw8WXUIpsyXO614l7qNEjkyVY_Qg/edit?usp=sharing)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow, dán trực tiếp vào n8n Editor hoặc import file JSON tải từ trang gốc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node sau:

- **Schedule Trigger:** Thiết lập mốc thời gian chạy tự động (ví dụ: chạy mỗi ngày vào lúc 2 giờ sáng).
- **Set your domain:** Thay đổi tên miền website của các sếp (định dạng URL property hoặc Domain property của Search Console).
- **Các node HTTP Request (`date`, `Get query Report`, `Get Page Report`):** 
  - Chọn Google OAuth2 Credentials đã kết nối với tài khoản Google Search Console.
  - Tùy chỉnh dải ngày (date ranges) trong phần Body của request nếu muốn lấy mốc thời gian khác.
- **Các node Google Sheets (`Update queries to Sheets`, `Update Pages to Sheets`, `Update date report to sheets`):**
  - Kết nối Google Sheets OAuth2 API.
  - Thay thế link Google Sheets mặc định bằng link bản sao Google Sheet của các sếp đã chuẩn bị ở phần chuẩn bị.
  - Kiểm tra chế độ `appendOrUpdate` tại mục `keyParameters` để đảm bảo dữ liệu không bị trùng lặp.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử nghiệm thủ công và kiểm tra dữ liệu trả về ở các node `Split Out` và `Edit Fields`.
- Sau khi kiểm tra mọi thứ đã khớp lệnh, bật công tắc **Active** để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối thông báo:** Thêm node Telegram hoặc Slack vào cuối workflow để nhận thông báo ngay khi dữ liệu được đồng bộ thành công hoặc nếu có lỗi xảy ra.
- **Mở rộng báo cáo:** Tận dụng dữ liệu trong Google Sheets để kết nối với Google Looker Studio, tạo dashboard SEO trực quan theo thời gian thực.
- **Quản lý nhiều domain:** Nhân bản các node xử lý để quét dữ liệu tự động cho một hệ thống nhiều website cùng lúc.

### 📌 Kết luận
Việc tối ưu hóa quy trình làm SEO chưa bao giờ dễ dàng đến thế với n8n. Hãy thiết lập ngay workflow này để giải phóng bản thân khỏi những tác vụ thủ công và tập trung vào chiến lược phát triển website bền vững các sếp nhé!