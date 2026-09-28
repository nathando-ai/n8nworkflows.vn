---
title: "🚀 Tự động khám phá, bổ sung và lưu trữ dữ liệu tiền điện tử với CoinMarketCap API"
description: "Xây dựng hệ thống tự động quét, lọc và lưu trữ dữ liệu hàng trăm đồng tiền mã hóa (crypto) từ CoinMarketCap vào NocoDB hoàn toàn tự động bằng n8n."
slug: "tu-dong-kham-pha-du-lieu-crypto-coinmarketcap-n8n"
tags: [n8n, automation, no-code, crypto, coinmarketcap, nocodb]
keywords: [n8n workflow, coinmarketcap api, tự động hóa crypto, nocodb n8n, thu thập dữ liệu tiền mã hóa]
---

# 🚀 Tự động khám phá, bổ sung và lưu trữ dữ liệu tiền điện tử với CoinMarketCap API

Các sếp làm trong lĩnh vực crypto hay nghiên cứu thị trường chắc chắn hiểu cảm giác mệt mỏi khi phải thủ công truy cập CoinMarketCap, tìm kiếm từng đồng coin, lọc website chính thức và copy-paste vào bảng dữ liệu. Công việc lặp đi lặp lại này vừa tốn thời gian, vừa dễ thiếu sót.

Workflow n8n này sinh ra để giải quyết triệt để vấn đề đó! Nó tự động hóa 100% quy trình: định kỳ quét dữ liệu từ CoinMarketCap API, làm sạch thông tin, lọc ra các website chính thức hợp lệ và lưu trữ gọn gàng vào database (NocoDB) mà không cần viết một dòng code phức tạp nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hoàn toàn**: Lịch trình chạy tự động (3 ngày/lần hoặc tùy chỉnh) giúp cập nhật dữ liệu crypto liên tục.
- **Dữ liệu sạch & chất lượng**: Tự động trích xuất, chuẩn hóa URL website (ép HTTPS), loại bỏ các token rác hoặc thiếu thông tin.
- **Tối ưu giới hạn API**: Sử dụng cơ chế chia lô (batching) và khoảng nghỉ thông minh để không bao giờ vượt quá giới hạn của Free API.
- **Lưu trữ linh hoạt**: Dữ liệu được gom nhóm gọn gàng và lưu thẳng vào NocoDB (hoặc Google Sheets, Airtable tùy ý).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n**: Đã hoạt động (Cloud hoặc Self-hosted).
- **CoinMarketCap API Key**: Đăng ký tài khoản miễn phí trên CoinMarketCap Developer Portal để lấy API Key.
- **NocoDB (hoặc Storage thay thế)**: Tài khoản NocoDB kèm API Token / Credentials để lưu trữ bảng dữ liệu.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này và dán trực tiếp vào n8n Editor của mình, hoặc import file JSON tải từ nguồn.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 16 nodes được sắp xếp logic qua 7 bước. Các sếp cần chú ý cấu hình các điểm sau:
- **Node `Every 3 Days At 10AM` (Schedule Trigger)**: Nơi thiết lập lịch chạy tự động. Các sếp có thể đổi tần suất tùy theo nhu cầu thực tế.
- **Node `Get 100 Tokens From CMC` & `Get Token Details From CMC` (HTTP Request)**: 
  - Tại đây các sếp cần thêm Credentials dạng **Header Auth** hoặc queryParam chứa **CoinMarketCap API Key** của mình.
- **Node `ADD TO CMC Sheet` (NocoDB)**: 
  - Chọn đúng Credentials kết nối với tài khoản NocoDB của các sếp.
  - Trỏ đến đúng Project, Table nơi lưu trữ dữ liệu token đầu ra (Name, Symbol, Website, Source, Timestamp...). *Lưu ý: Các sếp hoàn toàn có thể thay node này bằng Google Sheets hoặc Airtable nếu muốn.*
- **Các node Code (`Generate Random Page`, `CMC Token DATA`, `DATA`)**: Các đoạn mã xử lý dữ liệu JavaScript có sẵn đã được tối ưu, các sếp chỉ cần giữ nguyên cấu trúc.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** để chạy thử nghiệm thủ công với một vài bản ghi đầu tiên, kiểm tra xem dữ liệu đổ về NocoDB chính xác chưa.
- Sau khi test OK, gạt công tắc **Active** góc trên bên phải để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo**: Nối thêm node Telegram hoặc Slack vào cuối workflow để nhận thông báo ngay lập tức mỗi khi quét xong danh sách token mới.
- **Mở rộng lưu trữ**: Ngoài NocoDB, các sếp có thể đẩy dữ liệu sang Google Sheets để tiện chia sẻ cho team marketing hoặc phân tích.
- **Quản lý Rate Limit**: Nếu dùng gói API trả phí của CoinMarketCap, các sếp có thể giảm thời gian chờ ở node `Wait 1 Min` để tăng tốc độ quét dữ liệu.

### 📌 Kết luận
Với workflow này, việc xây dựng một cơ sở dữ liệu tiền điện tử tự cập nhật chưa bao giờ dễ dàng đến thế. Hãy cài đặt ngay để tiết kiệm hàng giờ đồng hồ làm việc thủ công mỗi tuần và tập trung vào các chiến lược đầu tư cốt lõi!