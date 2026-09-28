---
title: "📊 Tự động hóa Dashboard Analytics Email Campaign với Google Sheets"
description: "Hướng dẫn chi tiết cách tự động hóa việc thu thập và phân tích dữ liệu email campaign thông qua Smartlead API và Google Sheets, giúp các sếp tiết kiệm thời gian và tối ưu hóa chiến dịch marketing."
slug: "tu-dong-hoa-dashboard-analytics-email-campaign-voi-google-sheets"
tags: [n8n, automation, no-code, google-sheets, smartlead, marketing-automation]
keywords: [n8n workflow, tự động hóa email campaign, google sheets integration, smartlead analytics, marketing automation]
---

# 📊 Tự động hóa Dashboard Analytics Email Campaign với Google Sheets

[Các sếp đang gặp khó khăn khi phải theo dõi thủ công các chỉ số quan trọng của email campaign như open rate, click rate, domain health...? Bạn muốn có một dashboard tóm tắt toàn diện nhưng lại không muốn tốn thời gian vào việc thu thập và xử lý dữ liệu? Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình này chỉ trong vài bước đơn giản!]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động thu thập dữ liệu hàng ngày mà không cần can thiệp thủ công.
- **Chính xác và toàn diện**: Lấy dữ liệu từ nhiều nguồn khác nhau (email campaign, domain health) và lưu trữ trên Google Sheets.
- **Tối ưu hóa chiến dịch**: Có được dashboard tóm tắt toàn diện về hiệu suất email campaign và sức khỏe domain.
- **Hoạt động liên tục**: Workflow được kích hoạt tự động theo lịch trình hàng ngày.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Smartlead với API key (để truy cập dữ liệu email campaign).
- Tài khoản Google với quyền truy cập vào Google Sheets (để lưu trữ dữ liệu).
- Credentials cho Google Sheets trong n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hãy sao chép JSON dưới đây và dán vào n8n Editor:

```json
{
  "nodes": [
    {
      "name": "HTTP Request5",
      "type": "httpRequest"
    },
    {
      "name": "Append or update row in sheet5",
      "type": "googleSheets",
      "keyParameters": {
        "operation": "appendOrUpdate"
      }
    },
    {
      "name": "Split Out5",
      "type": "splitOut"
    },
    {
      "name": "HTTP Request6",
      "type": "httpRequest"
    },
    {
      "name": "Append or update row in sheet6",
      "type": "googleSheets",
      "keyParameters": {
        "operation": "appendOrUpdate"
      }
    },
    {
      "name": "Split Out6",
      "type": "splitOut"
    },
    {
      "name": "Schedule Trigger1",
      "type": "scheduleTrigger"
    },
    {
      "name": "HTTP Request",
      "type": "httpRequest"
    },
    {
      "name": "Append or update row in sheet",
      "type": "googleSheets",
      "keyParameters": {
        "operation": "appendOrUpdate"
      }
    },
    {
      "name": "Split Out",
      "type": "splitOut"
    },
    {
      "name": "Schedule Trigger",
      "type": "scheduleTrigger"
    },
    {
      "name": "HTTP Request1",
      "type": "httpRequest"
    },
    {
      "name": "Append or update row in sheet1",
      "type": "googleSheets",
      "keyParameters": {
        "operation": "appendOrUpdate"
      }
    },
    {
      "name": "Split Out1",
      "type": "splitOut"
    }
  ]
}
```

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node Schedule Trigger**: Cấu hình lịch trình chạy workflow hàng ngày (ví dụ: 00:00 mỗi ngày).
- **Node HTTP Request**: Cập nhật URL và headers cho Smartlead API (nếu cần).
- **Node Append or update row in sheet**: Chỉnh sửa Spreadsheet ID và Sheet Name trong Google Sheets credentials.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
- Bật Active workflow để bắt đầu thu thập dữ liệu hàng ngày.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi dữ liệu được cập nhật.
- Lưu log các lần chạy workflow để theo dõi lịch sử.
- Gửi báo cáo định kỳ (tuần/tháng) dựa trên dữ liệu đã thu thập.

### 📌 Kết luận
Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình thu thập và phân tích dữ liệu email campaign chỉ trong vài bước đơn giản. Hãy áp dụng ngay để tiết kiệm thời gian và tối ưu hóa chiến dịch marketing của mình!