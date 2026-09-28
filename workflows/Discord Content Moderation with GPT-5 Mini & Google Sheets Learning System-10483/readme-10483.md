---
title: "🚀 Tự động kiểm duyệt nội dung Discord thông minh với AI và Google Sheets"
description: "Xây dựng hệ thống tự động kiểm duyệt kênh Discord bằng AI GPT-5 Mini, kết hợp Google Sheets làm cơ sở tri thức để lọc tin nhắn vi phạm, spam và độc hại chính xác 100%."
slug: "tu-dong-kiem-duyet-noi-dung-discord-voi-ai-va-google-sheets"
tags: [n8n, automation, discord, ai-agent, openai, google-sheets]
keywords: [n8n workflow, discord moderation, kiểm duyệt discord tự động, gpt-5 mini, google sheets automation]
---

# 🚀 Tự động kiểm duyệt nội dung Discord thông minh với AI và Google Sheets

Việc quản lý và giữ gìn sự văn minh cho một cộng đồng Discord lớn là cơn ác mộng thực sự đối với các Admin và Moderator. Kiểm duyệt thủ công tốn rất nhiều thời gian, trong khi các bộ lọc từ khóa truyền thống (keyword filter) thường quá cứng nhắc—chúng vô tình xóa nhầm những câu đùa giỡn vô hại hoặc bỏ sót các hành via toxic tinh vi.

Giải pháp? Workflow n8n này sẽ thay các sếp "gác cửa" cộng đồng 24/7. Nhờ sức mạnh của **AI Agent**, **GPT-5 Mini** và **Google Sheets Learning System**, hệ thống không chỉ đọc từ khóa mà còn hiểu được **ngữ cảnh (context)** và **ý định (intent)** của người gửi.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 100%**: Theo dõi kênh Discord định kỳ 3 phút/lần, tự động phát hiện và xóa tin nhắn vi phạm (spam, quấy rối, toxic).
- **Học từ dữ liệu thực tế**: Tham khảo các mẫu ví dụ từ Google Sheets để hiểu rõ tiêu chuẩn kiểm duyệt riêng của cộng đồng các sếp.
- **Hiểu ngữ cảnh sâu sắc**: Phân biệt rõ ràng giữa "chửi thề vui vẻ trong ngữ cảnh tích cực" và "lăng mạ, tấn công cá nhân".
- **Báo cáo minh bạch**: Tự động gửi nhật ký chi tiết về các nội dung đã xử lý vào kênh riêng dành cho Admin.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Discord** với quyền Bot/OAuth2 để đọc, xóa tin nhắn và gửi thông báo.
- **Tài khoản Google Sheets** chứa bảng dữ liệu mẫu huấn luyện AI.
- **OpenAI API Key** (hỗ trợ mô hình GPT-5 Mini).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này và import trực tiếp vào giao diện n8n Editor của các sếp, hoặc sử dụng tính năng copy/paste JSON.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống hoạt động trơn tru theo đúng ý muốn, các sếp cần cấu hình chính xác các node sau:

- **Get sheet knowledgebase (`googleSheets`)**: 
  - Tạo bản sao từ [Google Sheet mẫu tại đây](https://docs.google.com/spreadsheets/d/1xodthGg8RpQJB62mB6fziuwblG9nn3udZvQvyRquCXM/edit?usp=sharing).
  - Điền các ví dụ mẫu vào cột `message_content`, `should_delete` (YES/NO) và `reason` để AI hiểu tiêu chuẩn của bạn.
  - Kết nối tài khoản Google Sheets OAuth2 và trỏ tới file Sheet vừa tạo.

- **Set Credentials Here (`set`) / Discord Nodes**:
  - Chỉnh sửa các thông số định danh như Server ID, Channel ID cần theo dõi và Admin Channel ID dùng để nhận báo cáo log.
  - Kết nối `discordOAuth2Api` cho các node: `Get recent messages`, `delete bad content`, và `update admin channel about moderation`.

- **GPT5 mini (`lmChatOpenAi`) & AI Agent (`agent`)**:
  - Kết nối `openAiApi` với OpenAI API Key của các sếp.
  - Đảm bảo model được chọn là `gpt-5-mini-2025-08-07`.
  - Tinh chỉnh system prompt trong node **AI Agent** để phù hợp với nội quy và văn hóa riêng của cộng đồng các sếp.

- **Schedule Trigger**:
  - Mặc định workflow chạy mỗi 3 phút. Các sếp có thể thay đổi thời gian này tùy theo lượng tương tác thực tế của server.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** chạy thủ công lần đầu để test với dữ liệu mẫu, kiểm tra kỹ xem bot đã lọc đúng và gửi thông báo về kênh Admin chưa.
- Sau khi mọi thứ mượt mà, gạt công tắc sang **Active** để bot chính thức làm việc 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo**: Thay vì chỉ gửi tin nhắn qua kênh Discord Admin, các sếp có thể kết hợp thêm node Telegram hoặc Slack để nhận cảnh báo ngay lập tức trên điện thoại.
- **Lưu trữ lịch sử vi phạm**: Tự động ghi lại log những thành viên vi phạm nhiều lần vào một sheet riêng để dễ bề xử lý (ban vĩnh viễn, cảnh cáo...).
- **Tinh chỉnh prompt định kỳ**: Dựa vào thực tế các tin nhắn bot xử lý sai, hãy bổ sung thêm các dòng ví dụ (few-shot examples) vào Google Sheets để AI ngày càng thông minh hơn.

### 📌 Kết luận
Với sự kết hợp hoàn hảo giữa n8n, AI Agent và Google Sheets, các sếp hoàn toàn có thể giải phóng bản thân khỏi công việc kiểm duyệt nhàm chán, giữ cho cộng đồng Discord luôn trong sạch, văn minh và chuyên nghiệp. Triển khai ngay thôi nào!