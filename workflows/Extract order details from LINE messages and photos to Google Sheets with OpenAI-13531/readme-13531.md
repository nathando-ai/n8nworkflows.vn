---
title: "🚀 Tự động trích xuất đơn hàng từ tin nhắn và hình ảnh LINE vào Google Sheets bằng AI"
description: "Hướng dẫn xây dựng workflow n8n tự động phân tích tin nhắn text và hình ảnh đơn hàng từ LINE, xử lý bằng OpenAI GPT và lưu trữ gọn gàng vào Google Sheets."
slug: "trich-xuat-don-hang-line-google-sheets-openai"
tags: [n8n, automation, no-code, line-bot, openai, google-sheets]
keywords: [n8n workflow, tự động hóa LINE, trích xuất đơn hàng AI, OpenAI GPT, Google Sheets automation]
---

# 🚀 Tự động trích xuất đơn hàng từ tin nhắn và hình ảnh LINE vào Google Sheets bằng AI

Các sếp đang kinh doanh qua ứng dụng chat LINE chắc chắn hiểu cảm giác mệt mỏi khi phải đọc từng tin nhắn đặt hàng, xem từng bức ảnh chụp ghi chú viết tay, sau đó thủ công copy dữ liệu vào file Excel hay Google Sheets. Quá trình này không chỉ tốn thời gian, dễ nhầm lẫn mà còn khiến khách hàng phải chờ đợi phản hồi lâu.

Giải pháp ở đây là gì? Workflow n8n này sẽ giúp các sếp tự động hóa 100% quy trình: Nhận tin nhắn/hình ảnh từ LINE $\rightarrow$ AI (OpenAI) phân tích và trích xuất thông tin đơn hàng $\rightarrow$ Xác nhận với khách hàng $\rightarrow$ Lưu thẳng vào Google Sheets. Tất cả diễn ra tự động mà không cần một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện**: Xử lý cả tin nhắn văn bản lẫn hình ảnh (như ảnh chụp hóa đơn, giấy ghi chú viết tay) gửi qua LINE.
- **Trợ lý AI thông minh**: Sử dụng OpenAI GPT để bóc tách chính xác tên sản phẩm, số lượng, ghi chú từ dữ liệu thô.
- **Tương tác mượt mà**: AI tự động hỏi lại khách hàng để xác nhận thông tin trước khi chốt đơn.
- **Đồng bộ thời gian thực**: Đơn hàng được ghi nhận ngay lập tức vào Google Sheets, giúp quản lý kho và doanh thu dễ dàng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **LINE Official Account / Messaging API**: Tài khoản LINE Developer để cấu hình Webhook.
- **OpenAI API Key**: Tài khoản OpenAI có quyền gọi mô hình GPT.
- **Google Account**: Tài khoản Google Drive/Sheets để lưu trữ dữ liệu đơn hàng.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ n8n template (ID: 13531) và import trực tiếp vào giao diện n8n của mình, hoặc tạo mới và thêm các node tương ứng.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống vận hành trơn tru, các sếp cần cấu hình chính xác các node cốt lõi sau:

- **Line Messaging Trigger1**: Kết nối với tài khoản LINE Messaging API của các sếp. Cấu hình Webhook URL từ n8n dán vào LINE Developer Console.
- **Route by Message Type (Switch)**: Node này sẽ phân loại dữ liệu đầu vào. Tin nhắn văn bản sẽ đi thẳng tới AI Agent, còn tin nhắn dạng hình ảnh sẽ được chuyển hướng sang node tải ảnh.
- **Download LINE Image**: Sử dụng `lineMessagingData` để tải ảnh đơn hàng mà khách gửi qua khung chat LINE.
- **AI Agent - Order Extractor1 & OpenAI GPT-4o1**: Cấu hình OpenAI Credentials. Chọn model (ví dụ: `gpt-4.1-mini` hoặc `gpt-4o`) và viết System Prompt hướng dẫn AI cách trích xuất dữ liệu chuẩn xác từ text/hình ảnh.
- **Simple Memory - Chat History1**: Giúp AI ghi nhớ ngữ cảnh hội thoại để trò chuyện mượt mà hơn với khách hàng.
- **Append Row to Google Sheets**: 
  - Chọn tài khoản Google Sheets Credentials (OAuth2).
  - Trỏ tới Spreadsheet ID và chọn đúng tên Sheet (Sheet Name) chứa bảng quản lý đơn hàng của các sếp.
  - Map các trường dữ liệu mà AI trích xuất được vào các cột tương ứng trong Google Sheets.
- **Reply via LINE**: Node gửi tin nhắn phản hồi tự động lại cho khách hàng qua LINE (xác nhận đơn hàng đã được ghi nhận).

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và gửi một tin nhắn hoặc hình ảnh test qua tài khoản LINE OA để kiểm tra luồng chạy.
- Sau khi test thành công, gạt công tắc sang **Active** để đưa bot vào hoạt động chính thức 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo nội bộ**: Thêm node gửi thông báo về Telegram hoặc Slack cho đội ngũ bán hàng ngay khi có đơn hàng mới được ghi vào Google Sheets.
- **Xử lý trạng thái đơn hàng**: Mở rộng Google Sheets với cột "Trạng thái" (Chờ xác nhận, Đang giao, Hoàn thành) để quản lý vòng đời đơn hàng tốt hơn.
- **Lưu file ảnh**: Kết hợp node Google Drive để lưu lại hình ảnh hóa đơn/ghi chú mà khách gửi lên cloud, giúp dễ dàng đối soát sau này.

### 📌 Kết luận
Việc tự động hóa quy trình nhận và xử lý đơn hàng từ LINE chưa bao giờ dễ dàng đến thế với sức mạnh của n8n và AI. Hãy áp dụng ngay workflow này để tối ưu hóa vận hành, tiết kiệm thời gian nhân sự và mang lại trải nghiệm chuyên nghiệp nhất cho khách hàng của các sếp nhé!