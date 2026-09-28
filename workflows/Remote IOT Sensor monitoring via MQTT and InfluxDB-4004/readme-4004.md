---
title: "🌡️ Tự Động Hóa Theo Dõi Thiết Bị IoT Xa Lãnh qua MQTT & InfluxDB - Không Cần Code"
description: "Giải pháp tự động hóa thu thập và lưu trữ dữ liệu nhiệt độ, độ ẩm từ thiết bị IoT xa lãnh (ESP32 + DHT22) vào InfluxDB 24/7, giúp các sếp theo dõi môi trường thực thời mà không cần viết một dòng code."
slug: "tu-dong-hoa-theo-doi-thiet-bi-iot-xa-lanh-mqtt-influxdb"
tags: [n8n, automation, IoT, MQTT, InfluxDB, engineering, self-hosted]
keywords: [n8n workflow IoT, tự động hóa thiết bị IoT, MQTT InfluxDB, theo dõi nhiệt độ độ ẩm, tự động hóa không code, n8n engineering]
---

# 🚀 **Tự Động Hóa Theo Dõi Thiết Bị IoT Xa Lãnh qua MQTT & InfluxDB**

### **Nỗi Đau Của Các Sếp**
Các sếp đang quản lý hệ thống IoT (như trạm khí tượng, nhà máy, hoặc hệ thống nông nghiệp) thường phải đối mặt với những vấn đề sau:
- **Thu thập dữ liệu thủ công**: Phải kiểm tra thiết bị ESP32/DHT22 thường xuyên để lấy nhiệt độ, độ ẩm.
- **Lưu trữ không hiệu quả**: Dữ liệu phân tán trên nhiều thiết bị hoặc không được lưu trữ hệ thống.
- **Không theo dõi thực thời**: Thiếu giải pháp tự động hóa để cảnh báo khi nhiệt độ vượt ngưỡng an toàn.

**Workflow này giải quyết tất cả đó!** Nó tự động:
✅ **Thu thập** dữ liệu từ thiết bị IoT xa lãnh (ESP32 + DHT22) qua MQTT.
✅ **Chuyển đổi** dữ liệu thô thành định dạng JSON chuẩn.
✅ **Lưu trữ** vào InfluxDB (cơ sở dữ liệu thời gian thực) để phân tích sau này.
✅ **Hoạt động liên tục** 24/7 mà không cần can thiệp của con người.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động ổn định, các sếp nên **self-host n8n** trên một VPS ổn định. InfluxDB cũng cần được cài đặt trên cùng một máy chủ hoặc VPS để tránh latency.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đủ sức mạnh cho n8n + InfluxDB)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần kiểm tra thiết bị thủ công hàng ngày.
- **Dữ liệu chính xác**: Thu thập tự động từ thiết bị IoT, giảm sai số con người.
- **Theo dõi thực thời**: Dữ liệu nhiệt độ/độ ẩm được cập nhật ngay khi thiết bị gửi.
- **Dễ dàng phân tích**: Dữ liệu lưu vào InfluxDB, có thể kết nối với Grafana để tạo dashboard.
- **Hoạt động 24/7**: Workflow chạy tự động, không cần restart.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Thiết bị IoT**:
   - ESP32 + mô-đun DHT22 (đọc nhiệt độ/độ ẩm).
   - Thiết bị kết nối internet (WiFi/ETH) để gửi dữ liệu qua MQTT.
2. **MQTT Broker**:
   - **Mosquitto** (cài đặt trên máy chủ hoặc VPS).
   - Topic: `wokwi-weather` (cần thiết cho node `mqttTrigger`).
3. **InfluxDB**:
   - Cài đặt InfluxDB 2.x trên cùng máy chủ hoặc VPS.
   - URL: `http://localhost:8086` (hoặc thay đổi trong node `httpRequest`).
