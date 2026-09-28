---
title: "🚀 Tự động sáng tạo công thức nấu ăn từ nguyên liệu có sẵn với Google Gemini và n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình nhận nguyên liệu từ form, kết hợp AI Google Gemini để tạo công thức nấu ăn và lưu trữ Google Sheets, gửi Gmail."
slug: "tao-cong-thuc-nau-an-tu-dong-google-gemini-n8n"
tags: [n8n, automation, google-gemini, google-sheets, gmail, ai-workflow]
keywords: [n8n workflow, tự động hóa n8n, google gemini ai, tạo công thức nấu ăn, google sheets, automation no-code]
---

# 🚀 Tự động sáng tạo công thức nấu ăn từ nguyên liệu có sẵn với AI

Các sếp có bao giờ rơi vào cảnh mở tủ lạnh ra thấy một đống nguyên liệu lộn xộn nhưng chẳng biết hôm nay nấu món gì chưa? Việc nghĩ thực đơn mỗi ngày vừa tốn thời gian, vừa đau đầu, đặc biệt là khi muốn tận dụng những thứ còn thừa trong tủ lạnh. 

Thay vì ngồi tra Google từng món một, tại sao các sếp không tự động hóa hoàn toàn quy trình này? Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ thông minh: Nhập nguyên liệu vào Form 👉 AI Google Gemini "biến hóa" thành các công thức món ăn độc đáo 👉 Tự động lưu vào Google Sheets và gửi email kết quả qua Gmail!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tối đa:** Chỉ mất chưa đầy 30 giây từ lúc điền nguyên liệu đến khi nhận được thực đơn chi tiết.
- **Tận dụng thông minh:** Giúp giảm thiểu lãng phí thực phẩm bằng cách gợi ý món ăn từ những nguyên liệu sẵn có trong nhà.
- **Cá nhân hóa cao:** AI Google Gemini tự động sáng tạo ra các công thức chuẩn vị, đầy đủ nguyên liệu, định lượng và hướng dẫn từng bước.
- **Lưu trữ & Chia sẻ tiện lợi:** Tự động ghi nhận lịch sử vào Google Sheets và gửi thẳng vào hộp thư Gmail cá nhân.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Google Gemini API Key:** Để kết nối với node LangChain Google Gemini.
- **Google Sheets Credentials:** Tài khoản Google để kết nối và ghi dữ liệu công thức.
- **Gmail Credentials:** Tài khoản Gmail để cấu hình node gửi email tự động.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ thư viện n8n gốc hoặc copy JSON và dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động mượt mà, các sếp cần cấu hình các node cốt lõi sau:

- **Form Trigger (n8n-nodes-base.formTrigger):** 
  - Tạo giao diện form đơn giản để người dùng nhập danh sách nguyên liệu đang có (ví dụ: Thịt bò, cà chua, hành tây...).
- **Set & Code Nodes (n8n-nodes-base.set, n8n-nodes-base.code):** 
  - Dùng để chuẩn hóa dữ liệu đầu vào từ form, làm sạch text trước khi truyền vào AI.
- **Google Gemini (LangChain Node - `@n8n/n8n-nodes-langchain.googleGemini`):**
  - Cần điền `Gemini API Key`.
  - Viết Prompt hướng dẫn AI (System Prompt) rõ ràng: *"Bạn là một đầu bếp chuyên nghiệp. Hãy dựa vào các nguyên liệu sau để tạo ra 2 công thức nấu ăn hấp dẫn, bao gồm tên món, nguyên liệu chi tiết và các bước thực hiện..."*
- **Google Sheets (n8n-nodes-base.googleSheets):**
  - Kết nối tài khoản Google.
  - Chọn file Spreadsheet và Sheet Name để lưu thông tin ngày tháng, nguyên liệu đầu vào và công thức do AI tạo ra.
- **Gmail (n8n-nodes-base.gmail):**
  - Cấu hình tài khoản gửi.
  - Soạn nội dung email động (lấy kết quả từ node Google Gemini) để gửi công thức hoàn chỉnh về hòm thư.
- **Sticky Notes (n8n-nodes-base.stickyNote):** 
  - Các ghi chú màu sắc hướng dẫn trực quan trên màn hình canvas giúp các sếp dễ dàng hình dung luồng chạy.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng cách điền form mẫu.
- Kiểm tra lại dữ liệu trên Google Sheets và hộp thư Gmail xem đã nhận được "thành quả" thơm ngon chưa.
- Nếu mọi thứ trơn tru, hãy gạt công tắc sang **Active** để bật chế độ tự động 24/7!

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Chatbot:** Thay vì dùng Form Trigger, các sếp có thể đổi thành Telegram Trigger hoặc Slack Trigger để gửi nguyên liệu qua tin nhắn cho nhanh.
- **Lưu lịch sử ăn uống:** Kết hợp thêm Google Calendar để lên thực đơn tuần tự động dựa trên các công thức đã tạo.
- **Đa dạng hóa phong cách:** Thêm lựa chọn "Món Á", "Món Âu", hoặc "Eat Clean" vào form để AI điều chỉnh công thức phù hợp với chế độ dinh dưỡng.

### 📌 Kết luận
Workflow này là một minh họa tuyệt vời cho thấy sức mạnh của việc kết hợp No-code (n8n) và Multimodal AI (Google Gemini) vào đời sống hàng ngày cũng như tối ưu hóa quy trình làm việc. Chúc các sếp cài đặt thành công và có những trải nghiệm tự động hóa thú vị! Nếu gặp khó khăn gì, cứ mạnh dạn để lại bình luận nhé!