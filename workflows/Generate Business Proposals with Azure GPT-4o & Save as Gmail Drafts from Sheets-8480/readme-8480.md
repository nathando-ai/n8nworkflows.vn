---
title: "🚀 Tự động tạo Hồ sơ năng lực (Business Proposal) với Azure GPT-4o và lưu Nháp Gmail từ Google Sheets"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa hoàn toàn quy trình tạo đề xuất kinh doanh cá nhân hóa bằng AI Azure OpenAI và lưu trực tiếp vào bản nháp Gmail."
slug: "tao-business-proposal-azure-gpt-4o-gmail-google-sheets"
tags: [n8n, automation, no-code, azure-openai, gmail, google-sheets, ai-agent]
keywords: [n8n workflow, tự động hóa business proposal, azure openai n8n, tao nhap gmail tu google sheets, ai agent n8n]
---

# 🚀 Tự động tạo Hồ sơ năng lực (Business Proposal) với Azure GPT-4o và lưu Nháp Gmail từ Google Sheets

Các sếp có bao giờ cảm thấy mệt mỏi khi phải ngồi hàng giờ liền để viết từng bản đề xuất kinh doanh (Business Proposal) cho khách hàng tiềm năng? Việc viết thủ công không chỉ tốn thời gian, dễ sai sót mà còn khó cá nhân hóa ở quy mô lớn, khiến doanh nghiệp bỏ lỡ nhiều cơ hội vàng.

Đừng lo, giải pháp đã có ở đây! Bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n cực kỳ thông minh, được sáng lập bởi chuyên gia Rahul Joshi. Workflow này sẽ tự động đọc danh sách khách hàng từ **Google Sheets**, sử dụng sức mạnh siêu việt của **Azure GPT-4o (AI Agent)** để soạn thảo những bản proposal chuyên nghiệp, sau đó tự động tạo sẵn **bản nháp trên Gmail** để các sếp chỉ cần duyệt và bấm gửi.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không còn cảnh copy-paste thủ công thông tin khách hàng để viết email hay proposal dài dòng.
- **Cá nhân hóa đỉnh cao:** AI Agent dựa trên dữ liệu thực tế từ Google Sheets để tạo ra các đề xuất chuẩn xác, trúng "tử huyệt" nhu cầu của từng khách hàng.
- **Kiểm soát tuyệt đối:** Workflow tự động lưu vào **Gmail Drafts**, giúp các sếp dễ dàng kiểm tra, tinh chỉnh lại nội dung trước khi chính thức gửi đi.
- **Vận hành trơn tru:** Xử lý danh sách hàng loạt với cơ chế chia lô (batching) thông minh, hạn chế tối đa tình trạng quá tải API.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và thông tin sau:
1. **Hệ thống n8n** (Cloud hoặc Self-hosted).
2. **Google Sheets**: Một file Google Sheets chứa thông tin khách hàng (Tên, Email, Yêu cầu/Dự án, Trạng thái...).
3. **Azure OpenAI Account**: API Key và Deployment Name cho model GPT-4o.
4. **Google Account (Gmail)**: Tài khoản Gmail dùng để kết nối và tạo bản nháp email.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải mã nguồn JSON của workflow từ hệ thống n8n (Link gốc: [n8n Workflow #8480](https://n8n.io/workflows/8480)) và import trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import thành công, các sếp cần cấu hình chính xác các node quan trọng sau đây:

- **Node `Get row(s) in sheet` (Google Sheets):** 
  - Chọn tài khoản Google Sheets Credentials của các sếp.
  - Điền chính xác `Document ID` và `Sheet Name` chứa dữ liệu khách hàng cần tạo proposal.
- **Node `checks propsal status` (If):** 
  - Cấu hình điều kiện kiểm tra (ví dụ: chỉ xử lý những dòng có trạng thái `Pending` hoặc chưa được tạo proposal) để tránh việc chạy trùng lặp dữ liệu.
- **Node `Loop Over Items` (Split In Batches):** 
  - Giúp xử lý dữ liệu theo từng nhóm nhỏ (mặc định có thể để batch size là 1) để AI và Gmail API không bị quá tải.
- **Node `AI Agent` & `Azure OpenAI Chat Model`:** 
  - Kết nối tài khoản Azure OpenAI (nhập Endpoint và API Key).
  - Viết Prompt chi tiết trong AI Agent, hướng dẫn AI cách đóng vai chuyên gia sales để viết bản proposal dựa trên thông tin nhận được từ Google Sheets.
- **Node `Code`:** 
  - Dùng để làm sạch (sanitize) dữ liệu đầu ra từ AI, định dạng lại tiêu đề và nội dung email/proposal cho chuẩn cú pháp trước khi đẩy sang Gmail.
- **Node `Create a draft` (Gmail):** 
  - Chọn tài khoản Gmail Credentials.
  - Map các trường dữ liệu đầu ra từ node Code vào các trường `To`, `Subject`, và `Message` (Body) của Gmail Draft.

#### 3. Kích hoạt ⚡️
- Bấm nút **`When clicking ‘Execute workflow’`** để test thủ công với 1-2 dòng dữ liệu mẫu trên Google Sheets xem bản nháp Gmail đã được tạo thành công chưa.
- Kiểm tra lại hộp thư Gmail phần **Drafts (Bản nháp)**. Nếu mọi thứ hiển thị hoàn hảo, hãy bật công tắc **Active** để workflow tự động hóa hoạt động ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tự động hóa theo lịch:** Thay thế node `Manual Trigger` bằng node `Schedule Trigger` để n8n tự động quét Google Sheets vào mỗi sáng thứ Hai hàng tuần.
- **Thông báo qua Telegram/Slack:** Thêm một node Telegram hoặc Slack vào cuối chuỗi để bắn thông báo về máy cho các sếp ngay khi tất cả các bản nháp proposal đã được tạo xong.
- **Cập nhật trạng thái Sheet:** Thêm node `Update row in sheet` ngay sau khi tạo nháp Gmail thành công để đổi trạng thái dòng đó thành `Draft Created`, giúp dễ dàng quản lý tiến độ.

### 📌 Kết luận
Việc tự động hóa quy trình viết Business Proposal bằng Azure GPT-4o và n8n không chỉ giúp tiết kiệm hàng đống thời gian mà còn nâng tầm chuyên nghiệp cho doanh nghiệp trong mắt khách hàng. Hãy cài đặt ngay workflow này để tối ưu hóa hiệu suất làm việc ngay hôm nay các sếp nhé!