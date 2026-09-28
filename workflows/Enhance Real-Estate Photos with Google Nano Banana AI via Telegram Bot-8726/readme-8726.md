---
title: "🚀 Biến Ảnh Bất Động Sản Thành Kiệt Tác Bằng AI Trực Tiếp Trên Telegram Bot"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa chỉnh sửa ảnh bất động sản qua Google Nano Banana AI và Telegram Bot, giúp tiết kiệm thời gian và tối ưu quy trình làm việc."
slug: "chinh-sua-anh-bat-dong-san-ai-telegram-bot-n8n"
tags: [n8n, automation, telegram-bot, google-drive, ai-image-editing]
keywords: [n8n workflow, tự động hóa telegram, ai chỉnh sửa ảnh, google nano banana, xử lý ảnh bất động sản]
---

# 🚀 Biến Ảnh Bất Động Sản Thành Kiệt Tác Bằng AI Trực Tiếp Trên Telegram Bot

Các sếp làm trong ngành bất động sản, marketing hay sáng tạo nội dung có thường xuyên gặp cảnh: Chụp ảnh căn nhà xong phải tốn hàng giờ đồng hồ vào Photoshop để chỉnh sáng, xóa chi tiết thừa hay làm nét ảnh không? Việc này vừa tốn thời gian, vừa làm chậm trễ tiến độ đăng bài quảng cáo.

Giải pháp là đây! Workflow n8n này sẽ biến chiếc **Telegram Bot** quen thuộc của các sếp thành một "phòng dựng ảnh AI" di động. Chỉ cần gửi một bức ảnh chụp vội vào khung chat Telegram, hệ thống sẽ tự động hóa 100% việc xử lý qua **Google Nano Banana AI (thông qua Wavespeed API)** và trả lại một bức ảnh bất động sản sắc nét, chuyên nghiệp chỉ trong tích tắc. Không cần code, không cần mở máy tính phức tạp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Chỉ cần "gửi ảnh lên Telegram -> nhận lại ảnh đẹp", không thao tác thủ công.
- **Tốc độ chớp nhoáng:** Xử lý bất động sản/ảnh sản phẩm ngay trên điện thoại khi đang di chuyển ngoài hiện trường.
- **Tiết kiệm chi phí:** Không cần thuê designer chỉnh sửa từng bức ảnh nhỏ lẻ hay mua phần mềm đắt đỏ.
- **Hoạt động 24/7:** Bot trực chiến liên tục trên Telegram, phục vụ nhu cầu mọi lúc mọi nơi.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow này "lên đồ" mượt mà, các sếp cần chuẩn bị sẵn các tài khoản và API sau:
- **Telegram Bot Token** (tạo qua `@BotFather`).
- **Tài khoản Google Drive** (dùng làm bộ nhớ tạm thời để lưu trữ và xử lý ảnh).
- **Wavespeed API Key** (để kết nối với Google Nano Banana AI).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể copy mã JSON của workflow này và paste trực tiếp vào n8n Editor, hoặc import file JSON tải từ nguồn cấp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 9 nodes chính hoạt động nhịp nhàng. Các sếp cần chú ý cấu hình các điểm sau:
- **Telegram Trigger & Get a file & Send a photo message:** Kết nối với Telegram Bot của các sếp bằng Telegram API Credentials. Node `Get a file` sẽ lấy nội dung ảnh mà người dùng gửi vào chat.
- **Upload file (Google Drive):** Kết nối tài khoản Google Drive để lưu tạm bức ảnh vừa gửi lên mây trước khi truyền vào AI.
- **Nano Banana POST Request & GET Result from Nano Banana Node (HTTP Request):** Cấu hình API endpoint của Wavespeed / Google Nano Banana, điền API Key vào Header và thiết lập prompt chỉnh sửa ảnh theo phong cách bất động sản (tăng sáng, cân bằng màu, làm sắc nét không gian).
- **Wait 15 Secs & Wait 15 Secs Again + If (Conditional):** Xử lý quy trình bất đồng bộ (async processing). Do AI cần thời gian để render ảnh, các node `Wait` sẽ tạm dừng vài giây trước khi gọi node `GET Result` để kiểm tra xem AI đã xử lý xong chưa.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và gửi thử một bức ảnh bất kỳ vào Telegram Bot của các sếp để test quá trình chạy.
- Sau khi kiểm tra mọi thứ trơn tru, hãy bật công tắc **Active** để đưa workflow vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa dạng hóa phong cách:** Thay đổi prompt trong HTTP Request để AI chuyển sang các mục đích khác như: làm đẹp chân dung (portrait retouching), tối ưu ảnh thương mại điện tử (e-commerce cleanup).
- **Lưu trữ lịch sử:** Thêm một node Google Sheets hoặc Airtable vào sau bước xử lý thành công để lưu lại log thông tin người dùng và ảnh đã chỉnh sửa.
- **Thông báo nhóm:** Kết nối thêm Slack hoặc một kênh Telegram khác để quản lý theo dõi số lượng ảnh được xử lý mỗi ngày.

### 📌 Kết luận
Một workflow cực kỳ thiết thực cho anh em môi giới bất động sản, nhà sáng tạo nội dung hoặc bất kỳ ai muốn ứng dụng AI vào quy trình xử lý hình ảnh hàng ngày. Hãy cài đặt ngay để tối ưu hóa công việc của mình nhé các sếp!