---
title: "🚀 Tự động giám sát hạn chót và ngân sách dự án Kimai mỗi ngày với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động kiểm tra tiến độ dự án Kimai, cảnh báo khi cận kề deadline hoặc vượt ngân sách qua email."
slug: "giam-sat-han-chot-ngan-sach-kimai-n8n"
tags: [n8n, automation, project-management, kimai, email-alerts]
keywords: [n8n workflow, kimai automation, giám sát ngân sách dự án, cảnh báo deadline n8n, tự động hóa quản lý dự án]
---

# 🚀 Tự động giám sát hạn chót và ngân sách dự án Kimai mỗi ngày với n8n

Việc quản lý thời hạn (deadline) và ngân sách (budget) của các dự án tính phí (billable projects) trên hệ thống Kimai thủ công thường tiêu tốn rất nhiều thời gian của các Project Manager. Nếu bỏ sót, doanh nghiệp có thể phải gánh chịu chi phí phát sinh hoặc trễ hạn bàn giao với khách hàng.

Giải pháp ở đây là gì? Workflow n8n này sẽ tự động hóa toàn bộ quy trình kiểm tra, tính toán và gửi cảnh báo qua email mỗi khi dự án chạm ngưỡng nguy hiểm (còn dưới 10 ngày đến hạn hoặc đã dùng quá 80% ngân sách), giúp các sếp luôn nắm thế chủ động mà không cần tốn một phút kiểm tra thủ công nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Chủ động thời gian:** Tự động quét dữ liệu mỗi ngày vào lúc 9:00 sáng mà không cần con người can thiệp.
- **Cảnh báo thông minh:** Chỉ gửi email khi thực sự có dự án cần lưu ý (deadline sắp hết hoặc ngân sách vượt 80%), tránh làm phiền hộp thư rác.
- **Báo cáo trực quan:** Email được tổng hợp dưới dạng HTML chuyên nghiệp, hiển thị rõ ràng thông tin dự án, thời hạn và số giờ đã dùng.
- **Vận hành trơn tru:** Giúp kiểm soát chi phí nhân sự và tiến độ dự án chặt chẽ, hạn chế tối đa rủi ro thất thoát.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Hệ thống **Kimai** (Time Tracking) đang hoạt động và có quyền truy cập API.
- Tài khoản **SMTP Server** để gửi email tự động (Gmail, SendGrid, Amazon SES,...).
- Nền tảng **n8n** (Cloud hoặc Self-hosted).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Copy đoạn JSON của workflow (hoặc tải file JSON từ nguồn gốc) và dán trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 11 nodes được chia làm 4 giai đoạn chính, các sếp cần cấu hình kỹ các điểm sau:

- **Node `Every Day at 9:00` (Schedule Trigger):** Mặc định chạy vào 9:00 sáng các ngày trong tuần. Có thể chỉnh lại lịch chạy nếu muốn.
- **Các node `GET Projects`, `GET Projects Details`, `GET Timesheet Records` (HTTP Request):** 
  - Điền URL của hệ thống Kimai của các sếp.
  - Cấu hình thông tin xác thực (`HTTP Bearer Auth`) với API Token lấy từ tài khoản Kimai.
- **Node `Calculate expiration` (Code Node):** 
  - Dòng 1: Tùy chỉnh khoảng thời gian cảnh báo hạn chót (mặc định là 10 ngày).
  - Hàm `getBudgetInfo()`: Tùy chỉnh ngưỡng cảnh báo ngân sách (mặc định là 80%).
- **Node `Send an Email` (Email Send):** 
  - Chọn thông tin kết nối SMTP (`smtp` credentials).
  - Điền email người gửi và người nhận báo cáo.

#### 3. Kích hoạt ⚡️
- Nhấn **Test step** hoặc **Execute Workflow** để kiểm tra kết quả trả về từ Kimai.
- Sau khi test thành công, bật công tắc **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh chat:** Thay vì chỉ gửi Email, các sếp có thể nối thêm node **Telegram** hoặc **Slack** để nhận tin nhắn cảnh báo ngay lập tức trên điện thoại.
- **Lưu log vào Google Sheets:** Thêm một node Google Sheets để ghi lại lịch sử các lần cảnh báo nhằm phục vụ việc kiểm toán nội dung dự án sau này.
- **Đa dạng hóa ngưỡng cảnh báo:** Tách code thành nhiều nhánh nếu muốn phân loại mức độ: Cảnh báo nhẹ (Vàng) khi đạt 70% ngân sách và Cảnh báo đỏ khi đạt 90%.

### 📌 Kết luận
Workflow giám sát dự án Kimai này là một "trợ lý ảo" đắc lực giúp các sếp quản lý agency hay team IT/Product của mình một cách tự động và chuyên nghiệp. Hãy cài đặt ngay hôm nay để tối ưu hóa quy trình vận hành doanh nghiệp!