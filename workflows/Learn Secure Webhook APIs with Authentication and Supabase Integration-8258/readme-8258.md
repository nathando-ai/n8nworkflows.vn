---
title: "🚀 Xây dựng Webhook API Bảo Mật với Xác Thực và Supabase trong n8n"
description: "Hướng dẫn chi tiết cách tạo và bảo mật Webhook API đa phương thức (GET, POST, PUT, PATCH, DELETE, HEAD) kết hợp cơ sở dữ liệu Supabase bằng n8n."
slug: "xay-dung-webhook-api-bao-mat-voi-supabase-trong-n8n"
tags: [n8n, automation, webhook, supabase, api-security, no-code]
keywords: [n8n webhook, secure webhook api, supabase n8n, xac thuc webhook, n8n tutorial tieng viet]
---

# 🚀 Xây dựng Webhook API Bảo Mật với Xác Thực và Supabase trong n8n

Các sếp có bao giờ gặp khó khăn khi muốn xây dựng một hệ thống API nhận dữ liệu từ bên thứ ba, nhưng lại lo lắng về vấn đề bảo mật (authentication), xử lý đa phương thức (GET, POST, PUT...) và lưu trữ dữ liệu tập trung không? Việc tự lập trình backend truyền thống vừa tốn kém thời gian, lại phức tạp trong khâu vận hành.

Với workflow mẫu được thiết kế bởi chuyên gia **Wayne Simpson**, các sếp sẽ sở hữu ngay một hệ thống **Secure Webhook API** hoàn chỉnh kết hợp cùng **Supabase** – giải quyết trọn gói bài toán nhận request, xác thực an toàn, xử lý dữ liệu và lưu trữ tự động 100% mà không cần viết một dòng code phức tạp nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **API Đa phương thức chuẩn RESTful:** Xử lý mượt mà các HTTP Method gồm `GET`, `POST`, `PUT`, `PATCH`, `DELETE` và `HEAD`.
- **Bảo mật nhiều lớp:** Tích hợp sẵn các cơ chế xác thực như Basic Auth, Header Auth, JWT Auth, kèm theo tính năng IP Whitelist và CORS.
- **Tích hợp Supabase mượt mà:** Tự động thực hiện các thao tác Đọc (`Get`), Tạo (`Create`), Cập nhật (`Update`) và Xóa (`Delete`) dữ liệu trên cơ sở dữ liệu Supabase.
- **Phản hồi linh hoạt:** Sử dụng node `Respond to Webhook` để trả kết quả về cho client theo thời gian thực hoặc bất đồng bộ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n (Cloud hoặc Self-hosted).
- Tài khoản **Supabase** và một bảng (Table) đã được cấu hình sẵn để lưu trữ dữ liệu.
- Supabase API Credentials (URL và Service Role / Anon Key) để kết nối với n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Các sếp tải file JSON của workflow hoặc sao chép mã nguồn JSON.
- Trong giao diện n8n Editor, chọn **Add workflow** -> Nhấp vào biểu tượng menu (3 chấm) ở góc trên bên phải -> Chọn **Import from File** hoặc **Import from Clipboard** và dán mã JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 15 nodes chia thành các nhánh xử lý HTTP request khác nhau. Các sếp cần chú ý cấu hình các điểm sau:

- **Các node Webhook (`Webhook`, `Webhook1`, `Webhook2`, v.v.):** 
  - Đảm bảo đường dẫn (`Path`) đồng bộ hoặc được phân tách rõ ràng theo logic của sếp (ví dụ: `07aaa04d-6c73-416f-82e2-1e6ededeacc4`).
  - Thiết lập phương thức HTTP tương ứng (`GET`, `POST`, `PUT`, `PATCH`, `DELETE`, `HEAD`).
  - **Cấu hình bảo mật:** Trong phần tùy chọn (Options) của Webhook, hãy bật các cơ chế xác thực (Header Auth với API Key hoặc JWT) và cấu hình **IP Whitelist** nếu cần thiết để bảo vệ API khỏi các truy cập trái phép.
- **Các node Supabase (`Get a row`, `Create a row`, `Update a row`, `Delete a row`):**
  - Tạo **Supabase API Credentials** bằng cách điền Supabase URL và Service Key của các sếp.
  - Chọn đúng Table Name trong cơ sở dữ liệu Supabase tương ứng với từng thao tác (Lấy dữ liệu, Thêm mới, Sửa, Xóa).
- **Các node chỉnh sửa dữ liệu (`Edit Fields`, `Edit Fields1`) & `Respond to Webhook`:**
  - Định dạng lại cấu trúc dữ liệu JSON trước khi lưu vào Supabase hoặc trước khi trả về phản hồi cho bên gọi API.

#### 3. Kích hoạt ⚡️
- Thực hiện **Test workflow** bằng cách gửi một HTTP Request mẫu (sử dụng Postman, cURL hoặc công cụ tương tự) đến Webhook URL (Test URL hoặc Production URL).
- Kiểm tra kết quả trả về và dữ liệu trên Supabase xem đã đồng bộ chính xác chưa.
- Gạt công tắc sang **Active** để chính thức đưa Webhook API vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối thông báo lỗi:** Thêm node Telegram hoặc Slack vào nhánh lỗi (Error Trigger) để nhận cảnh báo ngay lập tức nếu có request lỗi hoặc tấn công trái phép vào Webhook.
- **Lưu Log truy cập:** Kết hợp thêm một bảng Log trong Supabase để ghi lại lịch sử mọi request gọi vào API (IP, thời gian, method, payload) phục vụ việc kiểm tra và thống kê.
- **Rate Limiting:** Sử dụng Redis hoặc cấu hình tầng Proxy (như Nginx) bên ngoài để giới hạn số lượng request (Rate Limit) nhằm bảo vệ hệ thống n8n khỏi bị quá tải.

### 📌 Kết luận
Việc tự xây dựng các Secure Webhook API kết hợp với Supabase chưa bao giờ dễ dàng đến thế nhờ sự hỗ trợ của n8n. Hãy áp dụng ngay workflow này để tối ưu hóa hệ thống backend, tự động hóa dữ liệu và nâng cao bảo mật cho doanh nghiệp của các sếp!