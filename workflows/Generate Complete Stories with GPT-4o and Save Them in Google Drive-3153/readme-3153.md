---
title: "🚀 Tự động sáng tác câu chuyện hoàn chỉnh với GPT-4o và lưu trực tiếp lên Google Drive"
description: "Khám phá quy trình n8n tự động hóa toàn bộ quá trình viết truyện, từ lên ý tưởng, xây dựng nhân vật, cốt truyện đến hoàn thiện bản thảo và lưu trữ trên Google Drive bằng AI."
slug: "tu-dong-sang-tac-cau-chuyen-gpt4o-google-drive"
tags: [n8n, automation, no-code, AI, OpenAI, Google Drive]
keywords: [n8n workflow, viết truyện tự động, GPT-4o, Azure OpenAI, Google Drive automation, AI agent]
keywords: [n8n workflow, tự động hóa, viết truyện bằng AI, GPT-4o, Google Drive]
---

# 🚀 Tự động sáng tác câu chuyện hoàn chỉnh với GPT-4o và lưu trực tiếp lên Google Drive

Các sếp có bao giờ đau đầu khi phải nghĩ ý tưởng, xây dựng nhân vật, lên cốt truyện và viết hàng trang giấy cho các chiến dịch content marketing, kịch bản video hay sách truyện không? Việc này tốn hàng tá thời gian và đôi khi cạn kiệt cảm xúc. 

Đừng lo, workflow n8n cực kỳ mạnh mẽ mang tên **"Generate Complete Stories with GPT-4o and Save Them in Google Drive"** (tác giả *Ian Dikhtiar*) sẽ giúp các sếp giải quyết triệt để vấn đề này. Quy trình này kết hợp các AI Agent thông minh để tự động hóa 100% quy trình từ một ý tưởng thô thành một câu chuyện hoàn chỉnh và lưu ngay vào Google Drive của các sếp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Biến một từ khóa/ý tưởng đơn giản thành một câu chuyện hoàn chỉnh gồm nhân vật, cốt truyện, timeline và bản thảo chi tiết.
- **Tiết kiệm 95% thời gian:** Không còn cảnh ngồi nhìn màn hình trắng chờ cảm hứng, AI lo hết từ A-Z.
- **Đồng bộ hóa mượt mà:** Câu chuyện sau khi hoàn thiện sẽ được tự động đóng gói và lưu trữ an toàn dưới dạng file trên Google Drive.
- **Cấu trúc linh hoạt:** Sử dụng các Structured Output Parser để đảm bảo dữ liệu đầu ra từ AI luôn chuẩn xác và dễ dàng tái sử dụng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (phiên bản hỗ trợ LangChain và các AI Agent).
- **Azure OpenAI Credentials (hoặc OpenAI):** Để kết nối với model `gpt-4o` (thông qua node `gpt-4o1`).
- **Google Drive Credentials:** Tài khoản Google để cấp quyền cho node `create_story_file` tạo và lưu file truyện.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ nguồn cấp hoặc copy toàn bộ mã JSON.
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File** hoặc dán trực tiếp (Paste) vào workspace.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Quy trình này khá đồ sộ với 37 nodes, tập trung vào sức mạnh của AI Agent và Structured Output. Các sếp cần chú ý các điểm sau:
- **Node `gpt-4o1` (Azure OpenAI / OpenAI):** Cấu hình lại thông tin xác thực (Credentials) cho đúng tài khoản API của các sếp để gọi mô hình GPT-4o.
- **Node `prompt` & các node Set (`Connect`, `Convince`, `Explain`,...):** Nơi các sếp thiết lập ý tưởng ban đầu, góc nhìn hoặc sắc thái cảm xúc cho câu chuyện. Hãy thay đổi nội dung prompt theo chủ đề mà các sếp muốn sáng tác.
- **Hệ thống AI Agents (`pick cards`, `story baseline`, `story plot`, `story enhancement`, `characters`, `story timeline`, `story draft`, `edit notes`, `story rules`, `story_final`):** Kiểm tra xem các agent này đã liên kết đúng với model GPT-4o (`gpt-4o1`) và các node định dạng dữ liệu (`Structured Output Parser`, `timeline json`, `character json`,...) chưa.
- **Node `create_story_file` (Google Drive):** Kết nối tài khoản Google Drive, chọn thư mục đích (Folder ID) nơi các sếp muốn lưu trữ các file truyện được tạo ra.

#### 3. Kích hoạt ⚡️
- Nhấn **Test workflow** tại node `When clicking ‘Test workflow’` hoặc node `prompt` để chạy thử nghiệm xem toàn bộ chuỗi Agent có hoạt động trơn tru không.
- Sau khi kiểm tra file đã xuất hiện đẹp đẽ trong Google Drive, các sếp hãy gạt nút **Active** để bật workflow chạy tự động khi cần.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp Telegram/Slack:** Thêm một node thông báo qua Telegram hoặc Slack ở cuối luồng để báo cho các sếp biết khi nào câu chuyện đã được viết xong và lưu lên Drive.
- **Mở rộng nguồn ý tưởng:** Thay vì dùng `manualTrigger` hoặc node `prompt` cố định, các sếp có thể kết nối với Google Sheets hoặc Airtable để nhập danh sách hàng chục chủ đề, workflow sẽ tự động viết truyện hàng loạt (Batch processing).
- **Tự động dịch thuật:** Gắn thêm một bước AI Agent dịch thuật phía sau node `story_final` nếu các sếp muốn xuất bản truyện song ngữ Anh - Việt.

### 📌 Kết luận
Workflow **Generate Complete Stories with GPT-4o and Save Them in Google Drive** là một "vũ khí" cực kỳ lợi hại cho những ai làm sáng tạo nội dung, viết lách hay marketing. Hãy thiết lập ngay hôm nay để để AI làm thay những phần việc nặng nhọc nhất, các sếp chỉ việc tận hưởng thành quả!