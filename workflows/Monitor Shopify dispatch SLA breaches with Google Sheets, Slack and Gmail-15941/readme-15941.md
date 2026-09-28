---
title: "🚀 Tự động giám sát SLA giao hàng Shopify: Cảnh báo qua Slack & Gmail thông minh"
description: "Hướng dẫn xây dựng workflow n8n tự động kiểm tra đơn hàng chưa xử lý quá hạn SLA trên Shopify, chống spam thông báo bằng Google Sheets và gửi cảnh báo tức thì qua Slack, Gmail."
slug: "tu-dong-giam-sat-sla-giao-hang-shopify-slack-gmail"
tags: [n8n, automation, shopify, google-sheets, slack, gmail, e-commerce]
keywords: [n8n workflow, shopify sla breach, tu dong hoa shopify, canh bao don hang tre, google sheets dedup]
---

# 🚀 Tự động giám sát SLA giao hàng Shopify: Cảnh báo qua Slack & Gmail thông minh

Việc quản lý các đơn hàng chưa xử lý (unfulfilled orders) quá hạn SLA trên Shopify theo cách thủ công thường gây ra nhiều phiền toái: nhân viên dễ bỏ sót đơn hàng quan trọng, khách hàng phàn nàn vì giao hàng chậm, và việc kiểm tra lặp đi lặp lại hàng giờ liền ngốn rất nhiều thời gian của đội ngũ vận hành.

Workflow n8n này sinh ra để giải quyết triệt để nỗi đau đó. Hệ thống sẽ tự động hóa 100% quy trình kiểm tra, lọc đơn hàng quá hạn, thông minh loại bỏ các đơn đã cảnh báo (chống spam) và đẩy thông tin trực tiếp đến Slack cùng Gmail của đội ngũ quản lý.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 100%:** Kiểm tra đơn hàng mỗi giờ mà không cần sự can thiệp thủ công.
- **Chống spam thông minh:** Nhờ tích hợp Google Sheets để ghi log và deduplicate (khử trùng lặp), đội ngũ chỉ nhận cảnh báo cho các đơn hàng *mới phát sinh* quá hạn.
- **Phân loại khách hàng VIP:** Tự động đánh dấu các đơn hàng giá trị cao để ưu tiên xử lý trước.
- **Đa kênh thông báo:** Cảnh báo tức thì qua Slack team và gửi Email HTML chi tiết qua Gmail, kèm hệ thống bắt lỗi (Global Error Trigger) cực kỳ an toàn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Phiên bản 2.20 trở lên).
- Cửa hàng Shopify (đã cấu hình API/OAuth2).
- Tài khoản Google Sheets, Gmail và Slack để kết nối credentials.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow hoặc copy trực tiếp mã nguồn JSON và paste vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các node quan trọng sau đây:

- **Set SLA Config:** Node trung tâm cấu hình toàn bộ tham số:
  - `slaHours`: Số giờ tối đa trước khi đơn hàng bị tính là quá hạn SLA (ví dụ: `48`).
  - `vipThreshold`: Ngưỡng giá trị đơn hàng được tính là VIP (ví dụ: `3000`).
  - `recipientMail`: Địa chỉ email nhận báo cáo.
  - `googleSheetUrl`: Link Google Sheet lưu log.
  - `slackEscalationChannel`: ID của kênh Slack nhận cảnh báo (ví dụ: `C01ABC123`). *Lưu ý: Click chuột phải vào kênh trên Slack → Copy Link để lấy ID.*

- **Google Sheet chuẩn bị sẵn:** 
  Tạo một Google Sheet mới với các tiêu đề cột ở dòng 1 (phân biệt hoa thường):
  `runTimestamp` | `unfulfilledOrderIds` | `vipOrderIds` | `totalOrders` | `alertStatus`
  *(Tuyệt đối không đổi tên cột `unfulfilledOrderIds` vì node `Process & Deduplicate` dựa vào đây để chống trùng lặp).*

- **Slack - Post Alert & Slack - Error Alert:** 
  Mở các node Slack này và chọn lại kênh thông báo từ danh sách dropdown để đảm bảo tin nhắn gửi đúng nơi quy định.

- **Shopify & Google Sheets & Gmail Nodes:** 
  Tiến hành kết nối các tài khoản tương ứng (OAuth2) cho các node `Fetch Unfulfilled Orders`, `Read Previous Sheet Logs`, `Log Breach to Sheets`, và `Email SLA Breach Alert`.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (Test run) một lần để kiểm tra dữ liệu trả về từ Shopify và Google Sheets.
- Bật công tắc **Active** để workflow chạy tự động theo lịch hẹn hàng giờ từ `Hourly SLA Trigger`.

### ✍️ Mẹo & gợi ý nâng cao
- **Tăng tần suất:** Nếu cửa hàng có lượng đơn khủng, các sếp có thể chỉnh `Hourly SLA Trigger` thành chạy mỗi 30 phút.
- **Mở rộng kênh thông báo:** Có thể nhân bản node Slack hoặc kết hợp thêm node Telegram để bắn tin nhắn sang nhóm vận hành kho.
- **Lưu trữ nâng cao:** Kết hợp thêm cơ sở dữ liệu như Airtable hoặc PostgreSQL nếu muốn lưu log dài hạn thay vì Google Sheets.

### 📌 Kết luận
Với workflow này, bài toán giám sát SLA giao hàng trên Shopify sẽ được giải quyết triệt để, giúp giảm thiểu tối đa tình trạng trễ đơn, nâng cao uy tín cửa hàng và tiết kiệm hàng chục giờ làm việc thủ công mỗi tuần. Hãy thiết lập ngay hôm nay các sếp nhé!