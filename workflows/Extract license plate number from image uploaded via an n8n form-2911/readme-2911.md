---
title: "🚀 Tự động nhận diện biển số xe từ ảnh tải lên n8n Form bằng AI OpenRouter"
description: "Hướng dẫn xây dựng workflow n8n tự động trích xuất biển số xe từ hình ảnh người dùng upload qua Form trực tuyến, sử dụng AI Vision siêu nhạy."
slug: "tu-dong-nhan-dien-bien-so-xe-n8n-form-ai"
tags: [n8n, automation, ai, openrouter, computer-vision, workflow]
keywords: [n8n workflow, nhận diện biển số xe, đọc biển số xe qua ảnh, ai vision n8n, openrouter n8n]
---

# 🚀 Tự động nhận diện biển số xe từ ảnh tải lên n8n Form bằng AI OpenRouter

Các sếp có bao giờ cảm thấy đau đầu khi phải xử lý thủ công hàng loạt hình ảnh xe cộ, bãi đỗ xe hoặc hồ sơ phương tiện để ghi nhận biển số xe? Việc nhập liệu thủ công vừa tốn thời gian, dễ gây sai sót lại vừa làm giảm năng suất vận hành. 

Giải pháp tuyệt vời cho các sếp đây! Workflow n8n này sẽ tự động hóa 100% quy trình: khách hàng hoặc nhân viên chỉ cần tải ảnh xe lên một chiếc Form trực tuyến, AI thông minh sẽ tự động "soi" ảnh, đọc chính xác biển số xe và hiển thị kết quả ngay lập tức mà không cần con người nhúng tay vào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Loại bỏ hoàn toàn khâu nhập liệu biển số xe thủ công.
- **Tốc độ chớp nhoáng:** Trả kết quả ngay trên trang hoàn thành của Form chỉ sau vài giây tải ảnh lên.
- **Độ chính xác cao:** Ứng dụng sức mạnh của các mô hình AI Vision thông qua OpenRouter để đọc rõ biển số ngay cả trong điều kiện ảnh chụp thực tế.
- **Tiết kiệm chi phí:** Không cần đầu tư phần mềm OCR đắt đỏ, tận dụng mô hình AI giá rẻ qua API.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống **n8n** đang hoạt động (Self-hosted hoặc n8n Cloud).
- Tài khoản và **API Key của OpenRouter** (để sử dụng các mô hình AI hỗ trợ Vision như OpenAI GPT-4o, Claude 3, v.v.).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ kho lưu trữ n8n (Link gốc: [n8n workflow #2911](https://n8n.io/workflows/2911)) hoặc copy mã nguồn JSON và paste trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần chú ý cấu hình các node sau:

- **FromTrigger (Form Trigger):** Node này tạo ra một trang form công khai. Các sếp hãy cấu hình giao diện form để yêu cầu người dùng tải lên hình ảnh có chứa biển số xe.
- **Settings (Set Node):** Nơi cấu hình các tham số phụ trợ, ví dụ như tên mô hình AI (model) sẽ được truyền vào OpenRouter LLM.
- **OpenRouter LLM & Basic LLM Chain:** 
  - Kết nối credentials tài khoản OpenRouter của các sếp vào node **OpenRouter LLM**.
  - Chọn model AI có khả năng đọc hiểu hình ảnh (Vision) như `gpt-4o-mini` hoặc `claude-3-haiku` tại thông số Model (`={{ $json.model }}`).
  - Trong **Basic LLM Chain**, hãy viết một Prompt ngắn gọn, rõ ràng yêu cầu AI: *"Hãy phân tích hình ảnh được cung cấp và chỉ trích xuất ra định dạng văn bản duy nhất là dãy số/chữ của biển số xe."*
- **FormResultPage (Form Node):** Cấu hình để hiển thị kết quả trả về (chính là biển số xe mà AI vừa đọc được) cho người dùng xem ngay sau khi họ submit form.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** và test thử bằng cách truy cập vào URL của form, tải lên một bức ảnh xe có biển số rõ ràng để kiểm tra kết quả.
- Nếu mọi thứ hoạt động chính xác, hãy gạt công tắc sang chế độ **Active** để đưa workflow vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu trữ dữ liệu:** Thêm node *Google Sheets* hoặc *PostgreSQL* ngay sau AI Chain để tự động lưu lại lịch sử gồm: Ảnh tải lên, Biển số xe, Thời gian người dùng gửi form.
- **Thông báo qua Telegram/Slack:** Thêm node thông báo để gửi ảnh và biển số xe về nhóm chat nội bộ mỗi khi có khách hàng/nhân viên check-in bãi xe.
- **Xử lý hậu kỳ:** Thêm một bước kiểm tra định dạng biển số xe (regex) để đảm bảo kết quả trả về đúng chuẩn định dạng biển số xe của quốc gia bạn đang hoạt động.

### 📌 Kết luận
Với workflow tự động hóa nhận diện biển số xe này, các sếp đã có thể số hóa hoàn toàn quy trình quản lý bãi xe, kiểm soát ra vào hoặc quản lý tài sản chỉ trong vài phút thiết lập. Hãy bắt tay vào cài đặt ngay hôm nay để tối ưu hóa vận hành cho doanh nghiệp của mình nhé!