---
title: "🚀 Tự động hóa ghi chú cuộc họp từ YouTube sang Notion với Claude và Slack"
description: "Hướng dẫn tự động hóa chuyển đổi bản ghi cuộc họp YouTube thành ghi chú Notion và thông báo Slack bằng n8n, tiết kiệm thời gian và nâng cao hiệu suất làm việc."
slug: "tu-dong-hoa-ghi-chu-cuoc-hop-youtube-notion-slack"
tags: [n8n, automation, no-code, AI, Notion, Slack]
keywords: [n8n workflow, tự động hóa, AI, Notion, Slack, ghi chú cuộc họp]
---

# 🚀 Tự động hóa ghi chú cuộc họp từ YouTube sang Notion với Claude và Slack

[Các sếp đang mệt mỏi với việc phải xem lại bản ghi cuộc họp YouTube, sao chép ghi chú tay, và gửi thông báo Slack thủ công? Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình này trong vòng 5 phút với n8n!]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm **80% thời gian** xử lý bản ghi cuộc họp
- Ghi chú **đầy đủ, có cấu trúc** trong Notion
- Thông báo **tự động** đến Slack với các hành động cần thực hiện
- **Tự động hóa hoàn toàn** quy trình từ YouTube đến Notion
- **Tiết kiệm chi phí** nhờ sử dụng deAPI thay vì dịch vụ ghi âm chuyên nghiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản [deAPI](https://deapi.ai) (dùng để chuyển đổi video thành văn bản)
- Tài khoản [Anthropic](https://www.anthropic.com/) (dùng để phân tích nội dung)
- Workspace Notion với database ghi chú cuộc họp
- Workspace Slack để nhận thông báo
- Instance n8n phải chạy trên **HTTPS**
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n](https://n8n.io/workflows/13919)
2. Click vào nút "Import" và chọn "Import from URL"
3. Hoặc copy toàn bộ JSON workflow và paste vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node YouTube RSS Trigger**:
   - Thay đổi **Feed URL** thành URL RSS của kênh YouTube của các sếp
   - Để lấy URL RSS, các sếp có thể sử dụng công thức:
     ```
     https://www.youtube.com/feeds/videos.xml?channel_id=YOUR_CHANNEL_ID
     ```
   - Để tìm Channel ID, các sếp vào trang kênh YouTube → Click "More" → "Share channel" → "Copy channel ID"

2. **Node deAPI Transcribe Video**:
   - Tạo credentials cho deAPI trong n8n
   - Đảm bảo tài khoản deAPI có đủ credit để xử lý video

3. **Node Anthropic Chat Model**:
   - Tạo credentials cho Anthropic trong n8n
   - Chọn model "Claude Opus 4.6" (hoặc model khác phù hợp)

4. **Node Notion**:
   - Tạo credentials cho Notion trong n8n
   - Cấu hình Database ID của database ghi chú cuộc họp
   - Mapping các trường dữ liệu từ output của AI Agent vào các thuộc tính của database

5. **Node Slack**:
   - Tạo credentials cho Slack trong n8n
   - Chọn channel để gửi thông báo

#### 3. Kích hoạt ⚡️
1. Test run workflow với một video mẫu
2. Kiểm tra kết quả trong Notion và Slack
3. Bật Active workflow để chạy tự động khi có video mới

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh prompt**: Các sếp có thể chỉnh sửa prompt trong node AI Agent để phù hợp với nhu cầu cụ thể của team
2. **Thêm thông báo**: Kết nối thêm node để gửi email hoặc thông báo đến Microsoft Teams
3. **Lưu log**: Thêm node để lưu log các cuộc họp đã xử lý
4. **Xử lý video dài**: Đối với video dài, các sếp có thể chia nhỏ thành các đoạn trước khi xử lý

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quy trình chuyển đổi bản ghi cuộc họp YouTube thành ghi chú Notion và thông báo Slack. Với việc tích hợp AI của Anthropic và dịch vụ ghi âm giá rẻ của deAPI, các sếp có thể tiết kiệm thời gian đáng kể trong khi vẫn duy trì chất lượng ghi chú chuyên nghiệp.

Hãy áp dụng ngay workflow này để nâng cao hiệu suất làm việc của team! Nếu có bất kỳ câu hỏi nào, các sếp có thể tham gia cộng đồng [n8n Discord](https://discord.gg/n8n) hoặc hỏi trong [Forum](https://community.n8n.io/)!