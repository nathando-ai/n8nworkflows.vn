---
title: "📡 Tự Động Nhận Tin Nhắn MQTT 24/7 - Không Cần Code, Khả Năng Toàn Cầu"
description: "Workflow này giúp các sếp tự động nhận và xử lý tin nhắn từ queue MQTT một cách liên tục, không cần can thiệp thủ công. Giúp tối ưu hóa hệ thống IoT, giám sát thiết bị hoặc xử lý dữ liệu thời gian thực."
slug: "tu-dong-nhan-tin-nhan-mqtt"
tags: [n8n, automation, mqtt, iot, real-time-data]
keywords: [n8n workflow mqtt, tự động hóa nhận tin nhắn MQTT, xử lý dữ liệu thời gian thực, tự động hóa IoT]
---

# 📡 **Tự Động Nhận Tin Nhắn MQTT 24/7 - Không Cần Code**

### **Giải pháp cho các sếp quản lý hệ thống IoT, giám sát thiết bị hoặc xử lý dữ liệu thời gian thực**
Hiện nay, khi các thiết bị IoT hoặc hệ thống giám sát gửi tin nhắn qua **MQTT**, việc nhận và xử lý chúng thủ công là một công việc tẻ nhạt, dễ gây lỗi và không hiệu quả. **Workflow này giúp tự động hóa toàn bộ quá trình**, cho phép các sếp nhận và xử lý tin nhắn MQTT **liên tục, chính xác và không cần can thiệp thủ công**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động ổn định 24/7, các sếp nên **self-host n8n** trên một VPS ổn định.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Không cần phải kiểm tra thủ công queue MQTT.
- **Chính xác và không lỗi**: Tất cả tin nhắn được nhận và xử lý theo quy tắc đã thiết lập.
- **Hoạt động liên tục**: Duy trì hoạt động 24/7, không phụ thuộc vào thời gian làm việc.
- **Giám sát thời gian thực**: Phù hợp cho hệ thống IoT, cảm biến hoặc ứng dụng yêu cầu phản hồi tức thì.
:::

---

### 🔧 **Yêu cầu cần thiết**
Để workflow này hoạt động, các sếp cần:
- **Tài khoản MQTT hoạt động**: Có thể là một broker MQTT như **Mosquitto, HiveMQ, AWS IoT Core** hoặc dịch vụ khác.
- **Credentials MQTT**: Thông tin kết nối như **Client ID, Username, Password, Host, Port** (nếu có).
- **Topic MQTT**: Topic cụ thể mà workflow sẽ lắng nghe (ví dụ: `sensors/data`).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Workflow này rất đơn giản, chỉ có **1 node** (`MQTT Trigger`), nhưng cần cấu hình chính xác để hoạt động.

**Cách import:**
- Tải file JSON từ [n8n.io/workflows/657](https://n8n.io/workflows/657).
- Mở **n8n Editor** và chọn **Import Workflow** → Chọn file JSON vừa tải.
- Hoặc copy toàn bộ JSON và dán vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này chỉ có **1 node duy nhất**, nhưng cần cấu hình **MQTT Trigger** như sau:

##### **a. Thiết lập Credentials MQTT**
- Trong **n8n**, đi đến **Credentials** → **Add New Credential** → Chọn **MQTT**.
- Điền thông tin kết nối:
  - **Host**: Địa chỉ broker MQTT (ví dụ: `broker.hivemq.com`).
  - **Port**: Cổng mặc định (1883 cho MQTT không mã hóa, 8883 cho MQTT với TLS).
  - **Client ID**: ID duy nhất cho client (ví dụ: `n8n-mqtt-client`).
  - **Username/Password** (nếu có).
  - **Topic**: Topic mà workflow sẽ lắng nghe (ví dụ: `sensors/#` để nhận tất cả tin nhắn từ `sensors/`).
  - **QoS** (Quality of Service): Chọn **0** (At most once) hoặc **1** (At least once) tùy thuộc vào yêu cầu.

##### **b. Kết nối Credentials với Node**
- Trong **MQTT Trigger**, chọn **Credentials** và chọn credential MQTT vừa tạo.
- **Test Connection** để đảm bảo kết nối thành công.

#### **3. Kích hoạt ⚡️**
- **Test Run**: Chạy workflow với một tin nhắn mẫu để kiểm tra.
- **Active Workflow**: Sau khi kiểm tra thành công, bật **Active** để workflow hoạt động liên tục.

---

### ✍️ **Mẹo & gợi ý nâng cao**
- **Xử lý tin nhắn tự động**: Sau khi nhận tin nhắn MQTT, các sếp có thể **kết nối với các node khác** như:
  - **HTTP Request**: Gửi tin nhắn đến một API.
  - **Slack/Telegram**: Gửi thông báo tức thì.
  - **Database (Google Sheets, Airtable)**: Lưu dữ liệu vào bảng.
  - **LLM (ChatGPT, Bard)**: Xử lý tin nhắn bằng trí tuệ nhân tạo.
- **Log & Monitoring**: Sử dụng **n8n Dashboard** hoặc **Slack Alerts** để theo dõi hoạt động của workflow.
- **Queue Processing**: Nếu có nhiều tin nhắn, có thể sử dụng **Set** hoặc **Queue** node để xử lý tuần tự.

---

### 📌 **Kết luận**
Workflow này là **giải pháp tối ưu** cho các sếp cần tự động hóa việc nhận tin nhắn MQTT **không cần code**. Dễ dàng cài đặt, hoạt động liên tục và phù hợp cho **hệ thống IoT, giám sát thiết bị hoặc xử lý dữ liệu thời gian thực**.

**Hãy áp dụng ngay và tự động hóa quy trình của mình!** 🚀