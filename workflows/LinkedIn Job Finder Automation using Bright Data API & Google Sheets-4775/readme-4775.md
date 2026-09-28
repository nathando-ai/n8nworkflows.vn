---
title: "🚀 Tự động tìm kiếm việc làm trên LinkedIn bằng Bright Data API và Google Sheets"
description: "Xây dựng hệ thống tự động cào dữ liệu việc làm từ LinkedIn dựa trên từ khóa mong muốn, lưu trữ trực tiếp vào Google Sheets thông qua n8n và Bright Data API."
slug: "tu-dong-tim-kiem-viec-lam-linkedin-bright-data-google-sheets"
tags: [n8n, automation, no-code, bright-data, google-sheets, scraper]
keywords: [n8n workflow, linkedin job finder, bright data api, tự động tìm việc linkedin, google sheets automation]
---

# 🚀 Tự động tìm kiếm việc làm trên LinkedIn với Bright Data API & Google Sheets

Việc tìm kiếm việc làm thủ công trên LinkedIn tốn rất nhiều thời gian: các sếp phải liên tục lọc từ khóa, cuộn trang, copy thông tin công ty, vị trí và link ứng tuyển vào file Excel. Quá trình này vừa nhàm chán vừa dễ bỏ lỡ các cơ hội tốt. 

Giải pháp? Hãy để n8n và Bright Data API làm thay các sếp việc này 100% tự động! Workflow này sẽ nhận yêu cầu tìm kiếm qua một biểu mẫu (Form), gọi API cào dữ liệu tuyển dụng mới nhất từ LinkedIn, kiểm tra trạng thái xử lý và tự động cập nhật toàn bộ kết quả vào Google Sheets gọn gàng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Chỉ cần nhập từ khóa, thành phố, quốc gia và loại công việc vào Form, hệ thống tự lo phần còn lại.
- **Tiết kiệm hàng giờ đồng hồ**: Không còn phải copy-paste thủ công từng tin tuyển dụng.
- **Dữ liệu tập trung, trực quan**: Toàn bộ thông tin từ tiêu đề công việc, tên công ty, địa điểm cho đến link ứng tuyển được lưu trữ khoa học trên Google Sheets.
- **Vận hành thông minh**: Sử dụng cơ chế chờ (Wait) và kiểm tra trạng thái (IF/Check Status) để đảm bảo dữ liệu từ Bright Data được lấy về chính xác 100% mà không bị lỗi API do quá tải.
:::

### Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản **n8n** (Cloud hoặc Self-hosted).
- Tài khoản **Bright Data** kèm API Key dùng để truy cập dịch vụ cào dữ liệu LinkedIn dataset.
- Tài khoản **Google Sheets** đã chuẩn bị sẵn một file Google Sheet để lưu danh sách việc làm.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ nguồn cung cấp hoặc copy toàn bộ mã nguồn JSON dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần cấu hình chính xác các node quan trọng sau:

- **On form submission1 (Form Trigger)**: 
  - Nơi thiết lập giao diện nhập liệu để thu thập các tiêu chí tìm kiếm việc làm từ người dùng (như vị trí công việc, thành phố, quốc gia, loại hình công việc).
- **Create Snapshot ID (HTTP Request)**: 
  - Cần điền đúng Endpoint API của Bright Data, kèm theo API Key xác thực (Bearer Token hoặc Header phù hợp). Node này có nhiệm vụ gửi các tham số tìm kiếm và khởi tạo phiên cào dữ liệu (scraping job).
- **Check Snapshot Status & Wait 1 minute**: 
  - Hai node này phối hợp nhịp nhàng với node **Check Final Status (IF)** để liên tục kiểm tra xem Bright Data đã xử lý xong dữ liệu chưa. Việc chờ 1 phút giữa các lần kiểm tra giúp tránh làm quá tải API.
- **Scrape Data from SnapID (HTTP Request)**: 
  - Node gọi yêu cầu tải xuống tập dữ liệu công việc cuối cùng dưới định dạng JSON ngay khi trạng thái snapshot báo "ready".
- **Update Job Lists in sheet (Google Sheets)**: 
  - Chọn tài khoản kết nối **Google Sheets OAuth2 API**.
  - Chọn đúng file Google Sheet và Sheet Name tương ứng.
  - Ánh xạ các trường dữ liệu (Job Title, Company Name, Location, Apply Link...) từ kết quả trả về của node HTTP Request vào các cột tương ứng trong Sheet.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng cách điền thông tin vào form để kiểm tra toàn bộ luồng chạy.
- Sau khi test thành công, bật nút **Active** ở góc trên bên phải để workflow sẵn sàng phục vụ 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo**: Thêm node Telegram hoặc Slack ở cuối luồng để bot bắn thông báo ngay về máy mỗi khi có danh sách việc làm mới được cập nhật vào Google Sheet.
- **Lọc thông minh**: Sử dụng thêm các node **Filter** để loại bỏ các công việc không phù hợp (ví dụ: chỉ lấy các job Remote hoặc mức lương thỏa mãn điều kiện).
- **Tự động hóa định kỳ**: Thay vì dùng Form Trigger, các sếp có thể đổi thành Schedule Trigger để hệ thống tự động quét việc làm mới mỗi sáng lúc 8:00 AM.

### 📌 Kết luận
Workflow này là một "vũ khí" cực mạnh cho những ai đang tìm việc hoặc cácAgency tuyển dụng muốn xây dựng cơ sở dữ liệu việc làm tự động từ LinkedIn. Hãy cài đặt ngay lên hệ thống n8n của các sếp để tối ưu hóa thời gian và công sức!