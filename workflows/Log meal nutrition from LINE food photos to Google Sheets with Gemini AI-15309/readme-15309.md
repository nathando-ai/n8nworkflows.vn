---
title: "🚀 Tự động ghi nhận dinh dưỡng từ ảnh chụp món ăn trên LINE vào Google Sheets với Gemini AI"
description: "Hướng dẫn cài đặt workflow n8n tích hợp Gemini AI và LINE để tự động bóc tách calo, ghi log vào Google Sheets và cảnh báo khi vượt định mức."
slug: "tu-dong-ghi-nhan-dinh-duong-line-google-sheets-gemini-ai"
tags: [n8n, automation, gemini-ai, google-sheets, line-bot, ai-agent]
keywords: [n8n workflow, line bot nutrition, gemini ai food analysis, google sheets automation, tu dong hoa n8n]
---

# 🚀 Tự động ghi nhận dinh dưỡng từ ảnh chụp món ăn trên LINE vào Google Sheets với Gemini AI

Các sếp có đang chật vật trong việc ghi chép lại lượng calo và thành phần dinh dưỡng của từng bữa ăn mỗi ngày không? Việc nhập thủ công vào Excel hay các ứng dụng đếm calo thường rất nản và dễ bỏ cuộc chỉ sau vài ngày.

Giải pháp đây rồi! Workflow n8n này sẽ biến ứng dụng **LINE** quen thuộc thành một trợ lý dinh dưỡng cá nhân thông minh. Các sếp chỉ cần chụp ảnh bữa ăn và gửi vào LINE, hệ thống sẽ tự động dùng **Gemini AI** để phân tích món ăn, tính toán calo, ghi nhận vào **Google Sheets** và lập tức phản hồi lại thông tin chi tiết, đồng thời cảnh báo nếu vượt ngưỡng calo cho phép.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Không cần nhập liệu thủ công, chỉ cần chụp ảnh và gửi qua LINE.
- **AI Đa phương thức (Multimodal):** Gemini AI nhận diện chính xác món ăn và ước lượng calo, protein, mỡ, carb từ hình ảnh.
- **Quản lý sức khỏe thông minh:** Tự động tính tổng calo trong ngày, so sánh với hạn mức (Calorie Limit) và gửi cảnh báo ngay lập tức.
- **Báo cáo định kỳ:** Tự động tổng hợp thống kê hàng tuần và gửi báo cáo trực tiếp qua chat LINE.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản **n8n** (Cloud hoặc Self-hosted).
- **LINE Official Account (LINE Messaging API)** để nhận sự kiện và gửi tin nhắn.
- **Google Sheets** (tạo sẵn file log dinh dưỡng).
- **Google Gemini API Key** để sử dụng các node LangChain LLM.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow, sau đó vào giao diện n8n Editor, chọn **Import from JSON** và dán vào là xong.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 23 nodes hoạt động nhịp nhàng, các sếp chú ý cấu hình kỹ các điểm sau:

- **Node "Set Config Fields":** Điền đầy đủ các biến cấu hình quan trọng như:
  - `LINE_CHANNEL_ACCESS_TOKEN` (Lấy từ LINE Developer Console).
  - `GOOGLE_SHEET_ID` (ID của Google Sheets lưu dữ liệu).
  - `CALORIE_LIMIT` (Hạn mức calo tối đa mỗi ngày).
  - `LINE_USER_ID` (ID người dùng nhận cảnh báo/báo cáo).
- **Node "When LINE Event Received" (Webhook):** Cấu hình Webhook URL trong LINE Developers trỏ đến đường dẫn của node này (path: `nutrition-webhook`).
- **Node "Gemini Food Analysis Config" & "Gemini Weekly Report Config" (`lmChatGoogleGemini`):** Kết nối tài khoản Google Gemini Credentials và chọn model AI phù hợp (ví dụ: `gemini-1.5-pro` hoặc `gemini-1.5-flash`).
- **Node "Append Meal to Sheets" & "Read Today's Total from Sheets" (`googleSheets`):** Chọn Credentials Google Sheets, trỏ đúng file và tên Sheet dùng để lưu log bữa ăn.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và gửi thử một bức ảnh món ăn qua LINE Bot để test luồng dữ liệu.
- Kiểm tra xem Google Sheets đã ghi nhận dữ liệu chưa và LINE có nhận được tin nhắn phản hồi không.
- Nếu mọi thứ mượt mà, gạt nút **Active** để chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Kết hợp thêm node Telegram hoặc Slack để gửi bản tóm tắt dinh dưỡng vào nhóm làm việc chung nếu các sếp muốn thi đua giảm cân cùng đồng đội.
- **Lưu trữ hình ảnh:** Thêm bước lưu ảnh gốc vào Google Drive tương ứng với dòng log trong Google Sheets để dễ dàng xem lại trực quan.
- **Báo cáo tự động:** Tận dụng trigger `Weekly 9AM Schedule` kết hợp với LLM để tạo thêm các lời khuyên dinh dưỡng hàng tuần mang tính cá nhân hóa cao.

### 📌 Kết luận
Một trợ lý sức khỏe AI ngay trong khung chat LINE quen thuộc sẽ giúp các sếp kiểm soát calo cực kỳ nhẹ nhàng mà không tốn công sức. Hãy triển khai ngay workflow này để nâng tầm cuộc sống healthy của mình nhé!