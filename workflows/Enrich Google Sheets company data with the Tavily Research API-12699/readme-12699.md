---
title: "🚀 Tự động làm giàu dữ liệu công ty trên Google Sheets với Tavily Research API"
description: "Hướng dẫn xây dựng workflow n8n tự động đọc, tìm kiếm thông tin doanh nghiệp qua Tavily AI Research và cập nhật trực tiếp lên Google Sheets."
slug: "tu-dong-lam-giau-du-lieu-cong-ty-google-sheets-tavily-api"
tags: [n8n, automation, tavily-api, google-sheets, lead-generation, ai-research]
keywords: [n8n workflow, tavily research api, làm giàu dữ liệu công ty, tự động hóa google sheets, lead enrichment n8n]
---

# 🚀 Tự động làm giàu dữ liệu công ty trên Google Sheets với Tavily Research API

Các sếp có đang đau đầu vì danh sách khách hàng tiềm năng (Leads) trên Google Sheets bị thiếu thông tin quan trọng như tên CEO, doanh thu, địa chỉ trụ sở chính (HQ)? Việc ngồi tra cứu thủ công từng công ty trên Google tốn hàng giờ đồng hồ, cực kỳ mất thời gian và nhàm chán.

Đừng lo, bài viết này sẽ hướng dẫn các sếp cách "lên đồ" một workflow n8n cực kỳ thông minh. Workflow này sẽ tự động đọc danh sách công ty, sử dụng sức mạnh của **Tavily Research API** để cào dữ liệu từ internet, tự động điền các thông tin còn thiếu và ghi kết quả sang một Google Sheet mới mà không cần đụng tay vào code!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Quên đi việc tra cứu thủ công từng công ty, tiết kiệm hàng chục giờ làm việc mỗi tuần.
- **Dữ liệu phong phú & chính xác:** Tận dụng AI Web Research từ Tavily để tìm kiếm thông tin sâu và chính xác về doanh nghiệp.
- **Cơ chế Polling thông minh:** Workflow tự động lặp lại kiểm tra tiến độ (polling loop) cho đến khi AI gom đủ dữ liệu (tối đa ~5 phút).
- **An toàn cho dữ liệu gốc:** Đọc dữ liệu từ file gốc và xuất ra một file/sheet mới sạch sẽ, không lo ghi đè nhầm lẫn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n instance:** Bản self-hosted hoặc cloud.
- **Tài khoản Google:** Để kết nối Google Sheets (`googleSheetsOAuth2Api`).
- **Tavily API Key:** Tài khoản Tavily AI để sử dụng API Research (`httpHeaderAuth`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể copy mã JSON của workflow từ n8n (hoặc dùng file mẫu từ template ID 12699) và paste trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình chính xác các node sau để workflow không bị lỗi:

- **Read CSV file (Google Sheets):** 
  - Kết nối tài khoản Google Sheets OAuth2.
  - Nhập **Google Sheet ID** của bảng dữ liệu đầu vào.
  - Chọn đúng tên Sheet chứa danh sách công ty cần làm giàu.
- **Store Original Columns & Code Nodes:** Các node này dùng để xử lý logic lập trình JavaScript cơ bản, lưu lại các cột gốc để không làm mất cấu trúc dữ liệu ban đầu.
- **Start Tavily Research & Check Research Status (HTTP Request):** 
  - Cấu hình thông tin xác thực (`httpHeaderAuth`) bằng Tavily API Key của các sếp.
- **Wait 30s & Polling Logic (If, Code nodes):** 
  - Workflow sử dụng cơ chế chờ 30 giây và kiểm tra lại trạng thái (`Under 5 min?`, `Research Done?`). Đảm bảo không cần chỉnh sửa gì trừ khi muốn thay đổi thời gian chờ.
- **Enrich CSV file (Google Sheets):** 
  - ⚠️ **LƯU Ý QUAN TRỌNG:** Trước khi chạy, các sếp **phải tạo sẵn một Sheet trống** (Output Sheet) nằm trong cùng file Google Sheets chứa dữ liệu đầu vào.
  - Cấu hình Sheet ID và chọn tên Sheet trống này ở node ghi dữ liệu để hệ thống lưu kết quả vào.
  - Đảm bảo các sếp đã tạo sẵn các tên cột muốn tìm kiếm trên sheet trống đó (ví dụ: `CEO`, `Revenue`, `HQ`...).

#### 3. Kích hoạt ⚡️
- Bấm nút **Click to Start** (Manual Trigger) để chạy thử nghiệm (Test Run) với một vài dòng dữ liệu mẫu đầu tiên.
- Kiểm tra kết quả hiển thị bên Sheet output.
- Nếu mọi thứ chạy mượt mà, hãy bật công tắc **Active** để workflow chính thức đi vào hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống tự động hóa này trở nên "bá đạo" hơn, các sếp có thể mở rộng thêm:
- **Tích hợp Slack/Telegram:** Thêm node thông báo về điện thoại/nhóm chat ngay khi workflow hoàn tất việc quét dữ liệu.
- **Web Trigger:** Thay thế node `Click to Start` bằng Webhook hoặc Schedule Trigger để định kỳ hàng tuần tự động làm giàu danh sách khách hàng mới phát sinh.
- **Xử lý hàng loạt (Batching):** Nếu danh sách công ty có hàng nghìn dòng, hãy cấu hình phân lô (split in batches) để tránh vượt quá giới hạn Rate Limit của Tavily API.

### 📌 Kết luận
Việc làm giàu dữ liệu khách hàng chưa bao giờ dễ dàng đến thế nhờ sự kết hợp giữa n8n và Tavily AI Research. Hãy cài đặt ngay hôm nay để tối ưu hóa quy trình Sales và Marketing của doanh nghiệp các sếp nhé!