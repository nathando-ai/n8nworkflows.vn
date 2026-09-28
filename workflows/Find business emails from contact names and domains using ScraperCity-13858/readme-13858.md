---
title: "🚀 Tự động tìm email doanh nghiệp siêu tốc từ tên và tên miền với ScraperCity"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa tìm kiếm email doanh nghiệp B2B từ danh sách tên và tên miền website bằng API của ScraperCity, giúp tối ưu quy trình cold email."
slug: "tim-email-doanh-nghiep-tu-dong-voi-scrapercity-n8n"
tags: [n8n, automation, scrapercity, lead-generation, cold-email, b2b-leads]
keywords: [n8n workflow, tìm email doanh nghiệp, scrapercity api, lead generation tự động, cold email outreach]
keywords: [n8n workflow, tìm email doanh nghiệp, scrapercity api, lead generation tự động, cold email outreach]
---

# 🚀 Tự động tìm email doanh nghiệp siêu tốc từ tên và tên miền với ScraperCity

Trong các chiến dịch B2B Lead Generation và Cold Email, việc tìm kiếm chính xác email công việc của người ra quyết định (Decision Maker) chiếm rất nhiều thời gian nếu làm thủ công. Làm sao để scale danh sách lead hàng loạt mà vẫn đảm bảo tỷ lệ bounce rate thấp?

Giải pháp tuyệt vời từ chuyên gia Alex Berman (tác giả *The Cold Email Manifesto*) sẽ giúp các sếp giải quyết triệt để bài toán này. Workflow n8n tích hợp **ScraperCity** giúp tự động hóa 100% quy trình tìm kiếm email doanh nghiệp từ danh sách tên và tên miền có sẵn mà không cần viết code phức tạp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Nhập danh sách tên và tên miền, nhận ngay email liên hệ chính xác mà không tốn công search thủ công.
- **Tối ưu hóa chiến dịch Cold Email:** Cung cấp nguồn lead chất lượng cao, giúp tăng tỷ lệ mở email và chuyển đổi khách hàng.
- **Tiết kiệm thời gian & chi phí:** Thay vì thuê nhân sự cào dữ liệu thủ công, hệ thống tự động xử lý hàng nghìn contact chỉ trong vài phút.
- **Hoạt động linh hoạt:** Dễ dàng kết nối với Google Sheets, CRM hoặc các công cụ gửi email tự động.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Đã cài đặt sẵn (Self-hosted hoặc n8n Cloud).
- **Tài khoản & API Key ScraperCity:** Dịch vụ web scraping và B2B lead generation của Alex Berman (cung cấp API để trích xuất dữ liệu).
- **Google Sheets / File dữ liệu:** Chứa danh sách thô gồm Tên (First Name, Last Name) và Tên miền doanh nghiệp (Domain).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ nguồn hoặc copy đoạn mã JSON.
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File** (hoặc nhấn `Ctrl+V` / `Cmd+V` để paste trực tiếp vào màn hình canvas).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này sử dụng sự kết hợp của các node cơ bản trong n8n để xử lý dữ liệu hàng loạt:
- **Manual Trigger / Webhook:** Điểm khởi đầu để kích hoạt quy trình (có thể thay đổi thành Schedule Trigger nếu muốn chạy định kỳ).
- **Google Sheets Node:** Kết nối với file danh sách khách hàng tiềm năng của các sếp. Cần cấu hình đúng **Document ID** và **Sheet Name** chứa cột Tên và Tên miền.
- **Split In Batches Node:** Giúp chia nhỏ lượng dữ liệu (ví dụ: 10-50 dòng mỗi batch) để tránh quá tải API và xử lý mượt mà.
- **HTTP Request Node (Gọi API ScraperCity):** 
  - Cấu hình endpoint API của ScraperCity do Alex Berman cung cấp.
  - Thêm **Header** chứa API Key xác thực tài khoản.
  - Map các trường dữ liệu đầu vào từ Google Sheets (First Name, Last Name, Domain) vào payload gửi lên API.
- **Code / Set Node:** Dùng để xử lý, làm sạch dữ liệu trả về từ API trước khi lưu trữ.
- **If / Filter Node:** Lọc ra những kết quả tìm thấy email thành công để chuyển sang bước tiếp theo, loại bỏ các dòng lỗi hoặc không tìm thấy dữ liệu.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** với một vài dòng dữ liệu mẫu để kiểm tra xem API ScraperCity trả về kết quả chính xác chưa.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để workflow sẵn sàng tự động hóa.

### ✍️ Mẹo & gợi ý nâng cao
- **Đẩy dữ liệu về CRM:** Kết nối thêm node HubSpot, Close CRM hoặc Pipedrive để tự động tạo Deal/Contact mới ngay khi tìm được email.
- **Tích hợp thông báo Telegram/Slack:** Tạo một thông báo gửi thẳng vào nhóm chat mỗi khi quét xong một batch lead hoặc phát hiện khách hàng VIP.
- **Lưu log chi tiết:** Lưu trữ các trường hợp không tìm thấy email vào một sheet riêng để chạy chiến dịch retargeting hoặc tìm kiếm bằng phương pháp khác.

### 📌 Kết luận
Tự động hóa khâu tìm kiếm email với sự hỗ trợ của n8n và ScraperCity là chìa khóa giúp đội ngũ Sales và Marketing bứt phá doanh thu mà không cần tốn nhiều nhân lực. Hãy áp dụng ngay workflow này vào hệ thống của các sếp để tối ưu hóa quy trình B2B Lead Generation ngay hôm nay!