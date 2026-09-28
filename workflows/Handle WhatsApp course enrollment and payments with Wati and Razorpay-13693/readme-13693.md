---
title: "🚀 Tự động hóa đăng ký khóa học và thanh toán qua WhatsApp với Wati và Razorpay"
description: "Xây dựng hệ thống chatbot bán khóa học tự động 100% trên WhatsApp: Tra cứu danh mục, tạo link thanh toán Razorpay và kiểm tra trạng thái ghi danh qua Google Sheets."
slug: "tu-dong-hoa-dang-ky-khoa-hoc-whatsapp-wati-razorpay"
tags: [n8n, automation, no-code, whatsapp, wati, razorpay, google-sheets]
keywords: [n8n workflow, whatsapp chatbot, wati automation, razorpay payment link, google sheets automation, tự động hóa bán khóa học]
---

# 🚀 Tự động hóa đăng ký khóa học và thanh toán qua WhatsApp với Wati và Razorpay

Các sếp đang kinh doanh khóa học online chắc chắn hiểu cảm giác mệt mỏi khi phải túc trực trả lời tin nhắn tư vấn, gửi thông tin ngân hàng thủ công rồi ngồi check bill chuyển khoản từng học viên một. Quá trình thủ công này vừa chậm trễ, dễ bỏ lỡ khách hàng nóng (hot lead) lại vừa tốn kém nhân sự.

Workflow n8n này chính là giải pháp tự động hóa toàn diện giúp các sếp biến WhatsApp thành một "trợ lý sales" hoạt động 24/7: Khách nhắn tin là tự động gửi catalogue, tự động tạo link thanh toán quốc tế qua Razorpay và tự động ghi nhận dữ liệu vào Google Sheets!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phản hồi tức thì 24/7:** Học viên nhắn tin là hệ thống trả lời ngay lập tức, không để khách phải chờ đợi.
- **Tự động hóa thanh toán:** Tự động tạo link thanh toán Razorpay độc nhất cho từng học viên chỉ với một từ khóa.
- **Quản lý tập trung:** Mọi lịch sử đăng ký, trạng thái thanh toán đều được đồng bộ thời gian thực lên Google Sheets.
- **Trải nghiệm mượt mà:** Khách hàng có thể tự tra cứu danh sách khóa học và kiểm tra trạng thái học tập (`mystatus`) bất cứ lúc nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản WATI** kèm API Key để nhận/gửi tin nhắn WhatsApp.
- **Tài khoản Razorpay** để tạo link thanh toán (dùng HTTP Request gọi REST API trực tiếp).
- **Google Sheets** chứa danh sách khóa học và bảng lưu trữ thông tin đăng ký (Enrollments).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này, vào giao diện n8n chọn **New Workflow**, nhấn tổ hợp `Ctrl + V` (hoặc `Cmd + V`) để dán toàn bộ các nodes lên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 18 nodes được liên kết chặt chẽ. Các sếp cần tập trung cấu hình kỹ các điểm sau:

- **Wati Trigger & Các node Wati (Send a text message...):** 
  - Chọn đúng **Credentials** kết nối tới tài khoản WATI của các sếp.
  - Đảm bảo webhook từ WATI đã trỏ đúng đến URL webhook của n8n trigger.
- **Google Sheets Nodes (Read Courses, Read Course Detail, Log Pending Enrollment, v.v.):**
  - Kết nối tài khoản Google Sheets qua `googleSheetsOAuth2Api`.
  - Trỏ đúng đến file Google Sheets quản lý khóa học và bảng ghi danh của các sếp. Đảm bảo cấu trúc cột khớp với dữ liệu mà các node Code (`Build Course Catalogue`, `Parse Enroll Intent`,...) đang xử lý.
- **Razorpay – Create Payment Link (HTTP Request):**
  - Cấu hình thông tin xác thực (`httpBasicAuth`) bằng API Key/Secret của tài khoản Razorpay.
  - Kiểm tra lại endpoint API tạo link thanh toán của Razorpay trong node HTTP Request để đảm bảo đúng môi trường (Test/Live).

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và thử gửi một tin nhắn giả lập (hoặc nhắn trực tiếp qua số WhatsApp kết nối WATI) với cú pháp `courses` để test.
- Nếu mọi thứ phản hồi chính xác, các sếp gạt công tắc sang **Active** để hệ thống chính thức chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm thông báo:** Nối thêm một node Telegram hoặc Slack vào sau bước `Google Sheets – Log Pending Enrollment` để đội ngũ sales nhận được thông báo ngay khi có học viên tạo link thanh toán.
- **Gửi email xác nhận:** Kết hợp node Gmail hoặc SendGrid để tự động gửi tài liệu khóa học hoặc hóa đơn khi thanh toán thành công.
- **Mở rộng cổng thanh toán:** Có thể bổ sung hoặc thay thế Razorpay bằng các cổng thanh toán nội địa (Stripe, VNPAY, Momo qua API) tùy thuộc vào thị trường mục tiêu của các sếp.

### 📌 Kết luận
Việc tự động hóa quy trình tuyển sinh và thanh toán khóa học qua WhatsApp không chỉ giúp các sếp tiết kiệm hàng chục giờ làm việc thủ công mỗi tuần mà còn tối đa hóa tỷ lệ chốt đơn nhờ tốc độ phản hồi chớp nhoáng. Hãy áp dụng ngay vào hệ thống kinh doanh của mình nhé!