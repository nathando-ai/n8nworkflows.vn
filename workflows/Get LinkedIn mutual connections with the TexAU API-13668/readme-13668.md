---
title: "🚀 Tự động lấy danh sách kết nối chung trên LinkedIn qua TexAU API với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa việc truy xuất các mối quan hệ chung trên LinkedIn sử dụng TexAU API, phục vụ đắc lực cho việc làm giàu dữ liệu (data enrichment) và chấm điểm khách hàng tiềm năng."
slug: "lay-ket-noi-chung-linkedin-texau-api-n8n"
tags: [n8n, automation, no-code, linkedin, texau, lead-generation]
keywords: [n8n workflow, linkedin mutual connections, texau api, tu dong hoa lead generation, data enrichment linkedin]
---

# 🚀 Tự động lấy danh sách kết nối chung trên LinkedIn qua TexAU API

Việc tìm hiểu các mối quan hệ chung (mutual connections) trên LinkedIn với khách hàng tiềm năng là một "vũ khí bí mật" cực kỳ mạnh mẽ trong sales và networking. Tuy nhiên, việc thủ công click vào từng profile để dò xem ai là người quen chung vừa tốn thời gian, vừa nhàm chán và không thể scale số lượng lớn.

Đừng lo, các sếp hoàn toàn có thể tự động hóa 100% quy trình này bằng workflow n8n kết hợp với **TexAU API**. Workflow này sẽ giúp các sếp trích xuất toàn bộ danh sách kết nối chung của một profile LinkedIn bất kỳ một cách nhanh chóng và trả về dữ liệu có cấu trúc để phục vụ cho các bước tiếp theo.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn cảnh thủ công tìm kiếm các kết nối chung trên LinkedIn.
- **Dữ liệu có cấu trúc rõ ràng:** Nhận về tên, profile URL, chức danh (job title) và các thông tin liên quan của các mối quan hệ chung.
- **Dễ dàng tích hợp sâu:** Dễ dàng đẩy dữ liệu này vào CRM, Google Sheets hoặc kết hợp với AI để phân tích mức độ thân thiết/tiềm năng của lead.
- **Hoạt động trơn tru:** Cơ chế chờ thông minh (Wait node) đảm bảo lấy được kết quả từ TexAU API một cách chính xác nhất.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance **n8n** đang hoạt động.
- Tài khoản **TexAU** và **API Key** hợp lệ để gọi các automation script.
- URL hoặc ID của profile LinkedIn mục tiêu cần quét.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ kho lưu trữ n8n hoặc copy đoạn JSON và paste trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm các node chính sau đây, các sếp cần cấu hình cẩn thận:

- **When clicking ‘Test workflow’ (Manual Trigger):** Node khởi chạy thủ công. Các sếp có thể thay thế node này bằng *Webhook*, *Schedule Trigger* hoặc kết nối từ một workflow CRM khác khi muốn tự động hóa hoàn toàn.
- **LinkedIn_Mutual_Connections (HTTP Request):** 
  - Cấu hình endpoint gọi tới TexAU API chuyên dụng cho việc lấy mutual connections.
  - Thêm **TexAU API Key** vào phần Header của HTTP Request (thường là dạng `Authorization` hoặc `x-api-key` tùy theo cấu hình của TexAU).
  - Điền URL hoặc ID profile LinkedIn mục tiêu vào phần body/query parameters của request.
- **Wait (Wait Node):** 
  - Vì TexAU cần thời gian chạy ngầm (background job), node này đóng vai trò tạm dừng workflow trong một khoảng thời gian nhất định (ví dụ: 10 - 30 giây) để chờ TexAU xử lý xong dữ liệu. Các sếp có thể điều chỉnh thời gian này tùy thuộc vào tải của hệ thống TexAU.
- **Get Results / Mutual_Connections_Results / Mutual_Connections_Results1 (HTTP Request):**
  - Các node này thực hiện việc gọi endpoint kết quả của TexAU sau khi đã qua thời gian chờ để kéo toàn bộ dữ liệu mutual connections về n8n dưới dạng JSON.

#### 3. Kích hoạt ⚡️
- Nhấn **Test workflow** để chạy thử và kiểm tra xem dữ liệu trả về từ các HTTP Request có chính xác hay không.
- Sau khi test thành công, hãy gạt công tắc sang **Active** để đưa workflow vào trạng thái vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa quy trình Lead Generation, các sếp có thể mở rộng workflow này bằng cách:
1. **Lưu trữ tự động:** Đẩy toàn bộ kết quả nhận được từ TexAU vào **Google Sheets**, **Airtable** hoặc **Notion** để dễ dàng quản lý.
2. **Tích hợp CRM:** Tự động cập nhật thông tin mutual connections vào HubSpot, Salesforce hoặc Close CRM để đội ngũ Sales có thêm ngữ cảnh khi tiếp cận khách hàng.
3. **Phân tích bằng AI:** Kết nối thêm node OpenAI/Claude để AI đọc danh sách mutual connections này và gợi ý xem ai là người có khả năng giới thiệu (warm intro) tốt nhất.
4. **Giao tiếp qua Chat:** Gửi thông báo tóm tắt qua **Slack** hoặc **Telegram** ngay khi workflow quét xong một profile tiềm năng.

### 📌 Kết luận
Workflow tích hợp TexAU API này là trợ thủ đắc lực giúp các sếp tự động hóa khâu nghiên cứu quan hệ kết nối trên LinkedIn, tối ưu hóa quy trình sales outreach và làm giàu dữ liệu lead một cách chuyên nghiệp. Chúc các sếp cài đặt thành công và "chốt đơn" mỏi tay!