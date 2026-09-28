---
title: "🚀 Tự Động Hoàn Tất Dữ Liệu GA4 Về BigQuery Với Thông Báo Telegram - Giải Pháp Analytics Không Code"
description: "Workflow này tự động lấy dữ liệu chi tiết từ Google Analytics 4 (GA4) và lưu vào BigQuery, đồng thời gửi thông báo Telegram khi hoàn tất. Giúp các sếp tiết kiệm thời gian phân tích và tối ưu hóa chiến dịch marketing."
slug: "tự-dộng-hoàn-tất-du-lieu-ga4-ve-bigquery-telegram"
tags: [n8n, google-analytics-4, bigquery, telegram-alerts, analytics-engineering, marketing-automation]
keywords: [tự động hóa GA4 BigQuery, workflow n8n analytics, backfill dữ liệu GA4, báo cáo marketing tự động, tự động hóa dữ liệu marketing]
---

# 🚀 **Tự Động Hoàn Tất Dữ Liệu GA4 Về BigQuery Với Thông Báo Telegram**

## **Giải Pháp Cho Những Ai Đau Đầu Với Dữ Liệu Analytics**
Các sếp marketing hay chuyên gia phân tích thường phải mất **giờ đồng hồ** để thủ công xuất báo cáo từ Google Analytics 4 (GA4) và chuyển dữ liệu vào BigQuery để phân tích sâu. Kết quả? **Thời gian bị lãng phí**, **rủi ro sai sót cao**, và **không thể theo dõi dữ liệu liên tục** khi không có tự động hóa.

