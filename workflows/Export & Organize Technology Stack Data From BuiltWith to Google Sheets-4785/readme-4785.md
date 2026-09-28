---
title: "🚀 Tự động quét Tech Stack website từ BuiltWith vào Google Sheets với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động đọc danh sách tên miền từ Google Sheets, gọi BuiltWith API để phân tích công nghệ và cập nhật kết quả ngược lại Google Sheets."
slug: "tu-dong-quet-tech-stack-website-builtwith-google-sheets-n8n"
tags: [n8n, automation, marketing, builtwith, google-sheets, lead-generation]
keywords: [n8n workflow, builtwith api, quet tech stack, tu dong hoa marketing, google sheets n8n]
---

# 🚀 Tự động quét Tech Stack website từ BuiltWith vào Google Sheets

Các sếp làm sales, marketing hay nghiên cứu thị trường có bao giờ thấy nản khi phải ngồi check từng website xem họ đang dùng công nghệ gì (Shopify, WordPress, React, v.v.) rồi copy/paste thủ công vào Excel không? Việc này vừa tốn hàng giờ đồng hồ vừa cực kỳ nhàm chán.

Workflow n8n này sinh ra để giải quyết triệt để nỗi đau đó! Nó sẽ tự động hóa 100% quy trình đọc danh sách domain, gọi API BuiltWith để phân tích công nghệ, sau đó ghi gọn gàng kết quả vào Google Sheets cho các sếp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tuyệt đối:** Thay vì mất hàng ngày check thủ công, hệ thống xử lý hàng loạt domain trong vài phút.
- **Dữ liệu cấu trúc rõ ràng:** Tự động phân loại Technology, Category, thời gian First/Last Detected vào đúng từng dòng trên Google Sheets.
- **Hỗ trợ đắc lực cho Sales & Marketing:** Dễ dàng lọc khách hàng tiềm năng dựa trên công nghệ họ đang sử dụng (ví dụ: tìm các site chạy Shopify để bán app thương mại điện tử).
- **Vận hành linh hoạt:** Có thể chạy thủ công để test hoặc cấu hình chạy tự động định kỳ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Google Sheets** (để cấu hình kết nối OAuth2).
- **BuiltWith API Key** (để gọi dữ liệu công nghệ website qua HTTP Request).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trong n8n, sau đó copy toàn bộ mã JSON của workflow này và dán trực tiếp vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 5 nodes chính, các sếp cần chú ý cấu hình kỹ các điểm sau:

- **`Read Domains from Google Sheets` (Node Google Sheets):** 
  - Kết nối tài khoản Google của các sếp.
  - Chọn đúng file Spreadsheet và Sheet/Tab chứa danh sách tên miền (ví dụ tab `Domains` với cột `Domain`).
- **`Fetch detail via BuiltWith` (Node HTTP Request):** 
  - Điền Endpoint API của BuiltWith kèm theo API Key và tham số domain lấy từ node phía trước (`{{ $json.Domain }}`).
- **`Extract Tech Stack Info` (Node Code):** 
  - Node này dùng đoạn mã JS để lọc và bóc tách cấu trúc JSON phức tạp từ BuiltWith thành các trường gọn gàng như `Technology`, `Category`, `First Detected`, `Last Detected`.
- **`Update Google Sheet` (Node Google Sheets):** 
  - Chọn thao tác là `update`.
  - Khớp dòng dữ liệu dựa vào số thứ tự dòng (`row_number`) hoặc khóa chính để ghi đè hoặc bổ sung thông tin công nghệ tương ứng cho đúng domain.

#### 3. Kích hoạt ⚡️
- Bấm **"Test workflow"** bằng tay thông qua `Manual Trigger` để kiểm tra luồng chạy với 1-2 domain mẫu.
- Kiểm tra lại kết quả trên Google Sheets xem dữ liệu đã được điền chính xác chưa.
- Sau khi test ngon lành, các sếp có thể bật **Active** workflow hoặc thay thế `Manual Trigger` bằng `Schedule Trigger (Cron)` để chạy tự động định kỳ hàng ngày/tuần.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm node Wait:** Nếu các sếp quét số lượng lớn domain (hàng trăm/nghìn site), hãy chèn thêm node `Wait` giữa các request để tránh việc chạm ngưỡng giới hạn (Rate Limit) của BuiltWith API.
- **Tích hợp thông báo:** Nối thêm node Telegram hoặc Slack để nhận thông báo ngay khi workflow quét xong toàn bộ danh sách.
- **Mở rộng cột dữ liệu:** Tùy chỉnh node Code để lấy thêm thông tin như mức độ tin cậy (`Confidence`), thông tin mạng xã hội hoặc thông tin liên hệ của website.

### 📌 Kết luận
Workflow này biến một công việc thủ công cực kỳ nhàm chán thành một hệ thống thông tin thị trường tự động hóa hoàn toàn. Hãy áp dụng ngay để tối ưu hóa quy trình nghiên cứu khách hàng và bứt phá doanh số cho đội ngũ sales của các sếp!