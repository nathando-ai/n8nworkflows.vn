---
title: "🚀 Tự động tạo Cold Email và Thư Bán Hàng chuyên nghiệp với OpenAI GPT & Google Docs"
description: "Hướng dẫn cài đặt workflow n8n giúp tự động hóa quy trình viết cold email và sales letter thông qua trợ lý AI chat, tích hợp trực tiếp với Google Docs."
slug: "tu-dong-tao-cold-email-sales-letter-openai-google-docs"
tags: [n8n, automation, no-code, openai, google-docs, ai-agent, sales-automation]
keywords: [n8n workflow, tạo cold email tự động, sales letter AI, OpenAI GPT n8n, Google Docs automation, AI agent n8n]
---

# 🚀 Tự động hóa quy trình viết Cold Email & Thư Bán Hàng với AI & Google Docs

Các sếp có đang đau đầu vì tốn hàng giờ mỗi ngày để nghĩ ý tưởng, soạn thảo từng bức Cold Email hay viết thư bán hàng (Sales Letter) gửi khách hàng tiềm năng mà tỷ lệ phản hồi lại lẹt đẹt? Việc viết nội dung thủ công vừa tốn thời gian, vừa khó duy trì phong độ và tính cá nhân hóa cao.

Đừng lo, giải pháp đã ở đây! Workflow n8n này sẽ biến n8n thành một trợ lý ảo thông minh (AI Copy Assistant). Các sếp chỉ cần chat trực tiếp để yêu cầu, AI sẽ tự động nghiên cứu, viết nội dung chuyển đổi cao bằng OpenAI GPT và lưu trực tiếp kết quả vào Google Docs cho các sếp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không còn phải bắt đầu từ trang giấy trắng, AI lo toàn bộ phần cấu trúc và nội dung sơ khai.
- **Cá nhân hóa đỉnh cao:** Dễ dàng tinh chỉnh văn phong, đối tượng mục tiêu chỉ bằng vài câu lệnh chat đơn giản.
- **Lưu trữ tự động:** Nội dung tạo ra được tự động đồng bộ vào Google Docs, sẵn sàng để copy và gửi đi hoặc chỉnh sửa thêm.
- **Hoạt động liên tục 24/7:** Trợ lý ảo luôn sẵn sàng phục vụ các sếp bất cứ lúc nào cần ý tưởng hay kịch bản sale mới.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **OpenAI API Key** (có quyền truy cập mô hình GPT).
- **Tài khoản Google** để kết nối với Google Docs.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể copy mã JSON của workflow từ nguồn gốc hoặc import trực tiếp file JSON vào giao diện n8n Editor của mình bằng cách chọn `Add workflow` -> `Import from File`.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 7 nodes chính được cấu hình mạch lạc theo chuẩn LangChain Agent. Các sếp cần chú ý cấu hình kỹ các điểm sau:

- **When chat message received (`chatTrigger`):** Điểm khởi đầu nhận câu lệnh từ các sếp. Có thể cấu hình giao diện chat widget của n8n để tương tác trực tiếp.
- **Copy Assistant (`agent`):** Node điều phối chính sử dụng AI Agent để hiểu yêu cầu và quyết định gọi công cụ (tools) nào phù hợp (Cold Email hay Sales Letter).
- **OpenAI Chat Model (`lmChatOpenAi`):** 
  - Chọn Credentials OpenAI của các sếp.
  - Model: Khuyến nghị sử dụng `gpt-4o-mini` (hoặc `gpt-4.1-mini`) để tối ưu tốc độ và chi phí nhưng vẫn đảm bảo chất lượng ngữ nghĩa tiếng Việt tốt.
- **Simple Memory (`memoryBufferWindow`):** Giúp trợ lý nhớ ngữ cảnh các đoạn chat trước đó để các sếp có thể yêu cầu sửa đổi liên tục (ví dụ: *"làm ngắn lại đi"* hoặc *"đổi giọng văn thân thiện hơn"*).
- **Cold Email Writer Tool & Sales Letter Tool (`toolWorkflow`):** Các công cụ phụ trợ (sub-workflows) chuyên trách nhiệm vụ viết từng loại nội dung cụ thể.
- **Update a document (`googleDocs`):** 
  - Chọn Credentials `Google Docs OAuth2 API`.
  - Cấu hình thao tác (`operation`: `update`) để tự động cập nhật nội dung văn bản vào tài liệu Google Docs được chỉ định sẵn.

#### 3. Kích hoạt ⚡️
- Bấm **Test workflow** và gửi một tin nhắn mẫu qua chat (Ví dụ: *"Viết giúp tôi một cold email gửi CEO công ty phần mềm mời hợp tác dịch vụ SEO"*).
- Kiểm tra kết quả trả về trong chat và kiểm tra xem Google Doc đã được cập nhật chưa.
- Nếu mọi thứ mượt mà, gạt công tắc sang **Active** để bật workflow chạy chính thức!

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh nhận tin:** Thay vì dùng chat widget mặc định của n8n, các sếp có thể đổi trigger thành Telegram Bot hoặc Slack để ra lệnh viết bài ngay trên điện thoại cực kỳ tiện lợi.
- **Tích hợp CRM:** Kết nối thêm node HubSpot hoặc Google Sheets để lưu thông tin chiến dịch và nội dung email đã tạo theo từng khách hàng.
- **Gửi email tự động:** Nối tiếp workflow bằng node Gmail hoặc SendGrid để tự động gửi cold email sau khi được duyệt qua Google Docs.

### 📌 Kết luận
Với workflow tự động hóa này, việc sáng tạo nội dung sales không còn là gánh nặng. Hãy cài đặt ngay hôm nay để tối ưu hóa năng suất đội ngũ sales của các sếp!