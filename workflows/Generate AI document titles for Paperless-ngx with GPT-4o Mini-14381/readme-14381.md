---
title: "🚀 Tự động đổi tên tài liệu Paperless-ngx chuẩn hóa bằng GPT-4o Mini"
description: "Hướng dẫn xây dựng workflow n8n tự động trích xuất nội dung từ Paperless-ngx, sử dụng AI thông minh để sinh tiêu đề ngắn gọn, chuyên nghiệp và cập nhật trực tiếp vào hệ thống."
slug: "tu-dong-doi-ten-tai-lieu-paperless-ngx-voi-gpt-4o-mini"
tags: [n8n, automation, paperless-ngx, openai, ai-agent, document-management]
keywords: [n8n workflow, paperless-ngx, gpt-4o-mini, tự động đổi tên tài liệu, ai summarization]
---

# 🚀 Tự động đổi tên tài liệu Paperless-ngx chuẩn hóa bằng GPT-4o Mini

Các sếp đang quản lý hệ thống lưu trữ tài liệu số **Paperless-ngx** chắc chắn hiểu rõ nỗi khổ: tài liệu scan hoặc tải lên thường mang tên file gốc rườm rà, mã số khó hiểu (`DOC-2023-10-24-FINAL_v2.pdf`). Việc ngồi đổi tên từng tài liệu thủ công vừa tốn thời gian, vừa dễ gây nhầm lẫn khi tìm kiếm sau này.

Đừng lo, bài toán này sẽ được giải quyết triệt để với workflow n8n tự động hóa 100%. Workflow này sẽ lắng nghe sự kiện từ hệ thống, dùng AI (GPT-4o Mini) đọc hiểu nội dung tài liệu, tự động sinh ra một tiêu đề cực kỳ chuẩn chỉnh và cập nhật ngược lại vào Paperless-ngx, đồng thời dọn dẹp các tag rác không cần thiết.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công, tài liệu cứ lên hệ thống là được xử lý tên gọi.
- **Tiêu đề thông minh, chuẩn SEO/Quản trị**: GPT-4o Mini đọc nội dung chính để đặt tên ngắn gọn, súc tích và phản ánh đúng bản chất tài liệu.
- **Tối ưu hóa quản lý**: Tự động dọn dẹp các tag tạm/thừa (tag removal) trong quá trình xử lý, giúp kho tài liệu luôn ngăn nắp.
- **Vận hành trơn tru 24/7**: Kiểm soát tính hợp lệ của URL, xử lý lỗi thông minh không làm gián đoạn hệ thống.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Hệ thống **Paperless-ngx** đang hoạt động và có cấu hình Webhook.
- Tài khoản/API Key của **OpenAI** (để sử dụng model GPT-4o Mini).
- Thông tin xác thực **HTTP Basic Auth** để n8n kết nối và gọi API tới Paperless-ngx.
- Thông tin **HTTP Header Auth** cho Webhook nhận request.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ kho lưu trữ n8n (Link gốc: [Paperless-ngx GPT-4o Mini Workflow](https://n8n.io/workflows/14381)) và tiến hành Import trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 13 nodes hoạt động nhịp nhàng, các sếp cần chú ý cấu hình kỹ các điểm sau:

- **When Title Update Requested (Webhook)**: Cấu hình endpoint nhận request từ Paperless-ngx với phương thức `POST` tại đường dẫn `update-document-title`. Thiết lập Header Auth để bảo mật kết nối.
- **Check URL Validity & Set URL Components (If & Set)**: Đảm bảo các node kiểm tra và tách chuỗi URL hoạt động chính xác dựa trên cấu trúc đường dẫn API của Paperless-ngx.
- **Fetch Document Content, Fetch Removal Tag ID, Apply Document Updates (HTTP Request)**: Cần điền đúng thông tin **Credentials (httpBasicAuth)** chứa tài khoản/mật khẩu hoặc Token truy cập vào hệ thống Paperless-ngx của các sếp.
- **Apply Document Guardrails (Guardrails)**: Giúp lọc và làm sạch nội dung tài liệu trước khi đưa vào AI xử lý để đảm bảo an toàn thông tin.
- **Generate Title AI Agent & OpenAI GPT-4 Mini (Agent & lmChatOpenAi)**: 
  - Chọn model `gpt-4o-mini`.
  - Cấu hình Prompt trong AI Agent để hướng dẫn AI cách đặt tên tài liệu ngắn gọn, đúng trọng tâm (ví dụ: yêu cầu trả về định dạng `[Ngày/Loại tài liệu] - [Tên chủ đề]`).
- **Execute Tag Removal (Code)**: Tùy chỉnh đoạn code JavaScript bên trong nếu các sếp muốn thay đổi logic lọc hoặc loại bỏ các tag cụ thể sau khi đã xử lý xong tên tài liệu.

#### 3. Kích hoạt ⚡️
- Gửi một request mẫu (Test payload) thông qua Postman hoặc từ Paperless-ngx để kiểm tra luồng dữ liệu chạy qua các node.
- Kiểm tra kết quả trả về xem tiêu đề tài liệu trên Paperless-ngx đã được đổi mới thành công hay chưa.
- Sau khi test ngon lành, các sếp bấm nút **Active** để workflow chính thức đi vào vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo**: Thêm node Telegram hoặc Slack ở cuối workflow để bắn thông báo về máy mỗi khi có một tài liệu được AI đổi tên thành công.
- **Lưu lịch sử xử lý**: Kết nối thêm node Google Sheets hoặc Airtable để lưu lại log các tên cũ và tên mới sau khi AI tối ưu, phục vụ việc kiểm toán sau này.
- **Mở rộng AI**: Có thể thay thế hoặc bổ sung thêm bước phân tích danh mục tài liệu (Document Category) tự động ngoài việc đổi tên.

### 📌 Kết luận
Việc tự động hóa đặt tên tài liệu với Paperless-ngx và GPT-4o Mini không chỉ giúp tiết kiệm hàng giờ đồng hồ quản trị thủ công mà còn xây dựng một hệ thống tri thức số cực kỳ ngăn nắp, chuyên nghiệp cho doanh nghiệp. Hãy áp dụng ngay vào hệ thống của các sếp để cảm nhận sức mạnh của AI và No-code!