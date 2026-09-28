---
title: "📰 Tự động hóa tổng hợp bài viết kỹ thuật AI từ Qiita và note sang Slack"
description: "Workflow n8n tự động thu thập, lọc và tổng hợp các bài viết kỹ thuật AI hàng ngày từ Qiita và note, gửi báo cáo tóm tắt chất lượng cao đến Slack hàng ngày."
slug: "tu-dong-hoa-tong-hop-bai-viet-ky-thuat-ai-tu-qiita-va-note-sang-slack"
tags: [n8n, automation, no-code, AI, Slack]
keywords: [n8n workflow, tự động hóa, AI, Slack, Qiita, note]
---

# 📰 Tự động hóa tổng hợp bài viết kỹ thuật AI từ Qiita và note sang Slack

[Các sếp làm kỹ thuật AI và kỹ sư Nhật Bản thường gặp khó khăn khi phải theo dõi hàng trăm bài viết kỹ thuật hàng ngày trên các nền tảng như Qiita và note. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình từ thu thập dữ liệu đến gửi báo cáo tóm tắt chất lượng cao đến Slack hàng ngày.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động thu thập và xử lý hàng trăm bài viết mỗi ngày.
- **Chính xác cao**: Lọc và xếp hạng bài viết dựa trên tiêu chí kỹ thuật.
- **Cá nhân hóa**: Tóm tắt nội dung theo nhu cầu cụ thể của từng người dùng.
- **Hoạt động liên tục**: Nhận báo cáo hàng ngày mà không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Gemini API (để đánh giá và xếp hạng bài viết).
- Tài khoản OpenAI API (để tổng hợp nội dung bài viết).
- Tài khoản Slack OAuth2 (để gửi báo cáo).
- Một kênh Slack để nhận thông báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/14980](https://n8n.io/workflows/14980).
2. Nhấn nút "Import" để tải xuống file JSON.
3. Trong n8n Editor, nhấn vào "Import from File" và chọn file JSON đã tải xuống.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Trigger: Schedule Workflow**
   - Cấu hình lịch chạy workflow (ví dụ: hàng ngày lúc 9:00 sáng).

2. **Fetch RSS: Qiita Popular Feed**
   - Đảm bảo URL RSS của Qiita là chính xác.

3. **Fetch RSS: note Engineer Hashtag Feed**
   - Cập nhật URL RSS của note nếu cần thiết.

4. **Model: Gemini**
   - Thêm credentials cho Google Gemini API.
   - Đảm bảo API key có quyền truy cập đầy đủ.

5. **Model: OpenAI**
   - Thêm credentials cho OpenAI API.
   - Chọn model phù hợp (ví dụ: gpt-4.1-nano).

6. **Notify: Send to Slack**
   - Thêm credentials cho Slack OAuth2.
   - Cấu hình kênh Slack để nhận thông báo.

#### 3. Kích hoạt ⚡️
1. Nhấn nút "Execute Workflow" để test với dữ liệu mẫu.
2. Kiểm tra kết quả trên kênh Slack.
3. Bật "Active" workflow để chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Telegram**: Thay thế node Slack bằng node Telegram để nhận thông báo.
- **Lưu log**: Thêm node để lưu log các bài viết đã xử lý.
- **Gửi báo cáo định kỳ**: Cấu hình gửi báo cáo hàng tuần hoặc hàng tháng.
- **Tùy chỉnh tiêu chí đánh giá**: Điều chỉnh prompt trong node "AI: Score Articles" để phù hợp với nhu cầu cụ thể.

### 📌 Kết luận
Workflow này giúp các sếp kỹ thuật AI và kỹ sư Nhật Bản tiết kiệm thời gian và công sức trong việc theo dõi và tổng hợp thông tin từ các bài viết kỹ thuật hàng ngày. Bằng cách tự động hóa toàn bộ quy trình, các sếp có thể tập trung vào những nhiệm vụ quan trọng hơn. Hãy áp dụng ngay để nâng cao hiệu suất làm việc!