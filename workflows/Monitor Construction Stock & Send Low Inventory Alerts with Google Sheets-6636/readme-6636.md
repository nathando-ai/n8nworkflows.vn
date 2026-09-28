---
title: "🚀 Tự động Quản lý Kho Vật Tư Xây Dựng & Cảnh Báo Tồn Kho Thấp với n8n và Google Sheets"
description: "Hướng dẫn xây dựng hệ thống tự động kiểm tra tồn kho vật tư xây dựng mỗi ngày, cập nhật dữ liệu và gửi email cảnh báo khi sắp hết hàng nhờ n8n và Google Sheets."
slug: "tu-dong-quan-ly-kho-vat-tu-xay-dung-va-canh-bao-ton-kho-n8n"
tags: [n8n, automation, google-sheets, inventory-management, no-code, email-alert]
keywords: [n8n workflow, quản lý kho tự động, cảnh báo tồn kho, google sheets automation, tự động hóa n8n, quản lý vật tư xây dựng]
---

# 🚀 Tự động Quản lý Kho Vật Tư Xây Dựng & Cảnh Báo Tồn Kho Thấp với n8n

Trong ngành xây dựng, việc kiểm soát vật tư (xi măng, sắt thép, gạch ngói...) thủ công thường rất dễ sai sót, dẫn đến tình trạng thiếu hụt vật liệu làm gián đoạn tiến độ công trình hoặc tồn kho đọng vốn quá nhiều. Các sếp có đang tốn quá nhiều thời gian để kiểm tra sổ sách kho mỗi ngày?

Đừng lo, bài viết này sẽ hướng dẫn các sếp triển khai một **workflow n8n tự động hóa 100%** giúp kiểm tra kho vật tư xây dựng hàng ngày, tự động tính toán số liệu, cập nhật Google Sheets và gửi email cảnh báo ngay lập tức khi lượng tồn kho chạm ngưỡng báo động!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Không cần thủ công rà soát file Excel/Google Sheets mỗi ngày.
- **Cảnh báo kịp thời:** Gửi email thông báo ngay khi vật tư xuống dưới định mức tối thiểu, tránh tình trạng "cháy hàng" tại công trường.
- **Độ chính xác cao:** Xử lý dữ liệu nhập/xuất kho tự động bằng mã nguồn JavaScript qua node Code, loại bỏ sai sót do tính toán nhầm.
- **Hoạt động 24/7:** Chạy ngầm liên tục theo lịch trình định sẵn mà không cần sự can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Google Account:** Để kết nối với Google Sheets (chuẩn bị sẵn một file Google Sheets quản lý kho vật tư).
- **SMTP Server / Email Account:** Tài khoản email (Gmail, SendGrid, SMTP riêng...) để cấu hình node gửi email cảnh báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trên n8n Editor, sau đó copy toàn bộ mã JSON của workflow từ hệ thống Oneclick AI Squad và paste trực tiếp vào giao diện n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru, các sếp cần cấu hình chính xác các node sau:

- **Daily Stock Check (`cron`):** 
  - Node này đóng vai trò kích hoạt lịch chạy tự động. Các sếp có thể tùy chỉnh thời gian chạy (ví dụ: 8:00 sáng mỗi ngày) cho phù hợp với quy trình của công ty.
- **Fetch Stock Data (`googleSheets`):** 
  - Chọn kết nối **Google API Credentials**.
  - Trỏ tới file Google Sheets quản lý kho của công ty và chọn đúng tên Sheet/Range chứa dữ liệu vật tư.
- **Update Stock Levels (`code`):** 
  - Node này dùng để xử lý logic cộng trừ số lượng vật tư (nhập thêm hoặc xuất sử dụng). Các sếp có thể tùy chỉnh đoạn code JavaScript bên trong nếu công thức tính toán kho của công ty có đặc thù riêng.
- **Check Low Stock (`code`):** 
  - Đoạn code lọc ra các mặt hàng có số lượng tồn kho thấp hơn ngưỡng quy định (Threshold). 
- **Update Google Sheet (`googleSheets`):** 
  - Cấu hình lại thông số operation là `update` để ghi ngược dữ liệu tồn kho mới nhất trở lại Google Sheets.
- **Send Email Alert (`emailSend`):** 
  - Cấu hình thông tin **SMTP credentials** (Host, Port, User, Password).
  - Điền danh sách email nhận cảnh báo của đội ngũ quản lý kho hoặc ban chỉ huy công trường.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thử nghiệm với dữ liệu hiện tại xem email có gửi về hay Google Sheets có cập nhật đúng không.
- Nếu mọi thứ xanh mướt (success), các sếp bật công tắc **Active** ở góc trên cùng bên phải để hệ thống tự chạy.

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống tối ưu hơn nữa, các sếp có thể mở rộng workflow này bằng cách:
1. **Tích hợp thêm thông báo:** Thay vì chỉ gửi email, tích hợp thêm node **Telegram Bot** hoặc **Slack** để bắn tin nhắn thẳng vào group chat của đội vận hành kho.
2. **Lưu lịch sử giao dịch:** Thêm một bước ghi lại lịch sử xuất/nhập kho vào một Sheet riêng biệt ("Audit Log") để dễ dàng đối soát khi cần.
3. **Báo cáo tuần/tháng:** Kết hợp thêm cron chạy vào cuối tuần để tổng hợp lượng vật tư đã tiêu thụ gửi lên ban giám đốc.

### 📌 Kết luận
Việc tự động hóa quản lý kho vật tư xây dựng với n8n không chỉ giúp tiết kiệm hàng giờ đồng hồ làm việc thủ công mỗi tuần mà còn bảo vệ tiến độ công trình khỏi những sự cố thiếu hụt vật liệu bất ngờ. Hãy áp dụng ngay vào mô hình của mình nhé các sếp!