---
title: "🚀 Tự động soạn email chăm sóc khách hàng báo giá cũ với Claude AI và Google Sheets"
description: "Hướng dẫn xây dựng workflow n8n tự động quét Google Sheets mỗi ngày, dùng Claude AI viết email follow-up cá nhân hóa cho các báo giá cũ và lưu nháp vào Gmail."
slug: "tu-dong-soan-email-follow-up-bao-gia-cu-claude-ai-google-sheets"
tags: [n8n, automation, ai-agents, google-sheets, claude-ai, gmail]
keywords: [n8n workflow, tu dong hoa email, claude ai follow up, google sheets automation, cham soc khach hang tu dong]
---

# 🚀 Tự động soạn email chăm sóc khách hàng báo giá cũ với Claude AI và Google Sheets

Các sếp có đang gặp tình trạng gửi báo giá cho khách hàng nhưng khách "bặt vô âm tín"? Việc rà soát hàng trăm dòng trên Google Sheets mỗi ngày để lọc ra những báo giá quá hạn, sau đó ngồi viết từng email chăm sóc (follow-up) thủ công vừa tốn thời gian, vừa dễ bỏ sót khách hàng tiềm năng.

Đừng lo, bài toán này sẽ được giải quyết triệt để với workflow n8n tự động hóa 100%. Hệ thống sẽ tự động quét danh sách báo giá mỗi ngày, nhờ Claude AI phân tích ngữ cảnh và viết email cá nhân hóa siêu mượt, sau đó tạo sẵn bản nháp (Draft) trên Gmail để các sếp chỉ cần bấm "Gửi".

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không cần thủ công kiểm tra ngày tháng hay soạn email nhắc nhở từng khách hàng.
- **Cá nhân hóa cực cao:** Claude AI đọc lịch sử và thông tin báo giá để viết email tự nhiên, đúng trọng tâm và thuyết phục.
- **Hoạt động tự động 24/7:** Chạy ngầm mỗi ngày đúng giờ hẹn, không bỏ lỡ bất kỳ cơ hội chốt sale nào.
- **An toàn & Kiểm soát:** Lưu thành bản nháp (Draft) trên Gmail thay vì gửi thẳng, giúp các sếp dễ dàng kiểm duyệt trước khi gửi đi.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google Sheets:** File chứa danh sách khách hàng và thông tin báo giá (tên, email, ngày gửi, giá trị, trạng thái...).
- **Anthropic API Key:** Để kết nối với Claude AI.
- **Tài khoản Gmail:** Kết nối qua OAuth2 để tạo bản nháp email.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể copy mã JSON của workflow từ nguồn gốc (ID: 16065 trên n8n.io) và dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy trơn tru, các sếp cần cấu hình chính xác các node sau:

- **When Daily at 9am (`scheduleTrigger`):** Thiết lập khung giờ chạy tự động mỗi ngày (ví dụ: 9 giờ sáng).
- **Set Follow-up Parameters (`set`):** Khai báo các tham số quan trọng như số ngày tối đa được tính là "cũ" (`staleThresholdDays`), tên doanh nghiệp (`businessName`), tên người gửi (`senderName`), và chữ ký email (`emailSignature`).
- **Read Estimates from Sheets & Update Status in Sheets (`googleSheets`):** 
  - Kết nối tài khoản Google Sheets thông qua Credentials.
  - Chọn đúng file Spreadsheet và Range chứa dữ liệu báo giá của các sếp.
  - Đảm bảo node cập nhật trạng thái (`Update Status in Sheets`) trỏ đúng vào cột trạng thái (Status) và dòng tương ứng để đánh dấu báo giá đã được tạo bản nháp follow-up.
- **Filter Stale Estimate Rows & Parse Claude Response (`code`):** Các node JavaScript có sẵn nhiệm vụ lọc dữ liệu thô và bóc tách kết quả trả về từ AI. (Không cần chỉnh sửa code trừ khi sếp muốn tùy biến logic lọc).
- **Post to Claude API (`httpRequest`):** 
  - Thêm Anthropic API Key vào Header xác thực.
  - Chọn model Claude phù hợp (ví dụ: `claude-3-5-sonnet-...`).
  - Tinh chỉnh Prompt trong body request nếu muốn đổi giọng văn của email follow-up.
- **Send Draft via Gmail (`gmail`):** 
  - Kết nối tài khoản Gmail.
  - Map (ánh xạ) các trường dữ liệu tiêu đề và nội dung email được phân tích từ Claude AI vào node tạo Draft (`resource: draft`).

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (**Test step / Test workflow**) với một vài dòng dữ liệu mẫu để kiểm tra kết quả tạo nháp trên Gmail và cập nhật trên Google Sheets.
- Sau khi mọi thứ chạy mượt mà, gạt công tắc sang **Active** để hệ thống tự động chạy ngầm mỗi ngày.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh thông báo:** Nối thêm node Telegram hoặc Slack sau bước tạo nháp thành công để bắn một tin nhắn báo cáo về máy cho nhân viên sales: *"Đã tạo nháp 5 email follow-up mới, sếp vào kiểm tra nhé!"*.
- **Tùy biến Prompt AI:** Thay đổi prompt trong node HTTP Request để Claude viết email theo các phong cách khác nhau (hài hước, trang trọng, thúc giục khẩn cấp...).
- **Quản lý trạng thái chi tiết:** Mở rộng Google Sheets với nhiều trạng thái hơn như `Draft Created`, `Email Sent`, `Customer Replied` để quản lý pipeline bán hàng chuyên nghiệp hơn.

### 📌 Kết luận
Tự động hóa quy trình chăm sóc báo giá cũ không chỉ giúp giải phóng thời gian cho đội ngũ sales mà còn tăng tỷ lệ chốt đơn nhờ phản hồi khách hàng kịp thời. Hãy cài đặt ngay workflow này và tối ưu hóa hệ thống kinh doanh của các sếp ngay hôm nay!