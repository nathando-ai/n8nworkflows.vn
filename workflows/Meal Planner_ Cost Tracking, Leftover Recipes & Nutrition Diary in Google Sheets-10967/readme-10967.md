---
title: "🚀 Trợ lý Ẩm thực AI Thông minh: Quản lý Chi phí, Tận dụng Thừa & Nhật ký Dinh dưỡng trong Google Sheets"
description: "Tự động hóa toàn diện quy trình lên thực đơn: tính toán chi phí nguyên liệu, gợi ý món ăn từ đồ thừa, ghi chép nhật ký dinh dưỡng và gửi tin nhắn Twitter nhờ AI và n8n."
slug: "tro-ly-am-thuc-ai-n8n-google-sheets"
tags: [n8n, automation, no-code, ai-agent, google-sheets, openrouter, twitter]
keywords: [n8n workflow, trợ lý ẩm thực ai, quản lý chi phí nấu ăn, openrouter n8n, google sheets automation]
---

# 🚀 Xây dựng Trợ lý Ẩm thực AI Toàn diện với n8n, OpenRouter và Google Sheets

Các sếp có bao giờ đau đầu vì việc lên thực đơn hằng ngày, không biết chi phí nguyên liệu tốn bao nhiêu, làm sao để tận dụng đồ thừa trong tủ lạnh, hay quên ghi chép lại chế độ dinh dưỡng? Việc quản lý thủ công các công thức nấu ăn, tính toán giá tiền từng nguyên liệu và viết nhật ký ăn uống cực kỳ tốn thời gian và dễ nản chí.

Đừng lo! Workflow n8n này sẽ đóng vai trò là một **Trợ lý Ẩm thực AI cao cấp (Culinary AI Assistant)** giúp các sếp tự động hóa 100% các tác vụ trên: từ việc phân tích nguyên liệu, tính toán chi phí, gợi ý món ăn từ đồ thừa, ghi log vào Google Sheets cho đến việc soạn bài đăng chia sẻ lên mạng xã hội qua X/Twitter.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa tính toán chi phí:** AI phân tích món ăn đầu vào, bóc tách chi tiết danh sách nguyên liệu, đơn giá, số lượng và tổng chi phí vào Google Sheets.
- **Tối ưu hóa chống lãng phí:** Tự động nhận diện nguyên liệu thừa và gợi ý 3 công thức nấu ăn mới để tận dụng triệt để.
- **Theo dõi sức khỏe thông minh:** Tự động tạo nhật ký dinh dưỡng, phân tích dưỡng chất và đưa ra lời khuyên cá nhân hóa.
- **Chia sẻ liền mạch:** Biến nhật ký dinh dưỡng thành bài đăng hấp dẫn và gửi thẳng vào tin nhắn trực tiếp (Direct Message) trên X/Twitter để sẵn sàng chia sẻ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- Một instance n8n đang hoạt động.
- Tài khoản Google (để sử dụng Google Sheets).
- Tài khoản OpenRouter kèm API Key (để chạy các AI Agents và Chat Models).
- Tài khoản Twitter (X) có quyền Developer để gửi Direct Message.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ n8n template (ID: 10967) và import trực tiếp vào n8n Editor của các sếp, hoặc sử dụng tính năng copy/paste JSON.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 14 nodes với các thành phần cốt lõi cần cấu hình như sau:

- **Webhook Node**: 
  - Lấy Webhook URL để gửi dữ liệu đầu vào (tên món ăn hoặc công thức) qua phương thức `POST`.
- **OpenRouter Chat Model (1, 2, 3 và Model chính)**: 
  - Cần cấu hình OpenRouter Credentials và điền API Key hợp lệ. Các model này sẽ cung cấp sức mạnh cho các AI Agent.
- **Các AI Agent (Menu Agent, Leftovers Agent, Nutritionist Agent, Post Agent)**: 
  - Đảm bảo các Agent đã được liên kết chính xác với các Chat Models và `Structured Output Parser` để trả về đúng định dạng dữ liệu cần thiết.
- **Google Sheets Nodes (Append row in sheet, sheet1, sheet2)**: 
  - Tạo một Google Sheet mới (ví dụ: "Recipe List") gồm 3 trang tính (sheets):
    1. **"Recipe"**: Các cột cần có: `Date`, `Item`, `Ingredients`, `Ingredient Cost`, `Unit Price`, `Quantity`, `Total`, `Cost`, `Leftover Ingredients`.
    2. **"leftovers"**: Các cột cần có: `Date`, `Ingredients`.
    3. **"diary"**: Cột cần có: `Diary`.
  - Thay thế `Document ID` trong các node Google Sheets bằng ID của bảng tính vừa tạo, và chọn đúng Sheet Name tương ứng.
- **Create Direct Message (Twitter Node)**: 
  - Thiết lập Twitter Credentials.
  - Điền tên tài khoản Twitter (`User`) nhận tin nhắn trực tiếp (thường là tài khoản cá nhân của các sếp hoặc tài khoản test).

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và gửi một request `POST` chứa tên món ăn qua Webhook URL để test thử.
- Kiểm tra xem dữ liệu đã được đẩy vào Google Sheets và tin nhắn đã gửi về Twitter chưa.
- Nếu mọi thứ mượt mà, hãy gạt nút **Active** để đưa workflow vào vận hành chính thức!

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng thông báo**: Kết hợp thêm node Telegram hoặc Slack để nhận thông báo thực đơn và gợi ý món ăn ngay trên điện thoại thay vì chỉ dùng Twitter.
- **Lưu lịch sử chạy**: Thêm một bước xử lý lỗi (Error Trigger) để nếu API OpenRouter lỗi, hệ thống sẽ tự động nhắn tin cảnh báo cho các sếp.
- **Tự động hóa hàng tuần**: Thay vì dùng Webhook thủ công, các sếp có thể gắn thêm node Schedule Trigger để AI tự động lên thực đơn cho cả tuần vào mỗi Chủ Nhật.

### 📌 Kết luận
Với workflow n8n này, việc quản lý bếp núc, chi phí ăn uống và dinh dưỡng cá nhân nay đã được AI lo trọn gói. Chúc các sếp cài đặt thành công và tận hưởng một lối sống thông minh, tiết kiệm hơn!