---
title: "🚀 Tự động trích xuất metadata từ Gmail và lưu vào Google Sheets với n8n"
description: "Hướng dẫn xây dựng workflow n8n giúp tự động đọc email đến từ Gmail, thông minh bóc tách thông tin khách hàng và lưu trữ gọn gàng vào Google Sheets."
slug: "trich-xuat-gmail-metadata-google-sheets-n8n"
tags: [n8n, automation, no-code, gmail, google-sheets, ticket-management]
keywords: [n8n workflow, trích xuất email gmail, lưu email vào google sheets, tự động hóa n8n, quản lý ticket]
---

# 🚀 Tự động trích xuất metadata từ Gmail và lưu vào Google Sheets

Các sếp có đang đau đầu vì mỗi ngày phải nhận hàng tá email từ khách hàng, đơn hàng, hay form liên hệ? Việc cứ phải thủ công copy tên, email, tiêu đề rồi paste vào Google Sheets hay CRM không chỉ tốn thời gian, dễ bỏ sót khách hàng tiềm năng mà còn cực kỳ nhàm chán.

Giải pháp đây rồi! Workflow n8n này sẽ tự động hóa 100% quy trình: Lắng nghe email mới $\rightarrow$ Thông minh phân tích và bóc tách thông tin $\rightarrow$ Lưu ngay ngắn vào Google Sheets. Các sếp chỉ việc mở bảng ra và chăm sóc khách hàng thôi!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm hàng giờ đồng hồ:** Không còn cảnh copy-paste thủ công từ hộp thư đến sang bảng tính.
- **Không bao giờ bỏ lỡ lead:** Mọi email gửi đến đều được ghi nhận và lưu trữ tức thì, sẵn sàng để theo dõi.
- **Dữ liệu sạch sẽ, chuẩn hóa:** Code thông minh tự động dọn dẹp các định dạng lộn xộn, lọc ra Tên, Email, Tiêu đề và Nội dung chính xác.
- **Hoạt động 24/7:** Chạy ngầm liên tục, tự động xử lý dù các sếp đang ngủ hay đi chơi.
:::

### 📦 Các thành phần chính trong Workflow
Workflow này siêu gọn nhẹ chỉ gồm 4 nodes:
1. **Gmail Trigger:** Lắng nghe và kích hoạt ngay khi có email mới gửi đến.
2. **Code (JavaScript):** "Bộ não" thông minh trích xuất tên, email, tiêu đề, nội dung (xử lý cả trường hợp dữ liệu đến lộn xộn hoặc ẩn trong các định dạng khác nhau) và gắn timestamp.
3. **Edit Fields (Set):** Chuẩn hóa lại các trường dữ liệu trước khi đẩy đi.
4. **Append row in sheet (Google Sheets):** Tự động thêm hoặc cập nhật dòng mới vào Google Sheets của các sếp.

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Cloud hoặc Self-hosted).
- Tài khoản Google cá nhân/Workspace (để kết nối Gmail và Google Sheets).
- Một Google Sheet đã chuẩn bị sẵn các cột: `name`, `email`, `subject`, `message`, `timestamp`.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần tạo một workflow mới trong n8n, sau đó copy toàn bộ mã JSON của workflow và dán trực tiếp vào giao diện n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node `Gmail Trigger`**: Kết nối tài khoản Gmail của các sếp thông qua **Gmail OAuth2**. Chọn sự kiện kích hoạt khi có tin nhắn mới đến (`Message Received`).
- **Node `Code`**: Node này đã được viết sẵn logic JavaScript cực kỳ thông minh để xử lý các trường hợp:
  - Lấy Subject từ nhiều nguồn khác nhau (phòng khi trường dữ liệu bị thiếu).
  - Tách tên và email từ định dạng `John Doe <john@example.com>`.
  - Quét nội dung tin nhắn để tìm tên người gửi (ví dụ: *"Hi, I am Alice Johnson..."*).
  - Tự động gán giá trị mặc định (`No Subject`, `Unknown`) nếu không tìm thấy dữ liệu. Các sếp có thể giữ nguyên không cần sửa code!
- **Node `Append row in sheet` (Google Sheets)**: 
  - Chọn credentials **Google Sheets OAuth2 API**.
  - Chọn file Spreadsheet và Sheet Name mà các sếp muốn lưu dữ liệu.
  - Map các trường dữ liệu từ node trước vào đúng các cột tương ứng trên Google Sheets.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Node** hoặc **Test step** ở từng node để chạy thử với email mẫu.
- Sau khi test thấy dữ liệu đẩy vào Google Sheets mượt mà, gạt công tắc sang **Active** để workflow chính thức chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram/Slack:** Thêm một node Telegram hoặc Slack ngay sau Google Sheets để bắn thông báo "Tinh tưng! Có khách hàng mới gửi email!" về điện thoại ngay lập tức.
- **Phân loại tự động (AI):** Kết hợp thêm node OpenAI/Anthropic để phân tích xem email đó là "Khiếu nại", "Hỏi mua hàng" hay "Spam", từ đó tự động gán nhãn (Tag) vào Google Sheets.
- **Auto-reply:** Thiết lập gửi email phản hồi tự động cảm ơn khách hàng đã liên hệ.

### 📌 Kết luận
Một workflow nhỏ nhưng có võ, giúp các sếp tối ưu hóa hoàn toàn quy trình xử lý email đầu vào. Cài đặt ngay hôm nay để giải phóng thời gian và tập trung vào việc chốt đơn, chăm sóc khách hàng nhé các sếp!