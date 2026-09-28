---
title: "🚀 Tự Động Gửi Thông Báo Tin Nhắn Chat Tawk.to Sang Email Gmail - Không Cần Code!"
description: "Workflow tự động hóa nhận tin nhắn từ Tawk.to và chuyển ngay sang email Gmail, giúp hỗ trợ khách hàng 24/7 mà không tốn thời gian kiểm tra thủ công. Giảm thiểu phản hồi chậm và cải thiện trải nghiệm khách hàng."
slug: "tu-dong-hoa-thong-bao-tawk-to-sang-email-gmail"
tags: [n8n, automation, support-chatbot, gmail, tawk-to, no-code]
keywords: [tự động hóa n8n, gửi tin nhắn tawk.to sang email, hỗ trợ khách hàng tự động, workflow n8n gmail, tự động hóa chatbot]
---

# 🚀 **Tự Động Gửi Thông Báo Tin Nhắn Chat Tawk.to Sang Email Gmail**

### **Giải pháp hoàn hảo cho các sếp muốn hỗ trợ khách hàng 24/7 mà không tốn thời gian kiểm tra tin nhắn thủ công!**

Hiện nay, nhiều doanh nghiệp vẫn phải **kiểm tra tin nhắn từ Tawk.to thủ công** và phản hồi qua email, dẫn đến:
- **Thời gian phản hồi chậm** (khách hàng phải chờ lâu).
- **Rủi ro quên tin nhắn** (do nhiều tin nhắn đồng thời).
- **Không thể phản hồi ngay** khi đang offline.

**Workflow này tự động hóa toàn bộ quá trình:**
✅ **Nhận tin nhắn từ Tawk.to** (qua Webhook).
✅ **Định dạng lại tin nhắn** (tên khách hàng, nội dung, thời gian).
✅ **Gửi thông báo email tự động** đến email cá nhân hoặc nhóm hỗ trợ.

Kết quả? **Khách hàng nhận phản hồi nhanh chóng, đội ngũ hỗ trợ tiết kiệm thời gian, và không còn lo quên tin nhắn!**

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Hỗ trợ khách hàng 24/7** – Không cần phải online để phản hồi.
- **Tiết kiệm thời gian** – Không phải kiểm tra tin nhắn thủ công.
- **Trả lời nhanh chóng** – Thông báo email ngay khi có tin nhắn mới.
- **Cải thiện trải nghiệm khách hàng** – Khách hàng không phải chờ đợi.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản Tawk.to** (đã cài đặt và có Webhook URL).
2. **Tài khoản Gmail** (đã kích hoạt API và tạo **OAuth 2.0 Credential** trong n8n).
3. **Khóa API của n8n** (nếu tự host) hoặc tài khoản n8n.io miễn phí.
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/6024](https://n8n.io/workflows/6024) và import vào **n8n Editor**.
- **Cách 2:** Copy toàn bộ JSON dưới đây và **paste vào n8n Editor** (tab "Import"):

```json
{
  "nodes": [
    {
      "parameters": {
        "path": "a4bf95cd-a30a-4ae0-bd2a-6d96e6cca3b4",
        "httpMethod": "POST"
      },
      "name": "Receive Tawk.to Request",
      "type": "n8n-nodes-base.webhook",
      "typeVersion": 1,
      "position": [
        250,
        300
      ]
    },
    {
      "parameters": {},
      "name": "Format the message",
      "type": "n8n-nodes-base.set",
      "typeVersion": 1,
      "position": [
        450,
        300
      ]
    },
    {
      "parameters": {
        "subject": "New Tawk.to Chat Message: {{ $node["Format the message"].json["name"] }}",
        "html": "<p>New chat message from <strong>{{ $node["Format the message"].json["name"] }}</strong>:</p><p>{{ $node["Format the message"].json["message"] }}</p><p><a href=\"{{ $node["Format the message"].json["url"] }}\">View chat</a></p>",
        "to": ["your-email@gmail.com"]
      },
      "name": "Send alert email",
      "type": "n8n-nodes-base.gmail",
      "typeVersion": 1,
      "position": [
        650,
        300
      ]
    }
  ],
  "connections": {
    "Receive Tawk.to Request": {
      "main": [
        [
          {
            "node": "Format the message",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Format the message": {
      "main": [
        [
          {
            "node": "Send alert email",
            "type": "main",
            "index": 0
          }
        ]
      ]
    }
  }
}
```

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **🔹 Node 1: Receive Tawk.to Request (Webhook)**
- **Không cần chỉnh gì** nếu đã lấy **Webhook URL** từ Tawk.to và điền vào `path` (đã có sẵn: `a4bf95cd-a30a-4ae0-bd2a-6d96e6cca3b4`).
- **Lưu ý:** Nếu muốn thay đổi Webhook URL, hãy **cập nhật trong Tawk.to Dashboard** và trong node này.

##### **🔹 Node 2: Format the message (Set)**
- **Không cần chỉnh** vì nó tự động lấy dữ liệu từ Tawk.to và định dạng thành:
  ```json
  {
    "name": "Tên khách hàng",
    "message": "Nội dung tin nhắn",
    "url": "Link chat Tawk.to"
  }
  ```

##### **🔹 Node 3: Send alert email (Gmail) – CẦN CHỈNH TRỌN**
- **Tham số quan trọng:**
  - **`subject` (Tiêu đề email):** `New Tawk.to Chat Message: {{ $node["Format the message"].json["name"] }}`
    *(Hiển thị tên khách hàng trong tiêu đề)*
  - **`html` (Nội dung email):** Có thể chỉnh sửa để thêm thông tin khác (ví dụ: thời gian, avatar khách hàng).
  - **`to` (Địa chỉ email nhận):** Thay `your-email@gmail.com` bằng email của mình hoặc nhóm hỗ trợ (ví dụ: `team-support@doanhnghiep.com`).
- **Cách thiết lập OAuth 2.0 trong n8n:**
  1. Tạo **OAuth 2.0 Credential** trong n8n (Settings > Credentials > Add Credential).
  2. Chọn **Gmail** và đăng nhập tài khoản.
  3. Chọn credential này trong node **Send alert email**.

#### **3. Kích hoạt ⚡️**
1. **Test run** với một tin nhắn mẫu từ Tawk.to (đảm bảo Webhook hoạt động).
2. **Bật Active workflow** và kiểm tra email nhận được.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁC TỐI ƯU NÂNG CAO]
- **Thêm Slack/Telegram Notifications:** Sử dụng node **Slack** hoặc **Telegram Bot** để gửi thông báo đồng thời.
- **Lưu log tin nhắn:** Sử dụng node **Google Sheets** hoặc **Airtable** để lưu lịch sử chat.
- **Phân loại tin nhắn:** Sử dụng node **If** để phân loại tin nhắn (ví dụ: tin nhắn từ khách hàng VIP được gửi ưu tiên).
- **Gửi email định kỳ báo cáo:** Sử dụng **n8n Trigger** (Schedule) để gửi báo cáo tổng hợp tin nhắn hàng ngày.
:::

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc kiểm tra tin nhắn Tawk.to thủ công, đồng thời **cải thiện trải nghiệm khách hàng** bằng cách phản hồi nhanh chóng. **Hãy áp dụng ngay và tự động hóa hỗ trợ khách hàng của mình!**

👉 **Bắt đầu tự động hóa ngay:** [Tải workflow từ n8n.io](https://n8n.io/workflows/6024) hoặc import JSON trên!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::