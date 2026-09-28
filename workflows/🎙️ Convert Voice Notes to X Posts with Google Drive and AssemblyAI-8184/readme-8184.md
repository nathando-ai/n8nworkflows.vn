```yaml
---
title: "🎙️ Tự động chuyển đổi ghi âm thành bài đăng X (Twitter) với Google Drive và AssemblyAI"
description: "Hướng dẫn tự động hóa chuyển đổi ghi âm thành văn bản và đăng lên X (Twitter) hoàn toàn không cần code"
slug: "tu-dong-chuyen-doi-ghi-am-thanh-bai-dang-x-google-drive-assemblyai"
tags: [n8n, automation, no-code, google-drive, assemblyai, twitter]
keywords: [n8n workflow, tự động hóa ghi âm, chuyển đổi âm thanh, đăng bài X, assemblyai, google drive]
---

# 🎙️ Tự động chuyển đổi ghi âm thành bài đăng X (Twitter) với Google Drive và AssemblyAI

[Các sếp thường gặp tình trạng phải chuyển đổi thủ công các ghi âm thành văn bản để đăng lên X (Twitter). Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình này chỉ trong vài bước đơn giản.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động chuyển đổi ghi âm thành văn bản chính xác
- Đăng bài lên X (Twitter) một cách nhanh chóng và tự động
- Tiết kiệm thời gian và công sức cho các tác vụ lặp lại
- Hoạt động liên tục 24/7 mà không cần can thiệp thủ công
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Drive với thư mục chứa các file ghi âm
- Tài khoản AssemblyAI với API key
- Tài khoản X (Twitter) với quyền đăng bài
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/8184)
2. Click vào nút "Copy to clipboard" để sao chép JSON workflow
3. Trong n8n Editor, click vào "Import from Clipboard" và dán JSON đã sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Watch Google Drive Folder"**:
   - Chọn credentials Google Drive của bạn
   - Nhập ID của thư mục chứa các file ghi âm
   - Đảm bảo thư mục này chỉ chứa các file âm thanh (mp3, wav, m4a)

2. **Node "Transcribe with AssemblyAI"**:
   - Chọn credentials AssemblyAI của bạn
   - Đảm bảo tài khoản AssemblyAI có đủ credit để thực hiện chuyển đổi
   - Có thể điều chỉnh các tham số như ngôn ngữ, định dạng đầu ra nếu cần

3. **Node "Post to X (Twitter)"**:
   - Chọn credentials X (Twitter) của bạn
   - Có thể thêm các hashtag hoặc thông tin bổ sung vào nội dung bài đăng

#### 3. Kích hoạt ⚡️
1. Test run workflow với một file ghi âm mẫu
2. Kiểm tra kết quả chuyển đổi và bài đăng trên X (Twitter)
3. Nếu mọi thứ hoạt động tốt, bật Active workflow để chạy liên tục

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node gửi email thông báo khi có bài đăng mới
- Kết hợp với Slack để nhận thông báo khi workflow chạy
- Lưu trữ bản ghi âm và bản chuyển đổi vào Google Drive
- Tự động hóa việc đăng bài lên các nền tảng khác như LinkedIn

### 📌 Kết luận
Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình chuyển đổi ghi âm thành bài đăng X (Twitter) một cách nhanh chóng và chính xác. Hãy áp dụng ngay để tiết kiệm thời gian và công sức cho các tác vụ lặp lại!