---
title: "🚀 Tự động trích xuất thông tin sản phẩm từ URL tìm kiếm với MrScraper và Google Sheets"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình nghiên cứu thị trường, cào dữ liệu sản phẩm từ danh sách URL và lưu trữ trực tiếp vào Google Sheets."
slug: "trich-xuat-thong-tin-san-pham-mrscraper-google-sheets"
tags: [n8n, automation, no-code, mrscraper, google-sheets, market-research, web-scraping]
keywords: [n8n workflow, tự động hóa, mrscraper, google sheets, cào dữ liệu sản phẩm, nghiên cứu thị trường, trích xuất url]
---

# 🚀 Tự động trích xuất thông tin sản phẩm từ URL tìm kiếm với MrScraper và Google Sheets

Việc nghiên cứu thị trường, theo dõi giá cả và thu thập thông tin sản phẩm từ hàng loạt trang web thủ công luôn ngốn rất nhiều thời gian và dễ xảy ra sai sót. Mỗi ngày, nhân sự phải mất hàng giờ copy-paste từng URL, ghi chép giá, mô tả sản phẩm vào bảng tính.

Giải pháp là gì? Workflow n8n này sẽ giúp các sếp tự động hóa 100% quy trình cào dữ liệu sản phẩm bằng **MrScraper**, xử lý qua các bước logic và đồng bộ toàn bộ dữ liệu sạch sẽ vào **Google Sheets**, giúp tiết kiệm hàng chục giờ làm việc mỗi tuần!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Không còn cảnh thủ công đi copy từng URL sản phẩm và dán vào bảng tính.
- **Dữ liệu chuẩn xác, cập nhật**: Trích xuất chính xác thông tin sản phẩm (tên, giá, mô tả...) thông qua MrScraper.
- **Lưu trữ khoa học**: Đổ thẳng dữ liệu thu thập được vào Google Sheets để dễ dàng phân tích, báo cáo.
- **Hoạt động liên tục**: Lên lịch chạy tự động định kỳ hoặc kích hoạt thủ công bất cứ lúc nào các sếp cần.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống n8n (Cloud hoặc Self-hosted).
- Tài khoản và API Key của **MrScraper** (dịch vụ Web Scraping mạnh mẽ).
- Tài khoản **Google Sheets** (đã chuẩn bị sẵn file bảng tính để hứng dữ liệu).
- (Tùy chọn) Tài khoản **Gmail** nếu các sếp muốn cấu hình gửi thông báo sau khi hoàn tất.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này từ kho lưu trữ n8n.
- Trong giao diện n8n Editor, nhấn vào biểu tượng **Settings/Menu** (hoặc dấu cộng) -> **Import from File** và chọn file JSON vừa tải.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà không gặp lỗi "Unauthorized" hay "Not Found", các sếp cần cấu hình chính xác các node sau:

- **Google Sheets Node**: 
  - Chọn Credentials kết nối với tài khoản Google của các sếp.
  - Chỉ định đúng **Document** (Tên file Google Sheets) và **Sheet Name** (Tên tab chứa dữ liệu nguồn và đích).
- **MrScraper Node (`mrscraper`)**:
  - Nhập MrScraper API Key vào phần Credentials.
  - Cấu hình ID của kịch bản cào dữ liệu (Scraping recipe) hoặc URL mục tiêu tương ứng với cấu trúc dữ liệu các sếp muốn lấy.
- **Code Node & Split In Batches Node**:
  - Kiểm tra lại các đoạn mã JavaScript trong node `Code` (nếu có) để đảm bảo cấu trúc mảng dữ liệu đầu ra khớp với định dạng mà MrScraper và Google Sheets yêu cầu.
  - Node `Split In Batches` giúp chia nhỏ các URL thành từng lô (batches) để tránh vượt quá giới hạn API rate limit của các dịch vụ.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** để chạy thử nghiệm (Test run) với một vài URL mẫu.
- Kiểm tra lại Google Sheets xem dữ liệu đã được đổ về chính xác chưa.
- Nếu mọi thứ xanh mướt, gạt công tắc sang **Active** để workflow chính thức đi vào vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo Telegram/Slack**: Thêm node thông báo khi workflow hoàn tất quá trình cào dữ liệu hoặc khi phát hiện lỗi.
- **Lên lịch chạy tự động (Schedule Trigger)**: Thay vì dùng `Manual Trigger`, hãy kết hợp thêm node `Schedule Trigger` để hệ thống tự động cào giá đối thủ vào mỗi sáng thứ Hai hàng tuần.
- **Lọc và làm sạch dữ liệu**: Sử dụng thêm các Code Node bằng Python hoặc JavaScript để lọc bớt các ký tự đặc biệt, định dạng lại giá tiền (VND/USD) trước khi ghi vào Google Sheets.

### 📌 Kết luận
Workflow tích hợp giữa MrScraper và Google Sheets là một "vũ khí" cực kỳ lợi hại cho các đội ngũ Marketing, Sales và Nghiên cứu thị trường. Hãy triển khai ngay hôm nay để giải phóng sức lao động khỏi các tác vụ cào dữ liệu thủ công nhàm chán!