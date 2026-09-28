---
title: "📧 [Hướng dẫn tự động hóa] Kiểm tra email hợp lệ với APILayer API - 100% không cần code"
description: "Hướng dẫn chi tiết cách tự động hóa việc kiểm tra email hợp lệ bằng APILayer API trong n8n. Tiết kiệm thời gian và nâng cao chất lượng danh sách email cho chiến dịch marketing."
slug: "kiem-tra-email-hop-le-voi-apilayer-api"
tags: [n8n, automation, no-code, email-validation, apilayer]
keywords: [n8n workflow, tự động hóa email, kiểm tra email hợp lệ, apilayer api]
---

# 📧 [Hướng dẫn tự động hóa] Kiểm tra email hợp lệ với APILayer API - 100% không cần code

[Các sếp marketing và sales thường gặp vấn đề khi phải kiểm tra hàng loạt email để gửi thư quảng cáo. Việc làm thủ công tốn thời gian và dễ gây lỗi. Workflow này giúp tự động hóa quá trình này với APILayer API, đảm bảo danh sách email luôn sạch và chính xác.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian kiểm tra hàng loạt email
- Đảm bảo danh sách email luôn sạch và chính xác
- Tự động hóa hoàn toàn quá trình kiểm tra email
- Dễ dàng tích hợp với các hệ thống khác trong n8n
- Giảm thiểu rủi ro gửi email vào hộp thư rác
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản APILayer API (đăng ký tại [https://apilayer.com/](https://apilayer.com/))
- Access Key từ APILayer API
- Danh sách email cần kiểm tra (có thể nhập thủ công hoặc từ file CSV)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor
2. Click vào "Import from URL" trong menu Workflows
3. Dán link sau vào ô nhập liệu: `https://n8n.io/workflows/6230`
4. Click "OK" để hoàn tất import

Hoặc có thể copy/paste JSON sau vào n8n Editor:

```json
{
  "nodes": [
    {
      "parameters": {},
      "name": "When clicking ‘Execute workflow’",
      "type": "n8n-nodes-base.manualTrigger",
      "typeVersion": 1,
      "position": [
        250,
        300
      ]
    },
    {
      "parameters": {
        "fields": {
          "email": "={{$node['When clicking ‘Execute workflow’'].json['email']}}",
          "accessKey": "YOUR_APILAYER_ACCESS_KEY"
        }
      },
      "name": "Set Email & Access Key",
      "type": "n8n-nodes-base.set",
      "typeVersion": 1,
      "position": [
        450,
        300
      ]
    },
    {
      "parameters": {
        "url": "https://apilayer.net/api/check?access_key={{$node['Set Email & Access Key'].json['accessKey']}}&email={{$node['Set Email & Access Key'].json['email']}}",
        "method": "GET",
        "sendQuery": false,
        "sendBody": false,
        "sendHeaders": false,
        "sendAuth": false,
        "options": {}
      },
      "name": "Make Request to APILayer",
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 1,
      "position": [
        650,
        300
      ]
    }
  ],
  "connections": {
    "When clicking ‘Execute workflow’": {
      "main": [
        [
          {
            "node": "Set Email & Access Key",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Set Email & Access Key": {
      "main": [
        [
          {
            "node": "Make Request to APILayer",
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
1. **Node "Set Email & Access Key"**:
   - Thay thế `YOUR_APILAYER_ACCESS_KEY` bằng access key thực tế từ APILayer API
   - Điền email cần kiểm tra vào trường `email` (có thể sử dụng biểu thức n8n để lấy từ dữ liệu đầu vào)

2. **Node "Make Request to APILayer"**:
   - URL đã được cấu hình sẵn với các tham số từ node trước
   - Đảm bảo phương thức HTTP là GET
   - Không cần cấu hình headers, query parameters, body hoặc authentication riêng

#### 3. Kích hoạt ⚡️
1. Click vào nút "Execute workflow" để chạy thử với dữ liệu mẫu
2. Kiểm tra kết quả trả về từ APILayer API
3. Sau khi xác nhận hoạt động đúng, click vào nút "Active" để kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
1. **Xử lý hàng loạt email**: Có thể kết hợp với node "Read CSV" để đọc danh sách email từ file CSV và xử lý từng email trong vòng lặp
2. **Lưu kết quả**: Kết nối với node "Google Sheets" hoặc "MySQL" để lưu kết quả kiểm tra email
3. **Thông báo kết quả**: Kết nối với node "Slack" hoặc "Email" để nhận thông báo khi kiểm tra hoàn tất
4. **Xử lý lỗi**: Thêm node "Error Trigger" để xử lý các trường hợp lỗi trong quá trình kiểm tra

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quá trình kiểm tra email hợp lệ, tiết kiệm thời gian và đảm bảo chất lượng danh sách email cho các chiến dịch marketing. Hãy áp dụng ngay để nâng cao hiệu quả công việc!