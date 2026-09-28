---
title: "💧 🚀 Tự Động Hóa Theo Dõi Sử Dụng Nước - Ghi Chép Excel + Thông Báo Slack (AI Tự Động Lập Lời Nhắn)"
description: "Workflow tự động hóa theo dõi lượng nước uống hàng ngày, ghi dữ liệu vào Google Sheets và gửi thông báo cá nhân hóa qua Slack với lời nhắn AI. Giúp các sếp tiết kiệm thời gian, theo dõi sức khỏe và duy trì thói quen uống nước hiệu quả."
slug: "tieu-dong-ho-tieu-dung-nuoc-google-sheets-slack"
tags: [n8n, automation, no-code, google-sheets, slack, ai-chatbot, health-tracking]
keywords: [tự động hóa theo dõi nước uống, n8n workflow, ghi chép sức khỏe, thông báo Slack tự động, AI tự động lập lời nhắn, tự động hóa sức khỏe]
---

# 🚀 **Tự Động Hóa Theo Dõi Sử Dụng Nước: Ghi Chép Excel + Thông Báo Slack (AI Tự Động Lập Lời Nhắn)**

## **🔍 Nỗi Đau Của Các Sếp: Theo Dõi Nước Uống Thủ Công Làm Giảm Sức Khỏe**
Các sếp hiện nay thường phải ghi chép lượng nước uống vào ứng dụng hoặc giấy tờ thủ công, dễ quên hoặc không chính xác. Kết quả là:
- **Thói quen uống nước không đều** → ảnh hưởng đến sức khỏe, năng suất làm việc.
- **Không theo dõi được tiến trình** → khó khăn trong việc cải thiện thói quen.
- **Phải nhắc nhở bản thân** → mất thời gian và dễ quên.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Ghi chép lượng nước uống** vào Google Sheets.
✅ **Gửi thông báo Slack cá nhân hóa** với lời nhắn AI tự động lập.
✅ **Hỗ trợ tương tác qua Shortcut iOS** để ghi nhận nước uống một cách nhanh chóng.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần ghi chép thủ công, hệ thống tự động xử lý.
- **Dữ liệu chính xác**: Ghi chép tự động vào Google Sheets, dễ theo dõi và phân tích.
- **Thông báo cá nhân hóa**: Slack tự động gửi lời nhắn động viên với AI, giúp duy trì động lực.
- **Tương tác dễ dàng**: Sử dụng Shortcut iOS để ghi nhận nước uống một cách nhanh chóng.
- **Hỗ trợ sức khỏe**: Theo dõi lượng nước uống hàng ngày, cải thiện thói quen sống lành mạnh.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets**:
   - Một bảng Excel đã thiết lập cột: `Date`, `Time`, `Water (ml)`, `Shortcut URL` (nếu sử dụng Shortcut iOS).
   - **Credentials**: `googleSheetsOAuth2Api` (cài đặt trong n8n).
2. **Tài khoản Slack**:
   - Một workspace Slack để nhận thông báo.
   - **Credentials**: `slackOAuth2Api` (cài đặt trong n8n).
