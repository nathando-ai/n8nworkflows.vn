---
title: "🧹 Tự động dọn dẹp hộp thư Gmail: Lưu trữ email cũ bằng GPT-4o-mini"
description: "Hướng dẫn xây dựng workflow n8n tự động quét, phân loại email cũ bằng AI GPT-4 và tự động archive những email không còn quan trọng, giúp hộp thư luôn gọn gàng."
slug: "tu-dong-don-dep-gmail-archive-email-cu-bang-gpt-4"
tags: [n8n, automation, gmail, openai, ai-agent, productivity]
keywords: [n8n workflow, dọn dẹp gmail tự động, archive email bằng ai, gpt-4o-mini email classifier, tự động hóa n8n]
---

# 🧹 Tự động dọn dẹp hộp thư Gmail: Lưu trữ email cũ bằng GPT-4o-mini

Các sếp có bao giờ mở hộp thư Gmail lên và cảm thấy ngộp thở với hàng ngàn email cũ từ hàng tháng trước? Việc dọn dẹp thủ công từng email rác, bản tin cũ hay thông báo không quan trọng cực kỳ tốn thời gian. 

Workflow n8n này do **Matt Chong** thiết kế sẽ là trợ thủ đắc lực giúp tự động hóa 100% quy trình này: Quét các email cũ, sử dụng sức mạnh của **AI Agent (GPT-4o-mini)** để đọc hiểu, phân tích ngữ cảnh và tự động `Archive` (lưu trữ) những email không còn giá trị hành động. Các sếp không cần phải đụng tay vào nữa!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Hộp thư sạch sẽ (Inbox Zero):** Tự động loại bỏ các email rác, thông báo cũ ra khỏi tầm mắt mà không sợ bỏ lỡ thông tin quan trọng.
- **AI thông minh phân loại:** Thay vì dùng các bộ lọc (filter) cứng nhắc, GPT-4o-mini sẽ đọc nội dung để đánh giá xem email có còn cần xử lý (due date, action needed) hay có thể vứt đi (trashable).
- **Hoạt động hoàn toàn tự động:** Chạy ngầm định kỳ hàng ngày vào ban đêm mà không làm phiền đến công việc của các sếp.
- **Tiết kiệm hàng giờ đồng hồ:** Không còn cảnh phải ngồi click chọn từng trang email để xóa hoặc lưu trữ thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** (Self-hosted hoặc n8n Cloud).
- **Gmail Account:** Cấp quyền kết nối n8n với tài khoản Gmail của các sếp qua OAuth2.
- **OpenAI API Key:** Để sử dụng model `gpt-4o-mini` phân tích nội dung email.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow hoặc tải file JSON về, sau đó paste trực tiếp vào giao diện n8n Editor (mục **Workflows** -> **Import from File/Clipboard**).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình chính xác các node sau để hệ thống chạy mượt mà:

- **Schedule Trigger:** Mặc định workflow được thiết lập chạy vào lúc 2 giờ sáng mỗi ngày. Các sếp có thể đổi lịch trình này (chạy hàng tuần, hàng ngày...) theo ý muốn.
- **List old inbox emails (Node Gmail):** Node này mặc định lấy tất cả email trong hộp thư đến (Inbox) đã đọc và cũ hơn 45 ngày (`older_than:45d`). Các sếp có thể thay đổi bộ lọc thời gian này trong phần tham số nếu muốn quét các mốc thời gian khác (ví dụ: `30d` hoặc `90d`).
- **OpenAI Chat Model:** Chọn model `gpt-4o-mini` và điền OpenAI API Key của các sếp. Model này vừa thông minh, vừa tiết kiệm chi phí gọi API.
- **AI Agent & Structured Output Parser:** Các sếp giữ nguyên cấu trúc prompt hướng dẫn AI phân tích email (kiểm tra hạn chót, cần hành động hay có thể bỏ đi). Output trả về sẽ ở dạng JSON chuẩn để node `If` dễ dàng bắt điều kiện.
- **Archive Email (Node Gmail):** Khi điều kiện `If - Should archived?` trả về giá trị `true` (email rác/không cần thiết), node này sẽ thực hiện gỡ nhãn `INBOX` (chính là thao tác Archive) để dọn sạch hộp thư đến.

#### 3. Kích hoạt ⚡️
- Bấm nút **Execute Workflow** để chạy thử một vài email mẫu xem hệ thống phân loại chính xác không.
- Sau khi test thành công, bật công tắc **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp thông báo Telegram/Slack:** Thêm một node Telegram hoặc Slack ở nhánh hoàn thành (`Completed`) để gửi báo cáo tóm tắt mỗi sáng về số lượng email đã được AI dọn dẹp sạch sẽ.
- **Thêm nhãn (Label) trước khi Archive:** Thay vì archive thẳng tay, các sếp có thể cấu hình thêm một bước gắn nhãn `AI-Archived` để dễ dàng kiểm tra lại lịch sử nếu cần.

### 📌 Kết luận
Một hộp thư gọn gàng sẽ giúp các sếp giải phóng tâm trí và tập trung vào những email thực sự quan trọng. Hãy cài đặt ngay workflow này để AI giúp các sếp "detox" hộp thư Gmail mỗi ngày!