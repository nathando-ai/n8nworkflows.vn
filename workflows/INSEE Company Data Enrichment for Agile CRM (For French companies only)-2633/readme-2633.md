---
title: "🚀 Tự động làm giàu dữ liệu doanh nghiệp Pháp trong Agile CRM với INSEE API"
description: "Hướng dẫn xây dựng workflow n8n tự động đồng bộ, cập nhật địa chỉ trụ sở chính và mã SIREN từ cơ sở dữ liệu mở INSEE của Pháp vào Agile CRM."
slug: "tu-dong-lam-giau-du-lieu-cong-ty-phap-agile-crm-insee-n8n"
tags: [n8n, automation, agile-crm, insee-api, data-enrichment, france]
keywords: [n8n workflow, agile crm insee, insee api automation, lam giau du lieu crm, tu dong hoa n8n]
---

# 🚀 Tự động làm giàu dữ liệu doanh nghiệp Pháp trong Agile CRM với INSEE API

Các sếp làm việc với thị trường Pháp chắc chắn hiểu được nỗi đau khi quản lý dữ liệu khách hàng doanh nghiệp. Thông tin công ty thay đổi liên tục, việc tra cứu thủ công từng mã SIREN, địa chỉ trụ sở chính từ cơ sở dữ liệu chính phủ Pháp lên Agile CRM vừa tốn thời gian, vừa dễ xảy ra sai sót.

Giải pháp là đây! Workflow n8n này sẽ tự động hóa 100% quy trình quét dữ liệu công ty từ **Agile CRM**, đối chiếu qua **Cơ sở dữ liệu mở INSEE (SIREN)** và cập nhật lại thông tin chính xác nhất mà không cần tốn một giọt mồ hôi.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Cập nhật địa chỉ tự động:** Tự động đồng bộ và chuẩn hóa địa chỉ trụ sở chính thức của doanh nghiệp Pháp.
- **Bổ sung mã định danh:** Tự động thêm mã số doanh nghiệp chính phủ Pháp (SIREN) vào Custom Field trên CRM.
- **Kiểm soát thông tin linh hoạt:** Hỗ trợ tính năng khóa dữ liệu (Read-only) thông qua trường "RO" để tránh ghi đè các dữ liệu quan trọng đã chỉnh sửa thủ công.
- **Hoạt động 24/7:** Chạy tự động theo lịch định kỳ hoặc kích hoạt thủ công khi cần.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Agile CRM Account:** Tài khoản Agile CRM và thông tin API credentials.
- **INSEE API Key:** Tài khoản và API Key miễn phí từ cổng [Insee Opendata API](https://portail-api.insee.fr/).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Copy toàn bộ mã JSON của workflow và dán trực tiếp vào n8n Editor của các sếp, hoặc import file JSON thông qua giao diện n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động mượt mà, các sếp cần chú ý cấu hình các node sau:
- **Cấu hình Custom Fields trong Agile CRM (Admin Settings):**
  - Tạo trường Custom Field với Label: `"SIREN"`, Type: `"Text Field"`, Description: `"N° de SIREN"`
  - Tạo trường Custom Field với Label: `"RO"`, Type: `"Number"`, Description: `"Locks entry from update"`
- **Get all Compagnies from Agile CRM & Enrich CRM with INSEE Data:** Kết nối với tài khoản **Agile CRM** credentials của các sếp.
- **Set Insee API Key:** Điền API Key INSEE chính thức vào node này để cho phép gọi dữ liệu từ hệ thống API chính phủ Pháp.
- **FilterOut all Company that have the ReadOnly Key set:** Node này giúp lọc ra các công ty có bật khóa bảo vệ (`RO = 1`) để tránh hệ thống ghi đè dữ liệu không mong muốn.

#### 3. Kích hoạt ⚡️
- Nhấn **Test workflow** trên node `When clicking ‘Test workflow’` để kiểm tra luồng chạy mẫu.
- Kiểm tra lại lịch trình tại `Schedule Trigger` (nếu cần tự động hóa định kỳ).
- Chuyển trạng thái workflow sang **Active** để chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo qua Slack/Telegram:** Thêm một node thông báo để nhận báo cáo ngay lập tức về số lượng công ty vừa được làm giàu dữ liệu mỗi khi chạy xong.
- **Lưu log vào Google Sheets:** Thêm bước ghi lại lịch sử cập nhật dữ liệu để dễ dàng kiểm toán (audit) khi cần thiết.
- **Tùy chỉnh chế độ Read-only tự động:** Tại node `Enrich CRM with INSEE Data`, các sếp có thể cấu hình thêm custom property `RO` giá trị `1` nếu muốn tự động khóa các bản ghi sau khi được cập nhật thành công.

### 📌 Kết luận
Tự động hóa việc làm giàu dữ liệu CRM chưa bao giờ dễ dàng đến thế đối với thị trường Pháp. Áp dụng ngay workflow này để tiết kiệm hàng giờ thao tác thủ công và giữ cho cơ sở dữ liệu khách hàng luôn sạch, chuẩn xác!