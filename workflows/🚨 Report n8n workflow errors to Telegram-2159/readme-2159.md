---
title: "🚨 Tự động báo lỗi n8n qua Telegram - Workflow tự động hóa hoàn hảo"
description: "Hướng dẫn chi tiết cách tự động nhận thông báo lỗi từ n8n qua Telegram, giúp quản lý workflow hiệu quả hơn. Giải pháp không cần code, hoạt động 24/7."
slug: "tu-dong-bao-loi-n8n-qua-telegram"
tags: [n8n, automation, no-code, telegram, error-handling]
keywords: [n8n workflow, tự động hóa lỗi, telegram notification, error handling, no-code automation]
---

# 🚨 Tự động báo lỗi n8n qua Telegram - Workflow tự động hóa hoàn hảo

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi quản lý nhiều workflow n8n, khó theo dõi lỗi thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- 🔥 **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công khi workflow gặp lỗi
- ⏰ **Thông báo tức thì**: Nhận cảnh báo lỗi ngay khi xảy ra qua Telegram
- 📊 **Quản lý tập trung**: Theo dõi tất cả lỗi từ nhiều workflow trong một nơi
- 🔄 **Hoạt động liên tục**: Không bị gián đoạn ngay cả khi bạn không trực tiếp giám sát
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram cá nhân hoặc nhóm
- API Token từ Bot Telegram (hướng dẫn tạo tại [@BotFather](https://t.me/BotFather))
- ID của chat Telegram (có thể lấy từ [@RawDataBot](https://t.me/RawDataBot))
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/2159](https://n8n.io/workflows/2159)
2. Click vào nút "Import" ở góc trên bên phải
3. Chọn "Import from URL" và dán link trên vào ô nhập liệu
4. Click "OK" để hoàn tất import

Hoặc bạn có thể copy/paste JSON sau vào n8n Editor:

```json
{
  "nodes": [
    {
      "parameters": {},
      "name": "On Error",
      "type": "n8n-nodes-base.errorTrigger",
      "typeVersion": 1,
      "position": [
        250,
        300
      ]
    },
    {
      "parameters": {
        "options": {
          "dot": true
        },
        "values": {
          "message": "={{$node[\"On Error\"].error.message}}"
        }
      },
      "name": "Set message",
      "type": "n8n-nodes-base.set",
      "typeVersion": 1,
      "position": [
        450,
        300
      ]
    },
    {
      "parameters": {
        "chatId": "",
        "text": "={{$node[\"Set message\"].json.message}}"
      },
      "name": "Telegram",
      "type": "n8n-nodes-base.telegram",
      "typeVersion": 1,
      "position": [
        650,
        300
      ]
    }
  ],
  "connections": {
    "On Error": {
      "main": [
        [
          {
            "node": "Set message",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Set message": {
      "main": [
        [
          {
            "node": "Telegram",
            "type": "main",
            "index": 0
          }
        ]
      ]
    }
  }
}
```

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node Telegram**:
   - Thêm Telegram credentials:
     - Click vào nút "Add Credential" trong node Telegram
     - Chọn "Telegram API"
     - Nhập API Token của bạn (đã lấy từ @BotFather)
     - Click "Save"
   - 👆🏽 **Set chat id here**: Nhập ID của chat Telegram bạn muốn nhận thông báo (có thể lấy từ @RawDataBot)

#### 3. Kích hoạt ⚡️
1. Test run workflow bằng cách click vào nút "Execute Workflow" (hình mũi tên xanh)
2. Bật Active workflow bằng cách click vào nút "Activate" (hình công tắc)

### ✍️ Mẹo & gợi ý nâng cao
- 📱 **Kết hợp với Slack**: Thêm node Slack để nhận thông báo lỗi đồng thời qua cả Telegram và Slack
- 📊 **Lưu log lỗi**: Thêm node Google Sheets để lưu trữ lịch sử lỗi cho phân tích sau này
- 📅 **Gửi báo cáo định kỳ**: Sử dụng node Schedule Trigger để gửi báo cáo tổng hợp lỗi hàng ngày
- 🔗 **Kết nối với các hệ thống khác**: Kết nối với các dịch vụ khác như Email, Discord để mở rộng hệ thống thông báo

### 📌 Kết luận
Workflow "Report n8n workflow errors to Telegram" là giải pháp hoàn hảo cho các sếp muốn tự động hóa việc theo dõi và quản lý lỗi trong các workflow n8n. Với việc nhận thông báo tức thì qua Telegram, các sếp có thể nhanh chóng phản ứng và khắc phục lỗi, đảm bảo hệ thống hoạt động ổn định 24/7. Hãy áp dụng ngay để nâng cao hiệu suất làm việc của bạn!