---
title: "🚀 Tự động hóa LinkedIn Posts từ Voice Transcripts với Claude AI và Email"
description: "Hướng dẫn tự động hóa 100% không cần code để chuyển đổi voice transcripts thành bài viết LinkedIn chất lượng cao với AI và gửi tự động qua email"
slug: "tu-dong-hoa-linkedin-posts-tu-voice-transcripts-voi-claude-ai-va-email"
tags: [n8n, automation, no-code, linkedin, ai]
keywords: [n8n workflow, tự động hóa, linkedin, claude ai, voice transcripts]
---

# 🚀 Tự động hóa LinkedIn Posts từ Voice Transcripts với Claude AI và Email

[Các sếp] có biết không? Với công việc ngày càng bận rộn, việc phải chuyển đổi voice transcripts thành bài viết LinkedIn chất lượng thường tốn thời gian và công sức. Bạn phải:
- Chép tay ghi âm
- Sửa lỗi chính tả
- Tìm ảnh phù hợp
- Tối ưu nội dung cho LinkedIn

Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình này trong vòng vài phút, chỉ với một email!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Chỉ cần ghi âm và gửi email - hệ thống tự động xử lý
- **Nội dung chuyên nghiệp**: AI tạo bài viết theo phong cách của các sếp
- **Tối ưu LinkedIn**: Bài viết được định dạng đúng chuẩn 150-300 từ
- **Hiệu quả cao**: Tăng tương tác nhờ nội dung chất lượng
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản email IMAP (Gmail, Outlook, hoặc email doanh nghiệp)
- Tài khoản Anthropic Claude API (đăng ký tại [Anthropic](https://www.anthropic.com/))
- Google Doc chứa các ví dụ bài viết LinkedIn chất lượng (công khai hoặc chia sẻ qua link)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc](https://n8n.io/workflows/4874)
2. Copy toàn bộ JSON workflow
3. Trong n8n Editor, nhấn **Import from Clipboard** và dán JSON

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
**Node Email to Monitor**:
- Thêm credentials IMAP của các sếp
- Cấu hình IMAP trong email provider (Gmail, Outlook...)
- Kiểm tra kết nối để đảm bảo nhận email

**Node Limit email sender**:
- Thay thế "email@email.com" bằng địa chỉ email gửi transcripts
- Nếu dùng nhiều email khác nhau, thêm node filter mới

**Node Anthropic Chat Model**:
- Thêm credentials API Anthropic
- Đảm bảo model được chọn là "claude-sonnet-4-20250514"

**Node Google Doc Post Inspiration**:
- Tạo Google Doc mới chứa 10-15 ví dụ bài viết LinkedIn chất lượng
- Chia sẻ document công khai hoặc qua link
- Cập nhật URL trong node HTTP Request

#### 3. Kích hoạt ⚡️
1. Chạy test với dữ liệu mẫu để kiểm tra toàn bộ chuỗi
2. Bật Active workflow
3. Gửi email thử nghiệm từ địa chỉ được cấu hình

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Teams để nhận thông báo khi workflow chạy
- Lưu log hoạt động vào Airtable/Supabase để theo dõi hiệu suất
- Thêm node để tự động đăng bài lên LinkedIn (sử dụng node LinkedIn)
- Tạo báo cáo hàng tuần về hiệu quả nội dung

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc tạo nội dung LinkedIn chất lượng. Bằng cách kết hợp AI với email automation, các sếp có thể tập trung vào việc phát triển nội dung sáng tạo hơn. Hãy thử ngay và biến voice transcripts thành bài viết LinkedIn chuyên nghiệp chỉ trong vài phút!