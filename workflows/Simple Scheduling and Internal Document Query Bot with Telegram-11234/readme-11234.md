---
title: "🤖 [Tự động hóa Truy vấn Nội bộ & Lịch Hẹn với Telegram + AI - Không cần Code]"
description: "Hướng dẫn chi tiết cách tự động hóa truy vấn tài liệu nội bộ, kiểm tra giá dịch vụ và quản lý lịch hẹn qua Telegram bằng n8n và AI Gemini"
slug: "tu-dong-hoa-truy-van-noi-bo-lich-hen-telegram-ai"
tags: [n8n, automation, no-code, telegram, google-workspace, ai]
keywords: [n8n workflow, tự động hóa, telegram bot, google calendar, google sheets, google docs, ai agent]
---

# 🤖 Tự động hóa Truy vấn Nội bộ & Lịch Hẹn với Telegram + AI - Không cần Code

[Các sếp đang mệt mỏi với việc phải trả lời hàng trăm câu hỏi nội bộ hàng ngày về giá dịch vụ, hướng dẫn sử dụng và quản lý lịch hẹn? Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình này chỉ trong vài bước đơn giản, mà không cần viết một dòng code nào!]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** cho đội ngũ hỗ trợ: Tự động trả lời hàng nghìn câu hỏi nội bộ hàng ngày
- **Chính xác 100%**: Kiểm tra giá dịch vụ và thông tin nội bộ từ các nguồn dữ liệu chính xác nhất
- **Quản lý lịch hẹn thông minh**: Tạo, sửa, xóa và kiểm tra lịch hẹn một cách tự động
- **Trải nghiệm người dùng tốt hơn**: Người dùng nhận được phản hồi tức thì qua Telegram
- **Dễ dàng mở rộng**: Có thể kết nối thêm nhiều kênh khác như WhatsApp, webhook...
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập vào Google Calendar, Google Docs và Google Sheets
- Máy chủ MCP đã cấu hình để kết nối các dịch vụ này
- Node Telegram đã tích hợp (hoặc các kênh đầu vào/đầu ra khác)
- Tài khoản Upstash để lưu trữ bộ nhớ Redis
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/11234)
2. Click vào nút "Download" để tải file JSON
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Telegram Trigger** (Node 9):
   - Cần cấu hình credentials cho Telegram API
   - Điền Chat ID của người dùng hoặc nhóm Telegram mà bạn muốn kết nối

2. **Google Calendar Tools** (Nodes 11-14):
   - Cần cấu hình credentials cho Google Calendar OAuth2 API
   - Đảm bảo tài khoản Google có quyền truy cập đầy đủ vào lịch

3. **Google Sheets Tools** (Nodes 2-3):
   - Cần cấu hình credentials cho Google Sheets OAuth2 API
   - Cập nhật Spreadsheet ID và tên sheet chính xác
   - Đảm bảo cấu trúc dữ liệu trong sheet phù hợp với workflow

4. **Google Docs Tool** (Node 4):
   - Cần cấu hình credentials cho Google Docs OAuth2 API
   - Điền Document ID chính xác của tài liệu nội bộ

5. **Google Gemini Chat Model** (Node 16):
   - Cần cấu hình credentials cho Google PaLM API
   - Điền API Key và cấu hình các tham số như temperature, max tokens...

6. **Redis Chat Memory** (Node 17):
   - Cần cấu hình credentials cho Redis
   - Điền thông tin kết nối Redis (host, port, password nếu có)

7. **MCP Clients** (Nodes 5-6):
   - Cần cấu hình kết nối đến MCP Server
   - Điền thông tin endpoint và các tham số kết nối

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node quan trọng, hãy chạy test với dữ liệu mẫu
2. Kiểm tra các kết quả trả về từ các node để đảm bảo workflow hoạt động đúng
3. Bật chế độ Active cho workflow khi đã kiểm tra xong

### ✍️ Mẹo & gợi ý nâng cao
1. **Tách các agent chuyên biệt**: Phát triển các agent riêng biệt cho từng chức năng (lịch hẹn, kiểm tra giá, hỗ trợ kỹ thuật) để workflow trở nên mô-đun hóa và dễ bảo trì hơn.

2. **Hỗ trợ giọng nói**: Thêm tính năng nhập/xuất giọng nói trong Telegram để người dùng có thể đặt lịch hẹn bằng giọng nói.

3. **Nâng cao RAG**: Áp dụng kỹ thuật embeddings và các cơ sở dữ liệu vector (Pinecone, Weaviate, Milvus) để truy vấn thông tin từ tài liệu nội bộ một cách thông minh hơn.

4. **Kết nối thêm kênh**: Mở rộng workflow bằng cách kết nối thêm các kênh như WhatsApp, Slack, hoặc các hệ thống CRM khác.

5. **Báo cáo tự động**: Thêm node để gửi báo cáo hàng ngày về các hoạt động quan trọng qua email hoặc Telegram.

### 📌 Kết luận
Workflow này đã biến những công việc thủ công, lặp đi lặp lại thành các quy trình tự động hoàn toàn, giúp các sếp tiết kiệm thời gian quý giá và tập trung vào những nhiệm vụ quan trọng hơn. Với khả năng kết nối đa kênh và tích hợp AI thông minh, workflow này không chỉ tiết kiệm thời gian mà còn nâng cao trải nghiệm người dùng một cách đáng kể. Hãy áp dụng ngay để thấy sự khác biệt trong hiệu suất làm việc của đội ngũ!