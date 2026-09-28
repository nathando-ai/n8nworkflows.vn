---
title: "🚀 Tự động gửi tin nhắn WhatsApp cá nhân hóa theo KlickTipp với phản hồi tự động"
description: "Hướng dẫn chi tiết cách tự động hóa gửi tin nhắn WhatsApp cá nhân hóa theo KlickTipp và xử lý phản hồi tự động để điều khiển chiến dịch quảng cáo"
slug: "tu-dong-gui-tin-nhan-whatsapp-ca-nhan-hoa-theo-klicktipp"
tags: [n8n, automation, no-code, whatsapp, klicktipp]
keywords: [n8n workflow, tự động hóa, whatsapp, klicktipp, tin nhắn cá nhân hóa]
---

# 🚀 Tự động gửi tin nhắn WhatsApp cá nhân hóa theo KlickTipp với phản hồi tự động

[Các sếp đang gặp khó khăn khi phải gửi hàng loạt tin nhắn WhatsApp thủ công cho khách hàng, đặc biệt là khi cần cá nhân hóa nội dung cho từng người. Việc này tốn thời gian, dễ gây lỗi và không thể đảm bảo tính liên tục. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình này một cách hoàn toàn không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động gửi hàng loạt tin nhắn cá nhân hóa mà không cần can thiệp thủ công.
- **Chính xác cao**: Dữ liệu được lọc và cá nhân hóa chính xác theo thông tin từ KlickTipp.
- **Tương tác tự động**: Xử lý phản hồi từ khách hàng và điều khiển chiến dịch quảng cáo một cách liên tục.
- **Tích hợp hoàn chỉnh**: Kết nối liền mạch giữa KlickTipp và WhatsApp Business Cloud.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản KlickTipp đã được cấu hình và có API key.
- Tài khoản WhatsApp Business Cloud đã được cấu hình và có API key.
- Các trường tùy chỉnh sau trong KlickTipp:
  - `Whatsapp_Produkt/Dienstleistung` (Zeile)
  - `Whatsapp_Name/Unternehmen` (Zeile)
  - `Whatsapp_Link_Endung` (Zeile)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [trang workflow trên n8n.io](https://n8n.io/workflows/3937)
2. Click vào nút "Copy to clipboard" để sao chép JSON workflow
3. Trong n8n Editor, click vào "Import from Clipboard" và dán JSON đã sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "New message in WhatsApp"**:
   - Chọn credentials "whatsAppTriggerApi" đã được cấu hình
   - Đảm bảo tài khoản WhatsApp Business Cloud đã được kích hoạt webhook

2. **Node "KlickTipp Outbound triggered"**:
   - Chọn credentials "klickTippApi" đã được cấu hình
   - Đảm bảo tag kích hoạt Outbound trong KlickTipp đã được đặt chính xác

3. **Node "Sending WhatsApp offer template"**:
   - Chọn credentials "whatsAppApi" đã được cấu hình
   - Cập nhật ID template WhatsApp đã được phê duyệt
   - Đảm bảo các trường dữ liệu động ({{1}}, {{2}}, {{3}}) đã được ánh xạ đúng với các trường tùy chỉnh trong KlickTipp

4. **Node "Sending WhatsApp auto-responder template"**:
   - Chọn credentials "whatsAppApi" đã được cấu hình
   - Cập nhật ID template WhatsApp đã được phê duyệt cho phản hồi tự động

5. **Node "Subscribe number to opt-out from WA messages"**:
   - Chọn credentials "klickTippApi" đã được cấu hình
   - Đảm bảo các tham số operation và resource đã được đặt là "subscribe" và "subscriber"

6. **Node "Filter user messages"**:
   - Cấu hình điều kiện lọc để chỉ xử lý các tin nhắn từ người dùng (bỏ qua các tin nhắn từ hệ thống)

#### 3. Kích hoạt ⚡️
1. Thực hiện test run với dữ liệu mẫu:
   - Tạo một liên hệ thử nghiệm trong KlickTipp với các trường tùy chỉnh đã được điền đầy đủ
   - Gắn tag kích hoạt Outbound cho liên hệ thử nghiệm
2. Kiểm tra:
   - Tin nhắn WhatsApp được gửi thành công
   - Phản hồi từ khách hàng được xử lý đúng
   - Liên hệ được đăng ký và gắn tag trong KlickTipp
3. Bật Active workflow sau khi đã kiểm tra và xác nhận hoạt động ổn định

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp với email series**: Kết hợp với chuỗi email trong KlickTipp để tạo trải nghiệm đa kênh (email + WhatsApp)
2. **Phân đoạn người dùng**: Sử dụng các tag phân đoạn để gửi các tin nhắn khác nhau cho các nhóm người dùng khác nhau
3. **Theo dõi hiệu suất**: Thêm node để ghi log các tương tác và phân tích hiệu suất của các chiến dịch
4. **Tự động hóa phản hồi**: Mở rộng workflow để xử lý nhiều loại phản hồi khác nhau từ khách hàng

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc tự động hóa gửi tin nhắn WhatsApp cá nhân hóa theo KlickTipp và xử lý phản hồi tự động. Với các bước cấu hình đơn giản và các tính năng mạnh mẽ, các sếp có thể tối ưu hóa chiến dịch quảng cáo của mình một cách hiệu quả và chuyên nghiệp. Hãy áp dụng ngay để nâng cao trải nghiệm khách hàng và tăng tỷ lệ tương tác!