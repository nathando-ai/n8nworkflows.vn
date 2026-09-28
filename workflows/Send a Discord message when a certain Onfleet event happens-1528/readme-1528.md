---
title: "🚀 Tự Động Hóa Thông Báo Discord Khi Sự Kiện Onfleet Xảy Ra - Không Cần Code"
description: "Giải pháp tự động hóa thông báo tức thời trên Discord khi có sự kiện mới trên Onfleet (đơn hàng mới, thay đổi trạng thái,...) - tiết kiệm thời gian và tránh bỏ lỡ thông tin quan trọng."
slug: "tu-dong-hoa-thong-bao-discord-onfleet"
tags: [n8n, automation, discord, onfleet, no-code, logistics]
keywords: [n8n workflow discord onfleet, tự động hóa logistics, thông báo sự kiện onfleet, tự động hóa doanh nghiệp vận tải, n8n trigger onfleet]
---

# 🚀 **Tự Động Hóa Thông Báo Discord Khi Sự Kiện Onfleet Xảy Ra**

Bạn có bao giờ phải **ngồi chờ** hoặc **quên kiểm tra** các sự kiện quan trọng trên Onfleet như đơn hàng mới, thay đổi trạng thái giao hàng, hoặc lỗi vận chuyển? Điều này không chỉ **tốn thời gian** mà còn **mang lại rủi ro bỏ lỡ thông tin quan trọng**, ảnh hưởng đến hiệu quả vận hành của doanh nghiệp.

**Workflow này sẽ giải quyết vấn đề đó bằng cách:**
- **Thông báo tức thời** trên Discord khi có sự kiện mới trên Onfleet (ví dụ: đơn hàng mới, trạng thái thay đổi, lỗi vận chuyển,...).
- **Tiết kiệm thời gian** cho các sếp không phải theo dõi thủ công.
- **Cá nhân hóa thông báo** với nội dung chi tiết (ID đơn hàng, trạng thái, vị trí, thời gian,...).
- **Hoạt động 24/7** mà không cần can thiệp của con người.

---
### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Thông báo tức thời** trên Discord khi có sự kiện mới trên Onfleet (không bỏ lỡ bất kỳ đơn hàng nào).
- **Tiết kiệm thời gian** lên đến **30 phút/ngày** so với việc theo dõi thủ công.
- **Tăng cường sự đồng bộ** giữa đội ngũ vận chuyển và quản lý.
- **Giảm rủi ro** do bỏ lỡ thông báo quan trọng (ví dụ: đơn hàng bị trì hoãn).
- **Dễ dàng mở rộng** để kết nối với nhiều kênh thông báo khác (Slack, Email, Telegram,...).
:::

