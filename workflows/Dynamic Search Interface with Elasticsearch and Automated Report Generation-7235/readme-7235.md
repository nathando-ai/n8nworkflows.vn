---
title: "🚀 Xây dựng giao diện tìm kiếm động với Elasticsearch và tự động tạo báo cáo trên n8n"
description: "Hướng dẫn xây dựng hệ thống tìm kiếm giao dịch nghi vấn qua Web Form, truy vấn Elasticsearch và tự động xuất báo cáo dưới dạng TXT hoặc CSV bằng n8n."
slug: "giao-dien-tim-kiem-elasticsearch-va-tao-bao-cao-tu-dong-n8n"
tags: [n8n, automation, elasticsearch, report-generation, no-code, data-extraction]
keywords: [n8n workflow, elasticsearch n8n, tự động tạo báo cáo, tìm kiếm động n8n, form trigger n8n]
---

# 🚀 Tự động hóa tìm kiếm và xuất báo cáo với Elasticsearch trên n8n

Việc tra cứu dữ liệu giao dịch phức tạp, lọc các hoạt động khả nghi từ hệ thống cơ sở dữ liệu lớn (như Elasticsearch) và xuất báo cáo thủ công thường tiêu tốn rất nhiều thời gian của đội ngũ vận hành và kiểm toán. Các sếp thường phải mất hàng giờ để viết câu lệnh truy vấn, lọc dữ liệu trên Excel rồi format lại báo cáo.

Giải pháp? Workflow n8n này sẽ giúp các sếp xây dựng một hệ thống hoàn toàn tự động: Nhận yêu cầu từ Web Form, tự động dịch thành câu lệnh Elasticsearch, quét dữ liệu, tổng hợp báo cáo dạng Text hoặc CSV và lưu trực tiếp lên ổ cứng chỉ trong vòng 2-5 giây!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%**: Biến thao tác tra cứu dữ liệu phức tạp thành một Web Form đơn giản cho mọi phòng ban.
- **Tốc độ chớp nhoáng**: Trả kết quả và xuất file báo cáo (TXT/CSV) chỉ trong 2-5 giây.
- **Linh hoạt đầu ra**: Hỗ trợ xuất cả định dạng tóm tắt con người dễ đọc (Text) và định dạng bảng biểu để phân tích tiếp (CSV).
- **Chuẩn hóa lưu trữ**: Tự động đặt tên file kèm timestamp và lưu vào thư mục hệ thống phục vụ kiểm toán, tuân thủ (compliance).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Hệ thống **n8n** (Self-hosted hoặc Cloud).
- **Elasticsearch Cluster** đang hoạt động (có sẵn index chứa dữ liệu giao dịch, ví dụ: `bank_transactions`).
- Tài khoản xác thực Elasticsearch (**HTTP Basic Auth**).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và paste trực tiếp vào giao diện n8n Editor, hoặc import file JSON thông qua menu cấu hình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống hoạt động trơn tru với hạ tầng của các sếp, hãy chú ý cấu hình các node quan trọng sau:

- **Search Form (`formTrigger`)**: 
  - Node này tạo ra một Web Form giao diện cho người dùng nhập: Số tiền giao dịch tối thiểu, khoảng thời gian (1 giờ đến 3 ngày), bộ lọc mã khách hàng tùy chọn, và định dạng file đầu ra (Text/CSV).
  - Sau khi kích hoạt workflow, n8n sẽ cung cấp một URL public để truy cập form này.

- **Build Search Query (`code`)**: 
  - Node JavaScript này làm nhiệm vụ quy đổi các mốc thời gian thân thiện (như "Last 24 Hours" thành `now-24h`, "Last 3 Days" thành `now-3d`) và dựng cấu trúc JSON Query hoàn chỉnh cho Elasticsearch.

- **Search Elasticsearch (`httpRequest`)**: 
  - Cấu hình phương thức `POST` trỏ tới địa chỉ Elasticsearch của các sếp (ví dụ: `http://localhost:9220/bank_transactions/_search`).
  - Thiết lập **HTTP Basic Auth** với username và password chuẩn của Elasticsearch cluster.
  - Nhận tối đa 100 kết quả mới nhất cho mỗi lần quét.

- **Format Report (`code`)**: 
  - Nhận dữ liệu thô trả về từ Elasticsearch, tiến hành phân tích và định dạng lại thành 2 dạng: 
    - 📄 **TEXT**: Bản tóm tắt dễ đọc cho con người.
    - 📊 **CSV**: Dữ liệu chuẩn để mở bằng Excel/Google Sheets.
  - Tự động sinh tên file kèm timestamp (ví dụ: `report_2023-10-25.csv`).

- **Read/Write Files from Disk (`readWriteFile`)**: 
  - Cấu hình thao tác `write` để lưu file báo cáo xuống ổ cứng server tại thư mục `/tmp/`.
  - Sẵn sàng cho việc download hoặc tích hợp gửi tiếp qua email/Telegram.

#### 3. Kích hoạt ⚡️
- Bấm nút **Execute Workflow** và test thử điền thông tin trên Web Form để kiểm tra kết quả.
- Kiểm tra thư mục `/tmp/` trên server xem file `.txt` hoặc `.csv` đã được tạo thành công chưa.
- Gạt công tắc sang **Active** để đưa hệ thống vào vận hành chính thức!

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo**: Nối thêm node Telegram hoặc Slack ngay sau node File Saver để hệ thống tự động bắn tin nhắn báo cáo kèm file về nhóm chat khi có giao dịch khả nghi lớn.
- **Tự động gửi Email**: Kết hợp node Gmail hoặc Microsoft Outlook để tự động gửi file báo cáo đến bộ phận kiểm toán hoặc quản lý tài chính hàng ngày.
- **Mở rộng nguồn dữ liệu**: Thay vì chỉ tìm kiếm trên 1 index của Elasticsearch, các sếp có thể mở rộng logic code để quét nhiều index cùng lúc.

### 📌 Kết luận
Workflow **Dynamic Search Interface with Elasticsearch and Automated Report Generation** là một công cụ cực kỳ mạnh mẽ giúp các doanh nghiệp khai thác sức mạnh của Open Data và No-code automation. Hãy triển khai ngay hôm nay để tiết kiệm hàng chục giờ làm việc thủ công cho đội ngũ của các sếp!