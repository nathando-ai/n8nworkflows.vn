---
title: "🚀 Tự động tạo và gửi email truyện cười cá nhân hóa bằng GPT-4o-mini và Gmail"
description: "Hướng dẫn xây dựng workflow n8n tự động thu thập yêu cầu qua form, sử dụng AI thông minh để sáng tạo truyện cười theo ngôn ngữ tùy chọn và gửi trực tiếp qua Gmail."
slug: "tu-dong-tao-va-gui-email-truyen-cuoi-gpt-4o-mini-gmail"
tags: [n8n, automation, no-code, openai, gmail, ai-agents]
keywords: [n8n workflow, tự động hóa gmail, openai gpt-4o-mini, tạo truyện cười tự động, n8n form trigger]
---

# 🚀 Tự động tạo và gửi email truyện cười cá nhân hóa với GPT-4o-mini và Gmail

Các sếp có bao giờ muốn mang lại tiếng cười cho bạn bè, đồng nghiệp hoặc khách hàng mỗi ngày mà không tốn công nghĩ nội dung hay soạn email thủ công chưa? Việc phải nghĩ ra một câu chuyện cười hay, đúng chủ đề, đúng ngôn ngữ rồi lại lúi húi copy paste vào Gmail thực sự tốn thời gian và nhàm chán.

Với sự trợ giúp của **n8n**, bài toán này sẽ được giải quyết 100% tự động. Workflow này sẽ giúp các sếp tạo ra một hệ thống "pha trò" tự động: Nhận yêu cầu từ Form, nhờ siêu trí tuệ **GPT-4o-mini** sáng tạo truyện cười theo đúng ngôn ngữ tùy chọn, và tự động gửi thẳng vào hộp thư của người nhận qua **Gmail**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Từ lúc người dùng điền form cho đến khi email truyện cười nằm trong inbox chỉ mất vài giây.
- **Cá nhân hóa đỉnh cao:** AI (GPT-4o-mini) sẽ sáng tạo nội dung dựa trên thông tin đầu vào, hỗ trợ đa ngôn ngữ linh hoạt.
- **Tiết kiệm thời gian:** Không còn phải thủ công soạn thảo từng email chúc vui hay nội dung giải trí.
- **Hoạt động 24/7:** Hệ thống luôn sẵn sàng "pha trò" bất cứ lúc nào có request mới mà không cần con người can thiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow chạy mượt mà, các sếp cần chuẩn bị sẵn:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **OpenAI API Key** (để kết nối với node OpenAI sử dụng mô hình GPT-4o-mini).
- **Tài khoản Google/Gmail** (để cấu hình xác thực OAuth2 cho node Gmail gửi thư).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ thư viện n8n (ID: `5525`) hoặc copy đoạn mã JSON tương ứng và paste trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 4 nodes chính được bố trí cực kỳ gọn gàng. Các sếp cần cấu hình lần lượt các điểm sau:

- **Node `On form submission` (Form Trigger):** 
  - Đây là điểm khởi đầu. Các sếp hãy cấu hình giao diện Form (tiêu đề, các trường dữ liệu như: Tên người nhận, Email, Chủ đề truyện cười, Ngôn ngữ mong muốn...).
- **Node `LANG` (Set Node):** 
  - Dùng để xử lý và chuẩn hóa các biến đầu vào từ form trước khi chuyển sang AI. Các sếp hãy kiểm tra lại các trường dữ liệu (như thiết lập ngôn ngữ hiển thị dựa theo note canvas: *Set the output language*).
- **Node `OpenAI` (OpenAI Model / GPT-4o-mini):** 
  - Kết nối credentials bằng OpenAI API Key của các sếp.
  - Viết Prompt hướng dẫn AI (lưu ý theo canvas: *Prompt message approx. using 200 tokens*). Ví dụ: *"Hãy viết một câu chuyện cười ngắn gọn, hài hước, văn phong vui vẻ bằng ngôn ngữ [Biến ngôn ngữ] với chủ đề [Biến chủ đề từ form]"*.
- **Node `Gmail`:** 
  - Kết nối tài khoản Gmail thông qua **OAuth2**.
  - Thiết lập người nhận (`To`: lấy từ email điền trên form), tiêu đề email (`Subject`) và phần nội dung (`Body`: lấy kết quả trả về từ node OpenAI).

#### 3. Kích hoạt ⚡️
- Nhấn **Test step** hoặc **Execute Workflow** để thử nghiệm điền form mẫu và kiểm tra xem email đã được gửi đi thành công chưa.
- Sau khi test ngon lành, các sếp nhớ gạt công tắc **Active** ở góc trên bên phải để workflow chính thức đi vào hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Telegram/Slack:** Thêm một node thông báo về kênh chat nội bộ mỗi khi có ai đó sử dụng form xin truyện cười.
- **Lưu trữ dữ liệu:** Thêm node **Google Sheets** hoặc **Airtable** để lưu lại thông tin người nhận và câu chuyện cười đã tạo nhằm mục đích thống kê hoặc chăm sóc khách hàng.
- **Lên lịch định kỳ:** Thay vì dùng Form Trigger, các sếp có thể đổi thành **Schedule Trigger** để hệ thống tự động gửi truyện cười mỗi sáng cho danh sách VIP khách hàng hoặc team nội bộ.

### 📌 Kết luận
Một workflow đơn giản nhưng cực kỳ thú vị và thực tế phải không các sếp? Chỉ với 4 nodes cơ bản, các sếp đã có thể tự động hóa quy trình sáng tạo nội dung và chăm sóc người dùng bằng AI. Lên đồ và áp dụng ngay thôi nào!