---
title: "🚀 Tự động hóa ghi chú cuộc họp với Gemini AI và Notion"
description: "Tự động hóa toàn bộ quy trình xử lý bản ghi cuộc họp: chuyển đổi, tóm tắt và tạo danh sách công việc với Gemini AI, đồng thời lưu vào Notion và thông báo qua Slack"
slug: "tu-dong-hoa-ghi-chu-cuoc-hop-voi-gemini-ai-va-notion"
tags: [n8n, automation, no-code, ai, notion, slack]
keywords: [n8n workflow, tự động hóa, ghi chú cuộc họp, Gemini AI, Notion, Slack]
---

# 🚀 Tự động hóa ghi chú cuộc họp với Gemini AI và Notion

[Các sếp] có bao giờ cảm thấy mệt mỏi khi phải xử lý hàng loạt bản ghi cuộc họp hàng ngày? Từ việc nghe lại, tóm tắt nội dung đến tạo danh sách công việc và chia sẻ với team? Với workflow này, các sếp có thể tự động hóa hoàn toàn quy trình này chỉ trong vài bước đơn giản!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động xử lý bản ghi cuộc họp trong vài phút thay vì vài giờ
- **Chính xác cao**: Sử dụng công nghệ AI Gemini để tóm tắt và phân tích nội dung
- **Cá nhân hóa**: Tạo ghi chú chi tiết với danh sách công việc cụ thể
- **Hiệu quả teamwork**: Thông báo tức thời qua Slack và lưu trữ tổ chức trên Notion
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Cloud với API Gemini đã kích hoạt
- Tài khoản Notion với database đã tạo sẵn (xem hướng dẫn bên dưới)
- Tài khoản Slack với channel dành cho cuộc họp
- File bản ghi cuộc họp (MP3, WAV, MP4...)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập trang workflow gốc: [Summarize meeting recordings and create Notion action items with Gemini AI](https://n8n.io/workflows/13771)
2. Click vào nút "Import" và chọn "Import from URL"
3. Dán URL workflow vào ô nhập liệu và nhấn "Import"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Upload meeting recording"**:
   - Đảm bảo đường dẫn form trigger là duy nhất: `e5b77a90-f97d-47d8-bba2-75afca30c8d7`
   - Lưu ý: Đây là đường dẫn cố định, không nên thay đổi

2. **Node "Upload recording to Gemini"**:
   - Thêm credential cho Google Gemini API
   - Đảm bảo endpoint API là chính xác: `https://generativelanguage.googleapis.com/v1beta/files:upload`

3. **Node "Analyze recording with Gemini"**:
   - Thêm credential cho Google Gemini API
   - Đảm bảo endpoint API là chính xác: `https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-pro-latest:generateContent`
   - Cấu hình prompt trong node để phù hợp với nhu cầu của team

4. **Node "Create notes in Notion"**:
   - Thêm credential cho Notion API
   - Tạo database trong Notion với các cột sau:
     - Title (text)
     - Date (date)
     - Summary (rich text)
     - Action Items (rich text)
     - Status (select)
   - Cập nhật ID database trong node

5. **Node "Notify team on Slack"**:
   - Thêm credential cho Slack OAuth2
   - Chọn channel phù hợp để thông báo
   - Tùy chỉnh nội dung thông báo theo nhu cầu

#### 3. Kích hoạt ⚡️
1. Test run workflow với file bản ghi mẫu
2. Kiểm tra kết quả trên Notion và Slack
3. Bật Active workflow để sử dụng thực tế

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp với Google Drive**: Thêm node để tự động lưu bản ghi vào Google Drive sau khi xử lý
2. **Báo cáo định kỳ**: Tạo workflow phụ để gửi báo cáo tổng hợp hàng tuần qua email
3. **Phân tích cảm xúc**: Sử dụng tính năng phân tích cảm xúc của Gemini để đánh giá thái độ trong cuộc họp
4. **Tích hợp với Trello**: Thay thế node Notion bằng node Trello để tạo thẻ công việc trực tiếp

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm hàng giờ mỗi ngày trong việc xử lý bản ghi cuộc họp. Với sự kết hợp của Gemini AI, Notion và Slack, các sếp có thể tập trung vào những công việc quan trọng hơn. Hãy thử ngay và trải nghiệm cách làm việc hiệu quả hơn!