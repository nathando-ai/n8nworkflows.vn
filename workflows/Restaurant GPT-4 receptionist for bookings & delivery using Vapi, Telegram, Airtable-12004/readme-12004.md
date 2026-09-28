---
title: "🍽️ **AI Receptionist N8n: Bot Đặt Bàn & Giao Hàng Tự Động Cho Quán Ăn (Telegram + Vapi + Airtable)**"
description: "Workflow AI Receptionist tự động hóa toàn bộ quy trình đặt bàn, đặt hàng giao hàng/takeaway cho quán ăn bằng Telegram Bot + Vapi Voice Agent. Sử dụng GPT-4, Airtable làm database và Google Maps để xác thực địa chỉ. Giúp tiết kiệm 100% thời gian nhân viên, giảm lỗi và cải thiện trải nghiệm khách hàng."
slug: "ai-receptionist-n8n-restaurant-booking-delivery"
tags: [n8n, automation, ai-chatbot, restaurant, telegram-bot, airtable, openai-gpt-4, vapi-voice-agent]
keywords: [n8n workflow restaurant, tự động hóa đặt bàn quán ăn, bot giao hàng tự động, ai receptionist, n8n airtable telegram, đặt hàng qua telegram, vapi voice agent]
---

# 🚀 **AI Receptionist N8n: Bot Đặt Bàn & Giao Hàng Tự Động Cho Quán Ăn**

## **🔥 Giới Thiệu: Giải Pháp Tự Động Hóa Toàn Diện Cho Quán Ăn**
Hiện nay, việc quản lý đặt bàn, đặt hàng giao hàng và takeaway cho quán ăn vẫn phụ thuộc vào nhân viên, dẫn đến những vấn đề như:
- **Thời gian chờ lâu** khi khách gọi điện đặt bàn.
- **Lỗi thông tin** do ghi nhớ sai hoặc ghi nhầm.
- **Không hoạt động 24/7**, khiến khách hàng mất cơ hội đặt trước.
- **Khó theo dõi đơn hàng** và cập nhật trạng thái cho khách.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động hóa toàn bộ quy trình** đặt bàn, đặt hàng, hủy đơn, cập nhật thông tin.
✅ **Hỗ trợ 2 kênh tương tác**: Telegram Bot (text/voice) và Vapi Voice Agent (gọi điện thoại).
✅ **Sử dụng AI GPT-4** để hiểu ý khách hàng và xử lý logic phức tạp (kiểm tra sẵn bàn, tính giá, xác thực địa chỉ).
✅ **Lưu trữ dữ liệu trên Airtable** để quản lý dễ dàng và báo cáo thống kê.
✅ **Xác thực địa chỉ giao hàng** bằng Google Maps API để đảm bảo giao hàng chính xác.
✅ **Hoạt động liên tục 24/7** mà không cần nhân viên.

---
## **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/ngày** của nhân viên reception và phục vụ.
- **Giảm 90% lỗi** trong quá trình đặt bàn/đặt hàng.
- **Cải thiện trải nghiệm khách hàng** với phản hồi tức thời và thông tin chính xác.
- **Quản lý đơn hàng dễ dàng** trên Airtable, theo dõi từ đặt bàn đến giao hàng.
- **Hỗ trợ đa kênh**: Khách có thể đặt bàn qua Telegram, gọi điện thoại (Vapi) hoặc text.
- **Tự động gửi thông báo** (SMS/Telegram) khi đặt bàn thành công, hủy đơn, hoặc cập nhật trạng thái.
- **Cập nhật menu động** từ Airtable, không cần chỉnh sửa thủ công.
:::

