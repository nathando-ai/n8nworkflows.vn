---
title: "🐶 AI Petshop Assistant: Tự động hóa hoàn hảo cho cửa hàng thú cưng"
description: "Workflow n8n siêu phức tạp kết hợp GPT-4o, Google Calendar và các nền tảng truyền thông xã hội để tự động hóa hoàn toàn các tác vụ quản lý cửa hàng thú cưng."
slug: "ai-petshop-assistant-gpt4o-google-calendar-whatsapp-instagram-facebook"
tags: [n8n, automation, no-code, petshop, ai, marketing, social-media]
keywords: [n8n workflow, tự động hóa cửa hàng thú cưng, AI petshop, quản lý thú cưng, tự động hóa marketing]
---

# 🐶 AI Petshop Assistant: Tự động hóa hoàn hảo cho cửa hàng thú cưng

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa hoàn toàn các tác vụ quản lý cửa hàng thú cưng
- Tiết kiệm thời gian lên tới 80% cho các tác vụ lặp lại
- Cải thiện trải nghiệm khách hàng thông qua tương tác tự động thông minh
- Quản lý lịch hẹn và nhắc nhở tự động qua Google Calendar
- Tích hợp hoàn hảo với các nền tảng truyền thông xã hội (WhatsApp, Instagram, Facebook)
- Hệ thống nhớ nhớ dài hạn cho các cuộc trò chuyện với khách hàng
- Tự động hóa quản lý kho hàng và kiểm tra tồn kho
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản OpenAI API (cho GPT-4o)
- Tài khoản Google Calendar API
- Tài khoản Supabase (cho cơ sở dữ liệu)
- Tài khoản WhatsApp Business API (hoặc Evolution API)
- Tài khoản Instagram Graph API
- Tài khoản Facebook Graph API
- Tài khoản Mapbox API (cho tính năng địa lý)
- Tài khoản Google Drive API (cho quản lý tài liệu)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [trang workflow gốc](https://n8n.io/workflows/3683)
2. Nhấn nút "Download" để tải file JSON
3. Trong n8n Editor, nhấn vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

**1. Cấu hình cơ bản:**
- Node "Variaveis" (set): Cấu hình các biến môi trường cần thiết
- Node "Maps" (set): Cấu hình các bản đồ dữ liệu cho các nền tảng khác nhau

**2. Tích hợp AI:**
- Node "Modelo IA" (lmChatOpenAi): Cấu hình API key OpenAI và chọn model GPT-4o
- Node "Best Agent AI" (agent): Cấu hình các công cụ AI cho agent chính
- Node "AI Agent Products" (agent): Cấu hình agent quản lý sản phẩm
- Node "AI Agent FollowUP" (agent): Cấu hình agent theo dõi khách hàng

**3. Tích hợp Google Calendar:**
- Node "Create Event with Attendee" (googleCalendarTool): Cấu hình API key Google Calendar
- Node "Create Event" (googleCalendarTool): Cấu hình API key Google Calendar
- Node "Get Events" (googleCalendarTool): Cấu hình API key Google Calendar

**4. Tích hợp truyền thông xã hội:**
- Node "Send WhatsApp" (httpRequest): Cấu hình API key WhatsApp Business API
- Node "Send Instagram" (httpRequest): Cấu hình API key Instagram Graph API
- Node "Send Facebook" (httpRequest): Cấu hình API key Facebook Graph API

**5. Tích hợp cơ sở dữ liệu:**
- Node "Bloquear IA" (supabase): Cấu hình kết nối Supabase
- Node "Desbloquear IA" (supabase): Cấu hình kết nối Supabase
- Node "SalvaHistorico" (supabase): Cấu hình kết nối Supabase
- Node "Postgres Memory" (memoryPostgresChat): Cấu hình kết nối PostgreSQL

**6. Tích hợp thanh toán:**
- Node "WH Asaas" (webhook): Cấu hình webhook cho hệ thống thanh toán Asaas
- Node "Criar Cliente" (httpRequest): Cấu hình API key Asaas
- Node "Criar Cobrança" (httpRequest): Cấu hình API key Asaas

**7. Tích hợp địa lý:**
- Node "Mapbox Cliente" (httpRequest): Cấu hình API key Mapbox
- Node "Mapbox Distancia" (httpRequest): Cấu hình API key Mapbox

**8. Tích hợp Google Drive:**
- Node "Download File" (googleDrive): Cấu hình API key Google Drive
- Node "Delete File1" (googleDrive): Cấu hình API key Google Drive

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node quan trọng, nhấn nút "Activate" để kích hoạt workflow
2. Kiểm tra hoạt động bằng cách gửi một tin nhắn thử nghiệm qua WhatsApp, Instagram hoặc Facebook
3. Kiểm tra các node "Response" để đảm bảo workflow trả về kết quả đúng

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh prompt AI:** Chỉnh sửa node "Prompt" (set) để điều chỉnh cách AI tương tác với khách hàng
2. **Quản lý lịch hẹn:** Sử dụng node "CalendarAgentAI" (webhook) để quản lý lịch hẹn tự động
3. **Theo dõi khách hàng:** Cấu hình node "Follow Up Search" (supabase) để theo dõi khách hàng tiềm năng
4. **Quản lý kho hàng:** Sử dụng node "Check Stock" (webhook) để kiểm tra tồn kho tự động
5. **Tích hợp thêm kênh truyền thông:** Thêm các node tương tự cho các nền tảng khác như Telegram hoặc SMS

### 📌 Kết luận
Workflow AI Petshop Assistant này cung cấp giải pháp toàn diện cho việc tự động hóa cửa hàng thú cưng. Với việc tích hợp GPT-4o, Google Calendar và các nền tảng truyền thông xã hội, các sếp có thể quản lý cửa hàng một cách hiệu quả hơn, cải thiện trải nghiệm khách hàng và tiết kiệm thời gian đáng kể. Hãy áp dụng ngay để thấy kết quả ngay lập tức!