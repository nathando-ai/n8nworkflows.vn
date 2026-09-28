---
title: "📲 Tự Động Gửi Tin Nhắn WhatsApp Vía Twilio Khi Sự Kiện Onfleet Xảy Ra - Giảm Thời Gian Phản Hồi 90%"
description: "Workflow tự động hóa hoàn toàn không code giúp các sếp nhận thông báo tức thời qua WhatsApp khi có sự kiện quan trọng trên Onfleet (đơn hàng mới, trạng thái giao hàng thay đổi), tiết kiệm thời gian phản hồi và tránh bỏ lỡ đơn hàng."
slug: "tu-dong-hoa-gui-tin-nhan-whatsapp-onfleet-twilio"
tags: [n8n, automation, twilio, onfleet, sales, no-code, whatsapp-business]
keywords: [n8n workflow onfleet, tự động hóa whatsapp twilio, gửi tin nhắn tự động onfleet, giảm thời gian phản hồi, tự động hóa bán hàng, tự động hóa logistics]
---

# 🚀 **Tự Động Gửi Tin Nhắn WhatsApp Khi Có Sự Kiện Trên Onfleet - Giải Pháp "Không Code" Cho Doanh Nghiệp Logistics**

### **Nỗi Đau Của Các Sếp Logistics & Sales**
Các sếp quản lý logistics hay đội ngũ bán hàng thường phải:
- **Làm thủ công** theo dõi trạng thái đơn hàng trên Onfleet (đơn hàng mới, giao hàng thất bại, đến nơi nhưng không nhận...).
- **Phản hồi chậm** vì phải check nhiều lần trên hệ thống, dẫn đến mất khách hàng hoặc đơn hàng bị bỏ quên.
- **Tốn thời gian** để chuyển thông tin từ Onfleet sang WhatsApp (hay Slack) để thông báo cho nhân viên hoặc khách hàng.