---
### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow này hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Onfleet** và **API Key** của Onfleet (được tạo trong [Dashboard Onfleet](https://onfleet.com/)).
2. **Tài khoản Discord** và **Webhook URL** của một channel cụ thể (hướng dẫn tạo webhook [tại đây](https://support.discord.com/hc/en-us/articles/228383668-Intro-to-Webhooks)).
3. **n8n Self-hosted** (không thể chạy trên n8n.cloud vì yêu cầu trigger từ Onfleet).
:::

---
### 🚀 **Cách Import & Lưu ý khi "Lên Đồ"**

#### 1. **Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/1528) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** và chọn **"Import"** → **"From JSON"** → Dán hoặc tải file JSON.
- **Kích hoạt workflow** bằng cách bấm **"Active"** ở góc trên bên phải.

#### 2. **Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này chỉ có **2 node**, nhưng **cấu hình chính xác là rất quan trọng**:

##### **Node 1: Onfleet Trigger**
- **Loại sự kiện (Event Type):** Chọn sự kiện bạn muốn theo dõi (ví dụ: `order.created`, `order.updated`, `order.delivered`, `driver.location.updated`,...).
  - *Gợi ý:* Để theo dõi **tất cả sự kiện**, chọn **"All Events"**.
- **Credentials:** Chọn `onfleetApi` (đã cấu hình trước khi import).
- **API Key:** Điền **API Key** của Onfleet (tạo trong [Dashboard Onfleet](https://onfleet.com/) → **Settings → API Keys**).
- **Webhook URL:** Điền **URL Webhook** của Discord (tạo trong **Discord Developer Portal**).

##### **Node 2: Discord**
- **Credentials:** Chọn `discord` (nếu chưa có, tạo mới trong **Credentials → Add Credential → Discord**).
- **Webhook URL:** Điền **Webhook URL** của Discord (đã tạo ở trên).
- **Message Content:** Cấu hình nội dung thông báo (có thể sử dụng **template** từ Onfleet để hiển thị thông tin chi tiết như:
  ```json
  {
    "content": `🚚 **Sự kiện mới trên Onfleet** 🚚
    **ID Đơn hàng:** {{$node["onfleetTrigger"].json["id"]}}
    **Trạng thái:** {{$node["onfleetTrigger"].json["status"]}}
    **Tên Người nhận:** {{$node["onfleetTrigger"].json["recipient"]["name"]}}
    **Địa chỉ:** {{$node["onfleetTrigger"].json["recipient"]["address"]}}
    **Thời gian:** {{$node["onfleetTrigger"].json["created_at"]}}`,
    "username": "Onfleet Alert Bot",
    "avatar_url": "https://i.imgur.com/XYZabc.png"  // (Tùy chọn: avatar cho bot)
  }
  ```
  - *Lưu ý:* Sử dụng **expression mode** (`{{...}}`) để trích xuất dữ liệu từ Onfleet.

#### 3. **Kích hoạt ⚡️**
- **Test Run:** Chọn **"Run Once"** để kiểm tra workflow với dữ liệu mẫu.
- **Active Workflow:** Sau khi kiểm tra thành công, bật **Active** để workflow hoạt động liên tục.

---
### ✍️ **Mẹo & Gợi ý Nâng Cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết nối với Slack/Telegram:**
   - Thay vì Discord, bạn có thể sử dụng **Slack Webhook** hoặc **Telegram Bot** để thông báo.
   - *Hướng dẫn:* Thêm node `slack` hoặc `telegram` và cấu hình tương tự.

2. **Lưu log sự kiện:**
   - Thêm node **Google Sheets** hoặc **Airtable** để lưu tất cả sự kiện Onfleet vào một bảng dữ liệu.
   - *Lợi ích:* Dễ dàng phân tích và báo cáo sau này.

3. **Phân loại thông báo:**
   - Sử dụng **conditional node** để phân loại sự kiện (ví dụ: chỉ thông báo đơn hàng mới, bỏ qua đơn hàng đã hoàn thành).
   - *Ví dụ:*
     ```json
     {
       "if": "{{$node["onfleetTrigger"].json["status"] === 'completed'}}",
       "then": ["skip"], // Bỏ qua đơn hàng đã hoàn thành
       "else": ["discord"] // Thông báo nếu chưa hoàn thành
     }
     ```

4. **Gửi email cảnh báo:**
   - Thêm node **Email** (ví dụ: `n8n-nodes-base.email`) để gửi email cảnh báo cho quản lý khi có sự kiện quan trọng.

5. **Tự động phản hồi trên Discord:**
   - Sử dụng **Discord Interaction** để bot tự động phản hồi với thông tin chi tiết khi người dùng nhấp vào thông báo.
:::

---
### 📌 **Kết Luận**
Workflow này giúp **tự động hóa hoàn toàn** quá trình thông báo sự kiện Onfleet lên Discord, **giúp các sếp không phải lo lắng bỏ lỡ thông tin quan trọng** và **tiết kiệm thời gian** cho công việc quản lý.

**Hành động ngay:**
1. **Cài đặt n8n Self-hosted** (nếu chưa có) trên VPS để workflow hoạt động 24/7.
2. **Import workflow** và cấu hình theo hướng dẫn trên.
3. **Bật Active** và bắt đầu nhận thông báo tức thời!

---
:::success[💡 **LƯU Ý CUỐI CUNG**]
- Nếu gặp vấn đề với **API Key Onfleet**, hãy kiểm tra lại quyền hạn trong **Dashboard Onfleet**.
- Để **mở rộng chức năng**, bạn có thể kết hợp với **n8n Community Nodes** như `n8n-nodes-base.google-sheets` hoặc `n8n-nodes-base.airtable`.
- Nếu cần hỗ trợ thêm, tham khảo [n8n Docs](https://docs.n8n.io/) hoặc [Community n8n](https://community.n8n.io/).
:::