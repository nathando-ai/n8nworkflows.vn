---
title: "📚 Tự động tạo thẻ ghi nhớ Anki bằng Google Translate và GPT-4o"
description: "Hướng dẫn tự động hóa tạo thẻ ghi nhớ Anki cho học ngôn ngữ bằng cách kết hợp Google Translate, GPT-4o và Google Sheets trong n8n"
slug: "tu-dong-tao-the-ghi-nho-anki-voi-google-translate-va-gpt-4o"
tags: [n8n, automation, no-code, anki, google-translate, gpt-4o]
keywords: [n8n workflow, tự động hóa, học ngôn ngữ, thẻ ghi nhớ, anki, google translate, gpt-4o]
---

# 📚 Tự động tạo thẻ ghi nhớ Anki bằng Google Translate và GPT-4o

[Các sếp đang gặp khó khăn khi tạo thẻ ghi nhớ Anki thủ công cho việc học ngôn ngữ. Workflow này giúp tự động hóa toàn bộ quy trình từ dịch thuật đến tạo thẻ ghi nhớ hoàn chỉnh, tiết kiệm thời gian đáng kể và đảm bảo tính chính xác cao.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động dịch thuật từ tiếng Anh sang ngôn ngữ mục tiêu (ví dụ: tiếng Trung)
- Tạo tự động phiên âm và ví dụ câu mẫu
- Tìm và tải ảnh minh họa từ Pexels
- Cập nhật toàn bộ thông tin vào Google Sheets
- Hoạt động liên tục 24/7 khi được kích hoạt
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Cloud với API credentials cho:
  - Google Sheets
  - Google Translate
  - Google Drive
- Tài khoản OpenAI với API key cho GPT-4o
- API key từ Pexels (đăng ký miễn phí tại [pexels.com](https://www.pexels.com/onboarding/))
- Google Sheet đã được thiết lập với cột "initialText" để nhập từ cần dịch
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/3195](https://n8n.io/workflows/3195)
2. Chọn "Import" và sao chép JSON workflow
3. Trong n8n Editor, nhấn "Import from Clipboard" và dán JSON đã sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Trigger Added Row (Google Sheets Trigger)**:
   - Thêm Google Sheets API credentials
   - Chọn file Google Sheet chứa danh sách từ vựng
   - Chọn sheet chứa danh sách từ vựng

2. **Google Translate**:
   - Thêm Google Translate API credentials
   - Chọn ngôn ngữ mục tiêu (ví dụ: ZH-CN cho tiếng Trung)

3. **OpenAI Chat Model**:
   - Thêm OpenAI API credentials
   - Đảm bảo chọn model "gpt-4o-mini"

4. **Call API Pexels**:
   - Thêm API key Pexels vào header 'Authorization'
   - Đảm bảo tài khoản Pexels đã được kích hoạt

5. **Upload Picture (Google Drive)**:
   - Thêm Google Drive API credentials
   - Chọn parent drive và folder để lưu ảnh

6. **Add Results in Sheet (Google Sheets)**:
   - Thêm Google Sheets API credentials
   - Chọn file và sheet chứa danh sách từ vựng

#### 3. Kích hoạt ⚡️
1. Thêm từ mới vào cột "initialText" trong Google Sheet
2. Workflow sẽ tự động kích hoạt và xử lý từ mới
3. Kiểm tra kết quả trong Google Sheet sau khi workflow hoàn thành

### ✍️ Mẹo & gợi ý nâng cao
1. Kết hợp với Slack/Telegram để nhận thông báo khi workflow hoàn thành
2. Thêm node lưu log hoạt động để theo dõi lịch sử tạo thẻ
3. Tạo báo cáo định kỳ về số lượng từ đã học và tiến độ
4. Kết hợp với các công cụ học từ vựng khác như Quizlet

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc tạo thẻ ghi nhớ Anki cho việc học ngôn ngữ. Bằng cách tự động hóa toàn bộ quy trình từ dịch thuật đến tạo thẻ hoàn chỉnh, các sếp có thể tập trung vào việc học và cải thiện kỹ năng ngôn ngữ một cách hiệu quả hơn. Hãy thử ngay và nâng cao trải nghiệm học tập của mình!