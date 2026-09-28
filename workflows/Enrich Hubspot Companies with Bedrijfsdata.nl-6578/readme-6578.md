---
title: "🚀 Tự động làm giàu dữ liệu công ty trên Hubspot với Bedrijfsdata.nl qua n8n"
description: "Hướng dẫn chi tiết cách tự động cập nhật và làm giàu thông tin công ty từ Bedrijfsdata.nl vào Hubspot CRM ngay khi có thay đổi dữ liệu mà không cần viết code."
slug: "tu-dong-lam-giau-du-lieu-hubspot-bedrijfsdata"
tags: [n8n, automation, no-code, hubspot, crm, enrichment]
keywords: [n8n workflow, tự động hóa hubspot, bedrijfsdata, làm giàu dữ liệu crm, webhook n8n]
---

# 🚀 Tự động làm giàu dữ liệu công ty trên Hubspot với Bedrijfsdata.nl

Các sếp có đang gặp tình trạng dữ liệu công ty trên Hubspot CRM bị thiếu sót, sai sót hoặc mất quá nhiều thời gian để cập nhật thủ công từng doanh nghiệp? Việc để đội ngũ sales nhập liệu bằng tay không chỉ tốn thời gian mà còn làm giảm chất lượng dữ liệu đầu vào.

Workflow n8n này sẽ giải quyết triệt để bài toán trên bằng cách tự động lắng nghe sự thay đổi dữ liệu từ Hubspot, gọi API đến **Bedrijfsdata.nl** để lấy thông tin chi tiết về doanh nghiệp, sau đó cập nhật ngược lại vào Hubspot một cách hoàn toàn tự động!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Dữ liệu công ty trên Hubspot được làm giàu ngay lập tức khi có sự kiện thay đổi (như thêm domain mới).
- **Chính xác & Đầy đủ:** Khớp nối thông tin doanh nghiệp chính xác dựa trên ID hoặc thuật toán tìm kiếm thông minh từ Bedrijfsdata.nl.
- **Tiết kiệm thời gian:** Giải phóng đội ngũ sales khỏi công việc tra cứu và nhập liệu thủ công nhàm chán.
- **Xử lý lỗi thông minh:** Phân loại rõ ràng các lỗi từ Hubspot, Bedrijfsdata hoặc lỗi dữ liệu không tồn tại để dễ dàng kiểm soát.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Hubspot Account:** Tài khoản Hubspot có quyền tạo Private App và cấu hình Webhook.
- **Bedrijfsdata.nl Account:** Tài khoản và API Key để truy xuất dữ liệu doanh nghiệp từ Bedrijfsdata.nl.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể copy mã JSON của workflow này và dán trực tiếp vào n8n Editor, hoặc import file JSON tải từ trang chủ n8n (ID: `6578`).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động mượt mà, các sếp cần cấu hình chính xác các thành phần sau:

- **Hubspot - Company - Enrichment request (Webhook):** Thay vì dùng Hubspot Trigger phức tạp, workflow này dùng Webhook thông qua **Hubspot Private App**. Các sếp cần tạo Private App trên Hubspot, đăng ký webhook lắng nghe sự kiện `company.propertyChange` (ví dụ: theo dõi trường `domain`) và trỏ URL về webhook node này.
- **Get TEST Company Data & Update a company (Hubspot):** Cấu hình `hubspotOAuth2Api` credentials. Node này chịu trách nhiệm lấy thông tin công ty mẫu khi test và cập nhật dữ liệu mới sau khi được làm giàu.
- **Enrich company data & Get company (@bedrijfsdatanl/n8n-nodes-bedrijfsdata.bedrijfsdata):** Kết nối với tài khoản Bedrijfsdata.nl sử dụng `bedrijfsdataApi` credentials. Xử lý hai luồng: tìm kiếm thông minh dựa trên thông tin sẵn có hoặc lấy trực tiếp theo Bedrijfsdata ID.
- **Is TEST Mode? & Validate Incoming Data (If):** Kiểm tra xem request đến có hợp lệ không và có đang ở chế độ chạy thử nghiệm (Test Mode) hay không để chọn đúng công ty mẫu.
- **Output only the best match & Reformat for processing (Code):** Các node JavaScript giúp lọc ra kết quả công ty chính xác nhất và định dạng lại cấu trúc dữ liệu trước khi đẩy về Hubspot.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (`Test workflow`) với một bản ghi công ty cụ thể để kiểm tra dữ liệu trả về từ Bedrijfsdata.nl và quá trình update vào Hubspot.
- Sau khi test thành công, bật công tắc **Active** để workflow chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng thông báo lỗi:** Tận dụng các node `NoOp` như `Error type 3: Bedrijfsdata.nl API` hoặc `Error type 2 - Hubspot error` để tích hợp thêm node gửi thông báo qua Slack, Telegram hoặc Email khi hệ thống gặp sự cố (thiếu credit, lỗi API...).
- **Lưu log hệ thống:** Thêm node Google Sheets hoặc Database sau bước `Update a company` để lưu lại lịch sử các công ty đã được enrich thành công.
- **Trigger chuỗi hành động tiếp theo:** Sau khi làm giàu dữ liệu công ty, có thể kích hoạt tiếp các workflow tìm kiếm người ra quyết định (decision makers) hoặc tạo task tự động cho sales.

### 📌 Kết luận
Workflow **Enrich Hubspot Companies with Bedrijfsdata.nl** là một giải pháp cực kỳ mạnh mẽ giúp chuẩn hóa và nâng tầm chất lượng dữ liệu CRM của doanh nghiệp. Hãy "lên đồ" ngay hôm nay để tối ưu hóa quy trình sales và tiết kiệm hàng giờ làm việc thủ công cho đội ngũ của các sếp!