3. **API Key OpenAI**:
   - Đăng ký tại [OpenAI](https://platform.openai.com/) và thêm `openAiApi` vào n8n.
4. **Shortcut iOS (tùy chọn)**:
   - Tạo một Shortcut iOS để ghi nhận nước uống (ví dụ: `darrell_water`).
   - URL mẫu: `shortcuts://run-shortcut?name=darrell_water&input={"value":100,"time":"2025-03-04T16:10:15"}`.
:::

---

## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải workflow từ [đây](https://n8n.io/workflows/3042) hoặc sử dụng file JSON đã cung cấp.
2. Trong n8n Editor, nhấn **Import** và chọn file JSON.
3. Hoặc copy toàn bộ JSON và nhấn **Paste JSON** trong Editor.

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **16 nodes** quan trọng, các sếp cần chú ý cấu hình như sau:

#### **🔹 Node `Schedule Trigger` (Động cơ kích hoạt định kỳ)**
- **Cấu hình**:
  - Chọn thời gian kích hoạt (ví dụ: **mỗi 1 giờ** hoặc **mỗi 2 giờ**).
  - Đảm bảo thời gian này phù hợp với lịch uống nước của các sếp.

#### **🔹 Node `Google Sheets - Get Target` (Lấy mục tiêu nước uống)**
- **Cấu hình**:
  - Chọn **Sheet Name** và **Range** (ví dụ: `Sheet1!A1:D100`).
  - Đảm bảo cột `Date` và `Water (ml)` đã được định nghĩa rõ ràng.

#### **🔹 Node `OpenAI` (Tự động lập lời nhắn AI)**
- **Cấu hình**:
  - Chọn **Model** (ví dụ: `gpt-3.5-turbo`).
  - **Prompt mẫu** (có thể tùy chỉnh):
    ```
    You are a friendly water intake assistant. Suggest a motivational message for the user to drink more water.
    Current time: {{ $node["Wait"].json["time"] }}
    User's target: {{ $node["Google Sheets - Get Target"].json["water_target"] }} ml
    User's current intake: {{ $node["Google Sheets - Get Today Water Log"].json["total_water"] }} ml
    ```
  - **API Key**: Đảm bảo đã thêm `openAiApi` vào n8n.

#### **🔹 Node `Slack send drink notification` (Gửi thông báo Slack)**
- **Cấu hình**:
  - Chọn **Channel** (ví dụ: `#personal`).
  - **Message Template** (có thể tùy chỉnh):
    ```
    *💧 Water Reminder!*
    You have drunk **{{ $node["Google Sheets - Get Today Water Log"].json["total_water"] }} ml** today.
    Your target is **{{ $node["Google Sheets - Get Target"].json["water_target"] }} ml**.
    {{ $node["OpenAI"].json["message"] }}

    [Drink Water Now]({{ $node["slack_action_payload"].json["shortcut_url"] }})
    ```
  - **Buttons**: Thêm nút tương tác để ghi nhận nước uống (ví dụ: `Drink 250ml`, `Drink 500ml`).

#### **🔹 Node `Google Sheets - log water value to sheet` (Ghi dữ liệu vào Excel)**
- **Cấu hình**:
  - Chọn **Sheet Name** và **Range** (ví dụ: `Sheet1!A1:D100`).
  - **Operation**: Chọn `append` để thêm dữ liệu mới vào cuối bảng.
  - **Fields**:
    - `Date`: Ngày hiện tại.
    - `Time`: Thời gian ghi nhận.
    - `Water (ml)`: Lượng nước uống.
    - `Shortcut URL`: Nếu sử dụng Shortcut iOS, truyền URL tương tác.

#### **🔹 Node `If` (Kiểm tra nước uống gần đây)**
- **Cấu hình**:
  - **Condition**: Kiểm tra nếu lượng nước uống trong **30 phút qua** đã được ghi nhận.
  - Nếu **true**, kích hoạt **Node `Wait`** để chờ **3x phút ngẫu nhiên** trước khi gửi thông báo mới.

#### **🔹 Node `Webhook` (Nhận tương tác từ Slack)**
- **Cấu hình**:
  - **Key Parameters**:
    - `path`: `f992f346-0076-4a79-a046-5b5c295bf6c2` (không thay đổi).
    - `httpMethod`: `POST`.
  - **Credentials**: Không cần thêm, chỉ cần giữ nguyên.

---

### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Chạy **Test Run** với dữ liệu mẫu để kiểm tra workflow.
   - Kiểm tra:
     - Slack có nhận được thông báo không?
     - Dữ liệu có được ghi vào Google Sheets không?
     - Tương tác qua Shortcut iOS có hoạt động không?
2. **Bật Active**:
   - Sau khi kiểm tra thành công, bật **Active** để workflow chạy tự động.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết hợp với Telegram**:
   - Thay vì Slack, các sếp có thể gửi thông báo qua Telegram bằng **node Telegram Bot**.
2. **Lưu Log Dữ Liệu**:
   - Sử dụng **node Set** để lưu log hoạt động vào một sheet riêng để theo dõi lịch sử.
3. **Báo Cáo Định Kỳ**:
   - Sử dụng **node Schedule Trigger** để gửi báo cáo tổng hợp hàng tuần qua Email hoặc Slack.
4. **Tích Hợp với Wearable**:
   - Nếu sử dụng Apple Watch hoặc Fitbit, các sếp có thể tự động lấy dữ liệu từ API của thiết bị và so sánh với mục tiêu nước uống.
5. **Cảnh Báo Nước Uống Thiếu**:
   - Thêm **node If** để cảnh báo nếu lượng nước uống dưới 50% mục tiêu.
:::

---

## **📌 Kết Luận**
Workflow **Automated Water Consumption Tracker** là giải pháp **tự động hóa 100% không cần code** giúp các sếp:
✔ **Tiết kiệm thời gian** với ghi chép tự động.
✔ **Theo dõi sức khỏe** một cách chính xác.
✔ **Duy trì thói quen uống nước** với thông báo động viên từ AI.

**Hãy áp dụng ngay và bắt đầu sống lành mạnh hơn!** 💧🚀

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::