---
title: "🚀 Tự động hóa: Đồng bộ danh sách video YouTube vào Google Sheets với n8n"
description: "Hướng dẫn chi tiết cách tự động lấy danh sách video từ kênh YouTube và lưu vào Google Sheets bằng workflow n8n, tiết kiệm thời gian và công sức cho các sếp quản lý nội dung."
slug: "tu-dong-hoa-dong-bo-video-youtube-google-sheets-n8n"
tags: [n8n, automation, no-code, youtube, google-sheets]
keywords: [n8n workflow, tự động hóa, youtube api, google sheets, quản lý nội dung]
---

# 🚀 Tự động hóa: Đồng bộ danh sách video YouTube vào Google Sheets với n8n

[Các sếp quản lý nội dung] thường phải tốn nhiều thời gian để theo dõi và cập nhật danh sách video mới từ các kênh YouTube. Việc thủ công này không chỉ tốn thời gian mà còn dễ gây lỗi. Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình này chỉ trong vài bước đơn giản.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động lấy danh sách video mới từ YouTube mà không cần can thiệp thủ công.
- **Chính xác**: Dữ liệu được cập nhật liên tục và chính xác, giảm thiểu lỗi do nhập liệu.
- **Tích hợp dễ dàng**: Kết nối liền mạch với Google Sheets, giúp quản lý nội dung hiệu quả hơn.
- **Hoạt động liên tục**: Workflow có thể chạy tự động theo lịch trình hoặc khi có sự kiện mới.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Google Sheets**: Một bảng tính Google Sheets với hai sheet: `Sheet3` để lưu danh sách kênh YouTube và `Sheet2` để lưu danh sách video.
- **API Key YouTube**: Một API Key từ Google Cloud Console để truy cập YouTube API.
- **Google API Credentials**: Thông tin xác thực để truy cập Google Sheets.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow này vào n8n của bạn, các sếp có thể làm theo các bước sau:

1. Truy cập vào [n8n.io/workflows/3897](https://n8n.io/workflows/3897) để tải file JSON của workflow.
2. Mở n8n Editor và nhấn vào nút "Import from File" hoặc "Import from URL".
3. Chọn file JSON đã tải về và nhấn "Import".

Hoặc, các sếp có thể copy/paste JSON sau đây vào n8n Editor:

```json
{
  "nodes": [
    {
      "name": "Split Out",
      "type": "splitOut"
    },
    {
      "name": "Manual Trigger (When Clicking 'Test workflow'",
      "type": "manualTrigger"
    },
    {
      "name": "Get Youtube Channel Ids from Google Sheet",
      "type": "googleSheets",
      "credentials": [
        "googleApi"
      ]
    },
    {
      "name": "Get Youtube Video Urls form specific channel",
      "type": "httpRequest",
      "credentials": [
        "httpQueryAuth"
      ]
    },
    {
      "name": "Format fields as required to save in google sheet",
      "type": "set"
    },
    {
      "name": "Insert & Update Youtube Urls in Google Sheet",
      "type": "googleSheets",
      "credentials": [
        "googleApi"
      ],
      "keyParameters": {
        "operation": "appendOrUpdate"
      }
    }
  ]
}
```

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần chú ý cấu hình các node sau:

- **Manual Trigger (When Clicking 'Test workflow')**: Node này kích hoạt workflow khi các sếp nhấn "Test workflow" trong n8n Editor.
- **Get Youtube Channel Ids from Google Sheet**: Node này đọc danh sách kênh YouTube từ `Sheet3` trong Google Sheets. Các sếp cần cấu hình:
  - Chọn credentials Google API.
  - Điền thông tin bảng tính và sheet: `Sheet3`.
- **Get Youtube Video Urls form specific channel**: Node này gọi API YouTube để lấy danh sách video từ các kênh đã lấy được. Các sếp cần cấu hình:
  - Chọn credentials HTTP Query Auth.
  - Điền URL API YouTube và tham số truy vấn.
- **Format fields as required to save in google sheet**: Node này định dạng dữ liệu để lưu vào Google Sheets. Các sếp cần cấu hình các trường dữ liệu cần thiết.
- **Insert & Update Youtube Urls in Google Sheet**: Node này lưu danh sách video vào `Sheet2` trong Google Sheets. Các sếp cần cấu hình:
  - Chọn credentials Google API.
  - Điền thông tin bảng tính và sheet: `Sheet2`.
  - Chọn operation là `appendOrUpdate`.

#### 3. Kích hoạt ⚡️
Sau khi cấu hình xong, các sếp cần:

1. **Test run dữ liệu mẫu**: Nhấn "Test workflow" để kiểm tra workflow hoạt động đúng như mong đợi.
2. **Bật Active workflow**: Chuyển workflow sang trạng thái Active để nó chạy tự động theo lịch trình hoặc khi có sự kiện mới.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Các sếp có thể thêm node gửi thông báo qua Slack hoặc Telegram khi có video mới được cập nhật.
- **Lưu log hoạt động**: Thêm node lưu log hoạt động của workflow để theo dõi và kiểm tra lỗi.
- **Gửi báo cáo định kỳ**: Tạo một workflow phụ để gửi báo cáo định kỳ về danh sách video mới qua email.

### 📌 Kết luận
Workflow này giúp các sếp quản lý nội dung tự động hóa toàn bộ quá trình lấy danh sách video từ YouTube và lưu vào Google Sheets. Với việc tự động hóa, các sếp có thể tiết kiệm thời gian và công sức, đồng thời đảm bảo dữ liệu luôn được cập nhật và chính xác. Hãy áp dụng ngay để nâng cao hiệu quả quản lý nội dung!