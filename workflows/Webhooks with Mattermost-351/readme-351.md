---
title: "🚀 Tự động hóa thông báo Mattermost với Webhook - Giải pháp không cần code"
description: "Hướng dẫn chi tiết cách tự động gửi thông báo Mattermost qua webhook trong n8n, tiết kiệm thời gian và nâng cao hiệu suất làm việc"
slug: "tu-dong-hoa-thong-bao-mattermost-voi-webhook"
tags: [n8n, automation, no-code, mattermost, webhook]
keywords: [n8n workflow, tự động hóa, mattermost, webhook, no-code]
---

# 🚀 Tự động hóa thông báo Mattermost với Webhook - Giải pháp không cần code

[Các sếp đang gặp khó khăn khi phải gửi thông báo Mattermost thủ công qua các hệ thống khác nhau. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình thông qua webhook, giúp tiết kiệm thời gian và nâng cao hiệu suất làm việc.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động gửi thông báo Mattermost từ nhiều nguồn dữ liệu khác nhau
- Tiết kiệm thời gian và giảm thiểu lỗi thủ công
- Tích hợp dễ dàng với các hệ thống khác thông qua webhook
- Hoạt động liên tục 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Mattermost với quyền truy cập API
- URL webhook của Mattermost
- API key hoặc thông tin đăng nhập Mattermost
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow này vào n8n của bạn, các sếp có thể làm theo các bước sau:

1. Truy cập vào n8n Editor của bạn
2. Nhấn vào nút "Import" ở góc trên bên phải
3. Chọn "From File" và tải lên file JSON của workflow
4. Hoặc copy toàn bộ JSON bên dưới và paste vào phần import

```json
{
  "nodes": [
    {
      "parameters": {
        "path": "webhook",
        "httpMethod": "POST"
      },
      "name": "Webhook",
      "type": "n8n-nodes-base.webhook",
      "typeVersion": 1,
      "position": [
        250,
        300
      ]
    },
    {
      "parameters": {},
      "name": "HTTP Request",
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 1,
      "position": [
        550,
        300
      ]
    },
    {
      "parameters": {
        "operation": "sendMessage"
      },
      "name": "Mattermost",
      "type": "n8n-nodes-base.mattermost",
      "typeVersion": 1,
      "position": [
        850,
        300
      ]
    }
  ],
  "connections": [
    {
      "node": "Webhook",
      "type": "main",
      "index": 0
    },
    {
      "node": "HTTP Request",
      "type": "main",
      "index": 0
    },
    {
      "node": "Mattermost",
      "type": "main",
      "index": 0
    }
  ],
  "settings": {
    "saveDataErrorExecution": "all",
    "saveDataSuccessExecution": "all",
    "saveManualExecutions": true,
    "executionTimeout": 3600,
    "timezone": ""
  },
  "name": "Webhooks with Mattermost",
  "version": "1.0",
  "createdAt": "2023-05-15T08:00:00.000Z",
  "updatedAt": "2023-05-15T08:00:00.000Z"
}
```

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần chú ý cấu hình các node sau:

1. **Node Webhook**:
   - Đảm bảo đường dẫn "path" là duy nhất và không trùng lặp với các webhook khác
   - Phương thức HTTP nên được đặt là "POST" để đảm bảo an toàn dữ liệu

2. **Node HTTP Request**:
   - Cấu hình URL đích mà bạn muốn gửi dữ liệu đến
   - Đặt phương thức HTTP phù hợp (GET, POST, PUT, DELETE...)
   - Thêm các headers và body nếu cần thiết

3. **Node Mattermost**:
   - Tạo credentials cho Mattermost trong n8n
   - Nhập URL của Mattermost server
   - Điền thông tin xác thực (API key hoặc thông tin đăng nhập)
   - Cấu hình các tham số như channel, username, icon_url nếu cần

#### 3. Kích hoạt ⚡️
Sau khi cấu hình xong, các sếp nên thực hiện các bước sau:

1. Test run với dữ liệu mẫu để đảm bảo workflow hoạt động đúng
2. Kiểm tra lại các thông báo Mattermost để xác nhận dữ liệu được gửi đúng
3. Bật chế độ Active cho workflow để nó hoạt động liên tục

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với các webhook từ các dịch vụ khác như GitHub, Slack để nhận thông báo tự động
- Thêm node "Delay" để tạo khoảng thời gian giữa các thông báo
- Sử dụng node "Code" để xử lý dữ liệu trước khi gửi đến Mattermost
- Tạo nhiều phiên bản workflow cho các kênh Mattermost khác nhau

### 📌 Kết luận
Workflow "Webhooks with Mattermost" giúp các sếp tự động hóa việc gửi thông báo Mattermost một cách dễ dàng và hiệu quả. Với việc sử dụng webhook, các sếp có thể tích hợp với nhiều hệ thống khác nhau và nâng cao hiệu suất làm việc. Hãy áp dụng ngay để tiết kiệm thời gian và giảm thiểu công việc thủ công!