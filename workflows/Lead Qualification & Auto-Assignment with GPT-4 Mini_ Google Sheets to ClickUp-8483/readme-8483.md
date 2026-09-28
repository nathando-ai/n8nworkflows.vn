---
title: "🚀 Tự động hóa chấm điểm Lead và phân bổ công việc với GPT-4 Mini: Google Sheets kết hợp ClickUp"
description: "Hướng dẫn xây dựng workflow n8n tự động lấy lead từ Google Sheets, sử dụng AI đánh giá chất lượng và tự động tạo task, phân công trên ClickUp."
slug: "tu-dong-hoa-cham-diem-lead-gpt-4-mini-google-sheets-clickup"
tags: [n8n, automation, no-code, lead-generation, ai, clickup, google-sheets]
keywords: [n8n workflow, tự động hóa lead, gpt-4 mini, google sheets clickup, phân bổ lead tự động, ai agent automation]
---

# 🚀 Tự động hóa chấm điểm Lead và phân bổ công việc với GPT-4 Mini: Google Sheets kết hợp ClickUp

Các sếp có bao giờ cảm thấy đau đầu khi đội ngũ sales phải mất hàng giờ đồng hồ mỗi ngày chỉ để lọc danh sách khách hàng tiềm năng (lead) thủ công từ Google Sheets, sau đó lại loay hoay phân công task cho nhân sự trên ClickUp? Việc này không chỉ chậm trễ, dễ bỏ sót khách hàng nóng mà còn làm giảm hiệu suất chốt đơn.

Được thiết kế bởi chuyên gia tự động hóa **Rahul Joshi**, workflow n8n này chính là giải pháp tự động hóa 100% không cần code giúp các sếp giải quyết triệt để bài toán trên. Hệ thống sẽ tự động lấy lead mới, dùng AI (GPT-4 Mini) để chấm điểm và phân loại, sau đó tự động tạo task kèm phân công trên ClickUp và cập nhật lại trạng thái vào Google Sheets.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 24/7:** Kiểm tra và xử lý lead mới liên tục mỗi 5 phút mà không cần con người nhúng tay.
- **Chấm điểm thông minh bằng AI:** Sử dụng GPT-4 Mini để phân tích thông tin lead, lọc ra các lead chất lượng cao chuẩn xác.
- **Tăng tốc độ phản hồi:** Lead vừa đổ về Google Sheets lập tức được tạo task và phân bổ cho nhân sự phù hợp trên ClickUp trong chớp mắt.
- **Đồng bộ dữ liệu hai chiều:** Tự động ghi nhận và cập nhật trạng thái xử lý ngược lại vào Google Sheets để tránh trùng lặp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và thông tin sau:
- **n8n Instance** (Self-hosted hoặc n8n Cloud).
- **Tài khoản Google Sheets** (Chứa file dữ liệu lead mẫu).
- **Tài khoản OpenAI** (Cần có OpenAI API Key để dùng mô hình GPT-4 Mini).
- **Tài khoản ClickUp** (Workspace, Space, List ID để tạo task).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ n8n template (ID: 8483) và chọn **Import from File** hoặc copy trực tiếp mã JSON dán vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru, các sếp cần cấu hình chính xác các node quan trọng sau:

- **Getting New Tasks (`googleSheets`):** Kết nối tài khoản Google của bạn, chọn đúng file Sheet chứa danh sách lead và cấu hình để quét các dòng dữ liệu mới (chưa được xử lý).
- **OpenAI Chat Model (`lmChatOpenAi`) & Basic LLM Chain (`chainLlm`):** Thêm OpenAI API Credentials của các sếp. Tại đây, hãy cấu hình sử dụng model `gpt-4-mini` và viết prompt hướng dẫn AI cách đánh giá, chấm điểm lead dựa trên thông tin đầu vào.
- **Restructuring AI Output (`code`):** Node JavaScript này giúp làm sạch và chuyển đổi cấu trúc dữ liệu trả về từ AI thành định dạng JSON chuẩn cho các bước tiếp theo.
- **Qualifying Leads (`if`):** Node điều kiện để lọc ra các lead đạt tiêu chuẩn (Ví dụ: Điểm số từ AI > 7/10). Các lead không đạt sẽ được xử lý theo nhánh riêng (hoặc bỏ qua).
- **Creating and Assigning Tasks (`clickUp`):** Kết nối tài khoản ClickUp, chọn Workspace, Space và List phù hợp. Cấu hình tiêu đề task, mô tả lấy từ dữ liệu lead đã qua xử lý của AI và gán người phụ trách tự động.
- **Restructuring ClickUp Output (`code`):** Node code giúp tinh chỉnh lại dữ liệu phản hồi từ ClickUp sau khi tạo task thành công.
- **Updating New Tasks on Sheets (`googleSheets`):** Cập nhật lại trạng thái dòng lead tương ứng trong Google Sheets (đã chuyển thành công lên ClickUp, tránh việc quét trùng lặp ở lần chạy sau).

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** để chạy thử với dữ liệu mẫu (Test run) và kiểm tra kỹ lưỡng các bước chuyển dữ liệu qua AI, ClickUp và Google Sheets.
- Sau khi mọi thứ chạy mượt mà, gạt công tắc sang **Active** để hệ thống tự động chạy ngầm theo lịch trình node **Every 5 Minutes (`cron`)**.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node Telegram hoặc Slack sau bước tạo task thành công trên ClickUp để bắn thông báo "Nóng! Có lead mới chất lượng cao" thẳng vào nhóm chat của đội sales.
- **Mở rộng bộ lọc:** Tùy chỉnh prompt trong LLM Chain để phân loại lead thành nhiều cấp độ (Hot, Warm, Cold) và phân bổ vào các List khác nhau trên ClickUp tương ứng với từng độ ưu tiên.
- **Lưu trữ Log lỗi:** Thêm nhánh xử lý lỗi (Error Trigger) để tự động gửi email cảnh báo cho quản lý nếu có sự cố mất kết nối API với OpenAI hoặc ClickUp.

### 📌 Kết luận
Workflow tích hợp AI này không chỉ giúp tiết kiệm hàng chục giờ làm việc thủ công mỗi tuần mà còn đảm bảo không bỏ sót bất kỳ khách hàng tiềm năng nào. Hãy cài đặt ngay lên VPS của các sếp và tối ưu hóa quy trình sales ngay hôm nay!