---
title: "🚀 Tích hợp Trí tuệ Nhân tạo (AI) với Open-Meteo API để Dự báo Thời tiết Thông minh"
description: "Hướng dẫn xây dựng Agent AI tự động tra cứu tọa độ địa lý và dự báo thời tiết thông minh qua chat bằng n8n, OpenAI và Open-Meteo API."
slug: "tich-hop-ai-open-meteo-du-bao-thoi-tiet-n8n"
tags: [n8n, automation, no-code, ai-agent, openai, weather-api]
keywords: [n8n workflow, ai agent open-meteo, du bao thoi tiet ai, tich hop api weather n8n, openai tool calling n8n]
---

# 🚀 Tích hợp Trí tuệ Nhân tạo (AI) với Open-Meteo API để Dự báo Thời tiết Thông minh

Các sếp có bao giờ nghĩ đến việc xây dựng một trợ lý ảo thông minh có khả năng tự động hiểu câu hỏi ngôn ngữ tự nhiên của người dùng (ví dụ: *"Hôm nay thời tiết ở Hà Nội thế nào?"*), tự động tìm kiếm tọa độ, gọi API dự báo thời tiết và trả về câu trả lời hoàn chỉnh không? 

Thay vì phải code phức tạp, hôm nay tôi sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ thông minh do tác giả **Davi Saranszky Mesquita** thiết kế. Workflow này sử dụng **AI Agent** kết hợp các **Tool HTTP Request** để gọi Open-Meteo API một cách hoàn toàn tự động!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Trợ lý chat thông minh:** Tương tác trực tiếp qua giao diện chat nội bộ hoặc webhook bên ngoài.
- **AI Tool Calling tự động:** AI tự phân tích và biết gọi công cụ nào trước (Tool tìm tọa độ địa lý dựa trên tên thành phố trước, sau đó mới gọi Tool lấy dữ liệu dự báo thời tiết).
- **Dữ liệu thời tiết chính xác:** Kết nối trực tiếp với Open-Meteo API hoàn toàn miễn phí, không cần đăng ký API Key phức tạp cho phần thời tiết.
- **Tiết kiệm thời gian lập kế hoạch:** Giúp người dùng hoặc hệ thống tự động tra cứu thời tiết cho các quyết định du lịch, công tác, sự kiện.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (phiên bản hỗ trợ LangChain / AI Nodes).
- **OpenAI API Key:** Tài khoản OpenAI có số dư hoặc credit để gọi mô hình chat (GPT-4o hoặc GPT-3.5-turbo).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và dán trực tiếp vào n8n Editor, hoặc import file JSON thông qua giao diện n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 6 nodes chính hoạt động mượt mà cùng nhau:
- **When chat message received (`chatTrigger`):** Kích hoạt workflow mỗi khi có tin nhắn từ người dùng. Các sếp có thể test trực tiếp qua khung chat tích hợp của n8n hoặc lấy link Webhook để nhúng vào trang web riêng.
- **OpenAI Chat Model (`lmChatOpenAi`):** 
  - Chọn hoặc tạo mới `OpenAI API Credentials`.
  - Nhập API Key của các sếp vào đây để mô hình AI có "não" xử lý ngôn ngữ.
- **Generic AI Tool Agent (`agent`):** Node trung tâm điều phối, quyết định xem khi nào cần dùng tool nào dựa vào yêu cầu của người dùng.
- **Chat Memory Buffer (`memoryBufferWindow`):** Giúp AI ghi nhớ lịch sử trò chuyện trong phiên làm việc để giao tiếp mượt mà, tự nhiên hơn.
- **A tool for inputting the city and obtaining geolocation (`toolHttpRequest`):** 
  - Tool này gọi tới `https://geocoding-api.open-meteo.com/v1/search`.
  - AI sẽ tự động điền tên thành phố (`name`) do người dùng nhập vào tham số, trả về tọa độ latitude và longitude.
- **A tool to get the weather forecast based on geolocation (`toolHttpRequest`):** 
  - Tool này gọi tới `https://api.open-meteo.com/v1/forecast`.
  - Nhận các biến `latitude`, `longitude`, và `forecast_days` do AI tự động trích xuất từ tool trước đó để trả về kết quả thời tiết cho các ngày tới.

#### 3. Kích hoạt ⚡️
- Nhấn **Chat with node** hoặc sử dụng bảng test chat bên phải màn hình để thử nghiệm gõ câu lệnh: *"Thời tiết ở Tokyo trong 3 ngày tới thế nào?"*.
- Quan sát cách AI tự động gọi lần lượt 2 tools và trả về kết quả.
- Bật công tắc **Active** ở góc trên cùng bên phải để đưa workflow vào hoạt động chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh chat đa nền tảng:** Thay vì dùng Web chat mặc định của n8n, các sếp có thể thay thế node `chatTrigger` bằng **Telegram Trigger** hoặc **Slack Trigger** để biến bot thời tiết thành trợ lý trên nhóm chat công ty.
- **Lưu lịch sử chat:** Thêm node lưu log cuộc trò chuyện vào Google Sheets hoặc Database để phân tích nhu cầu tra cứu thời tiết của người dùng.
- **Mở rộng tool:** Có thể bổ sung thêm các tool khác như tra cứu tỷ giá ngoại tệ, tính khoảng cách di chuyển để biến bot thành trợ lý du lịch toàn diện.

### 📌 Kết luận
Việc kết hợp AI Agent với các API bên thứ ba thông qua HTTP Request Tool trong n8n mở ra khả năng tự động hóa vô tận mà không cần viết một dòng code phức tạp nào. Hãy áp dụng ngay workflow này vào hệ thống của các sếp để tối ưu hóa trải nghiệm khách hàng hoặc xây dựng các mini-app cực kỳ thú vị!