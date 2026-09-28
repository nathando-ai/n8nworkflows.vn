---
title: "🚀 Tự động tạo báo giá từ bản ghi âm cuộc họp với AI, Google Drive và PandaDoc"
description: "Xây dựng hệ thống Multi-Agent AI tự động đọc bản ghi cuộc họp, phân tích nhu cầu, tính toán giá cả và tạo hợp đồng PandaDoc chuyên nghiệp không cần thủ công."
slug: "tu-dong-tao-bao-gia-tu-ban-ghi-cuop-hop-ai-pandadoc"
tags: [n8n, automation, ai-agents, pandadoc, crm, google-drive]
keywords: [n8n workflow, tạo báo giá tự động, claude ai, gpt-4, pandadoc integration, ai multi-agent]
keywords: [n8n workflow, tự động hóa, tạo báo giá, pandadoc, claude, ai agents]
---

# 🚀 Tự động tạo báo giá từ bản ghi âm cuộc họp với Multi-Agent AI & PandaDoc

Các sếp có bao nhiêu thời gian bị chôn vùi vào việc nghe lại bản ghi âm cuộc họp (transcript), bóc tách yêu cầu khách hàng, tính toán chi phí và soạn thảo báo giá (SOW / Quote)? Công việc lặp đi lặp lại này không chỉ tốn hàng giờ đồng hồ mà còn dễ dẫn đến sai sót, báo giá chậm và mất cơ hội chốt sale vào tay đối thủ.

Workflow n8n cực khủng với 58 nodes này chính là giải pháp tự động hóa toàn diện (End-to-End) sử dụng kiến trúc **Multi-Agent AI** kết hợp giữa Claude, GPT, Perplexity, Google Drive, Notion và PandaDoc. Hệ thống sẽ tự động hóa từ khâu nhận file ghi âm, phân tích nhu cầu, định giá thông minh cho đến khi gửi bản thảo duyệt qua Slack và chuyển hợp đồng chuyên nghiệp cho khách hàng!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow quy mô lớn này chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100% quy trình sales:** Biến file transcript thô thành bản báo giá chuẩn chỉnh chỉ trong vài phút.
- **AI thông minh đa tầng (Multi-Agent):** Sử dụng các mô hình AI đỉnh cao (Claude Sonnet/Opus, GPT-4 Turbo, Grok) kết hợp tra cứu thị trường thời gian thực qua Perplexity để tối ưu biên lợi nhuận (>80%).
- **Kiểm soát chặt chẽ:** Tự động gửi thông báo xét duyệt qua Slack kèm nút bấm phê duyệt/từ chối trực quan trước khi gửi cho khách.
- **Đồng bộ CRM xuyên suốt:** Tự động cập nhật trạng thái khách hàng trên Notion và kích hoạt email chào mừng qua Gmail khi tài liệu được ký kết thành công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI "LÊN ĐỒ"]
Các sếp cần chuẩn bị sẵn các tài khoản và API Keys sau:
- **Tài khoản n8n** (Self-hosted hoặc Cloud).
- **Google Drive & Google Calendar** (OAuth2 Credentials) để theo dõi thư mục transcript và đối soát lịch họp.
- **OpenRouter API Key** (để cấu hình các model AI: Claude, GPT-4, Grok).
- **Perplexity API Key** (cho tool tìm kiếm thông tin dịch vụ và giá cả thị trường).
- **PandaDoc API Key & Template UUID** (để tạo và quản lý báo giá/hợp đồng).
- **Slack OAuth2** (để gửi yêu cầu phê duyệt và tương tác).
- **Gmail OAuth2** (để gửi email cho khách hàng).
- **Notion API Key** (để quản lý CRM cơ sở dữ liệu khách hàng).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ nguồn cung cấp.
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File** và tải file JSON lên.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow được chia thành 6 phân vùng chính trên canvas, các sếp cần chú ý cấu hình kỹ các node sau:
- **Google Drive Trigger & Download file**: Kết nối tài khoản Google Drive OAuth2 và chọn thư mục chuyên dụng chứa các file transcript định dạng `.vtt`.
- **OpenRouter (các node AI Models như Sonnet 4.5, Opus 4.5, GPT4 Turbo, Grok)**: Thêm thông tin xác thực OpenRouter API Key để các Agent hoạt động mượt mà.
- **Search Tools & pricing**: Kết nối Perplexity API để Agent có thể tự động tra cứu giá thị trường.
- **Create Quote & Update Pricing Section**: Nhập PandaDoc API Key và liên kết với template báo giá chuẩn của doanh nghiệp.
- **Send for Review & confirmation_message**: Cấu hình Slack OAuth2 để bot gửi tin nhắn yêu cầu sếp duyệt báo giá kèm nút bấm tương tác.
- **Search_CRM & Update status**: Cấu hình Notion API để hệ thống tự động tìm kiếm thông tin khách hàng và cập nhật trạng thái trong database.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) với một file transcript mẫu để kiểm tra luồng từ đầu đến cuối.
- Kiểm tra tính năng tương tác trên Slack và các bảng dữ liệu Notion/PandaDoc.
- Bật công tắc **Active** để workflow chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Tích hợp thêm Telegram hoặc Microsoft Teams bên cạnh Slack để đội ngũ quản lý linh hoạt phê duyệt báo giá mọi lúc mọi nơi.
- **Tùy chỉnh Prompt cho Pricing Agent:** Tinh chỉnh hệ thống quy tắc biên lợi nhuận trong prompt của agent định giá để phù hợp với từng dòng sản phẩm/dịch vụ đặc thù của công ty.
- **Lưu lịch sử báo giá:** Tận dụng các node `DataTable` sẵn có trong workflow để lưu log phản hồi của khách hàng, phục vụ cho việc tối ưu tỷ lệ chuyển đổi (Conversion Rate) về sau.

### 📌 Kết luận
Workflow tạo báo giá tự động ứng dụng Multi-Agent AI này là bước tiến đột phá giúp doanh nghiệp tối ưu hóa toàn bộ khâu tiền, giảm tải 90% công việc thủ công cho đội ngũ Sales và CS. Hãy triển khai ngay hôm nay để tăng tốc độ chốt đơn lên gấp nhiều lần!