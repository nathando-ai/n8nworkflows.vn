---
title: "🚀 Tự động hóa báo cáo Meta Ads vào Google Sheets hằng ngày và dữ liệu lịch sử"
description: "Hướng dẫn chi tiết cách sử dụng n8n workflow để tự động đồng bộ hiệu suất chiến dịch Meta (Facebook) Ads vào Google Sheets hằng ngày và backfill dữ liệu cũ."
slug: "meta-ads-to-google-sheets-daily-historical-report"
tags: [n8n, automation, meta-ads, facebook-ads, google-sheets, marketing-automation]
keywords: [n8n workflow, tự động hóa meta ads, facebook ads to google sheets, báo cáo quảng cáo facebook, market research automation]
---

# 🚀 Tự động hóa báo cáo Meta Ads vào Google Sheets hằng ngày và dữ liệu lịch sử

Việc tổng hợp thủ công dữ liệu quảng cáo từ Meta (Facebook) Ads vào file Excel hay Google Sheets mỗi ngày tốn rất nhiều thời gian của các Media Buyer và Performance Marketer. Chưa kể việc thiếu hụt dữ liệu lịch sử (historical data) hay sai sót khi tính toán các chỉ số như CPL, CPA, ROAS. 

Workflow n8n này sẽ giải quyết triệt để vấn đề đó bằng cách tự động hóa 100%: đồng bộ dữ liệu chiến dịch hằng ngày vào lúc 06:00 sáng và hỗ trợ nạp dữ liệu lịch sử (backfill) theo yêu cầu mà không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hoàn toàn hằng ngày:** Chạy ngầm mỗi ngày lúc 06:00 sáng để đẩy dữ liệu ngày hôm trước vào Google Sheet.
- **Linh hoạt nạp dữ liệu quá khứ (Backfill):** Dễ dàng cào lại dữ liệu lịch sử 12-24 tháng trước theo từng khoảng thời gian tùy chỉnh.
- **Tính toán sẵn các chỉ số quan trọng:** Tự động quy đổi và tính toán các KPI cốt lõi như **CPL, CPA, ROAS, frequency, CTR, CPC, CPM**.
- **Sẵn sàng làm Dashboard:** Dữ liệu chuẩn chỉnh, sạch sẽ, sẵn sàng làm nguồn dữ liệu cho Looker Studio, Power BI hoặc Excel.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản Facebook Developer / Meta Ads:** Đã tạo App hoặc Token có quyền truy cập Meta Ads Insights (`facebookGraphApi`).
- **Google Account:** Tài khoản Google Sheets để lưu trữ dữ liệu báo cáo (`googleSheetsOAuth2Api`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ n8n và import trực tiếp vào giao diện n8n Editor của các sếp, hoặc sao chép và dán trực tiếp vào workspace.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các node sau để workflow chạy mượt mà:

- **Node `Set config (Meta + Sheets)` & `Set backfill config`**: 
  - Điền `adAccountId` của tài khoản quảng cáo Meta cần lấy dữ liệu.
  - Điền `sheetId` của Google Sheet đích.
  - Cấu hình khoảng thời gian (`backfillSince` và `backfillUntil`) nếu các sếp chạy phần nạp dữ liệu lịch sử thủ công.
- **Cấu trúc Google Sheet (CỰC KỲ QUAN TRỌNG)**: 
  Trước khi chạy workflow, hãy chắc chắn Google Sheet của các sếp đã tạo dòng tiêu đề (Header row) với đầy đủ các cột sau theo đúng thứ tự:
  `date | account_id | account_name | publisher_platform | campaign_id | campaign_name | objective | adset_id | adset_name | ad_id | ad_name | impressions | reach | frequency | spend | clicks | inline_link_clicks | ctr | cpc | cpm | leads | on_facebook_lead | purchases | purchase_value | add_to_cart | initiate_checkout | cpl | cpa | roas`
- **Node `Fetch Meta Insights (yesterday)` & `Fetch Meta Insights (time_range)`**: 
  - Kết nối tài khoản thông qua **Facebook Graph API Credentials**.
- **Node `Append daily rows to Google Sheet` & `Append backfill rows to Google Sheet`**: 
  - Kết nối tài khoản thông qua **Google Sheets OAuth2 API Credentials** và chọn đúng Sheet Name.

#### 3. Kích hoạt ⚡️
- Chạy thử công cụ **Manual backfill trigger** một lần bằng cách bấm *Execute workflow* để test việc nạp dữ liệu lịch sử (lưu ý chọn khoảng thời gian ngắn trước khi chạy dải dài).
- Bật công tắc **Active** tại góc trên cùng bên phải để kích hoạt lịch chạy tự động hằng ngày (`Daily schedule (06:00)`).

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối Dashboard:** Sử dụng Google Sheet này làm nguồn dữ liệu trực tiếp cho Looker Studio để vẽ biểu đồ chi phí và doanh thu real-time cho sếp lớn xem.
- **Cảnh báo qua Slack/Telegram:** Thêm node Slack hoặc Telegram ở cuối workflow để thông báo ngay vào nhóm chat khi dữ liệu hằng ngày đã được đồng bộ thành công hoặc nếu có lỗi xảy ra từ API Meta.
- **Chia nhỏ Backfill:** Khi kéo dữ liệu lịch sử quá lâu (ví dụ 2 năm), hãy chia nhỏ theo từng Quý (`quarter`) để tránh việc API Meta trả về quá nặng gây timeout.

### 📌 Kết luận
Workflow này là "vũ khí" tối ưu thời gian tuyệt vời cho các Media Buyer, Agency hay các chủ doanh nghiệp chạy quảng cáo trực tiếp. Thay vì tốn hàng giờ mỗi tuần để xuất CSV và tổng hợp báo cáo thủ công, giờ đây hệ thống đã tự động hóa toàn bộ. Thiết lập ngay hôm nay và tối ưu hóa quy trình marketing của các sếp nhé!