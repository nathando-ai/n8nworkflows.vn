---
title: "🌍 Tự Động Hoàn Chỉnh Lịch Trình Du Lịch Tối Ưu Với AI Gemini, Máy Bay Amadeus & Khách Sạn Airbnb - Không Cần Code!"
description: "Workflow tự động hóa tạo lịch trình du lịch cá nhân hóa, tìm kiếm chuyến bay giá rẻ từ Amadeus, và đặt phòng Airbnb thông minh với AI Gemini AI - tiết kiệm thời gian lên đến 80% so với thủ công."
slug: "tieu-dong-hoan-chinh-lich-trinh-du-lich-ai-gemini-amadeus-airbnb"
tags: [n8n, automation, ai-chatbot, du-lich, amadeus, airbnb, gemini-ai, no-code]
keywords: [n8n workflow du lịch, tự động hóa lịch trình du lịch, AI Gemini du lịch, Amadeus API, Airbnb API, tự động đặt phòng du lịch]
---

# 🚀 **Tự Động Hoàn Chỉnh Lịch Trình Du Lịch Tối Ưu Với AI Gemini, Amadeus & Airbnb - Không Cần Code!**

### **📌 Nỗi Đau Của Các Sếp Khi Lên Kế Hoạch Du Lịch**
Bạn đã bao giờ phải:
- **Tìm kiếm và so sánh hàng trăm chuyến bay** để tìm giá tốt nhất?
- **Lựa chọn khách sạn phù hợp** với ngân sách và vị trí?
- **Tạo lịch trình chi tiết** từ điểm đến đến điểm đến, bao gồm thời gian di chuyển, hoạt động, và ngủ nghỉ?
- **Lo lắng về sự thay đổi của thời tiết hoặc giá vé** sau khi đã đặt?

