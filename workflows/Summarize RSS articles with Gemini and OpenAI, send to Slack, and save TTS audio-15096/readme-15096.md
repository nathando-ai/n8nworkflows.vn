---
title: "🚀 Tự động hóa tổng hợp tin tức RSS với AI Gemini & OpenAI, gửi Slack và lưu âm thanh TTS"
description: "Workflow n8n tự động thu thập, phân tích và tổng hợp tin tức từ nhiều nguồn RSS, lọc ra những bài viết hữu ích nhất, chuyển đổi thành âm thanh và gửi báo cáo qua Slack - giải pháp hoàn hảo cho người làm việc bận rộn."
slug: "tu-dong-hoa-tong-hop-tin-tuc-rss-voi-ai-gemini-openai-slack-tts"
tags: [n8n, automation, no-code, AI, Slack, Google Drive, RSS]
keywords: [n8n workflow, tự động hóa, AI tổng hợp tin tức, Slack báo cáo, TTS âm thanh]
---

# 🚀 Tự động hóa tổng hợp tin tức RSS với AI Gemini & OpenAI, gửi Slack và lưu âm thanh TTS

[Các sếp làm việc bận rộn thường phải mất hàng giờ mỗi ngày để đọc và lọc thông tin từ nhiều nguồn tin tức khác nhau. Bạn có biết rằng chỉ cần 25% thời gian đọc là đủ để hiểu nội dung chính của một bài viết? Với workflow này, các sếp sẽ tiết kiệm được hàng giờ mỗi ngày nhờ vào sức mạnh của trí tuệ nhân tạo.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động thu thập và lọc tin tức từ nhiều nguồn trong vòng 24 giờ
- **Chính xác cao**: AI Gemini và OpenAI đánh giá và chọn ra những bài viết hữu ích nhất
- **Cá nhân hóa**: Nhận báo cáo tổng hợp theo định dạng và nội dung phù hợp với nhu cầu
- **Hoạt động liên tục**: Workflow chạy tự động mỗi ngày mà không cần can thiệp
- **Đa dạng định dạng**: Nhận báo cáo dưới dạng văn bản (Slack) và âm thanh (Google Drive)
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Gemini API
- Tài khoản OpenAI API
- Tài khoản Slack với quyền truy cập vào channel nhận báo cáo
- (Tùy chọn) Tài khoản Google Drive để lưu trữ file âm thanh
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [trang workflow gốc](https://n8n.io/workflows/15096)
2. Click vào nút "Download" để tải file JSON
3. Trong n8n Editor, click vào menu "Workflow" > "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Trigger: Schedule Workflow"**:
   - Cấu hình thời gian chạy workflow (mặc định là mỗi ngày)

2. **Node "Fetch RSS: Roomie Feed", "Fetch RSS: Lifehacker Feed", "Fetch RSS: Note Work Tips", "Fetch RSS: Note Productivity", "Fetch RSS: Note Efficiency", "Fetch RSS: Note Cost Performance"**:
   - Thay đổi URL feed nếu muốn theo dõi các nguồn tin khác
   - Cấu hình số lượng bài viết tối đa cần lấy

3. **Node "Model: Gemini" và "Model: OpenAI"**:
   - Tạo và cấu hình credentials cho Google Gemini API và OpenAI API
   - Chọn model phù hợp (gpt-4.1-nano, gpt-3.5-turbo)

4. **Node "Notify: Send Summary to Slack"**:
   - Tạo và cấu hình credentials cho Slack OAuth2
   - Chọn channel nhận báo cáo

5. **Node "Upload: Save Audio to Google Drive" (tùy chọn)**:
   - Tạo và cấu hình credentials cho Google Drive OAuth2
   - Chọn thư mục lưu trữ file âm thanh

#### 3. Kích hoạt ⚡️
1. Click vào nút "Execute Workflow" để test chạy với dữ liệu mẫu
2. Kiểm tra kết quả trên Slack và Google Drive (nếu đã cấu hình)
3. Sau khi test thành công, click vào nút "Activate Workflow" để bật chế độ tự động

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh nội dung báo cáo**:
   - Chỉnh sửa prompt trong node "AI: Rank Articles by Practical Value" để thay đổi tiêu chí đánh giá
   - Điều chỉnh template trong node "Format: Slack Message Output" để thay đổi định dạng báo cáo

2. **Kết hợp với các công cụ khác**:
   - Thêm node để gửi báo cáo qua Telegram hoặc Email
   - Kết nối với Notion để lưu trữ báo cáo dưới dạng database

3. **Tối ưu hiệu suất**:
   - Thêm node "Delay" giữa các bước xử lý để tránh bị giới hạn API
   - Sử dụng cache để lưu trữ kết quả xử lý trước đó

4. **Phát triển thêm**:
   - Thêm chức năng phân loại tin tức theo chủ đề
   - Tích hợp với các công cụ quản lý công việc như Trello hoặc Asana

### 📌 Kết luận
Workflow này mang lại giải pháp toàn diện cho việc tự động hóa việc thu thập, phân tích và tổng hợp tin tức từ nhiều nguồn. Với sự kết hợp của AI Gemini và OpenAI, các sếp sẽ nhận được những báo cáo chất lượng cao, tiết kiệm thời gian và tối ưu hóa hiệu suất làm việc. Hãy áp dụng ngay để nâng cao năng suất làm việc của mình!