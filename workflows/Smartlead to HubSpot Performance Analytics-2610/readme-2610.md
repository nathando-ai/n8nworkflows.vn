---
title: "🚀 Tự động hóa phân tích hiệu suất HubSpot với Smartlead - Tiết kiệm 80% thời gian báo cáo"
description: "Hướng dẫn tự động hóa workflow n8n để đồng bộ dữ liệu Smartlead với HubSpot, tạo báo cáo hiệu suất chiến dịch tự động và lưu vào PostgreSQL/Google Sheets"
slug: "tu-dong-hoa-phan-tich-hieu-suat-hubspot-smartlead"
tags: [n8n, automation, no-code, hubspot, smartlead, postgres, google-sheets]
keywords: [n8n workflow, tự động hóa, hubspot analytics, smartlead integration, báo cáo marketing]
---

# 🚀 Tự động hóa phân tích hiệu suất HubSpot với Smartlead - Tiết kiệm 80% thời gian báo cáo

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Khi làm việc với HubSpot và Smartlead, các sếp thường phải đối mặt với những thách thức lớn:
- **Thời gian báo cáo dài**: Tạo báo cáo hiệu suất chiến dịch mất hàng giờ mỗi tuần
- **Dữ liệu không đồng bộ**: Dữ liệu giữa các nền tảng không được cập nhật liên tục
- **Công việc lặp lại**: Phải thủ công nhập liệu giữa các hệ thống
- **Khó theo dõi**: Không có báo cáo thống nhất về hiệu suất chiến dịch

Với workflow này, các sếp có thể:
- Tự động đồng bộ dữ liệu giữa Smartlead và HubSpot
- Tạo báo cáo hiệu suất chiến dịch tự động
- Lưu trữ dữ liệu vào PostgreSQL và Google Sheets
- Nhận báo cáo định kỳ mà không cần can thiệp

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm **80% thời gian báo cáo** hàng tuần
- Dữ liệu được cập nhật **liên tục** trong 24/7
- Báo cáo **chính xác và thống nhất** giữa các nền tảng
- Giảm **lỗi nhập liệu** do thủ công
- Có **báo cáo định kỳ** mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản HubSpot với quyền truy cập API
- Tài khoản Smartlead với API key
- PostgreSQL đã cài đặt và cấu hình (theo [hướng dẫn này](https://github.com/wukimidaire/postgres_table_templates))
- Tài khoản Google với quyền truy cập Google Sheets API
- Tạo 3 bảng trong PostgreSQL: `ce_campaign_activity`, `ce_campaign`, `hubspot`
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/2610](https://n8n.io/workflows/2610)
2. Click vào nút "Download" để tải file JSON
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **SET SMARTLEAD API KEY** (Node "set"):
   - Cấu hình API key của Smartlead (tìm kiếm ở [đây](https://app.smartlead.ai/app/settings/profile))

2. **HubSpot** (Node "hubspot"):
   - Chọn credentials HubSpot OAuth2 API
   - Đảm bảo tài khoản HubSpot có quyền truy cập đầy đủ

3. **UPDATE CAMPAIGN** (Node "postgres"):
   - Cấu hình kết nối PostgreSQL
   - Đảm bảo bảng `ce_campaign` đã được tạo

4. **UPSERT CAMPAIGN ACTIVITY** (Node "postgres"):
   - Cấu hình kết nối PostgreSQL
   - Đảm bảo bảng `ce_campaign_activity` đã được tạo

5. **HUBSPOT TABLE** (Node "postgres"):
   - Cấu hình kết nối PostgreSQL
   - Đảm bảo bảng `hubspot` đã được tạo

6. **Google Sheets** (Node "googleSheets"):
   - Chọn credentials Google Sheets OAuth2 API
   - Chỉ định ID của Google Sheet và tên sheet cần cập nhật

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng
2. Bật Active workflow để chạy tự động theo lịch trình

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Teams để nhận thông báo khi có chiến dịch mới
- Thêm node gửi email báo cáo định kỳ
- Tích hợp với Power BI/Tableau để tạo dashboard trực quan
- Thêm node lưu log hoạt động vào Google Sheets

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc phân tích hiệu suất chiến dịch HubSpot. Bằng cách tự động hóa quy trình này, các sếp có thể tập trung vào những nhiệm vụ quan trọng hơn và nhận được báo cáo chính xác, cập nhật liên tục. Hãy áp dụng ngay để nâng cao hiệu quả làm việc của đội ngũ marketing!