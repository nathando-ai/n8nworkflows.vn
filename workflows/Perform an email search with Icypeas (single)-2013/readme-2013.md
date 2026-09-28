---
title: "🔍 Tự Động Hóa Tìm Kiếm Email Bằng Icypeas (Không Cần Code) - Tiết Kiệm 100% Thời Gian Trau Cứu"
description: "Workflow tự động hóa tìm kiếm email cá nhân hoặc doanh nghiệp trên Icypeas chỉ với một cú nhấp chuột. Giúp các sếp tiết kiệm thời gian tra cứu thủ công, tăng hiệu quả trong sales & marketing."
slug: "tu-dong-hoa-tim-kiem-email-bang-icypeas"
tags: [n8n, automation, sales, marketing, icypeas, no-code]
keywords: [tìm kiếm email tự động, icypeas api, tự động hóa sales, tra cứu email doanh nghiệp, n8n workflow]
---

# 🔍 **Tự Động Hóa Tìm Kiếm Email Bằng Icypeas - Giải Pháp Tiết Kiệm Thời Gian Cho Sales & Marketing**

### **Nỗi Đau Của Các Sếp Trong Tra Cứu Email**
Trong công việc sales và marketing, việc tra cứu email của khách hàng hoặc đối tác là một trong những công việc tốn thời gian nhất. Thay vì mất nhiều giờ tra cứu thủ công trên Google, LinkedIn hay các công cụ tìm kiếm email, **các sếp có thể tự động hóa quy trình này chỉ với một workflow đơn giản trên n8n!**

