---
title: "🚀 Tự động gửi LinkedIn InMail cá nhân hóa cho CEO & Founder từ Google Sheets và Unipile"
description: "Hướng dẫn chi tiết cách tự động gửi LinkedIn InMail cá nhân hóa cho CEO & Founder từ Google Sheets và Unipile bằng n8n, tiết kiệm thời gian và tăng hiệu quả kết nối."
slug: "tu-dong-gui-linkedin-inmail-ca-nhan-hoa"
tags: [n8n, automation, no-code, linkedin, google-sheets]
keywords: [n8n workflow, tự động hóa, linkedin inmail, google sheets, unipile]
---

# 🚀 Tự động gửi LinkedIn InMail cá nhân hóa cho CEO & Founder từ Google Sheets và Unipile

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp có thể đã từng gặp tình trạng này: bạn phải gửi hàng trăm LinkedIn InMail cá nhân hóa cho các CEO và Founder tiềm năng, nhưng việc này tốn rất nhiều thời gian và công sức. Bạn phải tìm kiếm thông tin, viết nội dung, và gửi từng tin nhắn một. Quá trình này không chỉ tốn thời gian mà còn dễ gây lỗi và không nhất quán.

Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình này chỉ trong vài bước đơn giản. Workflow sẽ tự động lấy danh sách liên hệ từ Google Sheets, lọc những người chưa được gửi InMail, và gửi tin nhắn cá nhân hóa thông qua LinkedIn Sales Navigator hoặc Recruiter Classic.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đáng kể: Không cần phải gửi từng InMail một.
- Tăng hiệu quả kết nối: Tin nhắn cá nhân hóa giúp tăng tỷ lệ phản hồi.
- Hoạt động liên tục: Workflow có thể chạy tự động theo lịch trình đã đặt.
- Giảm lỗi: Tự động hóa giúp giảm thiểu sai sót do thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản LinkedIn Sales Navigator hoặc Recruiter Classic (InMail credits sẽ được trừ từ gói của bạn).
- Google Sheets với các cột: `first_name`, `company_name`, `linkedin_url`, `inmail`, `chat_ID`, `row_number`.
- Tài khoản Unipile (đăng ký tại unipile.com, kết nối LinkedIn, và sao chép API Key, DSN, và Account ID).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/14445](https://n8n.io/workflows/14445).
2. Nhấp vào nút "Import" để tải xuống file JSON.
3. Trong n8n Editor, nhấp vào "Import from File" và chọn file JSON vừa tải xuống.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **Schedule Trigger**: Đặt lịch chạy workflow theo thời gian mong muốn (ví dụ: mỗi 4-8 giờ).
- **Get Leads**: Cấu hình Google Sheets credentials và chọn sheet chứa danh sách liên hệ.
- **Data Arrangement**: Thay thế các giá trị placeholder (DSN, API Key, Account ID) bằng thông tin thực tế từ tài khoản Unipile của bạn.
- **Limit Connection Request**: Đặt giới hạn số lượng InMail gửi trong mỗi lần chạy (ví dụ: 10-15 InMail).
- **Wait**: Đặt thời gian chờ giữa các lần gửi InMail (ví dụ: 3-5 phút).
- **Send Inmail**: Nếu bạn sử dụng Recruiter Classic thay vì Sales Navigator, thay đổi giá trị `api` trong node này thành `recruiter`.

#### 3. Kích hoạt ⚡️
1. Nhấp vào nút "Execute Node" để kiểm tra dữ liệu mẫu.
2. Sau khi kiểm tra thành công, nhấp vào nút "Activate" để kích hoạt workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Theo dõi phản hồi**: Sử dụng `chat_ID` được lưu trong Google Sheets để xây dựng chuỗi tương tác tiếp theo (ví dụ: gửi tin nhắn nhắc lại sau 3 ngày nếu không có phản hồi).
- **Kết hợp với Slack/Telegram**: Thêm node để gửi thông báo khi workflow hoàn thành hoặc gặp lỗi.
- **Lưu log hoạt động**: Thêm node để lưu log hoạt động vào Google Sheets hoặc cơ sở dữ liệu để theo dõi hiệu suất của workflow.
- **Gửi báo cáo định kỳ**: Tạo một workflow phụ để gửi báo cáo tổng hợp kết quả hoạt động của workflow chính.

### 📌 Kết luận
Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình gửi LinkedIn InMail cá nhân hóa, tiết kiệm thời gian và tăng hiệu quả kết nối. Hãy áp dụng ngay để tối ưu hóa quy trình làm việc của mình!