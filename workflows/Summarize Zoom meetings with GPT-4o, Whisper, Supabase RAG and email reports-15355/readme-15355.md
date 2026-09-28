---
title: "🚀 Tự động hóa Zoom Meeting với GPT-4o, Whisper và Supabase - Workflow n8n hoàn chỉnh"
description: "Hướng dẫn chi tiết cách tự động hóa việc ghi lại, chuyển đổi giọng nói thành văn bản, phân tích nội dung cuộc họp Zoom bằng GPT-4o và gửi báo cáo email tự động - tất cả trong một workflow n8n đơn giản."
slug: "tu-dong-hoa-zoom-meeting-voi-gpt-4o-whisper-supabase"
tags: [n8n, automation, no-code, AI, RAG, Zoom, GPT-4o, Supabase]
keywords: [n8n workflow, tự động hóa cuộc họp, AI phân tích cuộc họp, RAG, Zoom, GPT-4o, Supabase]
---

# 🚀 Tự động hóa Zoom Meeting với GPT-4o, Whisper và Supabase - Workflow n8n hoàn chỉnh

[Các sếp] có biết không? Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình từ ghi lại cuộc họp Zoom đến gửi báo cáo email chi tiết - mà không cần phải can thiệp hay viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động ghi lại, chuyển đổi giọng nói và phân tích nội dung cuộc họp
- **Chính xác cao**: Sử dụng công nghệ AI tiên tiến của OpenAI (Whisper và GPT-4o)
- **Cá nhân hóa**: Phân tích nội dung cuộc họp theo ngữ cảnh và so sánh với các cuộc họp trước đó
- **Hoạt động liên tục**: Tự động gửi báo cáo email sau mỗi cuộc họp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Zoom với quyền truy cập webhook
- API Key từ OpenAI (cho cả Whisper và GPT-4o)
- Dự án Supabase với bảng `meeting_memories` hỗ trợ vector
- Tài khoản Gmail với OAuth2 đã được cấu hình
- Endpoint webhook phải có thể truy cập từ internet
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/15355)
2. Click vào nút "Download" để tải file JSON
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về

Hoặc bạn có thể copy/paste JSON trực tiếp vào n8n Editor bằng cách:
1. Click vào "Import from Clipboard"
2. Dán nội dung JSON của workflow

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

**Node quan trọng nhất cần cấu hình:**
1. **Zoom Meeting Trigger (Recording Webhook)**
   - Đảm bảo endpoint webhook có dạng: `https://your-n8n-domain.com/webhook/zoom-recording`
   - Cấu hình webhook trong tài khoản Zoom của bạn để gửi dữ liệu đến endpoint này

2. **GPT-4o Reasoning Model**
   - Chọn credentials `openAiApi` đã được cấu hình
   - Đảm bảo model được đặt là `gpt-4o`

3. **Historical Meeting Search Engine (RAG Retriever) và Meeting Memory Storage (Vector DB Insert)**
   - Cấu hình credentials `supabaseApi`
   - Đảm bảo bảng `meeting_memories` đã được tạo trong Supabase với cấu trúc phù hợp

4. **Meeting Summary Email Dispatcher**
   - Cấu hình credentials `gmailOAuth2`
   - Điền địa chỉ email người nhận trong node này

#### 3. Kích hoạt ⚡️
1. Test run workflow với dữ liệu mẫu để đảm bảo tất cả các node hoạt động đúng
2. Sau khi kiểm tra thành công, bật chế độ Active cho workflow

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Teams**: Thêm node để gửi báo cáo đến các kênh chat của bạn
2. **Lưu log hoạt động**: Thêm node để lưu log các cuộc họp đã xử lý
3. **Báo cáo định kỳ**: Tạo workflow phụ để gửi báo cáo tổng hợp hàng tuần/tháng
4. **Xử lý lỗi nâng cao**: Thêm node để xử lý các trường hợp lỗi và gửi thông báo cảnh báo

### 📌 Kết luận
Workflow này mang đến giải pháp toàn diện cho việc tự động hóa phân tích cuộc họp Zoom. Với sự kết hợp của công nghệ AI tiên tiến và cơ sở dữ liệu vector, các sếp có thể nhận được báo cáo chi tiết và có giá trị ngay sau mỗi cuộc họp - giúp tiết kiệm thời gian và nâng cao hiệu quả làm việc.

Hãy thử ngay và trải nghiệm cách làm việc thông minh hơn với n8n! 🚀