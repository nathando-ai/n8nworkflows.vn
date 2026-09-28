---
title: "🚀 Tự động phát hiện nền tảng thương mại điện tử và công nghệ web với Google Sheets và n8n"
description: "Hướng dẫn chi tiết cách xây dựng workflow n8n tự động quét danh sách domain từ Google Sheets, nhận diện nền tảng E-commerce và technology stack cực nhanh."
slug: "tu-dong-phat-hien-nen-tang-thuong-mai-dien-tu-va-cong-nghe-voi-google-sheets"
tags: [n8n, automation, no-code, lead-generation, e-commerce, google-sheets]
keywords: [n8n workflow, phát hiện công nghệ web, detect e-commerce platform, google sheets automation, lead generation n8n]
---

# 🚀 Tự động phát hiện nền tảng thương mại điện tử và công nghệ web với Google Sheets

Các sếp làm trong lĩnh vực Sales, Marketing hay Nghiên cứu thị trường chắc hẳn đã từng tốn hàng giờ đồng hồ để check xem một website đang chạy nền tảng gì (Shopify, WooCommerce, Magento hay tự code), dùng công nghệ gì phía sau nhằm phân khúc khách hàng hoặc tìm kiếm khách hàng tiềm năng (Lead Generation). Việc làm thủ công này vừa nhàm chán, vừa chậm chạp.

Hôm nay, em xin giới thiệu một siêu phẩm workflow n8n được chia sẻ bởi chuyên gia **Ajay Yadav** (ERP Linker), giúp tự động hóa 100% quy trình quét danh sách website từ Google Sheets, nhận diện nền tảng e-commerce và technology stack rồi ghi ngược lại kết quả vào chính Google Sheets đó!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Chỉ cần điền danh sách domain vào Google Sheets, phần việc còn lại để n8n lo.
- **Tiết kiệm 90% thời gian**: Không cần phải mở từng trang web lên kiểm tra mã nguồn hay dùng tool thủ công nữa.
- **Phân khúc Lead chuẩn xác**: Nắm bắt ngay khách hàng tiềm năng đang dùng Shopify, WooCommerce hay nền tảng custom để đưa ra kịch bản tiếp cận phù hợp.
- **Kiểm soát rate limit thông minh**: Tích hợp sẵn cơ chế chờ (Wait) giúp tránh bị các trang web chặn do quét quá nhanh.
:::

### Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một tài khoản **n8n** (Cloud hoặc Self-hosted).
- Tài khoản **Google Account** có quyền tạo và chỉnh sửa Google Sheets.
- Credentials kết nối **Google Sheets OAuth2 API** trong n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ nguồn gốc (ID: 7991) hoặc copy đoạn mã JSON tương ứng và dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần chú ý cấu hình các node cốt lõi sau:

- **Google Sheets Nodes (`Get row(s) in sheet1` & `Update Enhanced Results1`)**: 
  - Tạo sẵn một Google Sheet với cột `domain` để chứa danh sách website cần quét, và các cột kết quả như `Platform`, `Technology Stacks`, v.v.
  - Kết nối tài khoản Google Sheets của các sếp qua credentials OAuth2.
  - Chỉ định đúng Spreadsheet ID và Sheet Name ở cả hai node đọc và ghi dữ liệu.
- **URL Preprocessor & Enhanced Technology Detection1 (Code Nodes)**: 
  - Các node này chứa mã Javascript giúp chuẩn hóa URL đầu vào (thêm `https://`, loại bỏ ký tự thừa) và phân tích dữ liệu trả về từ HTTP Request để trích xuất tên nền tảng e-commerce.
- **Rate Limiting Wait1 (Wait Node)**: 
  - Giúp tạo khoảng nghỉ giữa các lần gọi request, bảo vệ IP của server n8n khỏi bị các tường lửa (Cloudflare, WAF) chặn. Các sếp có thể điều chỉnh thời gian chờ cho phù hợp.
- **Schedule Trigger**: 
  - Cấu hình lịch chạy tự động (ví dụ: chạy định kỳ mỗi ngày hoặc mỗi tuần) nếu các sếp muốn hệ thống tự động quét danh sách mới mà không cần bấm thủ công.

#### 3. Kích hoạt ⚡️
- Bấm nút **"Execute workflow"** ở node `When clicking 'Execute workflow'` để test thử với 1-2 dòng dữ liệu đầu tiên.
- Kiểm tra lại kết quả trả về trên Google Sheets xem đã đúng ý chưa.
- Sau khi test ngon lành, hãy bật nút **Active** ở góc trên bên phải để workflow tự động chạy theo lịch hẹn.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo**: Kết nối thêm node Telegram hoặc Slack ở cuối workflow để nhận báo cáo ngay khi quá trình quét hoàn tất.
- **Mở rộng nguồn dữ liệu**: Thay vì Google Sheets, các sếp có thể lấy danh sách domain từ Airtable, HubSpot CRM hoặc cơ sở dữ liệu PostgreSQL.
- **Kết hợp AI**: Thêm một bước xử lý bằng OpenAI/Anthropic node để phân tích sâu hơn về mô hình kinh doanh của trang web dựa trên công nghệ họ đang sử dụng.

### 📌 Kết luận
Workflow này là một vũ khí cực kỳ lợi hại cho các đội ngũ Sales B2B và Growth Hacker. Hãy cài đặt ngay lên hệ thống n8n của các sếp để tối ưu hóa quy trình nghiên cứu khách hàng và bứt phá doanh thu ngay hôm nay!