---
title: "🚀 Tự động tạo AI Prompt thông minh với Google Gemini và lưu trữ trực tiếp vào Airtable"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình sáng tạo AI prompt, phân loại tự động và lưu trữ có cấu trúc vào Airtable bằng Google Gemini."
slug: "tao-ai-prompt-tu-dong-google-gemini-airtable"
tags: [n8n, automation, ai, google-gemini, airtable, no-code, langChain]
keywords: [n8n workflow, tạo prompt tự động, Google Gemini n8n, Airtable automation, AI LangChain n8n]
---

# 🚀 Tự động tạo AI Prompt chuyên nghiệp với Google Gemini và Airtable

Các sếp có bao giờ cảm thấy mất quá nhiều thời gian để nghĩ, viết, tinh chỉnh và phân loại các câu lệnh (prompt) cho AI chưa? Việc quản lý hàng trăm prompt thủ công trong các tệp tin rời rạc không chỉ tốn thời gian mà còn cực kỳ khó tìm kiếm khi cần tái sử dụng.

Giải pháp ở đây là gì? Hãy để n8n tự động hóa toàn bộ quy trình này! Với workflow **"Generate AI Prompts with Google Gemini and store them in Airtable"** do chuyên gia **Imperol** thiết kế, các sếp có thể trò chuyện với AI, yêu cầu tạo prompt theo ý muốn, hệ thống sẽ tự động cấu trúc hóa, phân loại và lưu ngay vào cơ sở dữ liệu Airtable một cách mượt mà. Không cần viết code, mọi thứ hoạt động tự động 100%!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian:** Không còn phải tự viết prompt từ đầu hay loay hoay đặt tên, phân loại chúng.
- **Dữ liệu có cấu trúc rõ ràng:** Mọi prompt sinh ra đều được phân loại, đặt tên chuẩn và lưu trữ ngăn nắp trong Airtable.
- **Tương tác trực quan:** Dễ dàng trò chuyện và yêu cầu tạo prompt mới thông qua giao diện chat tích hợp sẵn của n8n.
- **Độ chính xác cao:** Ứng dụng sức mạnh của Google Gemini kết hợp LangChain Structured Output Parser giúp trả về kết quả đúng định dạng yêu cầu tuyệt đối.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Tài khoản n8n** (Self-hosted hoặc n8n Cloud).
- **Google Gemini API Key** (`googlePalmApi`) để kết nối với các mô hình ngôn ngữ AI.
- **Tài khoản Airtable** kèm theo Personal Access Token (`airtableTokenApi`) và một Base/Table đã được thiết kế sẵn các trường (Fields) để lưu prompt.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể truy cập link gốc workflow trên n8n (ID: 3027), tải file JSON về máy, sau đó vào giao diện n8n chọn **Add workflow** -> **Import from File** để đưa workflow lên hệ thống.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy trơn tru, các sếp cần chú ý cấu hình các node cốt lõi sau:

- **Google Gemini Chat Model** & **Google Gemini Chat Model1**: 
  - Chọn hoặc tạo mới credential `googlePalmApi` bằng cách điền Google Gemini API Key của các sếp vào.
  - Chọn model Gemini phù hợp (ví dụ: `gemini-1.5-pro` hoặc `gemini-1.5-flash`).

- **Structured Output Parser** & **Auto-fixing Output Parser**:
  - Các node này đảm bảo AI trả về dữ liệu đúng định dạng JSON (gồm tên prompt, nội dung prompt, danh mục, mô tả...). Hãy kiểm tra schema để chắc chắn nó khớp với các cột trên Airtable.

- **Categorize and name Prompt** & **Generate a new prompt** (LangChain `chainLlm` nodes):
  - Đây là các chuỗi xử lý ngôn ngữ tự nhiên. Các sếp có thể tùy chỉnh System Prompt bên trong nếu muốn AI sinh ra các loại prompt theo phong cách riêng của doanh nghiệp mình.

- **add to airtable** (`airtable` node):
  - Chọn credential `airtableTokenApi`.
  - Chỉ định đúng **Base** và **Table** mà các sếp đã tạo sẵn trên Airtable.
  - Map (ánh xạ) các trường dữ liệu từ output của AI vào đúng các cột tương ứng trong Airtable (Ví dụ: *Prompt Title*, *Prompt Content*, *Category*, v.v.).

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** và test thử qua giao diện **When chat message received** (Chat Trigger) để kiểm tra xem prompt có được sinh ra và đẩy thành công lên Airtable hay chưa.
- Sau khi test thành công, gạt công tắc sang **Active** để bật workflow chạy chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack/Telegram:** Thêm node gửi thông báo về kênh chat nội bộ mỗi khi có một prompt mới được tạo thành công và lưu vào Airtable để team cùng tham khảo.
- **Tự động chấm điểm Prompt:** Kết hợp thêm một chuỗi LangChain để đánh giá chất lượng prompt trước khi lưu vào cơ sở dữ liệu.
- **Xây dựng thư viện Prompt nội bộ:** Chia sẻ Base Airtable này cho toàn bộ nhân sự trong công ty để tận dụng kho tàng prompt tối ưu hóa hiệu suất làm việc.

### 📌 Kết luận
Workflow này là trợ thủ đắc lực giúp các cá nhân và doanh nghiệp xây dựng một hệ thống quản lý tri thức AI bài bản, chuyên nghiệp. Hãy triển khai ngay hôm nay để tối ưu hóa năng suất làm việc cùng AI!