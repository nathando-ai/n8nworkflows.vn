---
title: "🌍 **Trợ lý Du lịch H Hands-free với Claude AI: Đặt chuyến bay & lịch trình chỉ bằng giọng nói!**"
description: "Workflow tự động hóa 100% không code giúp các sếp đặt chuyến bay, khách sạn và lịch trình du lịch chỉ bằng giọng nói qua WhatsApp/Telegram, với AI Claude phân tích ý định và tự động book lịch trên Google Calendar. Giảm thời gian lên đến 90% so với cách thủ công!"
slug: "tro-ly-du-lich-hands-free-voi-claude-ai"
tags: [n8n, automation, ai-chatbot, travel-automation, google-calendar, whatsapp-telegram]
keywords: [n8n workflow du lịch, tự động hóa đặt chuyến bay, Claude AI, trợ lý giọng nói, đặt khách sạn tự động, Google Calendar API]
---

# **🌍 Trợ lý Du lịch Hands-free với Claude AI: Đặt chuyến bay & lịch trình chỉ bằng giọng nói!**

### **🚨 Nỗi đau của các sếp khi đặt du lịch thủ công?**
- **Tốn thời gian**: Soạn tin, gọi điện, tra cứu nhiều trang web khác nhau để tìm chuyến bay, khách sạn và hoạt động phù hợp.
- **Rủi ro lỡ quên**: Thường xuyên quên đặt lịch hoặc bỏ lỡ deal giá tốt.
- **Không cá nhân hóa**: Các gợi ý du lịch thường không phù hợp với sở thích, ngân sách hoặc lịch trình cá nhân.
- **Khó theo dõi**: Phải ghi chép thủ công lịch trình và lịch hẹn, dễ bị nhầm lẫn.

**Giải pháp?** **Workflow này tự động hóa toàn bộ quy trình du lịch chỉ bằng giọng nói!** Các sếp chỉ cần gửi **giọng nói** qua WhatsApp hoặc Telegram, AI Claude sẽ:
✅ **Hiểu ý định** (đi đâu, khi nào, với ai, ngân sách bao nhiêu).
✅ **Tìm kiếm đa nguồn** (chuyến bay Skyscanner, khách sạn Booking.com, hoạt động du lịch).
✅ **Lọc và xếp hạng** theo sở thích cá nhân.
✅ **Tự động book lịch** trên Google Calendar.
✅ **Trả lời bằng giọng nói** và gửi liên kết đặt vé ngay.

---
## **🎯 Kết quả các sếp nhận được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm thời gian**: Đặt du lịch chỉ trong **vài giây** thay vì 30-60 phút thủ công.
- **Chính xác 100%**: AI phân tích ý định và lọc kết quả phù hợp với ngân sách, sở thích.
- **Tự động hóa hoàn toàn**: Không cần nhớ ghi nhớ, lịch trình được cập nhật ngay trên Google Calendar.
- **Trải nghiệm cá nhân hóa**: AI nhớ lịch sử du lịch và ưu tiên gợi ý phù hợp.
- **Hands-free**: Đặt du lịch **không cần tay** (chỉ cần nói).
- **Giao tiếp đa kênh**: Hỗ trợ **WhatsApp và Telegram**, phù hợp với cách sử dụng hàng ngày.
:::

