---
title: "🚀 Tự động cập nhật dữ liệu ETF thời gian thực từ JustETF vào Microsoft Excel với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động trích xuất các chỉ số tài chính, cổ tức, phí và hiệu suất của quỹ ETF từ JustETF dựa trên mã ISIN và đồng bộ trực tiếp vào Microsoft Excel chỉ với một cú click."
slug: "tu-dong-cap-nhat-du-lieu-etf-tu-justetf-vao-excel"
tags: [n8n, automation, no-code, excel, trading, justetf, finance]
keywords: [n8n workflow, tự động hóa excel, justetf api, trích xuất dữ liệu etf, quản lý danh mục đầu tư]
---

# 🚀 Tự động cập nhật dữ liệu ETF thời gian thực từ JustETF vào Microsoft Excel

Các nhà đầu tư và chuyên gia tài chính thường đối mặt với nỗi đau lớn: Việc theo dõi thủ công danh mục quỹ ETF đòi hỏi phải truy cập liên tục vào các trang web tài chính như JustETF để copy-paste các chỉ số quan trọng như tỷ suất cổ tức (dividend yield), phí quản lý (fees) hay hiệu suất 5 năm (5Y performance) vào file Excel. Công việc nhàm chán này vừa tốn thời gian, dễ sai sót lại nhanh chóng lỗi thời.

Workflow n8n này chính là giải pháp tự động hóa 100% không cần code (No-code automation), giúp các sếp đồng bộ toàn bộ dữ liệu ETF thời gian thực vào Microsoft Excel chỉ với một cú click hoặc kích hoạt qua Macro!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và xử lý các tác vụ tài chính mượt mà, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn phải thủ công cập nhật từng mã ISIN trên bảng tính Excel.
- **Dữ liệu luôn chính xác & cập nhật:** Tự động lấy số liệu mới nhất trực tiếp từ JustETF.
- **Kích hoạt linh hoạt:** Có thể chạy thủ công qua n8n hoặc tích hợp nút bấm trực tiếp trong Excel thông qua Macro & Webhook.
- **Quản lý danh mục chuyên nghiệp:** Tập trung vào phân tích chiến lược đầu tư thay vì nhập liệu thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Self-hosted hoặc Cloud).
- Tài khoản Microsoft 365 (OneDrive/Excel Online) để kết nối với các node Microsoft Excel.
- Danh sách các mã định danh ETF (ISIN) được lưu sẵn trong bảng Excel của các sếp.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow hoặc sao chép toàn bộ mã nguồn JSON, sau đó dán (Paste) trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các node quan trọng sau đây để workflow hoạt động trơn tru:

- **When called by Excel Macro (`webhook`)**: Cấu hình đường dẫn (Path) là `ETF`. Node này sẽ nhận tín hiệu từ file Excel của các sếp (thông qua Macro VBA hoặc nút bấm).
- **Logs the date & time (`microsoftExcel`)**: Kết nối tài khoản Microsoft Excel của sếp, chọn đúng file và bảng tính (table) để ghi lại thời gian thực thi (Last updated).
- **Gets rows from table (`microsoftExcel`)**: Cấu hình lấy toàn bộ các dòng dữ liệu trong bảng "Div study" – nơi chứa danh sách các mã ISIN của ETF.
- **Forge a Get request with ISIN Values (`httpRequest`)**: Node này sẽ tạo yêu cầu GET đến trang web `justetf.com` dựa trên giá trị mã ISIN từ bảng Excel.
- **Extracts defined values with css selector (`html`)**: Sử dụng CSS Selector để trích xuất nội dung HTML thô từ trang chi tiết ETF thành văn bản có thể đọc được.
- **Extracts defined values in better format (`code`)**: Node JavaScript tùy chỉnh giúp làm sạch dữ liệu, bóc tách chính xác các chỉ số như cổ tức, phí, hiệu suất 5 năm.
- **Loop Over Items (`splitInBatches`)** & **Updates my table (`microsoftExcel`)**: Lần lượt xử lý từng mã ETF qua vòng lặp và cập nhật (Update) ngược lại các giá trị mới vào bảng worksheet Excel của các sếp.

#### 3. Kích hoạt ⚡️
- Nhấn **‘Test workflow’** để chạy thử với dữ liệu mẫu (hoặc bấm nút "Update Table" trên Excel đã tích hợp Webhook).
- Kiểm tra xem thời gian cập nhật và các chỉ số ETF đã đổ về bảng Excel chính xác chưa.
- Chuyển trạng thái workflow sang **Active** để sử dụng chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Thêm node Telegram hoặc Slack để nhận thông báo ngay khi quá trình cập nhật dữ liệu ETF hoàn tất.
- **Lên lịch tự động (Cron):** Thay vì dùng Webhook từ Excel, các sếp có thể thay thế trigger bằng node **Schedule Trigger** để hệ thống tự động cập nhật dữ liệu vào mỗi sáng thứ Hai hàng tuần.
- **Sao lưu lịch sử:** Kết hợp thêm một bảng Google Sheets hoặc bảng Excel phụ để lưu vết lịch sử biến động giá trị và cổ tức theo thời gian.

### 📌 Kết luận
Việc tự động hóa cập nhật dữ liệu tài chính từ JustETF vào Excel không chỉ giúp loại bỏ công việc thủ công nhàm chán mà còn giúp các sếp nắm bắt thông tin thị trường nhanh chóng để đưa ra quyết định đầu tư chính xác. Hãy cài đặt ngay workflow này và tối ưu hóa quy trình phân tích ETF của các sếp ngay hôm nay!