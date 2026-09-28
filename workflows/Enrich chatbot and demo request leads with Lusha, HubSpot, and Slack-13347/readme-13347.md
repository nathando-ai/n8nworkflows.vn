---
title: "🚀 Tự động làm giàu dữ liệu Lead từ Chatbot & Demo với Lusha, HubSpot và Slack"
description: "Hướng dẫn xây dựng workflow n8n tự động xác thực, tra cứu thông tin Lusha, chấm điểm ICP, đồng bộ HubSpot và phân loại thông báo Slack cho đội ngũ Sales."
slug: "tu-dong-lam-giao-lead-lusha-hubspot-slack"
tags: [n8n, automation, lead-generation, lusha, hubspot, slack, crm]
keywords: [n8n workflow, tự động hóa lead, lusha api, hubspot crm, slack alert, sales automation]
---

# 🚀 Tự động làm giàu dữ liệu Lead từ Chatbot & Demo với Lusha, HubSpot và Slack

Các sếp làm sales hay đội ngũ SDR chắc hẳn đã quá quen thuộc với cảnh tượng: Khách hàng điền form đăng ký demo hoặc nhắn tin qua chatbot với một chiếc email ngắn ngủn. Để biết họ là ai, công ty lớn hay nhỏ, chức vụ gì, các sếp lại phải mất công tra cứu thủ công trên Google, LinkedIn hay CRM. Quá trình này vừa chậm chạp, vừa khiến doanh nghiệp dễ bỏ lỡ cơ hội vàng chốt đơn khi khách hàng đang "nóng".

Giải pháp ở đây là gì? Hãy để chiếc workflow n8n này "gánh" thay toàn bộ công việc tẻ nhạt đó. Hệ thống sẽ tự động bắt dữ liệu, làm giàu thông tin, chấm điểm tiềm năng và bắn tin nhắn cảnh báo đến Slack chỉ trong tích tắc!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian tra cứu:** Tự động lấy thông tin chi tiết công ty, chức vụ, số điện thoại từ email đầu vào nhờ Lusha.
- **Phân loại Lead chuẩn xác:** Hệ thống tự động chấm điểm ICP (Ideal Customer Profile) dựa trên quy mô công ty và thâm niên của khách.
- **Đồng bộ CRM tức thì:** Tự động tạo hoặc cập nhật thông tin contact trên HubSpot mà không cần thao tác tay.
- **Phản hồi "thần tốc" với khách VIP:** Lead chất lượng cao sẽ nhận ngay cảnh báo khẩn cấp (Urgent Alert) lên kênh Slack riêng cho đội ngũ SDR.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Khuyên dùng bản self-hosted).
- **Lusha Community Node:** Cài đặt package `@lusha-org/n8n-nodes-lusha` vào n8n của các sếp kèm API Key.
- **HubSpot Account:** Tài khoản HubSpot có quyền cấu hình API/OAuth2.
- **Slack Workspace:** Đã kết nối Slack và có sẵn các channel để nhận thông báo.
- **Webhook Source:** Chatbot hoặc Form đăng ký trên website có khả năng gửi request POST.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow và paste trực tiếp vào n8n Editor, hoặc sử dụng tính năng import từ file JSON.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 8 nodes chính, các sếp cần chú ý cấu hình kỹ các điểm sau:

- **Chatbot/Demo Request Webhook:** 
  - Node này nhận dữ liệu đầu vào (`path`: `chat-demo-enrichment`). Các sếp cần cấu hình form/chatbot trên website trỏ request POST về endpoint này.
  - *Mẹo:* Tùy chỉnh các trường payload nhận về cho khớp với form thực tế của các sếp.

- **Validate & Clean Input (Code Node):** 
  - Node này có nhiệm vụ làm sạch dữ liệu, kiểm tra định dạng email trước khi đem đi tra cứu.

- **Enrich with Lusha:** 
  - Chọn credentials `lushaApi` và cấu hình operation là `enrichSingle` để lấy thông tin chi tiết dựa trên email khách hàng.

- **Build Summary & Score (Code Node):** 
  - Chạy logic chấm điểm lead dựa trên chức vụ (seniority), quy mô công ty (company size) và loại yêu cầu. Các sếp có thể tùy chỉnh lại ngưỡng điểm (threshold) trong code này cho phù hợp với doanh nghiệp mình.

- **Create/Update HubSpot Contact (HubSpot Node):** 
  - Chọn credentials `hubspotOAuth2Api`, thiết lập `resource` là `contact` và `operation` là `upsert` để hệ thống tự tạo mới nếu chưa có hoặc cập nhật nếu đã tồn tại.

- **Is High Priority? (IF Node) & Slack Alerts:** 
  - Phân luồng dữ liệu dựa trên điểm số. 
  - Nếu là lead nóng (High Priority), workflow sẽ kích hoạt node **Urgent SDR Alert** bắn tin nhắn gấp vào kênh Slack chuyên biệt. 
  - Ngược lại, lead thường sẽ đi qua node **Standard SDR Notification**.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (Test run) bằng một request giả lập qua webhook để kiểm tra dữ liệu chảy qua từng node.
- Sau khi chắc chắn mọi thứ trơn tru, hãy bật công tắc **Active** để workflow chính thức vận hành 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm AI:** Có thể tích hợp thêm một node OpenAI/Anthropic để phân tích sâu hơn nội dung tin nhắn chat/yêu cầu demo trước khi gửi lên Slack.
- **Ghi Log vào Google Sheets:** Thêm một node Google Sheets để lưu trữ toàn bộ lịch sử lead được enrich nhằm phục vụ cho việc đo lường chiến dịch marketing sau này.
- **Đa kênh thông báo:** Ngoài Slack, có thể cấu hình thêm nhánh gửi tin nhắn qua Telegram Bot để các sếp check điện thoại tiện hơn khi đang di chuyển.

### 📌 Kết luận
Việc tự động hóa quy trình phân loại và làm giàu lead không chỉ giúp đội ngũ Sales tiếp cận khách hàng nhanh hơn mà còn tối ưu hóa tỷ lệ chuyển đổi (Conversion Rate) đáng kể. Hãy setup ngay workflow này để không bỏ lỡ bất kỳ khách hàng tiềm năng nào nhé các sếp!