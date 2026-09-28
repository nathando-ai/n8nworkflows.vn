---
title: "🏈 Tự động hóa Roster Bóng đá Hư cấu với Sleeper API và Telegram Chatbot"
description: "Hướng dẫn tự động hóa workflow n8n để lấy thông tin đội bóng đá hư cấu từ Sleeper API và gửi qua Telegram Chatbot - tiết kiệm thời gian và nâng cao trải nghiệm người dùng."
slug: "tu-dong-hoa-roster-bong-da-hu-cau-voi-sleeper-api-va-telegram-chatbot"
tags: [n8n, automation, no-code, football, sleeper]
keywords: [n8n workflow, tự động hóa, bóng đá hư cấu, sleeper api, telegram chatbot]
---

# 🏈 Tự động hóa Roster Bóng đá Hư cấu với Sleeper API và Telegram Chatbot

[Các sếp] có bao giờ cảm thấy mệt mỏi khi phải tra cứu thông tin đội bóng đá hư cấu của mình trên Sleeper App? Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình lấy thông tin roster, từ việc nhập username đến gửi kết quả qua Telegram Chatbot - tất cả chỉ với một lệnh đơn giản!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải mở Sleeper App mỗi khi muốn kiểm tra roster
- **Thông tin chính xác**: Lấy dữ liệu trực tiếp từ Sleeper API
- **Tiện ích di động**: Nhận thông tin qua Telegram bất cứ nơi đâu
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công sau khi cài đặt
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram và bot được tạo qua BotFather
- Username Sleeper của các sếp (phải nhập chính xác chữ hoa/chữ thường)
- Credentials cho Telegram và Airtable (hoặc Google Sheets nếu thay thế)
- (Tùy chọn) Workflow Sleeper NFL Daily Sync để đồng bộ dữ liệu người chơi
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/6655)
2. Click vào nút "Import" ở góc trên bên phải
3. Copy toàn bộ JSON workflow và dán vào n8n Editor của các sếp

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Send Message to Chatbot"**:
   - Cấu hình credentials Telegram
   - Điền Chat ID của các sếp (có thể lấy từ BotFather)

2. **Node "Search records" (Airtable)**:
   - Cấu hình credentials Airtable
   - Điền Base ID và Table Name chứa dữ liệu người chơi
   - (Tùy chọn) Thay thế bằng Google Sheets nếu cần

3. **Node "Extract Username"**:
   - Kiểm tra logic trích xuất username từ tin nhắn Telegram
   - Đảm bảo xử lý cả chữ hoa và chữ thường

4. **Node "Get Sleeper User ID"**:
   - Cập nhật URL API nếu Sleeper thay đổi (đặc biệt là phần năm trong URL)

5. **Node "Get Rosters"**:
   - Kiểm tra logic lọc league (mặc định chỉ lấy league đầu tiên)

#### 3. Kích hoạt ⚡️
1. Test workflow với username Sleeper của các sếp
2. Kiểm tra kết quả trên Telegram Chatbot
3. Bật Active workflow để sử dụng liên tục

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh thông báo**: Chỉnh sửa nội dung tin nhắn trong node "Send a text message" để phù hợp với phong cách của các sếp
2. **Xử lý nhiều league**: Nâng cấp logic để xử lý trường hợp người dùng tham gia nhiều league
3. **Lịch sử truy vấn**: Thêm node lưu log các truy vấn để theo dõi hoạt động
4. **Thông báo định kỳ**: Kết hợp với workflow khác để gửi thông báo tự động về trạng thái đội bóng

### 📌 Kết luận
Workflow này mang lại giải pháp hoàn hảo cho các sếp muốn theo dõi thông tin đội bóng đá hư cấu một cách nhanh chóng và tiện lợi. Với việc tự động hóa toàn bộ quá trình từ lấy dữ liệu đến gửi thông báo, các sếp có thể tập trung vào những điều quan trọng hơn trong cuộc sống. Hãy thử ngay và trải nghiệm sự tiện lợi mà công nghệ mang lại!