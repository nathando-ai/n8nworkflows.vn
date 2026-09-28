---
title: "🚀 Tự động hóa tạo hóa đơn PDF chuyên nghiệp từ Webhook với CustomJS API trong n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động tiếp nhận dữ liệu qua Webhook, xử lý bằng Code Node và tạo file hóa đơn PDF đẹp mắt bằng CustomJS API mà không tốn công sức."
slug: "tao-hoa-don-pdf-tu-dong-voi-customjs-api-trong-n8n"
tags: [n8n, automation, no-code, finance, pdf, webhook]
keywords: [n8n workflow, tạo hóa đơn pdf, customjs api, html to pdf, tu dong hoa hoa don, n8n pdf toolkit]
---

# 🚀 Tự động hóa tạo hóa đơn PDF chuyên nghiệp từ Webhook với CustomJS API

Các sếp có bao giờ cảm thấy mệt mỏi khi phải tạo thủ công từng hóa đơn (invoice) cho khách hàng mỗi khi có đơn hàng mới phát sinh? Việc copy-paste dữ liệu vào file mẫu, căn chỉnh lề, xuất PDF rồi gửi email vừa tốn thời gian, vừa dễ xảy ra sai sót về số liệu hoặc thông tin khách hàng.

Đừng lo, bài toán này sẽ được giải quyết triệt để với **Workflow n8n tự động tạo hóa đơn PDF sử dụng CustomJS API**. Chỉ với một cú "hit" Webhook chứa dữ liệu đơn hàng, hệ thống sẽ tự động xử lý, biến hóa dữ liệu và trả về một file hóa đơn PDF chuẩn chỉnh, sẵn sàng gửi đi!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Biến dữ liệu thô từ hệ thống bán hàng (CRM, Website, Google Sheets...) thành file PDF chuyên nghiệp ngay lập tức.
- **Tiết kiệm thời gian:** Loại bỏ hoàn toàn thao tác thủ công, giải phóng nhân sự cho các công việc kinh doanh cốt lõi.
- **Chính xác tuyệt đối:** Dữ liệu được map tự động, hạn chế tối đa sai sót nhầm lẫn tên khách hàng, mã đơn hay tiền bạc.
- **Tùy biến linh hoạt:** Dễ dàng thay đổi giao diện, bố cục hóa đơn thông qua mã nguồn HTML/CSS kết hợp với CustomJS API.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động (Self-hosted hoặc n8n Cloud).
- Tài khoản và API Key của **CustomJS API** (để sử dụng node chuyển đổi HTML sang PDF).
- Công cụ test API như Postman, cURL hoặc một hệ thống gửi Webhook mẫu.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ kho lưu trữ n8n, sau đó copy toàn bộ nội dung và dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 5 nodes chính làm việc nhịp nhàng với nhau. Các sếp cần chú ý cấu hình kỹ các điểm sau:

- **Webhook Node**: 
  - Đóng vai trò là điểm tiếp nhận dữ liệu đầu vào. 
  - Lưu ý đường dẫn (path) mặc định: `526fd864-6f85-4cde-97aa-39b61a3e5b83`. Các sếp có thể đổi lại path này cho phù hợp với hệ thống bảo mật của mình hoặc dùng URL production khi golive.
- **Set data Node**: 
  - Dùng để định hình lại cấu trúc dữ liệu hoặc thêm các biến tĩnh cần thiết cho hóa đơn (như tên công ty, mã số thuế, địa chỉ, thông tin tài khoản ngân hàng...).
- **Preprocess (Code Node)**: 
  - Node này chạy mã JavaScript để tính toán tổng tiền, định dạng tiền tệ (VNĐ, USD), ngày tháng và tạo cấu trúc mã HTML hiển thị hóa đơn. Các sếp có thể tùy chỉnh lại phần thiết kế HTML/CSS bên trong node này để hóa đơn mang đậm dấu ấn thương hiệu của mình.
- **HTML to PDF Node (`@custom-js/n8n-nodes-pdf-toolkit.html2Pdf`)**: 
  - Node cốt lõi chịu trách nhiệm chuyển đổi HTML thành file PDF chất lượng cao.
  - **Bắt buộc:** Phải kết nối đúng **Credentials** của *CustomJS API* để node này có quyền gọi dịch vụ render PDF.
- **Respond to Webhook Node**: 
  - Nhận file PDF vừa được tạo từ bước trên và trả kết quả trực tiếp về cho người gọi Webhook (hoặc trình duyệt), giúp tải file PDF xuống ngay lập tức.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** và dùng Postman hoặc trình duyệt gửi một request mẫu tới Webhook URL để test thử.
- Kiểm tra xem file PDF trả về có hiển thị đúng định dạng, bố cục hay không.
- Sau khi test thành công, chuyển công tắc từ trạng thái **Inactive** sang **Active** để đưa workflow vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Gửi hóa đơn qua Email:** Thay vì chỉ trả về qua Webhook, các sếp có thể nối thêm node **Gmail** hoặc **SendGrid** ngay sau bước tạo PDF để tự động gửi hóa đơn đến email của khách hàng.
- **Lưu trữ đám mây:** Kết nối thêm node **Google Drive** hoặc **OneDrive** để tự động lưu một bản sao của hóa đơn vào thư mục kế toán theo tên khách hàng và ngày tháng.
- **Thông báo nội bộ:** Gửi một thông báo kèm link hoặc file hóa đơn vào kênh **Telegram** hoặc **Slack** của phòng kế toán để các bạn theo dõi dòng tiền dễ dàng.

### 📌 Kết luận
Việc tự động hóa quy trình tạo hóa đơn PDF với n8n và CustomJS API không chỉ giúp doanh nghiệp tăng tốc độ vận hành mà còn mang lại trải nghiệm chuyên nghiệp trong mắt khách hàng. Hãy triển khai ngay hôm nay để tối ưu hóa nguồn lực cho doanh nghiệp của các sếp!