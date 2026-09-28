---
title: "🚀 Tự động trích xuất Leads từ Apollo.io vào Google Sheets với n8n"
description: "Hướng dẫn chi tiết xây dựng workflow n8n tự động cào dữ liệu khách hàng tiềm năng từ Apollo.io search URL và lưu thẳng vào Google Sheets, kèm xử lý phân trang và rate limit."
slug: "trich-xuat-leads-apollo-io-vao-google-sheets-n8n"
tags: [n8n, automation, lead-generation, apollo-io, google-sheets, no-code]
keywords: [n8n workflow, apollo io scraper, trích xuất leads apollo, google sheets automation, tự động hóa lead generation]
---

# 🚀 Tự động trích xuất Leads từ Apollo.io vào Google Sheets

Việc tìm kiếm khách hàng tiềm năng (Lead Generation) trên các nền tảng như Apollo.io là một công việc tiêu tốn rất nhiều thời gian nếu làm thủ công. Việc copy-paste thông tin từng trang, lọc dữ liệu, rồi đưa vào Google Sheets không chỉ nhàm chán mà còn dễ xảy ra sai sót.

Được thiết kế bởi chuyên gia tự động hóa **Salman Mehboob**, workflow n8n này sẽ giúp các sếp tự động hóa 100% quy trình: chuyển đổi URL tìm kiếm trên Apollo thành payload API, cào toàn bộ thông tin leads, xử lý phân trang thông minh và tự động đồng bộ vào Google Sheets mà không cần viết code phức tạp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Biến một URL tìm kiếm trên Apollo thành danh sách leads sạch sẽ trong Google Sheets.
- **Xử lý phân trang thông minh**: Tự động duyệt qua từng trang kết quả cho đến hết danh sách (hoặc theo giới hạn tùy chỉnh).
- **Kiểm soát Rate Limit an toàn**: Tích hợp độ trễ (delay) thông minh giữa các request để tránh bị Apollo chặn IP/API.
- **Tiết kiệm hàng giờ thao tác thủ công**: Tập trung nguồn lực vào việc sales và chăm sóc khách hàng thay vì cào dữ liệu tay.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Cloud hoặc Self-hosted).
- Tài khoản **Apollo.io** có quyền truy cập API và đã tạo **API Key**.
- Tài khoản **Google** để kết nối với Google Sheets và một file Google Sheet chuẩn bị sẵn để lưu leads.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tạo một workflow mới trong n8n Editor, sau đó copy toàn bộ mã nguồn JSON của workflow này và paste trực tiếp vào không gian làm việc của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 10 nodes chính, các sếp cần chú ý cấu hình kỹ các điểm sau:

- **Apollo Search Input (Node `set`)**: Dán URL tìm kiếm từ Apollo.io vào đây. Đồng thời, cấu hình giá trị `start_page` nếu các sếp muốn bắt đầu từ một trang cụ thể (ví dụ: `start_page = 5` nếu muốn bỏ qua 4 trang đầu).
- **Fetch Leads (Apollo) (Node `httpRequest`)**: 
  - Gửi POST request tới endpoint `/v1/mixed_people/search`.
  - Thay thế `APOLLO_API_KEY` trong phần Header bằng API Key thực tế của các sếp từ Apollo.io developer settings.
- **Extract Pagination Info & Increment Page (Nodes `set`)**: Kiểm soát số lượng trang cần xử lý. Theo mặc định, workflow sẽ quét toàn bộ `total_pages`. Nếu chỉ muốn lấy giới hạn số trang (ví dụ 10 trang đầu), hãy bỏ biểu thức `total_pages` mặc định và đặt giới hạn cứng.
- **Rate Limit Delay (Node `wait`)**: Đảm bảo duy trì độ trễ (mặc định 2 giây) giữa các lần gọi API để tránh vi phạm giới hạn của Apollo.
- **Write to Google Sheets (Node `googleSheets`)**: 
  - Kết nối tài khoản Google Sheets thông qua OAuth2.
  - Chọn file Spreadsheet và Sheet cụ thể dùng để lưu trữ thông tin leads (Name, LinkedIn, Company, Email...).

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** trên node `When clicking ‘Execute workflow’` để chạy thử nghiệm với một lượng dữ liệu nhỏ.
- Kiểm tra kết quả hiển thị trên Google Sheets xem dữ liệu đã map đúng các trường chưa.
- Sau khi test thành công, bật trạng thái **Active** để đưa workflow vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo**: Thêm node Slack hoặc Telegram vào cuối chuỗi xử lý để nhận thông báo ngay khi workflow hoàn tất việc cào một lượng lớn leads.
- **Lọc trùng lặp (Deduplication)**: Thêm một bước kiểm tra email/LinkedIn trước khi ghi vào Google Sheets để tránh lưu trùng leads đã cào trước đó.
- **Chạy tự động định kỳ**: Thay vì dùng `manualTrigger`, các sếp có thể chuyển sang `Schedule Trigger` để hệ thống tự động cào leads mới hàng tuần/hàng tháng.

### 📌 Kết luận
Workflow trích xuất leads Apollo.io sang Google Sheets này là một "vũ khí" cực kỳ mạnh mẽ cho các đội ngũ Sales và Marketing thế hệ mới. Hãy thiết lập ngay hôm nay để tối ưu hóa quy trình tìm kiếm khách hàng tiềm năng của doanh nghiệp các sếp!