---
title: "🚀 Tự Động Làm Sạch & Làm Giàu Dữ Liệu Nhà Bán Hàng (Enrich Seller Data) với Bright Data & PostgreSQL"
description: "Hướng dẫn tự động hóa quy trình quét Google Search, tìm kiếm domain và email nhà bán hàng bằng Bright Data, xử lý dữ liệu thông minh và lưu trữ vào PostgreSQL."
slug: "tu-dong-lam-giau-du-lieu-nha-ban-hang-bright-data-postgresql"
tags: [n8n, automation, bright-data, postgresql, lead-generation, sales]
keywords: [n8n workflow, enrich seller data, bright data api, tìm kiếm email tự động, postgresql n8n]
---

# 🚀 Tự Động Làm Sạch & Làm Giàu Dữ Liệu Nhà Bán Hàng (Enrich Seller Data) với Bright Data & PostgreSQL

Các sếp trong ngành Sales, Marketing hay làm nền tảng Thương mại điện tử chắc chắn đều hiểu "nỗi đau" khi sở hữu một danh sách nhà bán hàng thô sơ: thiếu domain website, không có email liên hệ chính xác, hoặc dữ liệu phân mảnh lộn xộn. Việc ngồi thủ công tra cứu từng nhà bán hàng trên Google, click vào từng trang web để tìm email không chỉ ngốn hàng tá thời gian mà còn cực kỳ nhàm chán.

Đừng lo, workflow n8n cực kỳ mạnh mẽ này sẽ giúp các sếp giải quyết triệt để bài toán trên. Hệ thống sẽ tự động đọc dữ liệu từ database, kết hợp sức mạnh cào dữ liệu của **Bright Data**, thực hiện các truy vấn thông minh trên Google Search để tìm domain, trích xuất email chuẩn xác, sau đó làm sạch và cập nhật lại toàn bộ vào **PostgreSQL** mà không cần đụng tay vào thao tác thủ công nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, xử lý hàng ngàn bản ghi mà không lo bị ngắt kết nối, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100% quy trình Data Enrichment**: Biến danh sách nhà bán hàng thô thành profile hoàn chỉnh có đầy đủ Domain và Email.
- **Tiết kiệm 90% thời gian nhân sự**: Thay vì tốn hàng chục giờ tìm kiếm thủ công, workflow chạy tự động theo lịch trình (Schedule) hoặc kích hoạt thủ công khi cần.
- **Dữ liệu sạch sẽ & đồng bộ**: Tự động lọc, tách nhóm và cập nhật (Update) kết quả trực tiếp vào cơ sở dữ liệu PostgreSQL một cách chính xác.
- **Tối ưu hóa chiến dịch Outreach**: Sở hữu email chính chủ của nhà bán hàng giúp tăng tỷ lệ phản hồi cho các chiến dịch Email Marketing hoặc Sales Outreach.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **PostgreSQL Database**: Nơi lưu trữ bảng chứa thông tin nhà bán hàng (có sẵn các bảng để Read và Update dữ liệu).
- **Bright Data Account**: Tài khoản Bright Data để sử dụng API cào dữ liệu Google Search mạnh mẽ và chống chặn IP hiệu quả.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy toàn bộ mã JSON từ nguồn gốc.
- Trong giao diện n8n Editor, chọn **Add workflow** -> Click vào biểu tượng menu (3 chấm) ở góc trên bên phải -> Chọn **Import from File** hoặc **Import from Clipboard** và dán mã JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các thành phần sau:

- **Read the Database (Node PostgreSQL)**: 
  - Chọn Credentials kết nối tới database PostgreSQL của các sếp.
  - Cấu hình câu lệnh `SELECT` để lấy danh sách nhà bán hàng cần làm giàu dữ liệu (ví dụ: các record chưa có email hoặc domain).
- **Process by Batch (Node Split in Batches)**: 
  - Kiểm tra lại kích thước lô (batch size) để tránh quá tải API của Bright Data hoặc vượt quá giới hạn tài nguyên server.
- **BrightData & BrightData1 (Node Bright Data)**: 
  - Chọn Credentials tài khoản Bright Data của các sếp.
  - Theo ghi chú trên canvas, workflow sẽ thực hiện 2 luồng tìm kiếm chính:
    1. *Search Domain+Email in Google*: Nếu có sẵn domain, hệ thống sẽ query với cú pháp `{{$json.domain}}+email`.
    2. *Search Seller Name+Address+Email in Google*: Nếu chưa có domain, hệ thống kết hợp Tên nhà bán hàng + Địa chỉ + Email (`{{$json.seller_name}}+{{ $json.seller_address }}+email`).
- **HTML & HTML1 / Extract Emails (Nodes Xử lý dữ liệu)**: 
  - Các node `HTML`, `Code` (`Extract Emails`), `Filter`, `Aggregate` sẽ làm nhiệm vụ bóc tách mã HTML từ kết quả tìm kiếm Google, lọc ra các định dạng email hợp lệ.
- **Postgres1, Postgres2, Postgres3, Postgres4 (Nodes PostgreSQL Update)**: 
  - Cấu hình lại thông tin bảng, khóa chính (Primary Key) và các trường dữ liệu cần cập nhật (`UPDATE`) sau khi đã tìm thấy domain và email thành công.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm bằng nút **When clicking ‘Test workflow’** hoặc test qua node **Schedule Trigger** với 1 vài bản ghi mẫu để kiểm tra kết quả trả về ở các node Code và Postgres.
- Sau khi kiểm tra dữ liệu trong database đã được update chính xác, gạt công tắc **Active** ở góc trên bên phải để workflow tự động vận hành 24/7.

---

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo qua Telegram/Slack**: Thêm một node Telegram ở cuối quy trình để bắn tin nhắn báo cáo mỗi khi workflow chạy xong một batch (ví dụ: *"Đã enrich thành công 50 seller trong vòng 5 phút!"*).
- **Xử lý ngoại lệ (Error Handling)**: Thêm node `Error Trigger` để bắt lỗi khi Bright Data trả về kết quả trống hoặc lỗi kết nối database, giúp đội ngũ kỹ thuật dễ dàng theo dõi.
- **Mở rộng nguồn dữ liệu**: Kết hợp thêm các bước kiểm tra độ sống của email (Email Verification API như NeverBounce hoặc Hunter) trước khi lưu vào PostgreSQL để tăng chất lượng data.

---

### 📌 Kết luận
Workflow **Enrich Seller Data with Email & Domain Lookup using Bright Data & Google Search** là một cỗ máy tự động hóa hoàn hảo giúp tối ưu hóa toàn bộ quy trình thu thập dữ liệu khách hàng/nhà bán hàng. Triển khai ngay hôm nay để giải phóng sức lao động thủ công và nâng tầm hiệu suất kinh doanh cho doanh nghiệp của các sếp!