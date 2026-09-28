---
title: "🌌 [Tự động hóa] Gửi ảnh thiên văn hàng ngày lên Telegram mỗi ngày"
description: "Workflow n8n tự động lấy và gửi ảnh thiên văn hàng ngày từ NASA lên kênh Telegram của bạn mỗi sáng. Tiết kiệm thời gian và cá nhân hóa nội dung thiên văn cho cộng đồng."
slug: "tu-dong-gui-anh-thien-van-hang-ngay-len-telegram"
tags: [n8n, automation, no-code, telegram, nasa]
keywords: [n8n workflow, tự động hóa, ảnh thiên văn, telegram, nasa]
---

# 🌌 [Tự động hóa] Gửi ảnh thiên văn hàng ngày lên Telegram mỗi ngày

[Các sếp ơi! Bạn có biết rằng mỗi ngày NASA đều cập nhật một bức ảnh thiên văn tuyệt đẹp trên trang chủ của họ không? Nhưng việc phải truy cập trang web mỗi ngày để xem ảnh này thật là tẻ nhạt, phải không? Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình: từ lấy ảnh đến gửi lên Telegram của mình mỗi sáng, chỉ trong vài phút cài đặt.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần truy cập trang web NASA mỗi ngày để xem ảnh.
- **Cá nhân hóa**: Gửi ảnh thiên văn hàng ngày đến cộng đồng của bạn trên Telegram.
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công sau khi cài đặt.
- **Hoạt động liên tục**: Workflow chạy tự động mỗi ngày vào lúc bạn chỉ định.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Telegram**: Cần có một kênh Telegram để gửi ảnh.
- **API Key từ NASA**: Đăng ký tài khoản tại [NASA API](https://api.nasa.gov/) để lấy API Key.
- **API Token từ Telegram**: Tạo bot Telegram và lấy API Token từ [BotFather](https://core.telegram.org/bots#botfather).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/828](https://n8n.io/workflows/828) để tải file JSON của workflow.
2. Trong n8n Editor, nhấn vào **Import from File** và chọn file JSON đã tải về.
3. Hoặc, copy toàn bộ nội dung JSON từ trang web và paste vào **Import from Clipboard**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node Cron**:
   - Chỉnh sửa thời gian chạy theo lịch của bạn (ví dụ: `0 8 * * *` để chạy vào lúc 8h sáng mỗi ngày).

2. **Node NASA**:
   - Chọn **Credentials** là `nasaApi`.
   - Đảm bảo đã điền đúng **API Key** từ NASA vào credentials này.

3. **Node Telegram**:
   - Chọn **Credentials** là `telegramApi`.
   - Đảm bảo đã điền đúng **API Token** từ Telegram vào credentials này.
   - Chọn **Operation** là `sendPhoto`.
   - Điền **Chat ID** của kênh Telegram mà bạn muốn gửi ảnh đến.

#### 3. Kích hoạt ⚡️
1. Nhấn **Execute Workflow** để test với dữ liệu mẫu.
2. Sau khi test thành công, nhấn **Activate Workflow** để chạy tự động theo lịch đã cài đặt.

### ✍️ Mẹo & gợi ý nâng cao
- **Gửi báo cáo định kỳ**: Kết hợp với node Email để gửi báo cáo hàng tuần về ảnh thiên văn đã gửi.
- **Lưu trữ ảnh**: Kết hợp với node Google Drive để lưu trữ ảnh thiên văn hàng ngày.
- **Thông báo lỗi**: Cài đặt thông báo lỗi qua Telegram nếu workflow gặp sự cố.

### 📌 Kết luận
Với workflow này, các sếp có thể tự động hóa việc gửi ảnh thiên văn hàng ngày lên Telegram chỉ trong vài phút. Hãy áp dụng ngay để tiết kiệm thời gian và cá nhân hóa nội dung thiên văn cho cộng đồng của mình! 🚀