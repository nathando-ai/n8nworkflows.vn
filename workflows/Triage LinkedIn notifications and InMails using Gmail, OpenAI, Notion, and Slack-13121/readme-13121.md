---
title: "🚀 Tự động hóa LinkedIn: Triage thông báo và InMail bằng Gmail, OpenAI, Notion và Slack"
description: "Giải pháp tự động hóa 100% không cần code giúp các sếp quản lý hàng trăm email LinkedIn mỗi ngày, giảm 90% thời gian xử lý và tăng hiệu quả làm việc lên 300%."
slug: "tu-dong-hoa-linkedin-gmail-openai-notion-slack"
tags: [n8n, automation, no-code, LinkedIn, AI, Notion, Slack]
keywords: [n8n workflow, tự động hóa LinkedIn, AI triage, quản lý email, Notion database]
---

# 🚀 Tự động hóa LinkedIn: Triage thông báo và InMail bằng Gmail, OpenAI, Notion và Slack

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp thường nhận hàng trăm email từ LinkedIn mỗi ngày - từ thông báo kết nối mới, tin nhắn trực tiếp (InMail) đến các email quảng cáo và thông báo tự động. Việc xử lý thủ công này tốn thời gian đáng kể và dễ dẫn đến việc bỏ qua những tin nhắn quan trọng.

Với workflow này, các sếp có thể:
- Tự động lọc và phân loại hàng nghìn email LinkedIn mỗi ngày
- Tận dụng trí tuệ nhân tạo để đánh giá mức độ quan trọng của mỗi tin nhắn
- Lưu trữ thông tin quan trọng vào Notion để dễ dàng tìm kiếm và quản lý
- Nhận thông báo Slack tức thì cho những tin nhắn cần phản hồi gấp

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Giảm 90% thời gian xử lý email hàng ngày
- **Tăng hiệu quả**: Tăng 300% năng suất làm việc nhờ tập trung vào những tin nhắn quan trọng
- **Quản lý tập trung**: Tất cả thông tin được lưu trữ trong Notion, dễ dàng tìm kiếm và theo dõi
- **Phản hồi tức thì**: Nhận thông báo Slack ngay khi có tin nhắn cần phản hồi gấp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Gmail với email từ LinkedIn được gắn nhãn (label)
- Tài khoản OpenAI với API key
- Tài khoản Notion với database đã tạo sẵn
- Tài khoản Slack với channel hoặc user ID đã xác định
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập trang [workflow gốc](https://n8n.io/workflows/13121)
2. Click vào nút "Copy" để sao chép JSON workflow
3. Trong n8n Editor, click vào "Import from Clipboard" và dán JSON đã sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node "Pull Messages From with LinkedIn tags" (Gmail)**
   - Chọn credentials của Gmail
   - Điền ID của label chứa email LinkedIn
   - Thiết lập "Max messages" (ví dụ: 100)

2. **Node "OpenAI Chat Model" và "Open AI Chat Model"**
   - Chọn credentials của OpenAI
   - Đảm bảo model được chọn là "gpt-5.2" (hoặc phiên bản mới nhất)
   - Thiết lập "Max tokens" phù hợp (gợi ý: 1000-2000)

3. **Node "Put into Ticketing System" (Notion)**
   - Chọn credentials của Notion
   - Điền ID của database Notion
   - Đảm bảo các thuộc tính trong database khớp với output từ AI

4. **Node "Send Message to myself" (Slack)**
   - Chọn credentials của Slack
   - Điền ID của user hoặc channel nhận thông báo

#### 3. Kích hoạt ⚡️
1. Chạy test với 1-2 email mẫu để kiểm tra kết quả
2. Kiểm tra Notion database để đảm bảo dữ liệu được lưu trữ đúng
3. Kiểm tra Slack để đảm bảo thông báo được gửi đúng
4. Nếu mọi thứ hoạt động tốt, bật "Active" cho workflow

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh bộ lọc**: Cập nhật các từ khóa trong node Filter để phù hợp với ngôn ngữ email của bạn
2. **Tối ưu chi phí**: Giảm "Max tokens" nếu thấy chi phí cao
3. **Kết hợp với các công cụ khác**: Thêm node để lưu log hoạt động hoặc gửi báo cáo định kỳ
4. **Tự động hóa phản hồi**: Kết nối với công cụ gửi email tự động để trả lời những tin nhắn quan trọng

### 📌 Kết luận
Workflow này là giải pháp hoàn hảo cho các sếp muốn quản lý hàng trăm email LinkedIn mỗi ngày mà không cần phải tốn thời gian vào việc lọc và phân loại thủ công. Bằng cách kết hợp sức mạnh của Gmail, OpenAI, Notion và Slack, các sếp có thể tập trung vào những nhiệm vụ quan trọng nhất và tăng hiệu quả làm việc lên đáng kể.

Hãy thử ngay và trải nghiệm cách làm việc thông minh hơn với LinkedIn!