---
## **🔧 Yêu cầu cần thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI SỬ DỤNG**]
Để workflow hoạt động, các sếp cần chuẩn bị:
### **1. Tài khoản & API Keys**
| **Dịch vụ**               | **Mô tả**                                                                 | **Liên kết đăng ký**                                                                 |
|---------------------------|-----------------------------------------------------------------------------|---------------------------------------------------------------------------------------|
| **Anthropic API**         | API Claude AI (dùng cho phân tích ý định và trả lời tự nhiên).              | [Đăng ký miễn phí](https://www.anthropic.com/api)                                   |
| **OpenAI Whisper API**    | API chuyển giọng nói thành văn bản (transcription).                        | [Đăng ký miễn phí](https://platform.openai.com/)                                    |
| **WhatsApp Business API** | API nhận và gửi tin nhắn giọng nói qua WhatsApp.                          | [Đăng ký WhatsApp Business](https://developers.facebook.com/docs/whatsapp/cloud-api/) |
| **Telegram Bot API**      | API nhận và gửi tin nhắn giọng nói qua Telegram.                          | [Tạo bot Telegram](https://core.telegram.org/bots)                                  |
| **Google Calendar API**   | API tự động thêm sự kiện du lịch vào lịch Google.                         | [Bật Google Calendar API](https://developers.google.com/calendar/api/guides/overview) |
| **Skyscanner API**        | API tìm kiếm chuyến bay.                                                  | [Đăng ký Skyscanner API](https://partners.skyscanner.com/)                        |
| **Booking.com API**       | API tìm kiếm khách sạn.                                                    | [Đăng ký Booking.com API](https://developer.booking.com/)                           |
| **Google Sheets**         | Lưu trữ thông tin cá nhân và lịch sử đối thoại.                          | [Tạo Google Sheet](https://sheets.new)                                               |
| **VPS Self-hosted**       | Để workflow chạy 24/7.                                                     | 👉 [Đăng ký VPS TinoHost (Mã giảm: **VPSN8N**)](https://tino.vn/vps-n8n?affid=388)  |

### **2. Cấu hình thêm**
- **Tài khoản WhatsApp Business** (đăng ký tại [Meta for Business](https://business.facebook.com/)).
- **Bot Telegram** (tạo tại [@BotFather](https://t.me/BotFather)).
- **Google Sheet** với 2 tab:
  - `User_Profile`: Thông tin cá nhân (ngân sách, sở thích, lịch sử du lịch).
  - `Conversation_History`: Lịch sử các cuộc trò chuyện để AI nhớ context.

---
## **🚀 Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/14914](https://n8n.io/workflows/14914).
2. **Nhấn "Import"** trong n8n Editor.
3. **Chọn file JSON** và nhấn "Import Workflow".

#### **Phương pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ mã JSON** từ [n8n.io/workflows/14914](https://n8n.io/workflows/14914).
2. Trong n8n Editor, nhấn **"Import"** → **"Paste JSON"**.
3. **Chọn "Import"** để thêm workflow.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này **phức tạp** và cần cấu hình cẩn thận. Dưới đây là **các node quan trọng** cần thiết lập:

#### **🔹 Node 1: WhatsApp & Telegram Webhook**
- **Cấu hình WhatsApp Webhook**:
  - Đăng ký **WhatsApp Business API** và lấy **Phone Number ID**.
  - Trong node **"WhatsApp Voice Message Webhook"**, điền:
    - `path`: `whatsapp-voice`
    - `httpMethod`: `POST`
    - **Credentials**: Thêm `httpHeaderAuth` với `Authorization: Bearer <API_KEY>`.
  - **Test**: Gửi tin nhắn giọng nói đến số WhatsApp của bạn để kiểm tra.

- **Cấu hình Telegram Webhook**:
  - Trong node **"Telegram Voice Note Webhook"**, điền:
    - `path`: `telegram-voice`
    - `httpMethod`: `POST`
    - **Credentials**: Thêm `telegramApi` với `token` từ bot Telegram.

#### **🔹 Node 2: Transcribe Audio (OpenAI Whisper)**
- Trong node **"Transcribe Audio with OpenAI Whisper"**:
  - **Credentials**: Thêm `httpHeaderAuth` với `Authorization: Bearer <OPENAI_API_KEY>`.
  - **URL**: `https://api.openai.com/v1/audio/transcriptions`.
  - **Body**:
    ```json
    {
      "model": "whisper-1",
      "file": "{{$node["Download Audio File"].json["file_url"]}}",
      "response_format": "text"
    }
    ```

#### **🔹 Node 3: Claude AI Intent Classification**
- Trong node **"Claude AI Intent Classification & Entity Extraction"**:
  - **Credentials**: Thêm `anthropicApi` với `API_KEY`.
  - **Prompt**: AI sẽ phân tích ý định du lịch (ví dụ: "Đi Hà Nội tháng 12, 3 ngày, ngân sách 5 triệu").
  - **Output**: Trả về **loại chuyến bay** (đi lại), **khách sạn** (phòng nghỉ), **hoạt động** (tham quan).

#### **🔹 Node 4: Fetch User Profile & Preferences**
- Trong node **"Fetch User Profile & Preferences"**:
  - **Google Sheets Credentials**: Thêm `googleSheetsOAuth2Api`.
  - **Sheet Name**: `User_Profile`.
  - **Range**: `A1:D100` (đảm bảo có cột: `Name`, `Budget`, `Preferred_Airline`, `Past_Trips`).

#### **🔹 Node 5: Search Flights, Hotels & Activities**
- **Skyscanner API**:
  - Trong node **"Search Flights"**, điền:
    - `URL`: `https://api.skyscanner.net/apiservices/browsequeries`.
    - **Headers**: `AppId`, `AppKey` từ Skyscanner.
    - **Body**:
      ```json
      {
        "query": {
          "originplace": "{{$json["origin"]}}",
          "destinationplace": "{{$json["destination"]}}",
          "outbounddate": "{{$json["outbound_date"]}}"
        }
      }
      ```
- **Booking.com API**:
  - Trong node **"Search Hotels"**, điền:
    - `URL`: `https://api.booking.com`.
    - **Headers**: `Authorization: Bearer <BOOKING_API_KEY>`.
    - **Body**:
      ```json
      {
        "destination_id": "{{$json["destination_id"]}}",
        "checkin_date": "{{$json["checkin_date"]}}",
        "checkout_date": "{{$json["checkout_date"]}}",
        "room": [
          {
            "adults": 1,
            "children": []
          }
        ]
      }
      ```

#### **🔹 Node 6: Parse Response & Create Calendar Event**
- Trong node **"Parse Response & Create Calendar Event"**:
  - **Code**: Xử lý kết quả từ Claude AI và tạo **event** cho Google Calendar.
  - **Ví dụ**:
    ```javascript
    // Example code to extract event details
    const event = {
      summary: `Chuyến bay ${data.flight.airline} - ${data.flight.date}`,
      description: `Điểm đến: ${data.destination}\nKhách sạn: ${data.hotel.name}`,
      start: {
        dateTime: data.flight.departure_time,
        timeZone: "Asia/HoChiMinh"
      },
      end: {
        dateTime: data.flight.arrival_time,
        timeZone: "Asia/HoChiMinh"
      }
    };
    return event;
    ```

#### **🔹 Node 7: Send WhatsApp & Telegram Response**
- **WhatsApp**:
  - Node **"Send WhatsApp Response"** cần:
    - `URL`: `https://graph.facebook.com/v18.0/<PHONE_NUMBER_ID>/messages`.
    - **Body**:
      ```json
      {
        "messaging_product": "whatsapp",
        "to": "<RECIPIENT_PHONE_NUMBER>",
        "type": "text",
        "text": {
          "body": "{{$json["response"]}}"
        }
      }
      ```
- **Telegram**:
  - Node **"Send Telegram Response"** cần:
    - `chat_id`: ID chat của bot (lấy từ Telegram).
    - **Text**: `{{$json["response"]}}`.

---
### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Gửi **giọng nói** qua WhatsApp/Telegram (ví dụ: "Đi Đà Lạt tháng 12, 3 ngày").
   - Kiểm tra **Google Calendar** xem sự kiện có được tạo không.
   - Kiểm tra **Google Sheet** xem lịch sử cuộc trò chuyện có được lưu không.

2. **Bật Active**:
   - Trong n8n Editor, chuyển **Active** từ `false` sang `true`.

---
## **✍️ Mẹo & gợi ý nâng cao**
:::tip[**CẬP NHẬT & TỐT HÓA WORKFLOW**]
1. **Thêm Slack/Email Notification**:
   - Sử dụng node **Slack** hoặc **Email** để thông báo khi có **deal giá tốt** hoặc **sự kiện sắp đến**.
   - **Ví dụ**:
     ```json
     {
       "blocks": [
         {
           "type": "section",
           "text": {
             "type": "mrkdwn",
             "text": "*Cảnh báo:* Giá vé máy bay giảm 20% cho chuyến bay *{{$json["flight"]}}*!"
           }
         }
       ]
     }
     ```

2. **Lưu Log Chi tiết**:
   - Thêm node **Google Sheets** để lưu **tất cả cuộc trò chuyện** và **kết quả tìm kiếm** vào một sheet riêng.
   - **Cột cần lưu**: `Timestamp`, `User_ID`, `Intent`, `Response`, `Status`.

3. **Gửi Báo cáo Định kỳ**:
   - Sử dụng **n8n Scheduler** để chạy workflow hàng tuần và gửi **báo cáo du lịch** qua Email/Slack.
   - **Ví dụ**:
     - "Lịch trình du lịch tháng này: 2 chuyến bay, 1 khách sạn, 3 hoạt động."

4. **Kết hợp với Zapier/Make**:
   - Nếu cần **tích hợp thêm dịch vụ** (ví dụ: Airbnb, Uber), sử dụng **Zapier** hoặc **Make** để mở rộng.

5. **Optimize Claude AI Prompt**:
   - Cập nhật **prompt** trong node **"Claude AI Intent Classification"** để AI hiểu rõ hơn về:
     - **Ngôn ngữ địa phương** (ví dụ: "Đi Sài Gòn" thay vì "Hồ Chí Minh").
     - **Yêu cầu đặc biệt** (ví dụ: "Không muốn khách sạn có bể bơi").

---
## **📌 Kết luận**
Workflow này **giải phóng tay chân** cho các sếp trong việc đặt du lịch, đồng thời **tăng cường trải nghiệm cá nhân hóa** nhờ AI. **Chỉ cần nói là AI làm hết!**

### **🚀 Bắt đầu ngay!**
1. **Chuẩn bị tài khoản** (n8n, WhatsApp, Telegram, Google Calendar, API Keys).
2. **Import workflow** và **cấu hình các node** theo hướng dẫn.
3. **Test với giọng nói** và **bật Active** để tự động hóa du lịch!

**