Với **Icypeas** - công cụ tìm kiếm email chuyên nghiệp, kết hợp với **n8n**, các sếp có thể:
✅ **Tìm kiếm email chỉ trong vài giây** thay vì mất nhiều giờ tra cứu thủ công.
✅ **Lấy thông tin chính xác** về email cá nhân hoặc doanh nghiệp.
✅ **Tích hợp với CRM, Slack, Telegram** để tự động hóa tiếp theo.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định 24/7**, các sếp nên cài đặt n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản miễn phí.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Thay vì mất 30 phút tra cứu 1 email, chỉ cần **1 giây** với tự động hóa.
- **Chính xác cao**: Icypeas cung cấp kết quả tìm kiếm **độ chính xác lên đến 95%**.
- **Tích hợp dễ dàng**: Kết nối với **Slack, CRM, Email Marketing** để tự động hóa tiếp theo.
- **Hoạt động liên tục**: Workflow chạy **24/7** mà không cần can thiệp.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Icypeas** (đăng ký tại [icypeas.com](https://icypeas.com))
✔ **API Key, API Secret & User ID** (tìm tại [https://app.icypeas.com/bo/profile](https://app.icypeas.com/bo/profile))
✔ **n8n Self-hosted** (không dùng phiên bản miễn phí để tránh giới hạn)
✔ **VPS** (nếu chưa có, tham khảo gợi ý trên)

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể **import workflow từ JSON** hoặc **copy/paste mã JSON** vào n8n Editor.

**Bước 1:** Tải workflow từ [n8n.io/workflows/2013](https://n8n.io/workflows/2013) hoặc sử dụng mã JSON dưới đây:

```json
{
  "nodes": [
    {
      "parameters": {},
      "name": "When clicking \"Execute Workflow\"",
      "type": "manualTrigger",
      "typeVersion": 1,
      "position": [250, 300]
    },
    {
      "parameters": {
        "code": "const API_KEY = \"**PUT_API_KEY_HERE**\";\nconst API_SECRET = \"**PUT_API_SECRET_HERE**\";\nconst USER_ID = \"**PUT_USER_ID_HERE**\";\n\n// Do not modify the following code\nconst crypto = require('crypto');\nconst signature = crypto.createHmac('sha256', API_SECRET).update(new Date().toISOString()).digest('hex');\n\nreturn {\n  api: {\n    key: API_KEY,\n    signature: signature\n  }\n};"
      },
      "name": "Authenticates to your Icypeas account",
      "type": "code",
      "typeVersion": 1,
      "position": [250, 500],
      "credentials": {}
    },
    {
      "parameters": {
        "method": "POST",
        "url": "https://api.icypeas.com/v1/singlesearch/email",
        "credentials": {
          "httpHeaderAuth": {
            "name": "Authorization"
          }
        },
        "body": {
          "lastname": "{{$inputData.lastname}}",
          "firstname": "{{$inputData.firstname}}",
          "domainOrCompany": "{{$inputData.domainOrCompany}}"
        }
      },
      "name": "Run email search (single)",
      "type": "httpRequest",
      "typeVersion": 1,
      "position": [250, 700],
      "credentials": {
        "httpHeaderAuth": {
          "name": "Authorization"
        }
      }
    }
  ],
  "connections": [
    {
      "from": 0,
      "to": 1
    },
    {
      "from": 1,
      "to": 2
    }
  ]
}
```

**Bước 2:** Nhấn **"Import"** trong n8n Editor.

---

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

##### **🔐 Node 1: Authenticates to your Icypeas account (Code Node)**
- **Mở node này** và thay thế:
  ```javascript
  const API_KEY = "**PUT_API_KEY_HERE**";
  const API_SECRET = "**PUT_API_SECRET_HERE**";
  const USER_ID = "**PUT_USER_ID_HERE**";
  ```
  bằng **API Key, API Secret & User ID** từ [https://app.icypeas.com/bo/profile](https://app.icypeas.com/bo/profile).

- **Nếu tự host n8n**, cần **bật module crypto** theo hướng dẫn:
  1. Truy cập **Settings → General → Additional Node Packages**.
  2. Tìm **crypto** và **check** vào ô.
  3. **Save** và **restart n8n** để áp dụng.

##### **🔑 Node 2: Run email search (HTTP Request)**
- **Tạo credential mới** cho **Header Auth**:
  1. Mở **HTTP Request Node**.
  2. Trong **Credentials**, chọn **"httpHeaderAuth"**.
  3. Nhấn **"Create new Credential"**.
  4. Đặt **Name = "Authorization"**.
  5. Trong **Value**, chọn **expression** và nhập:
     ```javascript
     {{ $json.api.key + ':' + $json.api.signature }}
     ```
  6. **Save**.

- **Điền thông tin tìm kiếm**:
  - Trong **Body Parameters**, thêm:
    - `lastname`: Họ của người cần tìm.
    - `firstname`: Tên của người cần tìm.
    - `domainOrCompany`: Tên miền hoặc công ty.

  **Ví dụ**:
  ```
  lastname: "Nguyễn"
  firstname: "Văn"
  domainOrCompany: "gmail.com"
  ```

---

#### **3. Kích Hoạt ⚡️**
- **Test Run** với dữ liệu mẫu (ví dụ: `lastname: "Trần", firstname: "Thanh", domainOrCompany: "yahoo.com`).
- **Bật Active** workflow để sử dụng.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tích hợp với Slack/Telegram**:
   - Sau khi tìm kiếm, **gửi kết quả tự động** vào Slack/Telegram bằng **n8n-nodes-base.slack** hoặc **n8n-nodes-base.telegram**.

2. **Lưu log kết quả**:
   - Sử dụng **n8n-nodes-base.googleSheets** hoặc **n8n-nodes-base.notion** để lưu lịch sử tìm kiếm.

3. **Tự động hóa CRM**:
   - Kết nối với **HubSpot, Salesforce** để cập nhật email mới vào hệ thống CRM.

4. **Tìm kiếm nhiều email cùng lúc**:
   - Sử dụng **n8n-nodes-base.set** để lưu trữ nhiều tham số và chạy song song.

---

### 📌 **Kết Luận**
**Workflow này giúp các sếp:**
✔ **Tìm kiếm email chỉ trong vài giây** thay vì mất nhiều giờ tra cứu thủ công.
✔ **Tích hợp dễ dàng** với các công cụ khác (Slack, CRM, Email Marketing).
✔ **Hoạt động 24/7** mà không cần can thiệp.

**Hãy thử ngay và tiết kiệm thời gian cho công việc sales & marketing của mình!** 🚀

---
**🔗 [Xem workflow gốc tại n8n.io](https://n8n.io/workflows/2013)**
**💡 Cần hỗ trợ? Hãy để lại comment bên dưới!**