---
## **🔧 Yêu Cầu Cần Thiết**
Trước khi triển khai, các sếp cần chuẩn bị:
### **1. Tài Khoản & API Keys**
| **Dịch Vụ**          | **Thông Tin Cần Thiết**                                                                 | **Lưu Ý**                                                                 |
|----------------------|----------------------------------------------------------------------------------------|----------------------------------------------------------------------------|
| **Telegram Bot**     | - Token API từ [@BotFather](https://t.me/BotFather)                                   | Tạo bot mới và thêm vào n8n với tên `telegramApi`.                     |
| **OpenAI (GPT-4)**   | - API Key từ [OpenAI](https://platform.openai.com/account/api-keys)                   | Chọn model `gpt-4-1` trong workflow.                                    |
| **Airtable**         | - API Key và Base ID từ [Airtable](https://airtable.com/api)                          | Sử dụng base mẫu từ [đây](https://airtable.com/appO25aREhJMGVavR/shreEtStEqOedoYTT). |
| **Google Maps API**   | - API Key từ [Google Cloud Console](https://console.cloud.google.com/)                | Chọn API **Geocoding API** và kích hoạt.                              |
| **Vapi (Nếu dùng Voice Agent)** | - API Key từ [Vapi](https://vapi.ai/)                                                | Cần cấu hình trong MCP Server (chi tiết sau).                          |

### **2. Cấu Hình Airtable**
Workflow sử dụng **Airtable** để lưu trữ:
- **Bàn ăn** (Table Availability).
- **Đơn đặt bàn** (Bookings).
- **Đơn hàng** (Orders).
- **Menu** (Menu Items).

**Các bảng cần thiết:**
1. **Tables** (Bàn ăn) – Thông tin về số bàn, sức chứa, trạng thái.
2. **Bookings** (Đặt bàn) – Thông tin khách hàng, thời gian, bàn được đặt.
3. **Orders** (Đơn hàng) – Thông tin đặt hàng, trạng thái, địa chỉ giao hàng.
4. **Menu** (Menu) – Danh sách món ăn, giá, mã sản phẩm.

---
## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Tải JSON và Import**
1. **Tải file JSON** từ [Dropbox](https://www.dropbox.com/scl/fo/r6edgytt26f51vmibntqt/AM49duT1dDbdD2deCu2-J5c?rlkey=l495lzd5926yb5mbxxuj73a39&st=wgjc60dp&dl=0).
2. **Mở n8n Editor** và nhấn **Import** → Chọn file JSON vừa tải.
3. **Xác nhận import** và workflow sẽ hiện lên canvas.

#### **Phương pháp 2: Copy JSON vào Editor**
1. Mở n8n Editor và chọn **Create Workflow**.
2. Nhấn **Import** → Chọn **Paste JSON** và dán nội dung từ file JSON vào.
3. Nhấn **Import** để hoàn tất.

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này phức tạp và có **nhiều node cần cấu hình cẩn thận**. Dưới đây là hướng dẫn chi tiết:

#### **🔹 Cấu Hình MCP Server (Multi-Tool Call Platform)**
MCP Server là "não" của workflow, quản lý tất cả các **tool sub-workflow** (ví dụ: "Book Table", "Calculate Price", "Validate Address").
- **Bước 1**: Tạo một **MCP Server** mới trong n8n.
  - Tạo một workflow mới và thêm node **`mcpTrigger`** (đã có trong workflow).
  - Cấu hình **`path`** trong node này là `451141d4-f7c8-4a46-a1c0-b4fec65aa9d0` (từ file JSON).
- **Bước 2**: Cấu hình **MCP Client** trong node `Restaurant Tool` (type: `mcpClientTool`).
  - Điền **URL MCP Server** vào `url` và **API Key** (nếu có).
  - Chọn **`path`** là `451141d4-f7c8-4a46-a1c0-b4fec65aa9d0`.

#### **🔹 Cấu Hình Telegram Bot**
- **Node `Wait for New Message`** (type: `telegramTrigger`):
  - Chọn **credentials**: `telegramApi`.
  - Điền **`chatId`** của bot (có thể lấy từ Telegram khi tạo bot).
  - Chọn **`resource`**: `message`.
- **Node `Reply`** (type: `telegram`):
  - Chọn **credentials**: `telegramApi`.
  - Điền **`chatId`** của khách hàng (có thể lấy từ node trước).

#### **🔹 Cấu Hình OpenAI (GPT-4)**
- **Node `OpenAI Chat Model`** (type: `lmChatOpenAi`):
  - Chọn **credentials**: `openAiApi`.
  - Đảm bảo **model** được đặt là `gpt-4-1`.
  - Cấu hình **prompt** trong node `AI Agent` (type: `agent`) để phù hợp với ngôn ngữ và logic của quán ăn.
    - Ví dụ:
      ```json
      {
        "role": "system",
        "content": "Bạn là receptionist AI của quán ăn [Tên Quán]. Hãy xử lý các yêu cầu sau:\n
        1. Đặt bàn: Kiểm tra sẵn bàn, tính giá, xác nhận thời gian.\n
        2. Đặt hàng: Xác thực món ăn, tính giá, xác thực địa chỉ giao hàng.\n
        3. Hủy/đổi đơn: Xác nhận với khách trước khi thực hiện.\n
        Sử dụng các tool sau để hỗ trợ:\n
        - Get Menu: Lấy menu từ Airtable.\n
        - Check Availability: Kiểm tra sẵn bàn.\n
        - Validate Address: Xác thực địa chỉ giao hàng.\n
        - Calculate Price: Tính tổng giá đơn hàng.\n
        Trả lời khách bằng tiếng Việt và sử dụng ngôn ngữ thân thiện."
      }
      ```

#### **🔹 Cấu Hình Airtable**
- **Node `Get All Tables`**, `Get Availability`**, `Create a Booking`**, `Update Booking`**, `Delete Booking`** (tất cả type: `airtable`):
  - Chọn **credentials**: `airtableTokenApi`.
  - Điền **`baseId`** và **`tableName`** phù hợp với bảng trong Airtable.
  - Ví dụ:
    - `Get All Tables`: `tableName = "Tables"`.
    - `Create a Booking`: `tableName = "Bookings"`.
- **Node `Get Menu`**:
  - `tableName = "Menu"`.

#### **🔹 Cấu Hình Google Maps API**
- **Node `Geocode Address`** (type: `httpRequest`):
  - Điền **URL**: `https://maps.googleapis.com/maps/api/geocode/json`.
  - Thêm **query parameters**:
    - `address`: `$json["address"]` (địa chỉ từ khách hàng).
    - `key`: `$json["googleMapsApiKey"]` (API Key của Google).
  - Kết quả sẽ trả về tọa độ để kiểm tra khu vực giao hàng.

#### **🔹 Cấu Hình Timezone**
Workflow tự động chuyển đổi thời gian sang **UTC** để tránh xung đột. Các sếp cần:
1. **Thiết lập timezone** trong node `Set Timezone`, `Set Timezone1`, `Set Timezone2`, `Set Timezone3`, `Set Timezone4`.
   - Ví dụ: Nếu quán ở **Hà Nội**, chọn `Asia/Ho_Chi_Minh`.
2. **Node `Convert Time to UTC`** và `Convert Time to UTC1`** sẽ tự động tính toán.

#### **🔹 Thay Thế Node "Do Nothing" bằng SMS/Notification**
Workflow có nhiều node **`noOp`** (ví dụ: `Replace with SMS node`, `Replace with SMS node1`). Các sếp cần thay thế bằng:
- **Node SMS**: Sử dụng **Twilio**, **Firebase Cloud Messaging (FCM)**, hoặc **SMS API** khác.
- **Node Telegram**: Gửi thông báo lại qua Telegram.
- **Node Email**: Gửi email xác nhận (nếu cần).

---
### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run với Dữ Liệu Mẫu**:
   - Gửi một tin nhắn test qua Telegram Bot (ví dụ: "Đặt bàn cho 4 người vào 7h tối mai").
   - Kiểm tra:
     - AI có hiểu yêu cầu không?
     - Workflow có gọi đúng tool không?
     - Dữ liệu có lưu vào Airtable không?
2. **Bật Active Workflow**:
   - Nhấn **Active** trên tab workflow.
   - Kiểm tra log để đảm bảo không có lỗi.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**
### **1. Cấu Hình Vapi Voice Agent (Nếu Sử Dụng)**
Nếu muốn hỗ trợ **gọi điện thoại** thay vì chỉ Telegram:
1. **Cấu hình MCP Server trong Vapi**:
   - Tạo một **AI Agent** mới trong Vapi.
   - Chọn **model**: `gpt-4`.
   - Cấu hình **prompt** giống như trong n8n (đã mô tả trên).
   - Thêm **MCP Tool** vào tab **Tools** của Vapi, điền **URL MCP Server** và **API Key**.
2. **Kết nối Vapi với n8n**:
   - Sử dụng node **`executeWorkflowTrigger`** để gọi các tool từ Vapi.

### **2. Lưu Log & Báo Cáo**
- **Thêm node `Set`** sau các node quan trọng (ví dụ: `Create a Booking`) để lưu log:
  ```json
  {
    "json": {
      "action": "Booking created",
      "bookingId": "$json["id"]",
      "customerPhone": "$json["phone"]",
      "timestamp": "$node["datetime"]["$datetime"]"
    }
  }
  ```
- **Tạo workflow báo cáo định kỳ** (ví dụ: hàng ngày) để thống kê:
  - Số đơn đặt bàn.
  - Số đơn hàng.
  - Doanh thu.

### **3. Cập Nhật Menu Tự Động**
- Sử dụng **Airtable API** hoặc **Google Sheets** để cập nhật menu.
- Thêm node **`executeWorkflowTrigger`** để gọi workflow cập nhật menu khi có thay đổi.

### **4. Hỗ Trợ Nhiều Ngôn Ngữ**
- Cập nhật **prompt** trong node `AI Agent` để hỗ trợ tiếng Anh, Trung Quốc, hoặc tiếng Nhật.
- Ví dụ:
  ```json
  {
    "role": "system",
    "content": "Bạn có thể hiểu và trả lời bằng tiếng Việt, tiếng Anh và tiếng Trung. Hãy luôn sử dụng ngôn ngữ khách hàng yêu cầu."
  }
  ```

### **5. Xác Thực Địa Chỉ Giao Hàng Tự Động**
- Sử dụng **Google Maps API** để kiểm tra:
  - Địa chỉ có trong khu vực giao hàng không?
  - Khoảng cách từ quán đến địa chỉ có trong phạm vi giao hàng không?
- Thêm logic trong node `Check Eligibility`:
  ```javascript
  // Ví dụ: Kiểm tra nếu địa chỉ quá xa (>5km)
  if (distance > 50