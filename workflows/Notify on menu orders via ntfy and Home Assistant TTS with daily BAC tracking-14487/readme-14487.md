---
title: "🍷 Tự Động Hóa Thông Báo Đơn Đặt Món + Theo Dõi BAC Hàng Ngày Với n8n & Home Assistant"
description: "Giải pháp hoàn toàn không code để nhận thông báo push khi có đơn đặt món, tính toán BAC hàng ngày và phát âm thông báo qua giọng nói Home Assistant. Tiết kiệm thời gian quản lý và đảm bảo an toàn cho khách hàng."
slug: "tieu-dong-hoa-thong-bao-don-dat-mon-bac-ngay"
tags: [n8n, automation, home-assistant, ntfy, bac-tracking, no-code]
keywords: [tự động hóa đơn đặt món, tính toán BAC hàng ngày, n8n workflow, thông báo push, home assistant tts, quản lý bar]
---

# 🚀 **Tự Động Hóa Thông Báo Đơn Đặt Món + Theo Dõi BAC Hàng Ngày Với n8n & Home Assistant**

### **Giải pháp cho các sếp quán bar, nhà hàng, hoặc quản lý sự kiện**
Bạn đã bao giờ phải lo lắng về việc **quên theo dõi lượng rượu uống của khách hàng** hay **mất thời gian ghi chép đơn đặt món**? Hoặc thậm chí **không thể thông báo kịp thời** khi khách đã uống quá nhiều? Workflow này sẽ **tự động hóa toàn bộ quy trình**, từ nhận đơn đặt món đến tính toán **BAC (Blood Alcohol Concentration)** hàng ngày và **thông báo thông minh** qua giọng nói Home Assistant.

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần ghi chép thủ công đơn đặt món.
- **Đảm bảo an toàn**: Theo dõi BAC hàng ngày và cảnh báo khi vượt ngưỡng.
- **Trải nghiệm khách hàng cá nhân hóa**: Thông báo push và giọng nói Home Assistant giúp khách hàng biết đơn đặt của mình.
- **Hoạt động 24/7**: Workflow chạy tự động, không cần can thiệp người dùng.
- **Dữ liệu trung tâm**: Tất cả đơn đặt món được lưu vào DataTable, dễ dàng phân tích sau này.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản n8n Self-hosted** (để workflow chạy liên tục).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