Workflow này **giải quyết tất cả vấn đề trên** bằng cách:
✅ **Lấy tự động** tất cả dữ liệu GA4 quan trọng (từ nguồn traffic, hành vi người dùng đến chuyển đổi và quảng cáo).
✅ **Lưu vào BigQuery** để phân tích sâu với SQL, Looker Studio, hoặc các công cụ BI khác.
✅ **Gửi thông báo Telegram** khi hoàn tất, giúp các sếp **biết ngay** dữ liệu đã được cập nhật.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính bảo mật và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần xuất báo cáo thủ công hàng ngày/tuần.
- **Dữ liệu chính xác**: Tránh sai sót khi copy-paste từ GA4 sang BigQuery.
- **Phân tích sâu**: Dữ liệu GA4 được lưu vào BigQuery, hỗ trợ **SQL, Looker Studio, Tableau** để tạo báo cáo chuyên nghiệp.
- **Theo dõi thực thời**: Nhận **thông báo Telegram** khi workflow hoàn tất, giúp các sếp **biết ngay** dữ liệu đã được cập nhật.
- **Hoạt động liên tục**: Sử dụng **Schedule Trigger**, workflow chạy tự động theo lịch (ví dụ: hàng ngày, hàng tuần).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Google Analytics 4 (GA4)** với quyền truy cập vào các báo cáo cần lấy.
✔ **Tài khoản Google BigQuery** với quyền **quản trị viên** trên dataset mục tiêu.
✔ **Tài khoản Telegram** để nhận thông báo (cần **Chat ID** và **API Token**).
✔ **Thông tin cấu hình**:
   - `project_id` của BigQuery.
   - `dataset_id` để lưu dữ liệu.
   - **GA4 Property ID** (ID của tài khoản GA4).
   - **Khoảng thời gian** muốn lấy dữ liệu (ví dụ: 1 tháng, 3 tháng).

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/11010](https://n8n.io/workflows/11010) hoặc copy toàn bộ JSON từ canvas.
- Mở **n8n Editor**, nhấn **Import Workflow** và dán JSON vào.
- **Hoặc** tải file JSON từ [đây](https://github.com/aliasoblomov/N8N-GA4-Backfill-Workflow) (nếu có).

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **32 node**, nhưng các bước quan trọng nhất cần chú ý:

##### **A. Cấu Hình "Backfill Config" (Node `set`)**
- Mở node **"Backfill Config"**, chỉnh sửa các tham số:
  ```json
  {
    "project_id": "your-bigquery-project-id",
    "dataset_id": "your-dataset-name",
    "start_date": "2024-01-01",  // Ngày bắt đầu lấy dữ liệu
    "end_date": "2024-01-31",    // Ngày kết thúc
    "ga4_property_id": "G-XXXXXXXX"  // ID của GA4 Property
  }
  ```
  - **Lưu ý**: Đảm bảo `project_id` và `dataset_id` **không có khoảng trắng** và đúng định dạng.

##### **B. Cấu Hình Credentials cho GA4 & BigQuery**
- **Tất cả các node GA4** (ví dụ: `GA4 - Session Channel Group`, `GA4 - Ads Data`) **sử dụng credentials `googleAnalyticsOAuth2`**.
  - **Cách thiết lập**:
    1. Vào **Credentials** trong n8n.
    2. Tạo mới **Google Analytics OAuth2**.
    3. Đăng nhập tài khoản GA4 và cấp quyền **truy cập dữ liệu**.
- **Tất cả các node BigQuery** (ví dụ: `BQ - ga4_data_session_channel_group`, `BQ - ga4_ads_data`) **sử dụng credentials `googleBigQueryOAuth2Api`**.
  - **Cách thiết lập**:
    1. Vào **Credentials** trong n8n.
    2. Tạo mới **Google BigQuery OAuth2 API**.
    3. Đăng nhập tài khoản Google Cloud và cấp quyền **quản lý dataset**.

##### **C. Cấu Hình Telegram Alerts**
- Node **"Send a text message"** (Telegram) cần:
  - **Credentials**: `telegramApi` (API Token của Telegram Bot).
    - **Cách lấy API Token**:
      1. Trên Telegram, tìm bot `@BotFather`.
      2. Gửi lệnh `/newbot` và theo hướng dẫn.
      3. Lưu **API Token** (dài 36 ký tự).
  - **Chat ID**: ID của chat riêng (cần lấy bằng cách gửi tin nhắn cho bot và copy từ URL).
    - **Cách lấy Chat ID**:
      1. Gửi tin nhắn cho bot Telegram của bạn.
      2. Mở trình duyệt, truy cập: `https://api.telegram.org/bot<API_TOKEN>/getUpdates`.
      3. Tìm `chat.id` trong kết quả JSON.

##### **D. Schedule Trigger (Node `scheduleTrigger`)**
- Node này **khởi động workflow theo lịch**.
- Mặc định, nó chạy **mỗi ngày lúc 00:00** (giờ UTC).
- **Cách chỉnh sửa**:
  1. Mở node **Schedule Trigger**.
  2. Chỉnh sửa `cron` theo định dạng:
     - `0 0 * * *` → Hàng ngày lúc 00:00 (UTC).
     - `0 8 * * 1` → Hàng tuần thứ 2 lúc 08:00 (UTC).
  3. **Lưu ý**: Nếu muốn chạy theo giờ Việt Nam (UTC+7), thêm `+7` vào cron:
     ```json
     "cron": "0 0 * * * +7"
     ```

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  1. Chọn **Run Workflow** (mũi tên vòng tròn).
  2. Chọn **Run Once** và kiểm tra kết quả.
  3. Nếu có lỗi, kiểm tra **log** trong node tương ứng (ví dụ: GA4 trả về lỗi quyền, BigQuery không tìm thấy dataset).
- **Bật Active**:
  - Sau khi test thành công, chuyển **Active** sang **ON**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Lưu Log Dữ Liệu**:
   - Thêm node **Google Sheets** hoặc **Google Drive** sau BigQuery để lưu **log hoàn tất** của workflow.
   - Ví dụ: Lấy dữ liệu từ node **Merge** và lưu vào Sheet để theo dõi lịch sử.

2. **Gửi Báo Cáo Định Kỳ**:
   - Kết hợp với **Google Sheets** hoặc **Email** để gửi **báo cáo tổng hợp** hàng tuần/tháng.
   - Sử dụng node **Google Sheets** + **Email** để tự động gửi báo cáo cho team.

3. **Kết Hợp Với Slack**:
   - Thay vì Telegram, có thể sử dụng **Slack Webhook** để gửi thông báo.
   - Cách thiết lập:
     1. Tạo **Incoming Webhook** trên Slack.
     2. Thay thế node Telegram bằng node **Slack Webhook**.

4. **Tối Ưu Hiệu Suất**:
   - Nếu dữ liệu lớn, chia nhỏ **date range** thành nhiều workflow nhỏ (ví dụ: 1 tháng/lần).
   - Sử dụng **node Code** để **lọc dữ liệu** trước khi gửi vào BigQuery.

5. **Xây Dựng Dashboard Looker Studio**:
   - Sau khi dữ liệu ở BigQuery, tạo **dashboard** trong Looker Studio để theo dõi KPI marketing.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp marketing và phân tích, đồng thời **tăng cường độ chính xác** của dữ liệu. Bằng cách **tự động hóa hoàn tất GA4 về BigQuery** và **nhận thông báo Telegram**, các sếp có thể:
✔ **Tiết kiệm hàng giờ** mỗi tuần.
✔ **Phân tích sâu** với SQL và BI tools.
✔ **Theo dõi dữ liệu liên tục** mà không cần can thiệp thủ công.

**Hành động ngay!**
1. Import workflow vào n8n của mình.
2. Cấu hình **credentials** và **Backfill Config**.
3. **Bật Active** và bắt đầu tự động hóa dữ liệu!

---
**Nếu có vấn đề**, tham khảo [GitHub Repository](https://github.com/aliasoblomov/N8N-GA4-Backfill-Workflow) hoặc liên hệ với cộng đồng n8n trên [Discord](https://n8n.io/discord). 🚀