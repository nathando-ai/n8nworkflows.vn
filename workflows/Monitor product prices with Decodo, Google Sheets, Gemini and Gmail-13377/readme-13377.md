---
title: "🚀 Tự động giám sát giá sản phẩm đối thủ với Decodo, Google Sheets, Gemini và Gmail"
description: "Hướng dẫn thiết lập workflow n8n tự động cào dữ liệu giá sản phẩm, phân tích bằng AI Gemini và gửi email cảnh báo khi giá giảm sâu."
slug: "tu-dong-giam-sat-gia-san-pham-decodo-gemini-gmail"
tags: [n8n, automation, ai-agent, google-sheets, price-monitoring, gmail]
keywords: [n8n workflow, giám sát giá sản phẩm, cào giá web decodo, google gemini ai, tự động hóa n8n]
---

# 🚀 Tự động giám sát giá sản phẩm đối thủ với Decodo, Google Sheets, Gemini và Gmail

Các sếp có đang tốn hàng giờ mỗi ngày chỉ để vào các trang web đối thủ, kiểm tra giá sản phẩm và cập nhật vào bảng Excel/Google Sheets? Công việc thủ công này cực kỳ nhàm chán, dễ sai sót và khiến các sếp bỏ lỡ những thời điểm vàng khi đối thủ hạ giá hoặc thay đổi chiến lược.

Bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n cực kỳ thông minh, tự động hóa 100% quy trình: lấy danh sách link từ Google Sheets 👉 cào dữ liệu web 👉 dùng AI Google Gemini phân tích tên và giá 👉 so sánh với mức giá kỳ vọng 👉 tự động gửi email cảnh báo qua Gmail!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian:** Không còn phải thủ công truy cập từng website để check giá.
- **Phát hiện chớp nhoáng:** Nhận email cảnh báo ngay lập tức khi sản phẩm chạm hoặc thấp hơn mức giá mong muốn.
- **Sức mạnh AI thông minh:** Sử dụng Google Gemini để bóc tách tên sản phẩm và giá chính xác từ mã nguồn HTML phức tạp.
- **Vận hành tự động 24/7:** Chạy ngầm định kỳ hàng ngày mà không cần con người can thiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Sheets chứa danh sách URL sản phẩm và mức giá kỳ vọng ("Desired Price").
- Tài khoản Google Cloud / Google AI Studio để lấy API Key cho **Google Gemini**.
- Tài khoản **Gmail** để gửi email cảnh báo.
- Node **Decodo** (được tích hợp sẵn trong n8n để hỗ trợ xử lý dữ liệu web).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này và import trực tiếp vào n8n Editor của các sếp, hoặc sử dụng tính năng Copy/Paste JSON trực tiếp vào giao diện làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động mượt mà, các sếp cần cấu hình chính xác các node sau:

- **Daily Run (Schedule Trigger):** Cấu hình thời gian chạy tự động mỗi ngày (ví dụ: 8:00 sáng).
- **Get row(s) in sheet (Google Sheets):** Kết nối tài khoản Google Sheets của các sếp, chọn đúng file tài liệu *"Price monitoring"* và trỏ tới sheet chứa danh sách link sản phẩm kèm cột giá mong muốn.
- **Loop Over Items (Split In Batches):** Giúp duyệt qua từng URL một cách tuần tự để tránh tình trạng quá tải hoặc nghẽn mạng khi cào dữ liệu.
- **Decodo & HTML Node:** Xử lý và trích xuất toàn bộ phần thân (`<body>`) của trang web để AI có đầy đủ ngữ cảnh phân tích.
- **AI Agent & Google Gemini Chat Model:** 
  - Kết nối credentials của Google Gemini (Google Palm API).
  - Đảm bảo Prompt trong AI Agent yêu cầu rõ ràng việc trích xuất chính xác **"Product Name"** và **"Current Price"**.
- **Code in JavaScript2:** Chạy script Regex để lọc ra định dạng số từ chuỗi giá tiền mà AI trả về.
- **If Node:** Thiết lập logic so sánh dạng **"Less Than or Equal (<=)"** giữa giá hiện tại do AI quét được và "Desired Price" trong Google Sheets.
- **Send a message (Gmail):** Kết nối tài khoản Gmail cá nhân/doanh nghiệp để tự động bắn email cảnh báo khi điều kiện giá thỏa mãn.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (**Test run**) với 1-2 dòng dữ liệu đầu tiên trong Google Sheets để kiểm tra kết quả trả về của AI và email.
- Sau khi test thành công, bật công tắc **Active workflow** ở góc trên bên phải màn hình để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm thông báo chat:** Thay vì chỉ gửi Gmail, các sếp có thể gắn thêm node **Telegram** hoặc **Slack** để nhận tin nhắn ngay trên điện thoại khi có biến động giá.
- **Lưu lịch sử biến động:** Thêm một bước ghi log ngược lại vào một sheet khác trong Google Sheets để vẽ biểu đồ lịch sử thay đổi giá của đối thủ theo thời gian.
- **Xử lý lỗi (Error Handling):** Thêm Error Trigger để nhận cảnh báo qua Telegram nếu một trang web của đối thủ bị lỗi 404 hoặc chặn request.

### 📌 Kết luận
Việc tự động hóa giám sát giá sản phẩm đối thủ chưa bao giờ dễ dàng đến thế nhờ sự kết hợp giữa n8n, Decodo và sức mạnh phân tích ngữ cảnh từ Google Gemini AI. Hãy thiết lập ngay hôm nay để luôn đi trước đối thủ một bước trong cuộc đua chiến lược giá!