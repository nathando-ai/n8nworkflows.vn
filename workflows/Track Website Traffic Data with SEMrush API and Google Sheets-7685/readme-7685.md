---
title: "🚀 Theo dõi dữ liệu lưu lượng truy cập website với SEMrush API và Google Sheets"
description: "Tự động hóa hoàn toàn quá trình theo dõi lưu lượng truy cập website bằng cách lấy dữ liệu từ SEMrush API và lưu vào Google Sheets - không cần viết code."
slug: "theo-doi-luu-luong-truy-cap-website-voi-semrush-va-google-sheets"
tags: [n8n, automation, no-code, seo, semrush, google sheets]
keywords: [n8n workflow, tự động hóa, seo, semrush, google sheets]
---

# 🚀 Theo dõi dữ liệu lưu lượng truy cập website với SEMrush API và Google Sheets

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa toàn bộ quá trình theo dõi lưu lượng truy cập
- Chính xác: Lấy dữ liệu trực tiếp từ SEMrush API
- Cá nhân hóa: Lưu dữ liệu vào Google Sheets theo định dạng tùy chỉnh
- Hoạt động liên tục: Theo dõi 24/7 mà không cần can thiệp thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản SEMrush và API Key (đăng ký tại [SEMrush](https://www.semrush.com/))
- Tài khoản Google và Google Sheets API đã được kích hoạt (hướng dẫn [tại đây](https://developers.google.com/sheets/api/guides/authorizing))
- Tài khoản n8n đã được cài đặt và cấu hình (hướng dẫn [tại đây](https://docs.n8n.io/hosting/installation/))
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào nút "Import" ở góc trên bên phải
3. Chọn "From File" và tải lên file JSON của workflow
4. Hoặc copy/paste nội dung JSON sau vào n8n Editor:

```json
{
  "nodes": [
    {
      "parameters": {},
      "name": "On form submission",
      "type": "n8n-nodes-base.formTrigger",
      "typeVersion": 1,
      "position": [
        250,
        300
      ]
    },
    {
      "parameters": {
        "code": "return items[0].json.trafficSummary;"
      },
      "name": "Reformat",
      "type": "n8n-nodes-base.code",
      "typeVersion": 1,
      "position": [
        650,
        300
      ]
    },
    {
      "parameters": {
        "options": {
          "headers": {
            "X-RapidAPI-Key": "={{$credentials.rapidApi.apiKey}}",
            "X-RapidAPI-Host": "seo-api8.p.rapidapi.com"
          },
          "body": {
            "url": "={{$node[\"On form submission\"].json[\"website\"]}}"
          },
          "method": "POST",
          "url": "https://seo-api8.p.rapidapi.com/seo/traffic"
        },
        "sendQuery": true,
        "sendHeaders": true,
        "sendBody": true,
        "returnFullResponse": true
      },
      "name": "website traffic checker",
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 1,
      "position": [
        450,
        300
      ]
    },
    {
      "parameters": {
        "operation": "append",
        "resource": "data",
        "options": {},
        "additionalFields": {
          "spreadsheetId": "={{$credentials.googleApi.spreadsheetId}}",
          "data": "={{$node[\"Reformat\"].json}}",
          "range": "={{$credentials.googleApi.range}}"
        }
      },
      "name": "Append Data In Google Sheets",
      "type": "n8n-nodes-base.googleSheets",
      "typeVersion": 1,
      "position": [
        850,
        300
      ]
    }
  ],
  "connections": {
    "On form submission": {
      "main": [
        [
          {
            "node": "website traffic checker",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "website traffic checker": {
      "main": [
        [
          {
            "node": "Reformat",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Reformat": {
      "main": [
        [
          {
            "node": "Append Data In Google Sheets",
            "type": "main",
            "index": 0
          }
        ]
      ]
    }
  },
  "settings": {
    "saveManualExecutions": true,
    "saveExecutionProgress": true,
    "saveDataErrorExecution": "all",
    "saveDataSuccessExecution": "all",
    "executionTimeout": 3600,
    "timezone": ""
  },
  "name": "Track Website Traffic Data with SEMrush API and Google Sheets",
  "version": "1.0",
  "createdAt": "2023-07-20T10:00:00.000Z",
  "updatedAt": "2023-07-20T10:00:00.000Z"
}
```

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "On form submission"**:
   - Cấu hình form để nhận input là URL của website cần theo dõi
   - Đảm bảo form có trường "website" để nhập URL

2. **Node "website traffic checker"**:
   - Thêm credentials cho SEMrush API (X-RapidAPI-Key)
   - Kiểm tra URL API endpoint có chính xác không (https://seo-api8.p.rapidapi.com/seo/traffic)

3. **Node "Append Data In Google Sheets"**:
   - Thêm credentials cho Google Sheets API
   - Điền Spreadsheet ID (ID của Google Sheet cần lưu dữ liệu)
   - Điền Range (vị trí trong sheet để lưu dữ liệu, ví dụ: "Sheet1!A1")

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu:
   - Nhập một URL website vào form
   - Kiểm tra kết quả trả về từ SEMrush API
   - Xác nhận dữ liệu đã được lưu đúng vào Google Sheets

2. Bật Active workflow:
   - Nhấn vào nút "Active" ở góc trên bên phải của workflow
   - Workflow sẽ sẵn sàng nhận dữ liệu từ form và xử lý tự động

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Telegram**:
   - Thêm node gửi thông báo khi có dữ liệu mới được lưu vào Google Sheets
   - Tự động cảnh báo khi lưu lượng truy cập giảm đột ngột

2. **Lưu log lịch sử**:
   - Thêm node lưu log các lần chạy workflow
   - Giúp theo dõi lịch sử thay đổi dữ liệu

3. **Gửi báo cáo định kỳ**:
   - Thêm node gửi email báo cáo tổng hợp dữ liệu hàng tuần/tháng
   - Tự động hóa hoàn toàn quá trình báo cáo

4. **Xử lý dữ liệu nâng cao**:
   - Thêm node xử lý dữ liệu trước khi lưu vào Google Sheets
   - Tính toán các chỉ số KPI từ dữ liệu thô

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quá trình theo dõi lưu lượng truy cập website, tiết kiệm thời gian và giảm thiểu lỗi thủ công. Bằng cách kết hợp SEMrush API và Google Sheets, các sếp có thể dễ dàng theo dõi và phân tích dữ liệu lưu lượng truy cập website một cách hiệu quả. Hãy áp dụng ngay để nâng cao hiệu suất SEO và quản lý website của bạn!