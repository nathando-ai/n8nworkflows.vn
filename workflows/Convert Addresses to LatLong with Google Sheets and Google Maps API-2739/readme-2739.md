---
title: "🚀 Chuyển Địa Chỉ sang Tọa Độ Lat/Long Tự Động với Google Sheets & Google Maps API"
description: "Giải pháp tự động 100% chuyển địa chỉ trong Google Sheet thành tọa độ Lat/Long, giúp tiết kiệm thời gian và giảm lỗi nhập liệu."
slug: "chuyen-dia-chinh-sang-toc-do-lat-long-tro-dong"
tags: [n8n, automation, no-code, google-sheets, google-maps, data-automation]
keywords: [n8n workflow, tự động hóa, google sheets, google maps api, địa chỉ, tọa độ, lat long]
---

# 🚀 Chuyển Địa Chỉ sang Tọa Độ Lat/Long Tự Động với Google Sheets & Google Maps API

Bạn đang phải nhập liệu thủ công từng địa chỉ trong Google Sheet rồi tự tay tra cứu tọa độ trên Google Maps? Điều đó không chỉ tốn thời gian, dễ sai sót, mà còn làm giảm năng suất làm việc của đội ngũ. Workflow này sẽ giúp bạn **đổi địa chỉ thành tọa độ Lat/Long ngay lập tức** – hoàn toàn không cần viết code, chỉ cần cấu hình một vài tham số.

:::info[Hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Chuyển đổi hàng trăm địa chỉ chỉ trong vài giây.
- **Độ chính xác cao**: Dữ liệu tọa độ được lấy trực tiếp từ Google Maps API, tránh lỗi nhập liệu.
- **Tự động hóa 100%**: Không cần thao tác thủ công, workflow chạy khi bạn click “Test workflow”.
- **Dễ dàng mở rộng**: Thêm các bước gửi email, Slack, hoặc lưu log vào Google Drive.
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
- **Google Sheets**: Tài liệu chứa cột “Address” (địa chỉ) và cột “Lat”/“Long” (để lưu tọa độ).
- **Google Sheets OAuth2 API**: Credentials đã được cấu hình trong n8n.
- **Google Maps Geocoding API Key**: Tạo tại Google Cloud Console, bật API “Geocoding API”.
- **n8n**: Đã cài đặt và chạy (hoặc sử dụng n8n.cloud).
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON của workflow từ [link gốc](https://n8n.io/workflows/2739) hoặc copy toàn bộ JSON.
2. Trong n8n Editor, chọn **Import** → **Import from JSON** → dán JSON → **Import**.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Mô tả | Tham số cần cấu hình |
|------|-------|---------------------|
| **When clicking ‘Test workflow’** | Manual trigger | Không cần chỉnh |
| **Extract The Places from Google Sheet** | Lấy dữ liệu địa chỉ | *Spreadsheet ID*, *Sheet name*, *Range* (ví dụ: `Sheet1!A2:A100`) |
| **Using Google Map API to Return Lat Long Back** | Gọi API Google Maps | *URL*: `https://maps.googleapis.com/maps/api/geocode/json?address={{$json["Address"]}}&key=YOUR_API_KEY`<br>*Method*: GET |
| **Update Lat-Long in Each Places** | Cập nhật tọa độ vào Google Sheet | *Spreadsheet ID*, *Sheet name*, *Range* (ví dụ: `Sheet1!B2:C100`)<br>*Operation*: Update |

> **Lưu ý**: Thay `YOUR_API_KEY` bằng API key thực tế của bạn. Đảm bảo cột “Address” trong Google Sheet không trống.

### 3. Kích hoạt ⚡️
1. **Test run**: Nhấn nút “Execute Workflow” trong n8n Editor để kiểm tra dữ liệu mẫu.
2. **Bật Active**: Sau khi xác nhận mọi dữ liệu đúng, chuyển workflow sang trạng thái **Active** để tự động chạy khi trigger được kích hoạt.

## ✍️ Mẹo & gợi ý nâng cao
- **Gửi báo cáo định kỳ**: Thêm node “Cron” để chạy workflow hàng ngày, lưu kết quả vào Google Drive hoặc gửi email.
- **Thông báo Slack**: Thêm node “Slack” để gửi tin nhắn khi hoàn thành, giúp đội ngũ nắm bắt nhanh chóng.
- **Lưu log**: Sử dụng node “Google Sheets” hoặc “Google Drive” để ghi lại lịch sử địa chỉ và tọa độ đã xử lý.
- **Xử lý lỗi**: Thêm node “If” để kiểm tra phản hồi của Google Maps API, tránh cập nhật dữ liệu sai khi địa chỉ không hợp lệ.

## 📌 Kết luận
Workflow “Convert Addresses to Lat/Long with Google Sheets and Google Maps API” là công cụ tuyệt vời giúp các sếp **tiết kiệm thời gian, giảm sai sót và tăng tính chính xác** trong quản lý dữ liệu địa lý. Hãy thử ngay, áp dụng vào quy trình làm việc hiện tại và cảm nhận sự khác biệt!

---