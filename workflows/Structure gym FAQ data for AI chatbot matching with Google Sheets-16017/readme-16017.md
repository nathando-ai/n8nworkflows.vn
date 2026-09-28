---
title: "🏋️‍♂️ Tự động hóa dữ liệu FAQ Gym cho Chatbot AI với Google Sheets"
description: "Hướng dẫn chi tiết cách cấu hình workflow n8n để tự động lấy dữ liệu FAQ từ Google Sheets cho chatbot AI, phân biệt theo chi nhánh Rabieh và Bikfaya."
slug: "tu-dong-hoa-du-lieu-faq-gym-cho-chatbot-ai"
tags: [n8n, automation, no-code, google-sheets, ai-chatbot]
keywords: [n8n workflow, tự động hóa, google sheets, chatbot, ai]
---

# 🏋️‍♂️ Tự động hóa dữ liệu FAQ Gym cho Chatbot AI với Google Sheets

[Các sếp] có biết rằng việc quản lý và cập nhật dữ liệu FAQ cho chatbot AI thường là công việc tẻ nhạt và dễ gây lỗi? Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình lấy dữ liệu FAQ từ Google Sheets cho chatbot AI, phân biệt theo chi nhánh Rabieh và Bikfaya một cách hoàn toàn không cần code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa toàn bộ quá trình lấy dữ liệu FAQ từ Google Sheets.
- **Chính xác cao**: Dữ liệu được xử lý và định dạng một cách chuẩn xác.
- **Cá nhân hóa**: Phân biệt dữ liệu FAQ theo chi nhánh Rabieh và Bikfaya.
- **Hoạt động liên tục**: Workflow có thể được kích hoạt theo lịch hoặc theo yêu cầu từ các workflow khác.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập vào Google Sheets.
- Google Sheets credentials đã được cấu hình trong n8n.
- ID của Google Sheets chứa dữ liệu FAQ và cấu hình.
- Các workflow khác gọi workflow này cần truyền đúng các tham số đầu vào.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow này vào n8n, các sếp có thể làm theo các bước sau:

1. Truy cập vào n8n Editor.
2. Nhấn vào nút "Import from URL".
3. Dán link sau vào ô nhập liệu: `https://n8n.io/workflows/16017`.
4. Nhấn nút "Import" để hoàn tất quá trình import.

Hoặc, các sếp cũng có thể tải file JSON của workflow từ link trên và import trực tiếp từ file.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **Workflow Execution Start**: Node này sẽ kích hoạt workflow khi được gọi từ các workflow khác. Các sếp không cần cấu hình gì cho node này.

- **Process Parameters**: Node này sẽ xử lý các tham số đầu vào từ workflow gọi nó. Các sếp cần đảm bảo rằng các workflow gọi nó truyền đúng các tham số đầu vào.

- **Check Branch Location**: Node này sẽ kiểm tra chi nhánh được yêu cầu và chuyển hướng đến node tương ứng để lấy dữ liệu FAQ. Các sếp cần đảm bảo rằng giá trị chi nhánh được truyền vào khớp với điều kiện trong node này.

- **Fetch Rabieh FAQ from Sheets**: Node này sẽ lấy dữ liệu FAQ từ Google Sheets cho chi nhánh Rabieh. Các sếp cần cấu hình:
  - **Google Sheets credentials**: Chọn Google Sheets credentials đã được cấu hình trong n8n.
  - **Spreadsheet ID**: Nhập ID của Google Sheets chứa dữ liệu FAQ cho chi nhánh Rabieh.
  - **Sheet Name**: Nhập tên của sheet chứa dữ liệu FAQ cho chi nhánh Rabieh.
  - **Range**: Nhập phạm vi của dữ liệu FAQ trong sheet.

- **Fetch Bikfaya FAQ from Sheets**: Node này sẽ lấy dữ liệu FAQ từ Google Sheets cho chi nhánh Bikfaya. Các sếp cần cấu hình tương tự như node Fetch Rabieh FAQ from Sheets.

- **Format FAQ Data**: Node này sẽ định dạng dữ liệu FAQ thành cấu trúc đầu ra mong muốn. Các sếp có thể chỉnh sửa mã trong node này để thay đổi cấu trúc đầu ra.

- **Fetch Config from Sheets**: Node này sẽ lấy dữ liệu cấu hình từ Google Sheets. Các sếp cần cấu hình:
  - **Google Sheets credentials**: Chọn Google Sheets credentials đã được cấu hình trong n8n.
  - **Spreadsheet ID**: Nhập ID của Google Sheets chứa dữ liệu cấu hình.
  - **Sheet Name**: Nhập tên của sheet chứa dữ liệu cấu hình.
  - **Range**: Nhập phạm vi của dữ liệu cấu hình trong sheet.

#### 3. Kích hoạt ⚡️
Sau khi đã cấu hình các node cần thiết, các sếp có thể kích hoạt workflow bằng cách:

1. Nhấn vào nút "Activate" trên thanh công cụ của workflow.
2. Kiểm tra lại các cấu hình và nhấn "OK" để kích hoạt workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm chi nhánh mới**: Các sếp có thể thêm các node mới để lấy dữ liệu FAQ cho các chi nhánh khác và mở rộng logic điều kiện trong node Check Branch Location.
- **Tích hợp với Slack/Telegram**: Các sếp có thể kết nối workflow này với các kênh thông báo như Slack hoặc Telegram để nhận thông báo khi dữ liệu FAQ được cập nhật.
- **Lưu log hoạt động**: Các sếp có thể thêm node để lưu log hoạt động của workflow để theo dõi và kiểm tra lỗi.
- **Gửi báo cáo định kỳ**: Các sếp có thể cấu hình workflow để gửi báo cáo định kỳ về dữ liệu FAQ cho các thành viên trong nhóm.

### 📌 Kết luận
Workflow này cung cấp một giải pháp tự động hóa hoàn chỉnh để lấy dữ liệu FAQ từ Google Sheets cho chatbot AI, phân biệt theo chi nhánh Rabieh và Bikfaya. Với các bước cấu hình đơn giản và các mẹo nâng cao, các sếp có thể dễ dàng tích hợp và mở rộng workflow này để phù hợp với nhu cầu của mình. Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu quả hoạt động của chatbot AI!