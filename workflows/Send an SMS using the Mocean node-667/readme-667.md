---
title: "📱 Tự Động Gửi SMS Thông Báo Mọi Lúc - Không Cần Code Với Mocean & n8n"
description: "Hướng dẫn tự động hóa gửi tin nhắn SMS thông báo cho khách hàng, nhân viên hoặc hệ thống theo lịch trình hoặc sự kiện, tiết kiệm thời gian và tăng cường tương tác 24/7."
slug: "tu-dong-hoa-gui-sms-mocean-n8n"
tags: [n8n, automation, mocean, sms, no-code]
keywords: [n8n workflow sms, tự động hóa gửi tin nhắn, Mocean API n8n, tự động hóa doanh nghiệp, gửi SMS tự động]
---

# 🚀 **Tự Động Gửi SMS Thông Báo Mọi Lúc Với Mocean & n8n**

### **Tại sao các sếp cần tự động hóa gửi SMS?**
Hiện nay, việc gửi thông báo SMS thủ công không chỉ tốn thời gian mà còn dễ gây lỗi và không đồng bộ. Các sếp thường phải:
- **Gửi thông báo khẩn cấp** (đơn hàng, xác nhận đặt vé, cảnh báo hệ thống) cho khách hàng hoặc nhân viên.
- **Tự động nhắc nhở** (hẹn hò, deadline, sự kiện) để tránh quên.
- **Tăng cường tương tác** với khách hàng thông qua tin nhắn tự động hóa.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Gửi SMS một cách tự động** khi kích hoạt (hoặc kết hợp với các trigger khác như Webhook, cron job).
✅ **Không cần viết code** – chỉ cần cấu hình đơn giản trên n8n.
✅ **Hoạt động 24/7** – không phụ thuộc vào thời gian làm việc của nhân viên.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không phải gửi SMS thủ công mỗi khi cần.
- **Tăng độ chính xác**: Tránh sai sót khi nhập số điện thoại hoặc nội dung.
- **Hoạt động liên tục**: Gửi thông báo ngay cả khi hệ thống offline (nếu kết hợp với cron job).
- **Tương tác tự động**: Gửi thông báo khẩn cấp, nhắc nhở hoặc cập nhật tức thì.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần:
- **Tài khoản Mocean** (đăng ký tại [Mocean](https://mocean.io/)).
- **API Key của Mocean** (tạo trong tài khoản Mocean).
- **Số điện thoại nhận SMS** (đã đăng ký trong Mocean).
- **n8n Self-hosted** (hoặc n8n Cloud, nhưng không ổn định 24/7).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Workflow này rất đơn giản với **2 node**:
- **Manual Trigger**: Kích hoạt workflow khi nhấn "Execute".
- **Mocean Node**: Gửi SMS với nội dung và số điện thoại đã cấu hình.

**Cách import:**
1. **Tải file JSON** từ [n8n Workflows](https://n8n.io/workflows/667) hoặc copy toàn bộ JSON dưới đây.
2. **Mở n8n Editor** → Nhấn **"Import"** → Dán JSON hoặc tải file.
3. **Kích hoạt workflow** bằng cách bật switch **"Active"**.

```json
{
  "nodes": [
    {
      "parameters": {},
      "name": "On clicking 'execute'",
      "type": "n8n-nodes-base.manualTrigger",
      "typeVersion": 1,
      "nodeVersion": "1.0.0",
      "previousNode": null,
      "nextNodes": [
        "Mocean"
      ],
      "credentials": {}
    },
    {
      "parameters": {
        "apiKey": {
          "name": "moceanApi",
          "value": ""
        },
        "phoneNumber": "0123456789", // Thay bằng số điện thoại thực tế
        "message": "Xin chào! Đây là tin nhắn tự động từ n8n. Cảm ơn!" // Thay nội dung
      },
      "name": "Mocean",
      "type": "n8n-nodes-base.mocean",
      "typeVersion": 1,
      "nodeVersion": "1.0.0",
      "previousNode": "On clicking 'execute'",
      "nextNodes": [],
      "credentials": {
        "moceanApi": "moceanApi"
      }
    }
  ],
  "connections": {
    "On clicking 'execute'": [
      "Mocean"
    ]
  }
}
```

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
- **Node Manual Trigger**:
  - Không cần cấu hình gì thêm, chỉ cần nhấn **"Execute"** để test.
- **Node Mocean**:
  - **Thay đổi `phoneNumber`** bằng số điện thoại thực tế (đã đăng ký trong Mocean).
  - **Thay đổi `message`** bằng nội dung SMS muốn gửi.
  - **Điền `apiKey`** vào **Credentials** của n8n:
    1. Trong n8n Editor → **"Credentials"** → **"Add"** → **"Mocean API"**.
    2. Nhập tên `moceanApi` và dán **API Key** từ Mocean vào trường `apiKey`.
    3. Lưu và chọn `moceanApi` trong node Mocean.

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhấn **"Execute"** trên node **Manual Trigger**.
   - Kiểm tra SMS đã được gửi đến số điện thoại đã cấu hình.
2. **Bật Active**:
   - Đảm bảo workflow ở trạng thái **"Active"** để hoạt động tự động.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Cron Job** để gửi SMS theo lịch trình:
   - Thay node **Manual Trigger** bằng **Cron Trigger** (n8n-nodes-base.cron).
   - Cấu hình thời gian gửi (ví dụ: gửi SMS hàng ngày lúc 9h).
2. **Lưu log SMS đã gửi**:
   - Thêm node **Google Sheets** hoặc **Slack** sau node Mocean để ghi lại lịch sử.
3. **Tự động hóa từ Webhook**:
   - Thay node **Manual Trigger** bằng **HTTP Request** (n8n-nodes-base.httpRequest) để nhận yêu cầu từ API hoặc bot.
4. **Gửi SMS nhiều người**:
   - Sử dụng **Loop** (n8n-nodes-base.loop) để gửi SMS cho danh sách số điện thoại từ file CSV hoặc database.

---
### 📌 **Kết luận**
Workflow này giúp các sếp **gửi SMS tự động một cách dễ dàng**, tiết kiệm thời gian và tăng cường tương tác với khách hàng/nhân viên. **Bắt đầu ngay bằng cách import và cấu hình theo hướng dẫn trên!**

👉 **Bạn có thể mở rộng workflow này thêm nhiều tính năng khác như:**
- Gửi SMS xác nhận đơn hàng từ Shopify.
- Nhắc nhở khách hàng về sự kiện sắp diễn ra.
- Gửi thông báo khẩn cấp từ hệ thống IoT.

**Hãy thử và chia sẻ kết quả của bạn!** 🚀