**Workflow này giải quyết tất cả!** Khi có sự kiện quan trọng trên Onfleet (ví dụ: đơn hàng mới, trạng thái giao hàng thay đổi), hệ thống sẽ **tự động gửi tin nhắn WhatsApp** thông báo ngay lập tức, giúp các sếp **giảm thời gian phản hồi xuống còn 90%**, tránh bỏ lỡ đơn hàng và cải thiện trải nghiệm khách hàng.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian phản hồi**: Thông báo tức thời qua WhatsApp khi có sự kiện quan trọng trên Onfleet.
- **Không bỏ lỡ đơn hàng**: Hệ thống tự động cảnh báo khi có sự kiện cần hành động (ví dụ: đơn hàng đến nơi nhưng không nhận).
- **Cá nhân hóa thông báo**: Gửi tin nhắn cụ thể theo loại sự kiện (màu sắc, nội dung khác nhau).
- **Hoạt động 24/7**: Không cần can thiệp thủ công, tự động hóa hoàn toàn.
- **Tăng hiệu quả logistics**: Giúp đội ngũ giao hàng và sales phản hồi nhanh chóng, cải thiện trải nghiệm khách hàng.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Twilio**:
   - [Đăng ký Twilio](https://www.twilio.com/) và tạo **WhatsApp Sandbox** (hoặc WhatsApp Business Account).
   - **API Key** và **Auth Token** từ Twilio Console (để kết nối với node Twilio).
   - **WhatsApp Sandbox Number** (số điện thoại WhatsApp được cấp từ Twilio để gửi tin nhắn).

2. **Tài khoản Onfleet**:
   - [Đăng ký Onfleet](https://www.onfleet.com/) và lấy **API Key** từ Dashboard (để kết nối với node Onfleet Trigger).

3. **Số điện thoại WhatsApp của người nhận** (ví dụ: số điện thoại khách hàng hoặc nhân viên cần thông báo).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [link gốc](https://n8n.io/workflows/1525) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/1525) và paste vào **Import Workflow** trong n8n Editor.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **2 node chính**, các sếp cần cấu hình như sau:

##### **Node 1: Onfleet Trigger**
- **Loại sự kiện (Event)**: Chọn sự kiện Onfleet bạn muốn theo dõi (ví dụ: `order.created`, `order.status.updated`, `delivery.attempt.failed`).
  - *Gợi ý*: Chọn `order.status.updated` để nhận thông báo khi trạng thái đơn hàng thay đổi (ví dụ: từ "Đang giao" sang "Đã giao").
- **Credentials**: Chọn `onfleetApi` (đã cấu hình trước khi import).
- **Webhook URL**: Để trống (n8n sẽ tự động tạo URL khi workflow được kích hoạt).

##### **Node 2: Twilio (Gửi Tin Nhắn WhatsApp)**
- **Credentials**: Chọn `twilioApi` (đã cấu hình trước khi import).
- **From WhatsApp Number**: Nhập số WhatsApp Sandbox của bạn (ví dụ: `whatsapp:+14155238886`).
- **To WhatsApp Number**: Nhập số điện thoại của người nhận (ví dụ: `whatsapp:+841234567890`).
- **Message**: Cấu hình nội dung tin nhắn dựa trên sự kiện Onfleet:
  ```json
  {
    "body": "🚚 **Thông báo đơn hàng #{{$node["Onfleet Trigger"].json["order"]["id"]}}**:\n\n- **Trạng thái**: {{$node["Onfleet Trigger"].json["order"]["status"]}}\n- **Địa chỉ**: {{$node["Onfleet Trigger"].json["order"]["pickup_address"]["address1"]}}\n- **Người nhận**: {{$node["Onfleet Trigger"].json["order"]["customer"]["name"]}}\n\n🔗 **Xem chi tiết**: [Onfleet](https://app.onfleet.com/orders/{{$node["Onfleet Trigger"].json["order"]["id"]}})"
  }
  ```
  - *Lưu ý*: Sử dụng **Jinja2** để động tính nội dung tin nhắn (ví dụ: `$node["Onfleet Trigger"].json["order"]["status"]` để lấy trạng thái đơn hàng).

#### **3. Kích Hoạt ⚡️**
- **Test Run**: Chạy workflow với một sự kiện mẫu trên Onfleet để kiểm tra tin nhắn WhatsApp có được gửi đúng không.
- **Bật Active**: Sau khi kiểm tra thành công, bật **Active** để workflow hoạt động liên tục.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** để gửi thông báo đồng thời cho đội ngũ nội bộ.

2. **Lưu Log & Báo Cáo**:
   - Thêm node **Google Sheets** hoặc **Airtable** để lưu lịch sử sự kiện và tin nhắn đã gửi.

3. **Tự động Trả Lời Khách Hàng**:
   - Sử dụng **Twilio** kết hợp với **AI Chatbot** (ví dụ: Dialogflow) để tự động trả lời khách hàng khi nhận được tin nhắn.

4. **Phân Loại Sự Kiện**:
   - Sử dụng **Switch** node để gửi tin nhắn khác nhau tùy vào loại sự kiện (ví dụ: tin nhắn ưu tiên cho đơn hàng "Đã quá hạn").

5. **Gửi Email Kèm Tin Nhắn**:
   - Thêm node **Email** (ví dụ: Gmail) để gửi email cảnh báo cùng với tin nhắn WhatsApp.
:::

---

### 📌 **Kết Luận**
Workflow này giúp các sếp **tự động hóa hoàn toàn quá trình thông báo sự kiện Onfleet** qua WhatsApp, **giảm thời gian phản hồi**, và **tăng hiệu quả logistics**. Không cần viết code, chỉ cần cấu hình vài bước đơn giản là có thể **cảnh báo tức thời** khi có đơn hàng mới, trạng thái giao hàng thay đổi, hoặc sự kiện quan trọng khác.

**Hành động ngay!**
1. **Cài đặt n8n Self-hosted** trên VPS để workflow chạy 24/7 (đăng ký VPS với mã giảm giá **VPSN8N** tại [TinoHost](https://tino.vn/vps-n8n?affid=388)).
2. **Import workflow** và cấu hình theo hướng dẫn trên.
3. **Bật Active** và bắt đầu tự động hóa!

**🚀 Cải thiện trải nghiệm khách hàng và hiệu quả đội ngũ ngay hôm nay!**