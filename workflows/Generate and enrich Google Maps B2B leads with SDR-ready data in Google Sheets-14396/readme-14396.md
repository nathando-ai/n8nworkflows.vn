---
title: "🚀 Tự động quét và làm giàu danh sách khách hàng B2B từ Google Maps với n8n"
description: "Xây dựng hệ thống Lead Generation tự động hóa 100% từ Google Maps, lọc dữ liệu sạch sẽ và lưu vào Google Sheets sẵn sàng cho đội ngũ SDR gọi sale."
slug: "tu-dong-quet-va-lam-giau-lead-b2b-google-maps-n8n"
tags: [n8n, automation, lead-generation, google-maps, google-sheets, sdr]
keywords: [n8n workflow, quét lead google maps, b2b lead generation, tự động hóa n8n, google places api]
---

# 🚀 Tự động quét và làm giàu danh sách khách hàng B2B từ Google Maps với n8n

Việc tìm kiếm khách hàng tiềm năng (Lead Generation) thủ công trên Google Maps tốn rất nhiều thời gian của đội ngũ SDR: vừa phải copy-paste tên công ty, số điện thoại, địa chỉ, website, vừa dễ bị sót dữ liệu hoặc trùng lặp. 

Giải pháp? Workflow n8n này sẽ tự động hóa toàn bộ quy trình: nhận yêu cầu từ biểu mẫu (Form), quét dữ liệu từ Google Maps API, làm sạch, lọc chất lượng và lưu trữ gọn gàng vào Google Sheets – sẵn sàng cho các chiến dịch outreach!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian**: Tự động hóa hoàn toàn từ khâu tìm kiếm đến lưu trữ, không còn thao tác tay.
- **Dữ liệu chuẩn SDR**: Chỉ lọc ra các doanh nghiệp có thông tin liên hệ rõ ràng (số điện thoại, website hợp lệ).
- **Loại bỏ trùng lặp thông minh**: Tự động nhận diện và xóa các kết quả trùng lặp dựa trên Tên và Địa chỉ.
- **Lưu trữ khoa học**: Đổ thẳng dữ liệu sạch vào Google Sheets để đội sales bốc máy gọi ngay lập tức.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance** (Cloud hoặc Self-hosted).
- **Google Cloud Console Account**: Để lấy API Key cho **Google Places API** (Bật tính năng *Places API (New)* hoặc *Text Search & Place Details*).
- **Google Sheets Account**: Tạo sẵn một Google Sheet để lưu danh sách lead.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này hoặc sao chép toàn bộ mã nguồn JSON, sau đó dán trực tiếp vào n8n Editor của các sếp qua tính năng **Import from JSON**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các node quan trọng sau đây để workflow hoạt động trơn tru:

- **Forms Trigger**: Nơi người dùng nhập từ khóa tìm kiếm (Ví dụ: "Nhà hàng tại Quận 1, TP.HCM"). Các sếp có thể tùy chỉnh các trường input trên form theo ý muốn.
- **Format Search Query** (`Set` node): Node này chuẩn hóa từ khóa đầu vào từ form để truyền vào API tìm kiếm của Google Maps.
- **Google Maps Text Search** & **Fetch Place Details** (`HTTP Request` nodes): 
  - Cần cài đặt Header hoặc Query Parameter chứa **Google Places API Key** của các sếp.
  - Node *Text Search* xử lý việc tìm kiếm diện rộng và tự động phân trang (pagination) để gom đủ dữ liệu.
  - Node *Place Details* lấy chi tiết số điện thoại, website, giờ mở cửa... của từng địa điểm.
- **Data Cleaning Logic** (`Code` node): Chạy đoạn script JavaScript giúp chuẩn hóa chuỗi, loại bỏ các kết quả trùng lặp dựa trên khóa kết hợp (Tên + Địa chỉ) và định dạng lại schema JSON.
- **Validate Lead Quality** (`If` node): Bộ lọc kiểm tra chất lượng. Mặc định sẽ cấu hình chỉ cho phép các lead có **số điện thoại hợp lệ** đi tiếp.
- **Log Lead to Google Sheets** (`Google Sheets` node): 
  - Kết nối tài khoản Google thông qua **Google Sheets OAuth2 API**.
  - Chọn đúng file Spreadsheet và Sheet Name mà các sếp muốn lưu trữ dữ liệu lead.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và test thử bằng một form submission với từ khóa bất kỳ để kiểm tra luồng dữ liệu.
- Sau khi test thành công, bật nút **Active** ở góc trên cùng bên phải để đưa workflow vào trạng thái chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo**: Thêm một node Telegram hoặc Slack ở cuối workflow để bắn thông báo ngay về nhóm khi có một mẻ lead mới được quét xong.
- **Làm giàu thêm dữ liệu**: Có thể kết hợp thêm các API bên thứ ba (như Hunter.io hoặc Dropcontact) để quét thêm email cá nhân của chủ doanh nghiệp từ website vừa thu thập được.
- **Lưu lịch sử chạy**: Tạo thêm một bảng Google Sheets phụ để ghi log số lượng lead quét được theo từng ngày, giúp dễ dàng theo dõi hiệu suất.

### 📌 Kết luận
Workflow này là một "vũ khí bí mật" giúp tối ưu hóa công sức cho đội ngũ Sales & Marketing B2B. Thay vì mất hàng giờ lướt Google Maps thủ công, các sếp giờ đây chỉ cần vài cú click để sở hữu danh sách khách hàng tiềm năng chất lượng cao. Chúc các sếp "lên đồ" thành công và chốt thật nhiều deal!