2. **Tài khoản ntfy.sh** (để gửi thông báo push).
   - [Đăng ký ntfy.sh](https://ntfy.sh/) và tạo **topic** riêng (ví dụ: `your-topic`).

3. **Home Assistant** (để phát âm thông báo qua giọng nói).
   - Cài đặt **Home Assistant** và **cài plugin TTS (Text-to-Speech)**.

4. **API Key cho ntfy** (để xác thực gửi thông báo).
   - Tạo **HTTP Header Auth** trong ntfy.sh và lưu lại `Token`.

5. **DataTable trong n8n** với các cột:
   - `item` (món ăn)
   - `person` (tên khách)
   - `alcohol_grams` (số gram rượu)
   - `date` (ngày đặt món)
   - `order_time` (thời gian đặt món)

6. **Script Home Assistant** (để gọi dịch vụ TTS).
   - Tạo một **script** trong Home Assistant với tên ví dụ: `announce_order`.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/14487) hoặc copy toàn bộ JSON từ [Notion Documentation](https://paoloronco.notion.site/Documentation-Menu-Order-Push-Notifications-Home-Assistant-TTS-BAC-32ff0ba27c328075a886d89ebfbf5ce5).
- Mở **n8n Editor**, nhấn **Import Workflow** và dán JSON vào.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **A. Cấu hình Webhook (Nhận đơn đặt món)**
- Node: **"When Order Received"**
  - Đảm bảo **path** là `menu` và **HTTP Method** là `POST`.
  - **Không cần thay đổi gì** nếu sử dụng mặc định.

##### **B. Cấu hình DataTable (Lưu đơn đặt món)**
- Node: **"Log Order to Database"**
  - Chọn **DataTable** đã tạo trước đó.
  - Đảm bảo các cột (`item`, `person`, `alcohol_grams`, `date`, `order_time`) khớp với cấu trúc.

##### **C. Cấu hình ntfy (Gửi thông báo push)**
- Node: **"Send Ntfy Notification"**
  - **Headers**:
    - `Authorization: Token YOUR_NTFY_TOKEN` (thay `YOUR_NTFY_TOKEN` bằng token từ ntfy.sh).
  - **URL**: `https://ntfy.sh/your-topic` (thay `your-topic` bằng topic của bạn).
  - **Body**: Sử dụng **JSON template** mặc định (không cần chỉnh sửa nếu muốn giữ định dạng gốc).

##### **D. Cấu hình Home Assistant (Phát âm thông báo)**
- Node: **"Announce Order with Home Assistant"**
  - **Credentials**: Chọn **Home Assistant** đã cấu hình.
  - **Service**: Đặt tên script trong Home Assistant (ví dụ: `announce_order`).
  - **Data**:
    ```json
    {
      "message": "{{ $node["Calculate Alcohol and Format Order"].json["formattedOrder"] }}"
    }
    ```
  - **Không cần thay đổi** nếu script Home Assistant đã chuẩn bị sẵn.

##### **E. Cấu hình tính toán BAC (Widmark Formula)**
- Node: **"Calculate Cumulative BAC"** (Code Node)
  - Mở **Code Editor** và chỉnh sửa nếu cần:
    - **Trọng lượng khách hàng** (default: `70 kg`).
    - **Hệ số Widmark** (default: `0.68`).
    - **Ngưỡng BAC cảnh báo** (ví dụ: `0.08`).
  - **Ví dụ chỉnh sửa**:
    ```javascript
    // Thay đổi trọng lượng và hệ số Widmark
    const weight = 75; // kg
    const widmarkFactor = 0.68;

    // Tính BAC
    const totalAlcohol = $input.all().reduce((sum, order) => sum + order.alcohol_grams, 0);
    const bac = (totalAlcohol / (weight * widmarkFactor)) * 100;
    ```

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Gửi một **POST request** đến webhook với body:
     ```json
     {
       "name": "John Doe",
       "time": "18:30",
       "items[]": [
         {"name": "Beer", "alcohol_grams": 12},
         {"name": "Wine", "alcohol_grams": 8}
       ]
     }
     ```
   - Kiểm tra:
     - Đơn đặt có được lưu vào DataTable không?
     - Thông báo push có được gửi không?
     - Home Assistant có phát âm không?

2. **Bật Active workflow**:
   - Nhấn **Active** trên tab **Workflow**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack/Telegram** để gửi thông báo cho quản lý khi BAC vượt ngưỡng.

2. **Lưu log vào file**:
   - Sử dụng node **File** để lưu tất cả đơn đặt món vào một file CSV/JSON định kỳ.

3. **Báo cáo hàng ngày**:
   - Tạo một **cron job** trong n8n để gửi báo cáo tổng hợp BAC hàng ngày qua email.

4. **Cảnh báo âm thanh**:
   - Kết nối với **Home Assistant Media Player** để phát âm thanh cảnh báo khi BAC quá cao.

5. **Tùy chỉnh thông báo**:
   - Chỉnh sửa **template** trong node **Calculate Alcohol and Format Order** để thông báo thêm thông tin như:
     - Số lượng món đã uống.
     - Thời gian còn lại trước khi vượt ngưỡng BAC.

---

### 📌 **Kết luận**
Workflow này không chỉ **giúp các sếp tự động hóa việc nhận đơn đặt món**, mà còn **tính toán BAC hàng ngày** và **cảnh báo kịp thời** để đảm bảo an toàn cho khách hàng. **Không cần code**, chỉ cần cấu hình vài bước là có thể áp dụng ngay!

👉 **Hãy thử ngay và tiết kiệm thời gian quản lý bar/nhà hàng của mình!**
👉 **Cần hỗ trợ thêm?** Đăng ký VPS n8n tại [TinoHost](https://tino.vn/vps-n8n?affid=388) và liên hệ với chúng tôi để được tư vấn chi tiết!