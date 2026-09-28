---
title: "🚀 Tự động tạo ảnh quảng cáo Facebook, Instagram & Pinterest bằng Google Gemini Imagen"
description: "Hướng dẫn xây dựng workflow n8n tự động tạo hình ảnh quảng cáo đa nền tảng (Facebook, IG, Pinterest) theo đúng kích thước chuẩn bằng AI Google Gemini Imagen và gửi trực tiếp về Telegram."
slug: "tu-dong-tao-anh-quang-cao-facebook-instagram-pinterest-google-gemini"
tags: [n8n, automation, no-code, google-gemini, content-creation, telegram]
keywords: [n8n workflow, tạo ảnh quảng cáo tự động, google gemini imagen, facebook ad image, instagram feed story, pinterest pin automation]
---

# 🚀 Tự động tạo ảnh quảng cáo Facebook, Instagram & Pinterest bằng Google Gemini Imagen

Các sếp làm marketing chắc hẳn đều thấm thía cảnh tốn hàng giờ đồng hồ chỉ để resize, căn chỉnh và thiết kế hàng loạt kích thước ảnh quảng cáo khác nhau cho Facebook, Instagram và Pinterest. Việc này vừa tốn nhân sự, vừa làm chậm trễ chiến dịch. 

Đừng lo, bài toán đó sẽ được giải quyết triệt để với workflow n8n tự động hóa 100% không cần code này! Chỉ với một biểu mẫu (Form) đơn giản, hệ thống sẽ tự động điều phối, sử dụng sức mạnh AI của **Google Gemini Imagen** để vẽ ra những bức ảnh quảng cáo chuẩn từng milimet cho từng nền tảng, sau đó bắn thẳng kết quả về Telegram cho các sếp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian thiết kế:** Không còn phải thủ công tạo từng khung hình cho Facebook Feed, Story hay Pinterest Pin.
- **Chuẩn kích thước 100%:** Tự động định tuyến (Route) kích thước chính xác cho từng vị trí hiển thị (1200x630, 1080x1080, 1000x1500...).
- **Sức mạnh Multimodal AI:** Tận dụng Google Gemini Imagen để tạo ra hình ảnh sinh động, sáng tạo dựa trên ý tưởng/prompt của người dùng.
- **Nhận kết quả liền tay:** Toàn bộ ảnh được gom và gửi tự động qua Telegram ngay khi AI xử lý xong.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **n8n Instance:** Đã chạy ổn định (Cloud hoặc Self-hosted).
- **Google Gemini API Key:** Tài khoản Google Cloud / Google AI Studio có kích hoạt tính năng tạo ảnh (Imagen).
- **Telegram Bot Token & Chat ID:** Để hệ thống gửi hình ảnh thành phẩm về máy.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow (hoặc tải file từ nguồn gốc) và dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 16 nodes được sắp xếp cực kỳ khoa học. Các sếp cần chú ý cấu hình các phần sau:
- **📝 Form Trigger:** Cấu hình giao diện form đầu vào để người dùng (hoặc team content) điền mô tả ý tưởng quảng cáo (prompt) và chọn định dạng mong muốn.
- **🔀 Route by Dimensions:** Node Switch này sẽ đọc dữ liệu từ form và phân luồng yêu cầu đến đúng node tạo ảnh phù hợp.
- **🎨 Các node Google Gemini (FB Feed, IG Story, Pinterest Pin, v.v.):** 
  - Kết nối với **Google Gemini Credentials** của các sếp.
  - Cấu hình prompt động lấy từ Form Trigger và đảm bảo thông số kích thước (dimensions) được truyền chính xác cho từng nền tảng (ví dụ: `1200x630` cho FB Feed, `1000x1500` cho Pinterest Pin).
- **📤 Các node Telegram (Send FB Feed, Send IG Story, v.v.):**
  - Thêm **Telegram Credentials** (Bot Token).
  - Điền `Chat ID` nơi nhận ảnh thành phẩm.
  - Map dữ liệu hình ảnh trả về từ các node Google Gemini tương ứng vào trường `Photo` của tin nhắn Telegram.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và thử điền form mẫu để test xem ảnh có được tạo và gửi về Telegram mượt mà không.
- Nếu mọi thứ xanh mướt, hãy gạt công tắc sang **Active** để đưa vào sử dụng thực tế!

### ✍️ Mẹo & gợi ý nâng cao
Để workflow "xịn xò" hơn nữa, các sếp có thể tùy biến thêm:
- **Lưu trữ tự động:** Thêm node **Google Drive** hoặc **Airtable** để lưu lại lịch sử các hình ảnh đã tạo kèm theo prompt gốc.
- **Mở rộng kênh nhận:** Thay vì chỉ gửi Telegram, có thể cấu hình thêm node gửi qua **Slack** hoặc **Discord** cho team design.
- **Kiểm duyệt nội dung:** Thêm bước xét duyệt qua Slack trước khi gửi ảnh hàng loạt để đảm bảo AI không "vẽ bậy".

### 📌 Kết luận
Việc tự động hóa quy trình sáng tạo nội dung hình ảnh chưa bao giờ dễ dàng đến thế. Hãy cài đặt ngay workflow này để giải phóng sức lao động cho team marketing và tăng tốc các chiến dịch quảng cáo của các sếp ngay hôm nay!