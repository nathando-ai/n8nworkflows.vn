---
title: "🚀 Tự Động Tạo Bản Thảo Email Gmail Với OpenAI Assistant"
description: "Workflow n8n tự động quét email có label, dùng AI tạo bản thảo trả lời chuyên nghiệp và chèn vào Gmail, giúp tiết kiệm hàng giờ mỗi ngày."
slug: "tu-dong-tao-ban-thao-email-gmail-openai"
tags: [n8n, automation, no-code, gmail, openai, ai-assistant]
keywords: [n8n workflow, tự động hóa email, gmail ai, openai assistant, no-code automation]
---

# 🚀 Tự Động Tạo Bản Thảo Email Gmail Với OpenAI Assistant

Trong môi trường kinh doanh hiện đại, hộp thư Gmail thường xuyên bị "ngập" bởi các yêu cầu lặp đi lặp lại: hỗ trợ kỹ thuật, xác nhận đơn hàng, hay các câu hỏi thường gặp. Việc đọc từng email, suy nghĩ câu trả lời và gõ lại từ đầu không chỉ tốn thời gian mà còn dễ gây sai sót do mệt mỏi.

Workflow này chính là "trợ lý ảo" của các sếp. Nó hoạt động như một quy trình khép kín: **Quét email có label đặc biệt -> Gửi nội dung cho OpenAI Assistant -> Nhận câu trả lời AI -> Tạo bản thảo (Draft) trong Gmail -> Xóa label.** Các sếp chỉ cần mở Gmail, xem qua bản thảo AI đã soạn sẵn, chỉnh sửa nhẹ (nếu cần) và nhấn gửi. Toàn bộ quá trình diễn ra tự động, không cần viết một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian đáng kể:** Loại bỏ hoàn toàn bước gõ phím cho các email lặp lại, chỉ cần review và gửi.
- **Độ nhất quán cao:** AI luôn trả lời với giọng văn chuyên nghiệp, đúng chuẩn thương hiệu mà các sếp đã thiết lập trong Assistant.
- **Hoạt động liên tục:** Workflow chạy theo lịch (mỗi 1 phút), đảm bảo không có email nào bị bỏ sót dù là ngoài giờ hành chính.
- **Dễ kiểm soát:** Kết quả được đưa vào **Draft** (Bản thảo) thay vì gửi tự động, giúp con người vẫn giữ quyền quyết định cuối cùng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Gmail:** Đã bật quyền truy cập API (OAuth2).
- **Tài khoản OpenAI:** Có API Key và đã tạo sẵn một **Assistant** (trợ lý) được thiết lập với hệ thống prompt (System Prompt) phù hợp với ngành nghề của các sếp.
- **Label Gmail:** Tạo một label riêng (ví dụ: `AI-REPLY-TRIGGER`) để đánh dấu các email cần AI xử lý.
- **n8n Instance:** Đã cài đặt và chạy (Self-hosted hoặc Cloud).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON workflow từ link gốc hoặc copy toàn bộ code JSON.
2. Mở n8n Editor, chọn **Import from URL** hoặc **Import from File**.
3. Nếu copy JSON, hãy dán trực tiếp vào editor hoặc tạo workflow mới và dán vào tab JSON.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Đây là phần quan trọng nhất. Các sếp cần kiểm tra kỹ các node sau:

1.  **Node: `Schedule trigger (1 min)`**
    - Mặc định chạy mỗi 1 phút. Các sếp có thể điều chỉnh tần suất nếu muốn (ví dụ: mỗi 5 phút) để giảm tải API.

2.  **Node: `Get threads with specific labels`**
    - **Credentials:** Chọn tài khoản Gmail OAuth2 của các sếp.
    - **Parameters:** Trong phần `Labels`, nhập chính xác tên label mà các sếp đã tạo (ví dụ: `AI-REPLY-TRIGGER`). Đây là "công tắc" kích hoạt workflow.

3.  **Node: `Ask OpenAI Assistant`**
    - **Credentials:** Chọn API Key OpenAI.
    - **Assistant ID:** Nhập ID của OpenAI Assistant mà các sếp đã tạo.
    - **Prompt:** Mặc định là `define`. Các sếp có thể giữ nguyên hoặc tùy chỉnh prompt nếu muốn yêu cầu AI thêm thông tin cụ thể (ví dụ: "Trả lời ngắn gọn và thân thiện").
    - *Lưu ý:* Đảm bảo Assistant của các sếp đã được nạp dữ liệu (Knowledge) hoặc có System Prompt tốt để trả lời chính xác.

4.  **Node: `Add email draft to thread`**
    - **Credentials:** Chọn cùng tài khoản Gmail OAuth2.
    - Node này sẽ tự động lấy dữ liệu từ các node trước đó để tạo draft. Các sếp thường không cần chỉnh sửa gì thêm nếu cấu hình đúng các node trước.

5.  **Node: `Remove AI label from email`**
    - **Credentials:** Chọn tài khoản Gmail OAuth2.
    - **Label ID:** Nhập ID của label trigger (có thể lấy từ Gmail Settings hoặc dùng tên label nếu node hỗ trợ). Việc này giúp tránh việc AI xử lý lại cùng một email nhiều lần.

#### 3. Kích hoạt ⚡️
1. **Test Run:**
   - Gửi một email mẫu đến hộp thư của chính các sếp.
   - Đánh dấu email đó bằng label trigger (ví dụ: `AI-REPLY-TRIGGER`).
   - Chạy workflow thủ công (Manual Execution) hoặc chờ đến chu kỳ kế tiếp.
   - Kiểm tra hộp thư Gmail, xem có bản thảo (Draft) mới xuất hiện không.
2. **Bật Active:**
   - Sau khi test thành công, nhấn nút **Active** ở góc trên bên phải để workflow chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram/Slack:** Thêm một node `Telegram` hoặc `Slack` sau bước tạo draft để gửi thông báo: "Đã tạo bản thảo cho email từ [Người gửi], vui lòng kiểm tra Gmail."
- **Phân loại email:** Thay vì một label duy nhất, các sếp có thể tạo nhiều label (ví dụ: `AI-SUPPORT`, `AI-SALES`) và dùng node `Switch` để gọi các OpenAI Assistant khác nhau với giọng văn khác nhau.
- **Lưu log vào Google Sheets:** Thêm node `Google Sheets` để ghi lại lịch sử các email đã được AI xử lý, giúp theo dõi hiệu quả và thống kê.
- **Tự động gửi (Cẩn thận):** Nếu tin tưởng AI tuyệt đối, các sếp có thể thay đổi node `Add email draft to thread` thành `Send email` để gửi tự động. Tuy nhiên, khuyến nghị nên giữ ở chế độ Draft để con người kiểm duyệt.

### 📌 Kết luận
Workflow này là một bước tiến lớn trong việc ứng dụng AI vào quy trình làm việc hàng ngày. Bằng cách tự động hóa việc soạn thảo email, các sếp có thể tập trung vào những công việc sáng tạo và chiến lược hơn, trong khi AI lo phần "chân tay". Hãy thử ngay hôm nay và trải nghiệm sự khác biệt!