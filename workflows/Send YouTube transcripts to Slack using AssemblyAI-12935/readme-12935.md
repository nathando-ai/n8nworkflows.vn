---
title: "🎤 Tự động hóa chuyển đổi transcript YouTube sang Slack với AssemblyAI"
description: "Hướng dẫn chi tiết cách tự động hóa quá trình chuyển đổi transcript video YouTube sang Slack chỉ với 1 lệnh đơn giản, tiết kiệm thời gian và nâng cao hiệu suất làm việc."
slug: "tu-dong-hoa-transcript-youtube-sang-slack"
tags: [n8n, automation, no-code, youtube, slack]
keywords: [n8n workflow, tự động hóa, transcript youtube, slack, assemblyai]
---

# 🎤 Tự động hóa chuyển đổi transcript YouTube sang Slack với AssemblyAI

[Các sếp] có bao giờ phải tốn thời gian xem lại video YouTube để lấy nội dung quan trọng? Với workflow này, các sếp chỉ cần gửi link video qua Slack, hệ thống sẽ tự động chuyển đổi transcript và gửi lại kết quả ngay lập tức - không cần can thiệp thủ công!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Chuyển đổi transcript tự động trong vài giây thay vì phải xem lại video
- **Chính xác cao**: Sử dụng công nghệ AI tiên tiến của AssemblyAI
- **Tích hợp hoàn hảo**: Kết quả được gửi trực tiếp vào Slack channel
- **Tùy chỉnh dễ dàng**: Có thể điều chỉnh độ dài video tối đa và tùy chọn tóm tắt AI
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Slack với quyền tạo slash command
- API Key từ YouTube Data API
- API Key từ AssemblyAI
- API Key từ OpenAI (tùy chọn, cho chức năng tóm tắt AI)
- Tài khoản RapidAPI (để sử dụng YouTube to MP3 converter)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/12935)
2. Click vào nút "Download" để tải file JSON
3. Trong n8n Editor, click vào "Import from File" và chọn file vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Receive Slack command"**:
   - Cấu hình webhook với path: `/rippr`
   - Đảm bảo phương thức HTTP là POST

2. **Node "Check Video Duration"**:
   - Thêm credentials cho YouTube Data API
   - Cấu hình header với API Key của bạn

3. **Node "Convert YouTube video to MP3"**:
   - Thêm credentials từ RapidAPI
   - Cấu hình header với API Key của bạn

4. **Node "Create transcription job" và các node liên quan**:
   - Thêm credentials từ AssemblyAI
   - Cấu hình header với API Key của bạn

5. **Node "Generate AI summary" (tùy chọn)**:
   - Thêm credentials từ OpenAI
   - Cấu hình với API Key của bạn

6. **Node "Post result to Slack"**:
   - Đảm bảo cấu hình đúng response URL từ Slack

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node, click vào nút "Activate" để bật workflow
2. Test workflow bằng cách gửi lệnh Slack với link video YouTube
3. Kiểm tra kết quả trong channel Slack của bạn

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh độ dài video**: Thay đổi giá trị duration limit trong node "Is video longer than limit?" để phù hợp với nhu cầu của bạn
2. **Tích hợp với Google Drive**: Thêm node để lưu transcript dưới dạng file text vào Google Drive
3. **Thông báo lỗi nâng cao**: Cấu hình thêm node để gửi thông báo lỗi chi tiết qua Slack khi có vấn đề xảy ra
4. **Lịch sử transcript**: Thêm node để lưu trữ lịch sử các transcript đã xử lý

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong quá trình xử lý nội dung video. Với tích hợp hoàn hảo với Slack, các sếp có thể tiếp tục làm việc trong môi trường quen thuộc mà không cần chuyển đổi giữa các công cụ khác nhau. Hãy thử ngay và trải nghiệm cách làm việc hiệu quả hơn!