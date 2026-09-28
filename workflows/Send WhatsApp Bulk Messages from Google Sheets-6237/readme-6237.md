---
title: "🚀 Gửi Tin Nhắn WhatsApp Hàng Loạt Từ Google Sheets - Tự Động Hóa Nhanh Chóng"
description: "Hướng dẫn chi tiết cách tự động gửi tin nhắn WhatsApp hàng loạt từ Google Sheets bằng n8n, tiết kiệm thời gian và nâng cao hiệu quả marketing"
slug: "gui-tin-nhan-whatsapp-hang-loat-tu-google-sheets"
tags: [n8n, automation, no-code, whatsapp, google-sheets]
keywords: [n8n workflow, tự động hóa, gửi tin nhắn whatsapp, google sheets, marketing]
---

# 🚀 Gửi Tin Nhắn WhatsApp Hàng Loạt Từ Google Sheets - Tự Động Hóa Nhanh Chóng

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đáng kể trong việc gửi tin nhắn hàng loạt
- Tăng độ chính xác và độ cá nhân hóa trong các cuộc trò chuyện
- Theo dõi trạng thái gửi tin nhắn một cách tự động
- Tự động hóa hoàn toàn quá trình gửi tin nhắn
- Tiết kiệm chi phí so với các giải pháp gửi tin nhắn truyền thống
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập vào Google Sheets
- Tài khoản WhatsApp Business Cloud API (từ Meta Developer)
- Google Sheets đã được định dạng theo mẫu (xem phần dưới)
- Các template tin nhắn đã được phê duyệt từ Meta
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào "Import from URL" và dán link: https://n8n.io/workflows/6237
3. Hoặc tải file JSON về và chọn "Import from File"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Trigger Every 5 Minute** (scheduleTrigger):
   - Cấu hình thời gian chạy workflow (mặc định là mỗi 5 phút)

2. **Fetch All Pending Queries for Messaging** (googleSheets):
   - Chọn credentials Google Sheets OAuth2 API
   - Chọn spreadsheet và worksheet chứa dữ liệu
   - Thêm filter: `Status is empty` để chỉ lấy các hàng chưa được xử lý

3. **Limit** (limit):
   - Đặt giới hạn số lượng bản ghi xử lý trong mỗi lần chạy (ví dụ: 50 bản ghi)

4. **Loop Over Items** (splitInBatches):
   - Cấu hình số lượng bản ghi xử lý trong mỗi batch (ví dụ: 5 bản ghi/batch)
   - Thêm delay giữa các batch (ví dụ: 0.5 giây)

5. **Clean WhatsApp Number** (code):
   - Kiểm tra và làm sạch số điện thoại WhatsApp
   - Xóa các ký tự không hợp lệ và định dạng số điện thoại

6. **Send Message to 100 Phone No1** (whatsApp):
   - Chọn credentials WhatsApp API
   - Đảm bảo sử dụng template tin nhắn đã được phê duyệt từ Meta
   - Map các biến từ Google Sheets vào template tin nhắn

7. **Change State of Rows in Sent1** (googleSheets):
   - Cập nhật trạng thái của các hàng đã được xử lý
   - Cập nhật cột "Status" thành "Sent" hoặc "Failed" dựa trên kết quả gửi tin nhắn

#### 3. Kích hoạt ⚡️
1. Kiểm tra workflow bằng cách chạy thử với dữ liệu mẫu
2. Sau khi kiểm tra thành công, nhấn "Activate" để kích hoạt workflow
3. Workflow sẽ tự động chạy theo lịch trình đã cấu hình

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Telegram**: Thêm node để nhận thông báo khi workflow hoàn thành hoặc gặp lỗi
2. **Lưu log hoạt động**: Thêm node để lưu log các hoạt động quan trọng vào Google Sheets hoặc cơ sở dữ liệu
3. **Gửi báo cáo định kỳ**: Tạo một workflow phụ để gửi báo cáo tổng hợp về hoạt động gửi tin nhắn
4. **Xử lý lỗi tự động**: Thêm logic xử lý lỗi để tự động gửi lại tin nhắn khi gặp lỗi tạm thời

### 📌 Kết luận
Workflow "Send WhatsApp Bulk Messages from Google Sheets" giúp các sếp tự động hóa hoàn toàn quá trình gửi tin nhắn WhatsApp hàng loạt từ Google Sheets. Với việc tích hợp n8n, các sếp có thể tiết kiệm thời gian đáng kể, tăng độ chính xác và nâng cao hiệu quả marketing. Hãy áp dụng ngay để tối ưu hóa các chiến dịch truyền thông của bạn!