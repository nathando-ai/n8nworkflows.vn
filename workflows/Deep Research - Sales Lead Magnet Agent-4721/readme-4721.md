---
title: "🚀 Tự động hóa Deep Research & Tạo Sales Lead Magnet với AI trong n8n"
description: "Xây dựng hệ thống Sales Lead Magnet Agent cực mạnh mẽ với n8n, tự động nghiên cứu sâu (Deep Research) về khách hàng tiềm năng và biên soạn tài liệu chuyên sâu bằng Claude 3.7 Sonnet."
slug: "deep-research-sales-lead-magnet-agent-n8n"
tags: [n8n, automation, no-code, ai-agent, sales, lead-magnet, anthropic]
keywords: [n8n workflow, sales lead magnet, deep research ai, claude 3.7 sonnet, tự động hóa sales, ai agent n8n]
---

# 🚀 Xây dựng hệ thống Deep Research & Sales Lead Magnet Agent tự động với n8n

Việc nghiên cứu sâu (Deep Research) về một khách hàng tiềm năng, đối thủ cạnh tranh hoặc một thị trường ngách để làm Lead Magnet (tài liệu mồi) thường ngốn rất nhiều thời gian của đội ngũ Sales và Marketing. Các sếp có khi mất cả ngày trời để tổng hợp thông tin, viết báo cáo và đóng gói thành tài liệu. 

Đừng làm việc đó thủ công nữa! Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ thông minh do **Max Mitcham** sáng tạo mang tên **Deep Research - Sales Lead Magnet Agent**. Workflow này tận dụng sức mạnh của các AI Agent kết hợp với mô hình ngôn ngữ cao cấp như **Claude 3.7 Sonnet** để tự động hóa toàn bộ quy trình: Từ lên ý tưởng, tìm kiếm dữ liệu, phân công trợ lý ảo nghiên cứu, biên tập cho đến xuất thành Google Docs hoàn chỉnh để gửi tặng khách hàng!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100% quy trình Deep Research:** Thay vì mất hàng giờ tra cứu, AI Agent tự động chia nhỏ công việc và nghiên cứu đa chiều về chủ đề yêu cầu.
- **Tài liệu Lead Magnet chuyên nghiệp:** Tự động tổng hợp, biên tập và tạo trực tiếp một file Google Docs hoàn chỉnh, sẵn sàng chia sẻ cho khách hàng.
- **Cá nhân hóa đỉnh cao:** Dựa trên yêu cầu đầu vào từ chat, hệ thống tạo ra các báo cáo nghiên cứu chuyên sâu cực kỳ đúng trọng tâm.
- **Hoạt động liên tục 24/7:** Kích hoạt bất cứ lúc nào qua Chat Trigger, giúp đội ngũ sales luôn có tài liệu chất lượng cao trong nháy mắt.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API Keys sau:
- **n8n Instance** (phiên bản hỗ trợ LangChain / Advanced AI).
- **Anthropic API Key** (để sử dụng mô hình `claude-3-7-sonnet-20250219`).
- **OpenRouter API Key** (dùng cho mô hình `anthropic/claude-3.7-sonnet:thinking`).
- **Google Account** (có quyền kết nối Google Docs và Google Drive để tạo và phân quyền tài liệu tự động).
- **Perplexity API / Trigify API** (tùy thuộc vào cấu hình tool HTTP Request để tìm kiếm dữ liệu thời gian thực).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ [n8n Workflow Hub (Link 4721)](https://n8n.io/workflows/4721).
- Trong giao diện n8n Editor của các sếp, chọn **Add workflow** -> Nhấp vào biểu tượng menu (3 chấm) -> **Import from File** (hoặc copy/paste trực tiếp mã JSON vào).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống mượt mà trơn tru, các sếp cần chú ý cấu hình kỹ các node sau:
- **When chat message received (`chatTrigger`):** Điểm khởi đầu nơi các sếp nhập chủ đề hoặc yêu cầu nghiên cứu (Lead Magnet topic).
- **Anthropic Chat Model / OpenRouter Chat Model (`lmChatAnthropic`, `lmChatOpenRouter`):** 
  - Kết nối các node này với Credentials tương ứng (Anthropic API Key & OpenRouter API Key).
  - Đảm bảo model được chọn chính xác là `claude-3-7-sonnet-20250219` hoặc `anthropic/claude-3.7-sonnet:thinking` để AI có khả năng tư duy sâu (reasoning).
- **Các Agent & Tool Nodes (`Query Builder`, `Research Leader`, `Project Planner`, `Team of Research Assistants`, `Editor`):** Kiểm tra lại các system prompt bên trong để đảm bảo AI hiểu đúng vai trò (Lên khung tìm kiếm -> Lập kế hoạch -> Phân công trợ lý -> Biên tập viên tổng hợp).
- **Google Docs & Google Drive (`googleDocs`, `googleDrive`):** 
  - Kết nối tài khoản Google OAuth2.
  - Kiểm tra node **Google Docs1** (thao tác update nội dung) và node **Google Drive** (thao tác phân quyền chia sẻ - share URL) để tài liệu tạo ra có thể tự động cấp quyền đọc cho người dùng.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và thử nhập một chủ đề bất kỳ tại giao diện Chat Trigger để test run xem quá trình AI Research và tạo Google Docs diễn ra thành công không.
- Sau khi test ngon lành, gạt công tắc sang **Active** để chính thức vận hành hệ thống.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh thông báo:** Kết nối thêm node Telegram hoặc Slack ở cuối workflow để khi Google Docs được tạo xong, hệ thống sẽ tự động bắn link báo cáo về group chat cho các sếp.
- **Lưu trữ Lead vào CRM:** Bổ sung node HubSpot hoặc Google Sheets để lưu thông tin người yêu cầu Lead Magnet, giúp đội ngũ Sales dễ dàng chăm sóc (Nurturing).
- **Tùy chỉnh Văn phong (Tone of Voice):** Tinh chỉnh Prompt trong node **Editor** để văn phong báo cáo phù hợp với ngành hàng của doanh nghiệp (B2B, Tài chính, Công nghệ...).

### 📌 Kết luận
Workflow **Deep Research - Sales Lead Magnet Agent** là một cỗ máy tự động hóa cực kỳ đáng đồng tiền bát gạo cho các đội ngũ Sales và Marketing hiện đại. Chỉ với vài cú click và một câu lệnh chat, các sếp đã có ngay một tài liệu nghiên cứu chuyên sâu chuẩn chỉnh. Cài đặt ngay lên VPS của mình và trải nghiệm sức mạnh của AI Agent ngay hôm nay thôi nào các sếp!