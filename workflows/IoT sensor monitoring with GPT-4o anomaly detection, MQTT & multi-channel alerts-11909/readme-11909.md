---
title: "🚀 Giám sát cảm biến IoT thông minh với GPT-4o, MQTT và Cảnh báo đa kênh"
description: "Xây dựng hệ thống giám sát cảm biến IoT thời gian thực, phát hiện bất thường tự động bằng AI GPT-4o và gửi cảnh báo qua Email, Slack, đồng thời lưu trữ lịch sử."
slug: "giam-sat-cam-bien-iot-gpt-4o-mqtt-canh-bao"
tags: [n8n, automation, no-code, iot, ai, openai, mqtt]
keywords: [n8n workflow, giám sát iot, gpt-4o anomaly detection, mqtt trigger, cảnh báo slack email, tự động hóa n8n]
---

# 🚀 Giám sát cảm biến IoT thông minh với GPT-4o, MQTT và Cảnh báo đa kênh

Các kỹ sư và quản lý hệ thống IoT thường đối mặt với bài toán đau đầu: Làm thế nào để giám sát hàng ngàn luồng dữ liệu cảm biến thời gian thực, phát hiện chính xác các bất thường (rò rỉ nhiệt độ, quá tải áp suất...) mà không bị ngập trong hàng đống cảnh báo giả (false alarm)? Việc cấu hình các ngưỡng cố định (thresholds) truyền thống thường rất cứng nhắc và kém hiệu quả.

Workflow n8n này chính là giải pháp tự động hóa 100% không cần code, kết hợp hoàn hảo giữa giao thức **MQTT**, trí tuệ nhân tạo **GPT-4o (OpenAI)** để phân tích ngữ cảnh, và hệ thống cảnh báo đa kênh (Slack, Gmail) cùng khả năng lưu trữ tự động vào Google Sheets.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phát hiện bất thường bằng AI:** Không chỉ dựa vào ngưỡng thô, AI Agent (GPT-4o-mini) phân tích sâu xu hướng dữ liệu, đưa ra lý do và đề xuất khắc phục cụ thể.
- **Tiết kiệm thời gian & Loại bỏ nhiễu:** Tự động tạo mã băm dữ liệu (SHA256) và lọc bỏ các bản ghi trùng lặp trước khi phân tích.
- **Cảnh báo đa kênh thông minh:** Tự động phân loại mức độ nghiêm trọng (Critical, Warning) để bắn tin nhắn tức thời qua Slack hoặc gửi Email khẩn cấp.
- **Lưu trữ dữ liệu xuyên suốt:** Tự động ghi nhận toàn bộ lịch sử cảm biến và kết quả phân tích vào Google Sheets để phục vụ báo cáo.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và thông tin sau:
- **MQTT Broker:** Thông tin kết nối (Host, Port, Username, Password) để nhận dữ liệu cảm biến.
- **OpenAI API Key:** Để sử dụng mô hình `gpt-4o-mini` trong AI Agent.
- **Slack Bot Token:** Tài khoản Bot đã được cấp quyền gửi tin nhắn vào kênh Slack.
- **Google Sheets & Gmail:** Tài khoản kết nối qua OAuth2 để ghi log và gửi email cảnh báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Copy mã JSON của workflow hoặc tải file JSON từ n8n.
- Mở n8n Editor, chọn **Add workflow** -> **Import from File** (hoặc dán trực tiếp vào workspace).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các node trọng điểm sau đây:
- **MQTT Sensor Trigger**: Điền thông tin kết nối MQTT Broker và định nghĩa Topic cảm biến cần lắng nghe.
- **Define Sensor Thresholds**: Thiết lập các thông số ngưỡng cơ bản (nếu cần thiết cho logic phụ trợ).
- **AI Anomaly Detector & OpenAI Chat Model**: Chọn đúng OpenAI Credentials và cấu hình model `gpt-4o-mini` để AI hiểu được ngữ cảnh dữ liệu cảm biến.
- **Route by Switch**: Kiểm tra lại các điều kiện rẽ nhánh (Routing) dựa trên mức độ nghiêm trọng mà AI phân tích (Critical, Warning, Info).
- **Send Critical Email (Gmail) & Slack Critical/Warning Alert**: Liên kết tài khoản Gmail và Slack cá nhân/doanh nghiệp của sếp.
- **Archive to Google Sheets**: Chọn file Google Sheets đích và map đúng các cột dữ liệu (Timestamp, Sensor ID, Value, AI Analysis, Status).

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và gửi một gói tin MQTT mẫu để test luồng chạy.
- Kiểm tra kết quả trên Slack, Gmail và Google Sheets.
- Nếu mọi thứ mượt mà, bật công tắc **Active** góc trên cùng bên phải để hệ thống tự động chạy 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram:** Thay thế hoặc bổ sung node Slack bằng Telegram Bot để nhận cảnh báo ngay trên điện thoại cá nhân với tốc độ bàn thờ.
- **Webhooks bổ sung:** Kết hợp thêm node Webhook để các hệ thống phần cứng khác (Edge Device, PLC) có thể chủ động đẩy dữ liệu thủ công khi cần.
- **Báo cáo định kỳ:** Thêm Schedule Trigger chạy vào cuối tuần để tổng hợp số liệu bất thường từ Google Sheets và gửi báo cáo tóm tắt qua Email cho ban quản lý.

### 📌 Kết luận
Hệ thống giám sát cảm biến IoT tích hợp AI này giúp tự động hóa hoàn toàn khâu kiểm tra và cảnh báo sự cố phần cứng, giúp doanh nghiệp chủ động xử lý rủi ro trước khi chúng trở thành thảm họa. Chúc các sếp cài đặt thành công!