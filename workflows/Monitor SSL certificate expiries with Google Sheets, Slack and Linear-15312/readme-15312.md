---
title: "🚀 Tự động giám sát hạn chứng chỉ SSL với Google Sheets, Slack và Linear"
description: "Hướng dẫn thiết lập workflow n8n tự động kiểm tra hạn chứng chỉ SSL hàng ngày, cảnh báo qua Slack và tạo task khẩn cấp trên Linear khi sắp hết hạn."
slug: "tu-dong-giam-sat-han-chung-chi-ssl-n8n"
tags: [n8n, automation, secops, ssl-monitor, slack, linear, google-sheets]
keywords: [n8n workflow, tự động hóa secops, kiểm tra ssl tự động, cảnh báo ssl slack, linear integration]
---

# 🚀 Tự động giám sát hạn chứng chỉ SSL với Google Sheets, Slack và Linear

Các sếp có bao giờ gặp cảnh "dở khóc dở cười" khi hệ thống sập chỉ vì chứng chỉ SSL (HTTPS) hết hạn mà không ai hay biết? Việc kiểm tra thủ công hàng chục, hàng trăm tên miền (domain) là một cực hình, dễ bỏ sót và tốn thời gian. 

Giải pháp ở đây là gì? Hãy để **n8n** lo toàn bộ! Workflow tự động này sẽ quét trạng thái SSL của toàn bộ domain lưu trong Google Sheets mỗi ngày, tự động cảnh báo lên Slack và tạo ticket trên Linear nếu phát hiện chứng chỉ sắp "lên đường".

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 100%**: Chạy ngầm định kỳ hàng ngày, không cần con người nhúng tay.
- **Phòng bệnh hơn chữa bệnh**: Phát hiện sớm chứng chỉ SSL sắp hết hạn (trước 30 ngày, 7 ngày...).
- **Đa kênh thông báo**: Bắn tin nhắn cảnh báo trực tiếp vào kênh Slack của team kỹ thuật.
- **Quản lý công việc mượt mà**: Tự động tạo task (issue) trên Linear cho đội DevOps xử lý và lưu log audit chi tiết vào Google Sheets.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI BẮT ĐẦU]
- Tài khoản n8n (Cloud hoặc Self-hosted).
- File **Google Sheets** chứa danh sách các domain cần theo dõi.
- Tài khoản **Slack** và quyền tích hợp Bot/Webhook vào kênh cảnh báo (ví dụ: `#ssl-alerts`).
- Tài khoản **Linear** và API Token để tự động tạo issue.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow này và paste trực tiếp vào n8n Editor, hoặc import file JSON thông qua menu tuỳ chọn của n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm **9 nodes** chính, các sếp cần chú ý cấu hình kỹ các phần sau:

- **Node `Every Day at 8 AM` (scheduleTrigger)**: 
  - Cấu hình múi giờ (Timezone) chính xác theo giờ Việt Nam (`Asia/Ho_Chi_Minh`) để workflow chạy đúng 8 giờ sáng mỗi ngày.
- **Node `Read Domains from Sheets` (googleSheets)**: 
  - Kết nối tài khoản Google Sheets của các sếp.
  - Chọn đúng file Spreadsheet và Sheet chứa danh sách domain cần kiểm tra.
- **Các node Code xử lý (`Check SSL Certificate Expiry`, `Classify Alert Severity`, `Filter Expiring Certs`, `Filter High Priority Alerts`)**:
  - Không cần sửa code quá nhiều, nhưng các sếp có thể điều chỉnh ngưỡng thời gian (threshold) hết hạn SSL (ví dụ: đổi từ 30 ngày xuống 15 ngày tùy chính sách bảo mật).
- **Node `Post Alert to Slack` (slack)**:
  - Chọn Credentials Slack và trỏ tới kênh nhận thông báo (ví dụ: `#ssl-alerts`).
- **Node `Create Issue in Linear` (linear)**:
  - Cấu hình Linear API Key để hệ thống tự động tạo ticket giao việc cho dev khi có chứng chỉ đạt mức cảnh báo cao (High Priority).
- **Node `Append Alert Log to Sheets` (googleSheets)**:
  - Cấu hình ghi log lịch sử kiểm tra vào một sheet khác trên Google Sheets để làm báo cáo kiểm toán (audit trail).

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** để test thử nghiệm với dữ liệu hiện tại xem các node code và kết nối API có hoạt động mượt mà không.
- Nếu mọi thứ xanh mướt, gạt công tắc sang **Active** để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Telegram/Discord**: Nếu team dùng Telegram thay vì Slack, các sếp chỉ cần thay thế node Slack bằng node Telegram.
- **Báo cáo định kỳ hàng tuần**: Thêm một nhánh gửi tổng kết trạng thái tất cả SSL vào mỗi Thứ Hai đầu tuần.
- **Gắn nhãn Team trên Linear**: Phân loại issue tự động giao cho đúng team phụ trách dựa vào thông tin cột "Team" trong Google Sheets.

### 📌 Kết luận
Việc để SSL hết hạn là lỗi "chí mạng" nhưng cực kỳ dễ tránh nếu sử dụng hệ thống tự động hóa. Hãy triển khai ngay workflow này để bảo vệ website và uy tín doanh nghiệp của các sếp ngay hôm nay!