4. **n8n Self-hosted**:
   - Cài đặt n8n trên VPS (hướng dẫn: [n8n.io/docs](https://n8n.io/docs/)).
   - Node `mqttTrigger` cần **credentials MQTT** (tên host, port, username/password nếu có).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/4004](https://n8n.io/workflows/4004) (ấn "Download").
- **Import vào n8n Editor**:
  - Mở n8n Dashboard → **Create Workflow** → **Import** → Chọn file JSON.
  - **Hoặc** copy toàn bộ JSON và paste vào **Import Workflow** trong Editor.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này có **3 node chính**, các sếp cần cấu hình kỹ lưỡng:

##### **Node 1: Remote Sensor MQTT Trigger (`mqttTrigger`)**
- **Credentials**:
  - Tạo **MQTT Credentials** trong n8n:
    - **Host**: `localhost` (nếu Mosquitto chạy trên cùng máy) hoặc IP VPS của bạn.
    - **Port**: `1883` (mặc định).
    - **Username/Password**: Nếu Mosquitto yêu cầu.
  - **Topic**: `wokwi-weather` (không đổi).
- **Lưu ý**:
  - Chắc chắn thiết bị ESP32 đã cấu hình gửi dữ liệu đến topic này.
  - Dữ liệu từ DHT22 sẽ có định dạng:
    ```json
    {
      "temperature": 25.5,
      "humidity": 60.0
    }
    ```

##### **Node 2: Payload Data Preparation (`code`)**
- **Mã JavaScript**:
  ```javascript
  // Kiểm tra và chuẩn hóa dữ liệu
  const payload = {
    temperature: Number($input.all().temperature),
    humidity: Number($input.all().humidity),
    timestamp: new Date().toISOString()
  };
  return payload;
  ```
- **Lưu ý**:
  - Node này **chuyển đổi dữ liệu thô thành JSON chuẩn** với trường `timestamp` để InfluxDB phân tích.
  - Nếu dữ liệu từ ESP32 không đúng định dạng, sửa mã ở đây.

##### **Node 3: Data Ingest to InfluxDB (`httpRequest`)**
- **Method**: `POST`
- **URL**: `http://localhost:8086/api/v2/write?bucket=iot_data&org=your-org&precision=s`
  - **Thay đổi**:
    - `bucket=iot_data`: Tên bucket trong InfluxDB (tạo trước trong InfluxDB UI).
    - `org=your-org`: Tên organization trong InfluxDB.
    - `precision=s`: Độ chính xác thời gian (giây).
- **Headers**:
  - `Content-Type`: `application/json`
  - `Authorization`: `Token YOUR_INFLUXDB_API_TOKEN` (tạo token trong InfluxDB).
- **Body (JSON)**:
  ```json
  {
    "temperature": "{{$node["Payload data preparation"].json["temperature"]}}",
    "humidity": "{{$node["Payload data preparation"].json["humidity"]}}",
    "time": "{{$node["Payload data preparation"].json["timestamp"]}}"
  }
  ```
- **Lưu ý**:
  - **Tạo bucket và token** trong InfluxDB trước:
    1. Mở InfluxDB UI → **Buckets** → Tạo bucket `iot_data`.
    2. **Users** → Tạo user → **Tokens** → Tạo token và sao chép.
  - **Test API InfluxDB**:
    ```bash
    curl -X POST "http://localhost:8086/api/v2/write?bucket=iot_data&org=your-org&precision=s" \
    -H "Authorization: Token YOUR_TOKEN" \
    -H "Content-Type: application/json" \
    -d '{"temperature":25.5,"humidity":60.0,"time":"2024-01-01T00:00:00Z"}'
    ```
    Nếu thành công, workflow sẽ hoạt động.

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Gửi một dữ liệu mẫu từ ESP32 (giống định dạng trên) để kiểm tra.
  - Kiểm tra InfluxDB UI → **Buckets** → `iot_data` → **Explore** để xem dữ liệu đã lưu.
- **Bật Active**:
  - Đánh dấu workflow thành **Active** trong n8n Dashboard.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết Nối với Grafana**:
   - Cài đặt Grafana và kết nối với InfluxDB để tạo **dashboard theo dõi nhiệt độ/độ ẩm thực thời**.
   - Hướng dẫn: [InfluxData Grafana Docs](https://grafana.com/docs/grafana/latest/datasources/influxdb/).

2. **Cảnh Báo Ngưỡng**:
   - Thêm node **Slack/Telegram** để gửi thông báo khi nhiệt độ > 30°C hoặc độ ẩm > 80%.
   - Ví dụ:
     ```javascript
     // Trong node code, thêm logic:
     if ($node["Payload data preparation"].json.temperature > 30) {
       return { alert: "Temperature too high!" };
     }
     ```
     Sau đó kết nối với node **Slack Webhook**.

3. **Lưu Log**:
   - Thêm node **Google Sheets** hoặc **Airtable** để lưu lịch sử dữ liệu dài hạn.

4. **Scale Up**:
   - Nếu có nhiều thiết bị, sử dụng **MQTT Wildcard Topic** (`wokwi-weather/#`) và phân loại dữ liệu trong node `code`.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp quản lý hệ thống IoT xa lãnh, giúp:
✔ **Tự động hóa thu thập dữ liệu** từ ESP32/DHT22.
✔ **Lưu trữ hệ thống** vào InfluxDB.
✔ **Theo dõi thực thời** và phân tích dễ dàng với Grafana.

**Hành động ngay!**
1. **Cài đặt VPS** (n8n + InfluxDB + Mosquitto).
2. **Import workflow** và cấu hình MQTT/InfluxDB.
3. **Test và bật hoạt động** để bắt đầu theo dõi dữ liệu IoT!

---
**Có thắc mắc?** Để lại comment bên dưới hoặc liên hệ qua [n8n Community](https://community.n8n.io/).