Với **Workflow này**, các sếp sẽ **tự động hóa toàn bộ quy trình** chỉ bằng một yêu cầu đơn giản qua **Webhook** hoặc **Slack/Telegram**. AI **Gemini** sẽ phân tích yêu cầu, **Amadeus API** sẽ tìm kiếm chuyến bay giá rẻ nhất, **Airbnb API** sẽ lọc ra những lựa chọn phù hợp, và cuối cùng là **lịch trình hoàn chỉnh** với thời gian, địa điểm, và gợi ý hoạt động.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian lên đến 80%** so với thủ công (không cần tra cứu, so sánh, và tính toán thủ công).
✅ **Lịch trình cá nhân hóa** dựa trên yêu cầu cụ thể (ngày đi, điểm đến, ngân sách, sở thích).
✅ **Tìm kiếm chuyến bay giá rẻ nhất** từ Amadeus API (không cần phải check nhiều trang web).
✅ **Lựa chọn khách sạn phù hợp** từ Airbnb (đảm bảo an toàn và phù hợp với ngân sách).
✅ **Hoạt động liên tục 24/7** (không phụ thuộc vào giờ làm việc của cá nhân).
✅ **Cập nhật tự động** khi có thay đổi giá vé hoặc thời tiết (nếu kết hợp với các API mở rộng).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Amadeus API** (để tìm kiếm chuyến bay):
   - [Đăng ký API Amadeus](https://developers.amadeus.com/) (miễn phí với giới hạn).
   - **API Key** và **Client ID/Secret** (cần thiết cho `Flight Search with fare` node).
2. **Tài khoản Airbnb API** (để tìm kiếm và đặt phòng):
   - [Đăng ký Airbnb API](https://www.airbnb.com/api) (cần liên hệ với Airbnb để được cấp).
   - **Access Token** và **Client ID** (cần thiết cho `Flight Data + Airbnb Listings` node).
3. **Google Vertex AI API Key** (để sử dụng Gemini AI):
   - [Cài đặt API Key Vertex AI](https://cloud.google.com/vertex-ai/docs/general/access/access-control-overview).
   - **API Key** (cần thiết cho `Google Vertex Chat Model` node).
4. **Credentials cho n8n**:
   - **MCP Client Tool** (nếu sử dụng MCP để quản lý công cụ).
   - **Webhook URL** (để nhận yêu cầu từ Slack/Telegram hoặc ứng dụng khác).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/6652) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** → Nhấn `Import` → Dán JSON hoặc tải file `.json`.
- **Lưu workflow** với tên mới (ví dụ: `DuLichCuaToi`).

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **10 node**, nhưng **3 node chính cần cấu hình kỹ**:
##### **A. Webhook (Nhận Yêu Cầu)**
- **Node**: `Webhook`
- **Cấu hình**:
  - **Method**: `POST` (để nhận dữ liệu từ Slack/Telegram hoặc ứng dụng khác).
  - **Credentials**: Tạo một **Webhook Credential** mới trong n8n (để bảo mật).
  - **URL**: Lưu ý URL này để gửi yêu cầu (ví dụ: `https://tên-vps-của-bạn/n8n/webhook/your-webhook-id`).

##### **B. Google Vertex Chat Model (AI Gemini)**
- **Node**: `Google Vertex Chat Model`
- **Cấu hình**:
  - **API Key**: Điền **API Key Vertex AI** (từ Google Cloud).
  - **Model**: Chọn `gemini-pro` (hoặc phiên bản mới nhất).
  - **Prompt**: AI sẽ tự động tạo prompt từ dữ liệu đầu vào (không cần chỉnh sửa).
  - **Yêu cầu**: Đảm bảo **ngôn ngữ đầu vào** là tiếng Việt (ví dụ: `"Tôi muốn đi du lịch Hà Nội từ ngày 15/12 đến 20/12, ngân sách 10 triệu, yêu cầu khách sạn 4 sao và có bể bơi"`).

##### **C. Flight Search with Amadeus (Tìm Chuyến Bay)**
- **Node**: `Flight Search with fare`
- **Cấu hình**:
  - **Headers**:
    - `Authorization`: `Bearer {API_KEY_AMADEUS}`.
    - `Content-Type`: `application/json`.
  - **Body**:
    ```json
    {
      "originLocationCode": "HAN", // Mã sân bay xuất phát (Hà Nội)
      "destinationLocationCode": "SGN", // Mã sân bay đến (Sài Gòn)
      "departureDate": "2024-12-15", // Ngày đi
      "returnDate": "2024-12-20", // Ngày về
      "maxPrice": 10000000 // Ngân sách tối đa (đơn vị: VND)
    }
    ```
  - **Lưu ý**:
    - Thay đổi `originLocationCode`, `destinationLocationCode`, và `departureDate` theo yêu cầu.
    - **API Amadeus** có giới hạn free tier (nên kiểm tra tài liệu [đây](https://developers.amadeus.com/)).

##### **D. Flight Data + Airbnb Listings (Xử Lý Dữ Liệu)**
- **Node**: `Grabbing Clean Data` (Code) và `Flight Data + Airbnb Listings` (Code)
- **Cấu hình**:
  - **Node `Grabbing Clean Data`**:
    - Sử dụng **JavaScript** để xử lý dữ liệu từ Amadeus (lọc chuyến bay phù hợp, tính thời gian bay, giá vé).
    - **Mẫu code tham khảo**:
      ```javascript
      // Lấy dữ liệu từ node trước
      const flights = $input.all();
      const cleanedFlights = flights.map(flight => ({
        price: flight.offerDetails.totalPrice.amount,
        departure: flight.itineraries[0].departure.iataCode,
        arrival: flight.itineraries[0].arrival.iataCode,
        date: flight.itineraries[0].departure.at
      }));
      return cleanedFlights;
      ```
  - **Node `Flight Data + Airbnb Listings`**:
    - Sử dụng **API Airbnb** để tìm khách sạn phù hợp (tương tự Amadeus).
    - **Mẫu code tham khảo**:
      ```javascript
      // Gọi API Airbnb (cần thay thế URL và headers)
      const response = await $http.request({
        method: 'GET',
        url: 'https://api.airbnb.com/v1/search',
        headers: {
          'Authorization': 'Bearer {AIRBNB_ACCESS_TOKEN}',
          'Content-Type': 'application/json'
        },
        params: {
          location: 'Hà Nội',
          check_in: '2024-12-15',
          check_out: '2024-12-20',
          price_max: 1000000
        }
      });
      return response.json().results;
      ```

##### **E. AI Agent (Tạo Lịch Trình)**
- **Node**: `AI Agent`
- **Cấu hình**:
  - **Tool**: Chọn `Google Vertex Chat Model` (đã cấu hình trước).
  - **Prompt**: AI sẽ tự động tạo lịch trình từ dữ liệu chuyến bay và khách sạn.
  - **Yêu cầu**:
    - Đảm bảo **dữ liệu đầu vào** (chuyến bay + khách sạn) được truyền đúng vào AI Agent.
    - **Mẫu yêu cầu**:
      ```
      Tôi có dữ liệu chuyến bay và khách sạn sau:
      - Chuyến bay: {flights}
      - Khách sạn: {airbnbListings}
      Hãy tạo một lịch trình chi tiết từ ngày {departureDate} đến {returnDate}, bao gồm:
      1. Thời gian di chuyển.
      2. Hoạt động mỗi ngày (thăm quan, ăn uống, nghỉ ngơi).
      3. Gợi ý điểm ăn uống gần khách sạn.
      ```

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Gửi một yêu cầu mẫu qua **Webhook** (ví dụ: `POST` với JSON sau):
    ```json
    {
      "destination": "Hà Nội",
      "departureDate": "2024-12-15",
      "returnDate": "2024-12-20",
      "budget": 10000000,
      "preferences": ["4 sao", "có bể bơi"]
    }
    ```
  - Kiểm tra **output** của workflow để đảm bảo dữ liệu đúng.
- **Bật Active**:
  - Nhấn `Active` trên workflow trong n8n Editor.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết Nối Với Slack/Telegram**:
   - Sử dụng **node `n8n-nodes-slack`** hoặc **`n8n-nodes-telegram`** để nhận yêu cầu từ chatbot.
   - **Cách làm**:
     - Tạo một **Webhook Credential** mới.
     - Gửi yêu cầu từ Slack/Telegram đến URL Webhook của n8n.

2. **Lưu Log & Báo Cáo**:
   - Sử dụng **node `n8n-nodes-base.googleSheets`** để lưu lịch trình vào Google Sheets.
   - **Cách làm**:
     - Tạo một **Google Sheet** mới.
     - Cấu hình node `Google Sheets` với **credentials** và **Sheet Name**.
     - Chọn **append row** để thêm dữ liệu mới mỗi lần chạy.

3. **Cập Nhật Thời Gian Thực**:
   - Kết hợp với **API thời tiết** (ví dụ: OpenWeatherMap) để cập nhật dự báo thời tiết.
   - **Cách làm**:
     - Thêm **node `httpRequest`** gọi API OpenWeatherMap.
     - Sử dụng **node `set`** để merge dữ liệu thời tiết vào lịch trình.

4. **Tự Động Đặt Vé & Phòng**:
   - Nếu có **API Booking.com** hoặc **AirAsia**, có thể thêm node để đặt vé/phòng tự động.
   - **Lưu ý**: Các API này thường yêu cầu **OTP** hoặc xác nhận thủ công.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc **tìm kiếm, so sánh, và lên kế hoạch du lịch thủ công**. Với **AI Gemini**, **Amadeus**, và **Airbnb**, các sếp sẽ luôn có **lịch trình tối ưu**, **giá vé rẻ nhất**, và **khách sạn phù hợp**.

**🚀 Hành động ngay!**
1. **Import workflow** vào n8n của mình.
2. **Cấu hình API** (Amadeus, Airbnb, Vertex AI).
3. **Test với yêu cầu mẫu** và **bật Active**.
4. **Kết nối với Slack/Telegram** để sử dụng dễ dàng hơn.

**Chúc các sếp có những chuyến du lịch tuyệt vời và tiết kiệm thời gian!** 🌴✈️