---
title: "🌦️ Tự Động Gửi Báo Cáo Thời Tiết Chi Tiết Qua Telegram Với n8n"
description: "Workflow n8n tự động lấy dữ liệu thời tiết hiện tại và dự báo 5 ngày từ OpenWeatherMap, định dạng báo cáo chuyên nghiệp và gửi ngay vào Telegram theo lịch trình."
slug: "tu-dong-gui-bao-cao-thoi-tiet-telegram-n8n"
tags: [n8n, automation, no-code, openweathermap, telegram, productivity]
keywords: [n8n workflow, tự động hóa thời tiết, openweathermap n8n, telegram bot n8n, báo cáo thời tiết]
---

# 🌦️ Tự Động Gửi Báo Cáo Thời Tiết Chi Tiết Qua Telegram Với n8n

Các sếp có bao giờ cảm thấy phiền toái khi phải mở app thời tiết mỗi sáng để xem hôm nay trời thế nào, hay cuối tuần có mưa không để sắp xếp lịch trình? Việc kiểm tra thủ công không chỉ tốn thời gian mà còn dễ bỏ sót những thay đổi thời tiết đột ngột.

Workflow này là giải pháp "cứu cánh" hoàn hảo: nó tự động hóa 100% quy trình lấy dữ liệu thời tiết từ OpenWeatherMap, xử lý và định dạng thành một báo cáo đẹp mắt, sau đó đẩy thẳng vào Telegram của các sếp. Không cần code, không cần mở app, chỉ cần ngồi yên và nhận thông tin chính xác nhất vào điện thoại.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tuyệt đối:** Không cần thao tác thủ công, báo cáo tự động đến đúng giờ các sếp mong muốn.
- **Dữ liệu tổng hợp & Chính xác:** Kết hợp cả thời tiết hiện tại và dự báo 5 ngày tới trong cùng một tin nhắn, giúp ra quyết định nhanh chóng.
- **Cá nhân hóa vị trí:** Dễ dàng thay đổi tọa độ (lat/long) để theo dõi thời tiết tại bất kỳ đâu (Văn phòng, Nhà riêng, Điểm du lịch).
- **Hoạt động liên tục:** Chạy nền trên n8n, đảm bảo các sếp không bao giờ bỏ lỡ thông tin thời tiết quan trọng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản OpenWeatherMap:** Đăng ký miễn phí tại [openweathermap.org](https://openweathermap.org/) và lấy **API Key**.
2. **Tài khoản Telegram Bot:**
   - Tạo bot qua @BotFather.
   - Lấy **Bot Token**.
   - Lấy **Chat ID** của các sếp (có thể dùng @userinfobot hoặc @getmyid_bot).
3. **Tọa độ địa lý (Latitude & Longitude):** Của vị trí các sếp muốn theo dõi (có thể tìm trên Google Maps).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ link gốc hoặc copy toàn bộ code JSON và dán vào n8n Editor.
- Mở n8n -> Chọn **Import from URL** hoặc **Import from File**.
- Sau khi import, workflow sẽ hiển thị đầy đủ 7 nodes: `Schedule Trigger`, `Set Location`, `Weather: Current`, `Weather: 5Days`, `Merge`, `Report: Prepare`, và `Send a text message`.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Đây là phần quan trọng nhất. Các sếp cần click vào từng node và cấu hình như sau:

**📍 Node: `Set Location`**
- Node này dùng để định nghĩa vị trí lấy dữ liệu.
- Các sếp cần điền 3 trường dữ liệu:
  - `lat`: Vĩ độ (Ví dụ: 21.0285 cho Hà Nội).
  - `long`: Kinh độ (Ví dụ: 105.8542 cho Hà Nội).
  - `telegram_chat_id`: ID chat của các sếp (số hoặc chuỗi ký tự từ Bot).

**🌡️ Node: `Weather: Current` & `Weather: 5Days`**
- Cả hai node này đều sử dụng credentials `openWeatherMapApi`.
- Các sếp cần tạo credentials mới trong n8n, chọn **OpenWeatherMap**, và dán **API Key** vừa lấy ở bước chuẩn bị.
- Đảm bảo node `Weather: 5Days` đang ở chế độ `5DayForecast` (mặc định thường đã đúng).

**📝 Node: `Report: Prepare`**
- Đây là node Code (JavaScript) dùng để xử lý dữ liệu thô từ OpenWeatherMap và ghép chúng lại thành một chuỗi văn bản dễ đọc.
- Các sếp **không cần sửa code** nếu chỉ muốn dùng mặc định. Tuy nhiên, nếu muốn đổi đơn vị đo (Celsius/Fahrenheit) hoặc thêm các trường thông tin khác, các sếp có thể chỉnh sửa logic trong node này.

**📤 Node: `Send a text message`**
- Node này dùng để gửi tin nhắn qua Telegram.
- Các sếp cần tạo credentials mới, chọn **Telegram**, và dán **Bot Token**.
- Kiểm tra trường `Chat ID`: Nó thường được lấy từ node `Set Location` ở bước trước. Đảm bảo giá trị này khớp với Chat ID thực tế của các sếp.

#### 3. Kích hoạt ⚡️
1. **Test Run:** Click vào nút **Execute Workflow** (hoặc click vào từng node để test riêng).
   - Kiểm tra xem node `Weather: Current` và `Weather: 5Days` có trả về dữ liệu không (màu xanh lá cây).
   - Kiểm tra node `Report: Prepare` xem nội dung báo cáo đã được định dạng đẹp chưa.
   - Kiểm tra node `Send a text message` xem tin nhắn có vào Telegram không.
2. **Bật Active:** Nếu mọi thứ ổn, click vào nút **Active** ở góc trên bên phải để workflow bắt đầu chạy theo lịch trình.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa vị trí:** Các sếp có thể nhân bản workflow và tạo nhiều bản với các tọa độ khác nhau (Ví dụ: 1 bản cho Hà Nội, 1 bản cho TP.HCM) để theo dõi nhiều thành phố cùng lúc.
- **Gửi qua Email:** Thay vì hoặc kết hợp thêm node `Send Email` để gửi báo cáo thời tiết vào hộp thư, phù hợp cho những ai ít dùng Telegram.
- **Cảnh báo thời tiết cực đoan:** Chỉnh sửa node `Report: Prepare` để thêm điều kiện: nếu nhiệt độ > 35°C hoặc có mưa bão, gửi thêm một tin nhắn cảnh báo riêng biệt với icon ⚠️.
- **Tùy chỉnh lịch trình:** Click vào `Schedule Trigger` để đổi giờ gửi (Ví dụ: 6:00 sáng mỗi ngày, hoặc 17:00 chiều trước khi tan sở).

### 📌 Kết luận
Việc tự động hóa việc theo dõi thời tiết không chỉ giúp các sếp tiết kiệm thời gian mà còn nâng cao trải nghiệm cá nhân hóa. Với workflow n8n này, các sếp sẽ luôn nắm bắt được thông tin thời tiết chính xác nhất, kịp thời nhất, chỉ với vài phút cấu hình ban đầu. Hãy import và thử ngay hôm nay để thấy sự khác biệt!