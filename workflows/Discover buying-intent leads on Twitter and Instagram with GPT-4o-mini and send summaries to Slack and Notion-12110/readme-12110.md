---
title: "🚀 Tự động phát hiện khách hàng tiềm năng có ý định mua hàng trên Twitter & Instagram bằng GPT-4o-mini"
description: "Hướng dẫn cài đặt workflow n8n sử dụng AI agent và GPT-4o-mini để quét, lọc khách hàng tiềm năng có nhu cầu mua sắm trên mạng xã hội và tự động đồng bộ về Slack, Notion."
slug: "phat-hien-khach-hang-tiem-nang-twitter-instagram-ai-n8n"
tags: [n8n, automation, no-code, ai-agent, gpt-4o-mini, social-listening]
keywords: [n8n workflow, tim khach hang tiem nang, social listening ai, gpt-4o-mini n8n, tich hop slack notion]
---

# 🚀 Tự động săn "cá lớn" trên mạng xã hội với n8n và AI Agent

Các sếp có bao giờ đau đầu vì đội ngũ sale phải lướt Twitter, Instagram cả ngày chỉ để tìm kiếm những khách hàng đang thực sự có nhu cầu mua sản phẩm/dịch vụ (buying-intent leads)? Việc này vừa tốn thời gian, dễ bỏ sót cơ hội vàng, lại cực kỳ mệt mỏi khi làm thủ công.

Đừng lo, giải pháp ở đây rồi! Với workflow n8n được thiết kế bởi chuyên gia Rahul Joshi, hệ thống sẽ tự động hóa toàn bộ quy trình: Lắng nghe mạng xã hội, sử dụng sức mạnh của **GPT-4o-mini** để phân tích ý định mua hàng, và ngay lập tức bắn thông báo về **Slack** đồng thời lưu trữ vào **Notion** để đội ngũ chăm sóc khách hàng chốt đơn ngay lập tức.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không cần nhân sự ngồi canh mạng xã hội thủ công.
- **Lọc leads cực chuẩn:** AI Agent phân tích ngữ cảnh, chỉ lọc ra những bài đăng thực sự có ý định mua hàng (buying-intent).
- **Phản hồi thần tốc:** Tin nhắn tự động đổ về **Slack** ngay khi phát hiện khách hàng tiềm năng.
- **Lưu trữ bài bản:** Tự động tạo trang mới trên **Notion** kèm theo bản tóm tắt và phân tích chi tiết từ AI để đội ngũ sale dễ dàng theo dõi.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động mượt mà, các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- Máy chủ n8n (Self-hosted hoặc Cloud).
- Tài khoản **OpenAI API / Azure OpenAI** (để sử dụng mô hình GPT-4o-mini).
- Workspace **Slack** (đã cấp quyền cho n8n bot gửi tin nhắn).
- Tài khoản **Notion** (đã tạo sẵn một Database để lưu leads và kết nối Integration).
- Tài khoản **Gmail** (nếu cần cấu hình thêm các bước gửi email thông báo).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ nguồn cung cấp.
- Trong giao diện n8n Editor, nhấn vào dấu **`+`** hoặc chọn **Add workflow** -> **Import from File** và tải file JSON lên.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các node sau để hệ thống chạy trơn tru:
- **Chat Trigger / Agent Node (`@n8n/n8n-nodes-langchain.agent`):** Điểm khởi đầu của quy trình AI. Cần kiểm tra lại các thiết lập prompt để định hướng AI tìm kiếm đúng tệp khách hàng mục tiêu.
- **Language Model (`@n8n/n8n-nodes-langchain.lmChatAzureOpenAi` hoặc OpenAI Chat Model):** Kết nối credentials của OpenAI và chọn model `gpt-4o-mini` để tối ưu chi phí và tốc độ xử lý.
- **Memory Buffer (`@n8n/n8n-nodes-langchain.memoryBufferWindow`):** Giúp AI ghi nhớ ngữ cảnh cuộc trò chuyện hoặc lịch sử quét gần nhất.
- **Output Parser Structured (`@n8n/n8n-nodes-langchain.outputParserStructured`):** Cấu hình định dạng đầu ra chuẩn JSON để chuyển dữ liệu mượt mà sang Slack và Notion.
- **Slack Node (`n8n-nodes-base.slack`):** Chọn kênh (Channel) trên Slack mà bạn muốn bot gửi thông báo cáo cáo leads mới.
- **Notion Node (`n8n-nodes-base.notion`):** Chọn đúng Database ID trên Notion để lưu trữ thông tin khách hàng, nội dung bài đăng và đánh giá của AI.
- **Error Trigger (`n8n-nodes-base.errorTrigger`):** Nên cấu hình thêm một nhánh nhỏ gửi cảnh báo về Telegram hoặc Email cá nhân nếu workflow gặp lỗi trong quá trình chạy ngầm.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Test workflow** để chạy thử nghiệm với dữ liệu giả lập, kiểm tra xem dữ liệu có đổ về Slack và Notion chính xác chưa.
- Sau khi test thành công, gạt công tắc sang chế độ **Active** để hệ thống tự động chạy 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Telegram:** Thay vì chỉ báo cáo qua Slack, các sếp có thể nối thêm node Telegram để nhận thông báo trực tiếp trên điện thoại cá nhân.
- **Tự động gửi email chào hàng:** Kết hợp thêm node Gmail để tự động gửi tin nhắn tiếp cận (outreach) ngay khi AI xác định đây là một khách hàng "tiềm năng vàng".
- **Lưu log chi tiết:** Sử dụng Google Sheets làm kho lưu trữ phụ để dễ dàng xuất báo cáo (export CSV) hàng tuần cho sếp lớn.

### 📌 Kết luận
Việc ứng dụng AI Agent và GPT-4o-mini vào việc săn tìm khách hàng tiềm năng trên mạng xã hội sẽ giúp doanh nghiệp của các sếp đi trước đối thủ một bước trong việc tiếp cận khách hàng. Hãy import workflow này ngay hôm nay và tối ưu hóa quy trình sales của bạn!