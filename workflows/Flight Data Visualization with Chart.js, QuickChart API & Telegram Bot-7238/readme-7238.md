---
title: "🚀 Tự động hóa trực quan hóa dữ liệu chuyến bay với Chart.js, QuickChart API và Telegram Bot trên n8n"
description: "Hướng dẫn cài đặt workflow n8n tích hợp Telegram Bot đọc file CSV dữ liệu chuyến bay, xử lý qua JavaScript và tạo biểu đồ trực quan (Bar, Pie, Doughnut, Line) bằng QuickChart API."
slug: "truc-quan-hoa-du-lieu-chuyen-bay-telegram-bot-n8n"
tags: [n8n, automation, telegram-bot, chart-js, quickchart-api, data-visualization]
keywords: [n8n workflow, telegram bot n8n, quickchart api, chart.js n8n, tu dong hoa du lieu]
---

# 🚀 Tự động hóa trực quan hóa dữ liệu chuyến bay với Chart.js, QuickChart API và Telegram Bot

Các sếp có bao giờ gặp khó khăn khi phải tổng hợp hàng ngàn dòng dữ liệu chuyến bay (hoặc dữ liệu kinh doanh nói chung) từ file CSV, sau đó vẽ biểu đồ báo cáo thủ công để gửi cho sếp lớn hoặc khách hàng chưa? Việc này vừa tốn thời gian, vừa nhàm chán và dễ sai sót.

Đừng lo! Workflow n8n siêu việt này sẽ giúp các sếp xây dựng một **Telegram Bot thông minh**. Bot này sẽ đọc dữ liệu từ file CSV (`/data/flights.csv`), xử lý dữ liệu theo thời gian thực bằng JavaScript, tạo cấu hình Chart.js, gọi **QuickChart API** để biến dữ liệu thô thành những bức ảnh biểu đồ (Bar, Pie, Doughnut, Line) cực kỳ sắc nét và gửi thẳng lại cho người dùng trên Telegram chỉ trong tích tắc!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tương tác trực quan qua Telegram:** Người dùng chỉ cần bấm nút trên bàn phím Telegram (Reply Keyboard) để chọn loại biểu đồ muốn xem.
- **Tự động hóa 100% dữ liệu lớn:** Xử lý hơn 1.000+ bản ghi chuyến bay từ CSV (hãng hàng không, giá vé, thời gian, điểm đi/đến...) thành JSON một cách mượt mà.
- **Đa dạng dạng biểu đồ chuyên nghiệp:** Hỗ trợ 4 loại biểu đồ (Bar, Pie, Doughnut, Line) được thiết kế màu sắc bắt mắt, tối ưu cho thiết bị di động (800x600).
- **Phản hồi tức thì:** Cho ra kết quả biểu đồ kèm thông tin phân tích chỉ trong ~3 giây mà không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **Telegram Bot Token:** Tạo một bot mới thông qua `@BotFather` trên Telegram để lấy API Token.
- **File dữ liệu CSV:** Chuẩn bị sẵn file `flights.csv` đặt tại đường dẫn `/data/flights.csv` trên server n8n của các sếp (hoặc tùy chỉnh lại đường dẫn trong node đọc file). File cần chứa các cột: `airline, flight, source_city, departure_time, arrival_time, duration, price, class, destination_city, stops`.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này hoặc copy đoạn mã JSON, sau đó paste trực tiếp vào giao diện n8n Editor của các sếp qua tính năng **Import from Clipboard**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy trơn tru, các sếp cần cấu hình kỹ các điểm sau:
- **Telegram Trigger & các node Telegram (`Send Welcome Message`, `Send Bar Chart to Telegram`, v.v.):** 
  - Tạo Credentials loại **Telegram API** bằng cách điền Bot Token nhận được từ `@BotFather`.
  - Gán Credentials này cho tất cả các node liên quan đến Telegram trong workflow.
- **Read CSV File:** 
  - Kiểm tra lại đường dẫn file (File Path) trỏ chính xác tới `/data/flights.csv` trên môi trường n8n của các sếp.
  - Đảm bảo định dạng mã hóa là `UTF-8` để tránh lỗi font chữ tiếng Việt (nếu có).
- **Các node Code (`Process Data & Create Bar Chart/Pie Chart/Doughnut Chart/Line Chart`):**
  - Các node này sử dụng mã JavaScript thuần túy để nhóm dữ liệu (groupby), tính toán số lượng/giá trung bình và dựng cấu hình JSON cho thư viện Chart.js. Các sếp có thể tùy chỉnh lại logic code bên trong nếu muốn thay đổi cách hiển thị dữ liệu.
- **Các node HTTP Request (`Fetch Bar Chart Image`, v.v.):**
  - Các node này gọi tới endpoint của **QuickChart API** để render ảnh từ chuỗi JSON config của Chart.js. Không cần API Key phức tạp, QuickChart hoạt động ngay lập tức!

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và thử gửi lệnh `/start` tới bot Telegram của các sếp để test luồng tương tác.
- Nếu mọi thứ hoạt động hoàn hảo, hãy gạt công tắc sang **Active** để Bot chính thức đi vào hoạt động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng nguồn dữ liệu:** Thay vì đọc file CSV cố định trên local, các sếp có thể kết nối thêm Google Sheets hoặc Airtable để người dùng cập nhật dữ liệu chuyến bay liên tục mà không cần SSH vào server.
- **Thêm AI Phân tích:** Kết hợp thêm node OpenAI hoặc Claude LLM sau bước xử lý dữ liệu để bot Telegram không chỉ trả về ảnh biểu đồ mà còn viết thêm một đoạn nhận xét, phân tích xu hướng giá vé cực kỳ chuyên nghiệp.
- **Lưu lịch sử truy vấn:** Đưa thêm node Google Sheets / PostgreSQL vào cuối luồng để ghi lại log xem người dùng nào đã tra cứu biểu đồ gì và vào thời gian nào.

### 📌 Kết luận
Việc kết hợp n8n, Telegram Bot và QuickChart API mở ra một hướng đi cực kỳ mạnh mẽ để tự động hóa các báo cáo dữ liệu trực quan mà không cần tốn tiền mua cácBI tool đắt đỏ. Chúc các sếp "lên đồ" thành công và xây dựng được những trợ lý ảo báo cáo dữ liệu đỉnh cao!