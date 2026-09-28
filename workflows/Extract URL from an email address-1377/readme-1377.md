---
title: "🚀 Cách Tự Động Trích Xuất Tên Miền (Domain) Từ Địa Chỉ Email Trong n8n"
description: "Hướng dẫn chi tiết cách sử dụng n8n để tự động phân tích và trích xuất URL hoặc tên miền doanh nghiệp từ bất kỳ địa chỉ email nào một cách nhanh chóng và chính xác."
slug: "trich-xuat-url-tu-email-trong-n8n"
tags: [n8n, automation, no-code, email-parsing, data-processing, javascript]
keywords: [n8n workflow, trích xuất domain từ email, extract domain from email, n8n function node, tự động hóa xử lý dữ liệu]
---

# 🚀 Cách Tự Động Trích Xuất Tên Miền (Domain) Từ Địa Chỉ Email Trong n8n

Trong quá trình làm dữ liệu khách hàng (Lead Generation) hoặc xử lý form đăng ký, các sếp thường xuyên phải đối mặt với một bài toán quen thuộc: Làm thế nào để lấy nhanh tên miền website (như `gmail.com`, `tino.vn`, `company.com`) từ một danh sách hàng ngàn địa chỉ email mà không phải copy-paste thủ công từng dòng?

Việc xử lý thủ công không chỉ tốn thời gian, dễ sinh lỗi chính tả mà còn làm gián đoạn chu trình tự động hóa dữ liệu. Giải pháp ư? Hãy để workflow n8n "Extract URL from an email address" làm thay các sếp việc này trong chớp mắt!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Bóc tách tên miền chính xác từ chuỗi email bất kỳ mà không cần can thiệp thủ công.
- **Tiết kiệm thời gian:** Xử lý hàng loạt dữ liệu trong vài mili-giây, tối ưu hóa các quy trình CRM hoặc làm giàu dữ liệu (Data Enrichment).
- **Linh hoạt tích hợp:** Dễ dàng ghép nối vào bất kỳ workflow lớn nào có sẵn (như nhậnlead từ Form, Webhook, Google Sheets).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống n8n đang hoạt động (Cloud hoặc Self-hosted).
- Kiến thức cơ bản về JavaScript (đối với node `Function` dùng để cắt chuỗi email).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trong n8n, sau đó copy toàn bộ mã nguồn JSON của template (hoặc tạo thủ công 3 nodes theo danh sách bên dưới) để bắt đầu:
- **On clicking 'execute' (`manualTrigger`)**: Kích hoạt chạy thử thủ công.
- **Sample email (`set`)**: Khởi tạo dữ liệu email mẫu đầu vào.
- **Extract domain name (`function`)**: Sử dụng đoạn mã JavaScript ngắn gọn để bóc tách phần tên miền phía sau ký tự `@`.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 3 nodes cốt lõi, các sếp cần chú ý tùy chỉnh tại:
- **Node `Sample email` (`set`)**: Mặc định node này sẽ chứa một vài email mẫu để test. Các sếp hãy thay đổi trường dữ liệu này bằng biến (variable) thực tế lấy từ các bước trước của các sếp (ví dụ: email từ Google Sheets, Webhook, Typeform...).
- **Node `Extract domain name` (`function`)**: Node này sử dụng hàm JavaScript để tìm vị trí ký tự `@` và lấy phần chuỗi phía sau nó làm domain. Nếu các sếp muốn chuẩn hóa tên miền về dạng URL hoàn chỉnh (thêm `https://`), có thể chỉnh sửa lại đoạn mã JS trong đây một chút.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** để test chạy thử với dữ liệu mẫu xem domain đã được bóc tách đúng ý chưa.
- Sau khi kiểm tra mọi thứ mượt mà, các sếp có thể thay trigger thủ công bằng các trigger tự động (như Webhook, Email trigger, hay Google Sheets Trigger) và bật **Active**.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp Data Enrichment:** Sau khi lấy được domain từ email công ty, các sếp có thể nối thêm các node HTTP Request để gọi API tra cứu thông tin công ty (Clearbit, Hunter.io) hoặc kiểm tra xem website đó có còn hoạt động không.
- **Lưu trữ tự động:** Đẩy domain vừa trích xuất cùng email gốc thẳng vào Google Sheets hoặc CRM (HubSpot, Notion) để làm dữ liệu marketing.
- **Loại bỏ email cá nhân:** Viết thêm một điều kiện (If node) để lọc bỏ các domain phổ biến như `gmail.com`, `yahoo.com`, `outlook.com` nếu các sếp chỉ muốn tập trung lấy domain doanh nghiệp (B2B).

### 📌 Kết luận
Một workflow nhỏ gọn nhưng cực kỳ hữu ích trong bộ công cụ tự động hóa của các sếp. Hãy "lên đồ" ngay để giải phóng sức lao động khỏi những tác vụ xử lý chuỗi thủ công nhàm chán!