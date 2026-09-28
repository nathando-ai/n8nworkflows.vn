---
title: "🚀 Tự động hóa đồng bộ đơn hàng và hoàn tiền Eventbrite sang KlickTipp cho Marketing Sự kiện Tự động"
description: "Tự động đồng bộ dữ liệu đơn hàng và hoàn tiền từ Eventbrite sang KlickTipp để quản lý và phân khúc khách hàng một cách hiệu quả, tiết kiệm thời gian và tránh sai sót thủ công."
slug: "tu-dong-hoa-don-hang-hoan-tien-eventbrite-klicktipp"
tags: [n8n, automation, no-code, eventbrite, klicktipp]
keywords: [n8n workflow, tự động hóa, eventbrite, klicktipp, marketing sự kiện]
---

# 🚀 Tự động hóa đồng bộ đơn hàng và hoàn tiền Eventbrite sang KlickTipp cho Marketing Sự kiện Tự động

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp có thể đã từng gặp phải tình trạng này: quản lý đơn hàng và hoàn tiền từ Eventbrite thủ công, đồng bộ dữ liệu sang KlickTipp để phân khúc khách hàng, nhưng lại tốn nhiều thời gian và dễ xảy ra sai sót. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình này một cách hoàn toàn không cần viết code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động đồng bộ dữ liệu đơn hàng và hoàn tiền từ Eventbrite sang KlickTipp mà không cần can thiệp thủ công.
- Chính xác: Dữ liệu được đồng bộ chính xác và cập nhật liên tục, tránh sai sót do nhập liệu thủ công.
- Cá nhân hóa: Phân khúc khách hàng một cách hiệu quả dựa trên dữ liệu sự kiện.
- Hoạt động liên tục: Workflow chạy tự động 24/7, không phụ thuộc vào lịch trình của các sếp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Eventbrite với quyền truy cập OAuth2.
- Tài khoản KlickTipp với quyền truy cập API.
- Các trường tùy chỉnh trong KlickTipp:
  - `Eventbrite | Event name`
  - `Eventbrite | Start timestamp`
  - `Eventbrite | Event page URL`
- Các thẻ trong KlickTipp:
  - `Eventbrite | Buyer`
  - `Eventbrite | Refundee`
  - `Eventbrite | Registrant`
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow này vào n8n của các sếp, các sếp có thể làm theo các bước sau:

1. Truy cập vào trang [Eventbrite Orders & Refunds to KlickTipp](https://n8n.io/workflows/10024) để tải file JSON của workflow.
2. Mở n8n Editor và nhấn vào nút "Import from File" hoặc "Import from URL".
3. Chọn file JSON đã tải về và nhấn "Import".

Hoặc các sếp cũng có thể copy/paste JSON từ trang web vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **Check for new orders and refunds**: Node này sử dụng Eventbrite Trigger để lắng nghe các sự kiện đơn hàng mới và hoàn tiền. Các sếp cần cấu hình credentials cho Eventbrite OAuth2 Api.
- **Get event data**: Node này sử dụng HTTP Request để lấy dữ liệu sự kiện từ Eventbrite. Các sếp cần cấu hình credentials cho Eventbrite OAuth2 Api.
- **Subscribe event attendee to KlickTipp**: Node này sử dụng KlickTipp để đăng ký người tham gia sự kiện. Các sếp cần cấu hình credentials cho KlickTipp Api.
- **Tag attendee in case of purchase**: Node này sử dụng KlickTipp để gắn thẻ cho người tham gia sự kiện trong trường hợp mua hàng. Các sếp cần cấu hình credentials cho KlickTipp Api.
- **Tag contact for refund**: Node này sử dụng KlickTipp để gắn thẻ cho liên hệ trong trường hợp hoàn tiền. Các sếp cần cấu hình credentials cho KlickTipp Api.

#### 3. Kích hoạt ⚡️
Sau khi đã cấu hình các node quan trọng, các sếp cần thực hiện các bước sau để kích hoạt workflow:

1. Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng như mong đợi.
2. Bật Active workflow để cho phép workflow chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Theo dõi sự tham gia và không tham gia**: Sử dụng các thẻ để theo dõi sự tham gia và không tham gia của khách hàng.
- **Phân khúc theo loại vé**: Điều chỉnh quy tắc gắn thẻ để phân khúc khách hàng theo loại vé.
- **Kích hoạt tự động hóa theo dõi**: Kích hoạt các tự động hóa theo dõi cho khách hàng đã hoàn tiền hoặc đã tham gia sự kiện.
- **Kết nối với các công cụ khác**: Kết nối với các công cụ khác để gửi nhắc nhở, khảo sát hoặc bán hàng thêm.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình đồng bộ đơn hàng và hoàn tiền từ Eventbrite sang KlickTipp, tiết kiệm thời gian và tránh sai sót thủ công. Các sếp chỉ cần cấu hình các node quan trọng và kích hoạt workflow để bắt đầu sử dụng.