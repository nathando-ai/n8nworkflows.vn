---
title: "🚀 Tự động làm sạch & lưu dữ liệu cảm biến IoT vào InfluxDB"
description: "Workflow n8n nhận dữ liệu cảm biến IoT, làm sạch, chuyển đổi và ghi vào InfluxDB chỉ trong vài giây, giúp các sếp giảm lỗi và tiết kiệm thời gian."
slug: "tu-dong-lam-sach-luu-du-lieu-cam-bien-iot-vao-influxdb"
tags: [n8n, automation, no-code, iot, influxdb, data-cleaning]
keywords: [n8n workflow, tự động hóa, IoT, InfluxDB, data cleaning]
---

# 🚀 Tự động làm sạch & lưu dữ liệu cảm biến IoT vào InfluxDB

Các sếp thường phải đối mặt với việc **dữ liệu cảm biến IoT** được gửi về dạng thô, lộn xộn, thậm chí có giá trị sai lệch hoặc trùng lặp. Việc **xử lý thủ công** mỗi lần nhận dữ liệu không những tốn thời gian mà còn dễ gây lỗi, ảnh hưởng đến độ tin cậy của hệ thống giám sát.

💡 **Giải pháp:** Workflow n8n này sẽ nhận dữ liệu từ webhook, tự động **làm sạch, chuẩn hoá** và **đẩy trực tiếp** vào **InfluxDB** – một cơ sở dữ liệu thời gian thực mạnh mẽ. Hoàn toàn không cần viết code, chỉ cần cấu hình một lần và để nó chạy 24/7.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian:** Dữ liệu được xử lý tự động ngay khi nhận, không cần thao tác thủ công.  
- **Độ chính xác cao:** Loại bỏ giá trị ngoại lệ, chuẩn hoá đơn vị đo, tránh trùng lặp.  
- **Giữ lịch sử liên tục:** Dữ liệu được ghi vào InfluxDB, sẵn sàng cho dashboard Grafana hoặc các công cụ phân tích.  
- **Mở rộng dễ dàng:** Thêm node Slack/Telegram để nhận cảnh báo khi dữ liệu bất thường.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n** (cài đặt trên VPS hoặc Docker).  
- **InfluxDB** (phiên bản 2.x) đã tạo **Organization**, **Bucket** và **API Token** có quyền `write`.  
- **URL** của InfluxDB Write API, ví dụ: `https://your-influxdb.com/api/v2/write?org=YOUR_ORG&bucket=YOUR_BUCKET&precision=s`.  
- **Công cụ kiểm thử** (Postman, curl) để gửi dữ liệu mẫu tới webhook.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Vào **n8n → Workflows → Import**.  
2. Chọn **Upload JSON** và tải file `clean-and-log-iot-to-influxdb.json` (hoặc copy toàn bộ JSON từ nguồn).  
3. Nhấn **Import** → Workflow sẽ xuất hiện trong danh sách.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Dưới đây là **các node** cần cấu hình chi tiết:

| Node | Loại | Cấu hình cần chỉnh |
|------|------|--------------------|
| **Sensor Input** | `webhook` | - **Path:** `sensor-data` <br> - **HTTP Method:** `POST` <br> - **Response Mode:** `Last Node` (để trả về kết quả cuối cùng). |
| **Clean & Transform Data** | `function` | Dán đoạn code sau vào **Function Code** để làm sạch dữ liệu (loại bỏ null, chuyển đổi kiểu, chuẩn hoá timestamp):<br>```js\n// data mẫu: { temperature: "23.5", humidity: "45", ts: "2024-09-22T12:00:00Z" }\nconst raw = items[0].json;\n// Loại bỏ giá trị rỗng\nif (!raw.temperature || !raw.humidity) {\n  throw new Error('Missing sensor values');\n}\n// Chuyển đổi sang số và chuẩn hoá timestamp (giây)\nreturn [{\n  json: {\n    temperature: parseFloat(raw.temperature),\n    humidity: parseFloat(raw.humidity),\n    time: Math.floor(new Date(raw.ts).getTime() / 1000), // epoch seconds\n  }\n}];\n``` |
| **Set Config** | `set` | Thêm các trường sau (đánh dấu **Keep Only Set**):<br> - `measurement` = `"sensor_data"`<br> - `tags` = `{ location: "factory_1", device: "sensor_A" }`<br> - `fields` = `{ temperature: {{$json["temperature"]}}, humidity: {{$json["humidity"]}} }`<br> - `timestamp` = `{{$json["time"]}}` |
| **HTTP Request** | `httpRequest` | **Method:** `POST` <br> **URL:** `https://your-influxdb.com/api/v2/write?org=YOUR_ORG&bucket=YOUR_BUCKET&precision=s` <br> **Authentication:** **Header Auth** → `Authorization: Token YOUR_INFLUXDB_TOKEN` <br> **Headers:** `Content-Type: text/plain` <br> **Body:** `Line Protocol` dạng: `{{ $json["measurement"] }},location={{ $json["tags"]["location"] }},device={{ $json["tags"]["device"] }} temperature={{ $json["fields"]["temperature"] }},humidity={{ $json["fields"]["humidity"] }} {{ $json["timestamp"] }}` |
| **(Optional) Error Handling** | `function` (nếu muốn) | Thêm node **Function** sau `Clean & Transform Data` để log lỗi vào Slack/Telegram. |

> **Lưu ý:** Thay `your-influxdb.com`, `YOUR_ORG`, `YOUR_BUCKET` và `YOUR_INFLUXDB_TOKEN` bằng thông tin thực tế của các sếp.

#### 3. Kích hoạt ⚡️
1. **Test run**: Dùng Postman gửi POST tới `https://<n8n-domain>/webhook/sensor-data` với body JSON mẫu:  
   ```json\n{ \"temperature\": \"23.5\", \"humidity\": \"45\", \"ts\": \"2024-09-22T12:00:00Z\" }\n```  
2. Kiểm tra **Execution Log** của n8n, đảm bảo không có lỗi và dữ liệu đã xuất hiện trong InfluxDB (kiểm tra qua UI hoặc query).  
3. Bật **Active** cho workflow → **Save** → **Activate**.

### ✍️ Mẹo & gợi ý nâng cao
- **Giám sát lỗi:** Thêm node **Slack** hoặc **Telegram** để nhận thông báo khi `Clean & Transform Data` ném lỗi.  
- **Batching:** Nếu lượng dữ liệu lớn, dùng node **SplitInBatches** để gửi từng nhóm 5000 điểm tới InfluxDB, giảm tải mạng.  
- **Dashboard:** Kết nối InfluxDB với **Grafana** để tạo biểu đồ thời gian thực cho nhiệt độ, độ ẩm.  
- **Backup:** Định kỳ (hàng ngày) dùng node **Cron** + **HTTP Request** để export dữ liệu InfluxDB sang file CSV và lưu vào S3/Google Drive.  

### 📌 Kết luận
Với workflow này, các sếp có thể **tự động hoá toàn bộ quy trình** từ nhận dữ liệu cảm biến, làm sạch, chuẩn hoá, tới ghi vào InfluxDB chỉ trong vài giây. Không còn lo lắng về lỗi nhập liệu, không cần viết code, và có thể mở rộng dễ dàng cho các hệ thống IoT phức tạp hơn. Hãy **import ngay**, cấu hình nhanh và để n8n làm việc cho bạn! 🚀