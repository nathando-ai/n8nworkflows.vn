---
title: "🚀 Nhận thông báo khi dự án mới được tạo trong Copper"
description: "Tự động nhận thông báo ngay khi một dự án mới được tạo trong CRM Copper, giúp các sếp không bỏ lỡ cơ hội bán hàng."
slug: "nhan-thong-bao-du-an-moi-copper"
tags: [n8n, automation, no-code, copper, sales]
keywords: [n8n workflow, tự động hóa, copper crm, project trigger, sales automation]
---

# 🚀 Nhận thông báo khi dự án mới được tạo trong Copper

Khi làm việc với **Copper CRM**, các sếp thường phải mở giao diện, lọc danh sách dự án mới và cập nhật thông tin thủ công. Việc này không chỉ tốn thời gian mà còn dễ bỏ sót những cơ hội bán hàng quan trọng.  
Workflow này sẽ **tự động lắng nghe** sự kiện “project created” trong Copper và kích hoạt ngay lập tức, giúp các sếp luôn nắm bắt mọi dự án mới mà không cần viết một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không còn phải kiểm tra thủ công trong Copper.  
- **Đảm bảo độ chính xác 100%**: Thông báo được kích hoạt ngay khi dự án được tạo.  
- **Kích hoạt hành động ngay lập tức**: Có thể nối tiếp gửi email, Slack, hoặc cập nhật Google Sheet.  
- **Hoạt động liên tục 24/7**: Workflow chạy trên server riêng, không phụ thuộc vào máy tính cá nhân.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Copper** với quyền **API Access**.  
- **API Key** của Copper (được tạo trong phần Settings → API & Webhooks).  
- **Credential “copperApi”** trong n8n, chứa API Key trên.  
- Kết nối internet ổn định cho n8n server.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập **n8n → Workflows → Import**.  
2. Tải file JSON (được đính kèm ở cuối README) hoặc **Copy/Paste** toàn bộ JSON vào ô “Import from Clipboard”.  
3. Nhấn **Import** → Workflow sẽ xuất hiện trong danh sách.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Mô tả | Cấu hình cần chỉnh |
|------|------|--------------------|
| **Copper Trigger** | Lắng nghe sự kiện **project created** trong Copper. | - **Credentials**: Chọn `copperApi` (đã tạo ở mục chuẩn bị). <br> - **Resource**: Để mặc định là `project`. <br> - **Operation**: `Created` (được tự động thiết lập). |

> **Lưu ý:** Nếu muốn nhận thông báo cho các loại tài nguyên khác (lead, opportunity...), chỉ cần thay đổi **Resource** trong node này.

#### 3. Kích hoạt ⚡️
1. Nhấn **Execute Workflow** để chạy thử với dữ liệu mẫu (nếu có).  
2. Kiểm tra log trong **Execution** để xác nhận node nhận được payload từ Copper.  
3. Khi mọi thứ ổn, bật **Active** (nút chuyển đổi ở góc trên bên phải) để workflow chạy liên tục.

### ✍️ Mẹo & gợi ý nâng cao
- **Gửi email tự động**: Thêm node **Email** sau Copper Trigger, đính kèm chi tiết dự án.  
- **Thông báo Slack/Telegram**: Kết nối node **Slack** hoặc **Telegram** để nhận tin tức ngay trên kênh nhóm.  
- **Lưu log vào Google Sheet**: Thêm node **Google Sheets** để ghi lại mọi dự án mới, tiện cho báo cáo tuần.  
- **Filter theo người phụ trách**: Sử dụng node **IF** để chỉ thông báo khi `owner_id` khớp với ID của sếp.

### 📌 Kết luận
Với chỉ **một node duy nhất**, workflow này đã biến việc theo dõi dự án mới trong Copper thành một quá trình **tự động, nhanh chóng và không lỗi**. Các sếp chỉ cần cấu hình API một lần, bật workflow và để n8n lo phần còn lại. Hãy triển khai ngay hôm nay để không bỏ lỡ bất kỳ cơ hội bán hàng nào!  

---  

**File JSON để import** (copy toàn bộ nội dung dưới đây và dán vào “Import from Clipboard”):

```json
{
  "nodes": [
    {
      "parameters": {
        "resource": "project",
        "operation": "created"
      },
      "name": "Copper Trigger",
      "type": "n8n-nodes-base.copperTrigger",
      "typeVersion": 1,
      "position": [
        250,
        300
      ],
      "credentials": {
        "copperApi": "Copper API"
      }
    }
  ],
  "connections": {}
}
```