---
title: "📊 Tự động gửi báo cáo lưu lượng ngoại tài TWSE hàng tuần lên Telegram"
description: "Hướng dẫn tự động hóa báo cáo lưu lượng ngoại tài TWSE hàng tuần với n8n, tiết kiệm thời gian và tăng hiệu quả phân tích thị trường"
slug: "tu-dong-gui-bao-cao-luu-luong-ngoai-tai-twse-hang-tuan-len-telegram"
tags: [n8n, automation, no-code, twse, telegram]
keywords: [n8n workflow, tự động hóa báo cáo, lưu lượng ngoại tài, twse, telegram]
---

# 📊 Tự động gửi báo cáo lưu lượng ngoại tài TWSE hàng tuần lên Telegram

[Bài toán thực tế: Các nhà đầu tư và nhà phân tích thị trường thường phải theo dõi thủ công lưu lượng ngoại tài hàng ngày từ TWSE (Taiwan Stock Exchange), một quá trình tốn thời gian và dễ sai sót. Workflow này giúp tự động hóa quy trình này hoàn toàn, tiết kiệm thời gian và đảm bảo độ chính xác cao.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 2-3 giờ mỗi tuần cho việc thu thập và phân tích dữ liệu
- Đảm bảo độ chính xác cao với quy trình tự động hóa hoàn toàn
- Nhận báo cáo định kỳ với dữ liệu được tổng hợp sẵn
- Tự động bỏ qua các ngày nghỉ lễ của thị trường TWSE
- Dễ dàng tùy chỉnh các tham số báo cáo theo nhu cầu
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram và một bot Telegram (cần API token)
- ID của kênh/nhóm Telegram muốn gửi báo cáo
- Tài khoản n8n đã được cài đặt và chạy
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào "Import from URL" và dán link sau: `https://n8n.io/workflows/16101`
3. Hoặc tải file JSON từ [đây](https://n8n.io/workflows/16101) và import thủ công

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Weekly Report Trigger"**:
   - Cấu hình lịch chạy hàng tuần (ví dụ: mỗi Chủ Nhật lúc 9:00 sáng)
   - Đặt múi giờ phù hợp với thị trường TWSE (GMT+8)

2. **Node "Set Report Config Parameters"**:
   - Thay đổi `chatId` thành ID của kênh/nhóm Telegram bạn muốn gửi báo cáo
   - Điều chỉnh `topN` để chọn số lượng cổ phiếu có lưu lượng ngoại tài lớn nhất muốn hiển thị
   - Cập nhật `holidaySkipList` với các ngày nghỉ lễ của thị trường TWSE

3. **Node "Send Report to Telegram"**:
   - Thêm credentials cho Telegram API (cần token của bot Telegram)
   - Đảm bảo bot có quyền gửi tin nhắn đến kênh/nhóm đã cấu hình

#### 3. Kích hoạt ⚡️
1. Chạy test với dữ liệu mẫu để kiểm tra kết quả
2. Bật chế độ Active cho workflow
3. Kiểm tra kênh Telegram để xác nhận báo cáo được gửi đúng định dạng

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node gửi email để lưu trữ lịch sử báo cáo
- Kết hợp với workflow khác để phân tích xu hướng lưu lượng ngoại tài
- Tùy chỉnh định dạng báo cáo để phù hợp với các công cụ phân tích khác
- Thiết lập cảnh báo khi lưu lượng ngoại tài vượt ngưỡng nhất định
- Tích hợp với các công cụ khác như TradingView để tạo báo cáo thị trường toàn diện

### 📌 Kết luận
Workflow này giúp các nhà đầu tư và nhà phân tích thị trường tự động hóa quy trình theo dõi lưu lượng ngoại tài TWSE hàng tuần, tiết kiệm thời gian và đảm bảo độ chính xác cao. Hãy thử ngay và nâng cao hiệu quả phân tích thị trường của bạn!