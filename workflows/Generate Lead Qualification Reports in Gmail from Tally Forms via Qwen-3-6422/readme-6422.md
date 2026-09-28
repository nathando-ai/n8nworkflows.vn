---
title: "🚀 Tự động chấm điểm và gửi báo cáo Lead từ Tally Forms qua Qwen-3 và Gmail"
description: "Hướng dẫn xây dựng workflow n8n tự động tiếp nhận thông tin từ Tally Forms, sử dụng AI Qwen-3 qua OpenRouter để chấm điểm lead và gửi báo cáo chi tiết qua Gmail."
slug: "tu-dong-cham-dieu-lead-tally-form-qwen-3-gmail"
tags: [n8n, automation, taly-forms, ai-lead-qualification, qwen-3, openrouter]
keywords: [n8n workflow, tally forms n8n, qwen-3 openrouter, tự động hóa lead generation, chấm điểm lead bằng ai, gửi email tự động gmail]
---

# 🚀 Tự động chấm điểm và gửi báo cáo Lead từ Tally Forms qua Qwen-3 và Gmail

Các sếp có đang gặp tình trạng mỗi khi có khách hàng điền form đăng ký trên website (Tally Forms), đội ngũ kinh doanh lại mất hàng giờ để đọc, phân tích và đánh giá xem khách hàng này có tiềm năng hay không? Việc làm thủ công này không chỉ chậm trễ, dễ bỏ sót khách hàng nóng mà còn tốn rất nhiều thời gian nhân sự.

Giải pháp ở đây là gì? Một hệ thống tự động hóa 100% không cần code (No-code) với **n8n**. Workflow này sẽ ngay lập tức tiếp nhận thông tin từ Tally Form, nhờ trí tuệ nhân tạo (AI model Qwen-3 hoặc Gemini thông qua OpenRouter) phân tích, đánh giá chất lượng (lead qualification) và gửi ngay một báo cáo chi tiết vào hộp thư Gmail của các sếp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phản hồi & Xử lý tức thì:** Ngay khi khách bấm "Submit" form, AI đã phân tích xong xuôi trong tích tắc.
- **Chấm điểm Lead chuẩn xác:** AI tự động đọc insight câu trả lời để phân loại mức độ tiềm năng (Nóng, Ấm, Lạnh) và đưa ra gợi ý tiếp cận.
- **Tiết kiệm thời gian nhân sự:** Không cần đọc thủ công từng câu trả lời dài dằng dặc, nhận ngay bản tóm gọn trực tiếp qua Gmail.
- **Vận hành 24/7 không gián đoạn:** Hệ thống tự động hoàn toàn, không bỏ sót bất kỳ một khách hàng tiềm năng nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản **n8n** (Cloud hoặc Self-hosted).
- Tài khoản **Tally.so** để tạo form thu thập thông tin khách hàng.
- Tài khoản **OpenRouter** (để kết nối các mô hình AI mạnh mẽ như Qwen-3 hoặc Gemini).
- Tài khoản **Gmail** (để cấu hình node gửi email báo cáo).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng file JSON của workflow này, copy và paste trực tiếp vào không gian làm việc (n8n Editor) của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các thành phần sau:

- **Tally Form Response (Node Webhook):** 
  - Lấy đường dẫn **Production URL** từ node này.
  - Mang đường dẫn đó dán vào phần Integrations/Webhook trong bảng điều khiển của Tally Form.
- **Set Email (Node Set):** 
  - Vào node này và điền chính xác địa chỉ email của các sếp (hoặc email của đội Sales) vào phần cấu hình để nhận báo cáo từ LLM.
- **Qwen3-07-25 & Gemini 2.5 pro (Node Chat Model / OpenRouter):** 
  - Cần thêm **OpenRouter API Credentials** của các sếp vào đây để mô hình AI có thể hoạt động.
- **Qualify Lead (Node Chain LLM):** 
  - Nơi thiết lập Prompt để hướng dẫn AI cách đọc dữ liệu từ Tally Form và đưa ra tiêu chí chấm điểm lead phù hợp với sản phẩm/dịch vụ của công ty.
- **Send a message (Node Gmail):** 
  - Kết nối tài khoản Gmail cá nhân hoặc doanh nghiệp thông qua **Gmail OAuth2** để cho phép n8n gửi email thay mặt các sếp.

#### 3. Kích hoạt ⚡️
- Thực hiện một lượt **Test Run** bằng cách submit thử một form trên Tally để kiểm tra dòng dữ liệu chạy qua từng node.
- Kiểm tra hộp thư Gmail xem đã nhận được báo cáo từ AI hay chưa.
- Nếu mọi thứ mượt mà, hãy gạt công tắc sang **Active** để workflow chính thức đi vào hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa kênh thông báo:** Ngoài gửi Gmail, các sếp có thể nối thêm node Telegram hoặc Slack để bắn tin nhắn thông báo lead nóng vào nhóm chat công ty ngay lập tức.
- **Lưu trữ dữ liệu:** Thêm node Google Sheets ngay sau Webhook để lưu lại toàn bộ thông tin khách hàng điền form làm cơ sở dữ liệu (CRM thu nhỏ).
- **Cá nhân hóa Prompt:** Tinh chỉnh prompt trong node *Qualify Lead* để AI phân loại lead theo đúng bộ khung BANT (Budget, Authority, Need, Timeframe) của doanh nghiệp.

### 📌 Kết luận
Việc tự động hóa khâu phân loại khách hàng tiềm năng chưa bao giờ dễ dàng đến thế với sự kết hợp giữa Tally Forms, n8n và các mô hình AI mạnh mẽ như Qwen-3. Hãy triển khai ngay hôm nay để tối ưu hóa quy trình sales và không bỏ lỡ bất kỳ khách hàng chất lượng nào các sếp nhé!