---
title: "🎥 Tự động hóa tạo video từ ý tưởng trên Google Sheets với GPT-4o và Fal.AI Veo 3"
description: "Hướng dẫn tự động hóa tạo video từ ý tưởng trên Google Sheets với GPT-4o và Fal.AI Veo 3, tiết kiệm thời gian và nâng cao hiệu quả marketing"
slug: "tu-dong-hoa-tao-video-tu-google-sheets-voi-gpt-4o-va-fal-ai-veo-3"
tags: [n8n, automation, no-code, ai, marketing]
keywords: [n8n workflow, tự động hóa, tạo video, google sheets, fal.ai, gpt-4o]
---

# 🎥 Tự động hóa tạo video từ ý tưởng trên Google Sheets với GPT-4o và Fal.AI Veo 3

[Các sếp] có biết rằng việc tạo nội dung video chất lượng thường tốn nhiều thời gian và công sức? Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình từ ý tưởng đến video hoàn chỉnh chỉ với một dòng trong Google Sheets.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tạo video chỉ với một dòng trong Google Sheets
- **Chính xác cao**: Sử dụng GPT-4o để tạo prompt chuyên nghiệp
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công trong quá trình tạo video
- **Theo dõi dễ dàng**: Kết quả được cập nhật trực tiếp trong Google Sheets
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với Google Sheets API đã kích hoạt
- API Key từ OpenAI
- Tài khoản Fal.AI với số dư đủ để tạo video
- File Google Sheets mẫu đã được chia sẻ (có thể tải từ [đây](https://n8n.io/workflows/4881))
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/4881)
2. Chọn "Download" để tải file JSON
3. Trong n8n Editor, nhấn vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Google Sheets Trigger**:
   - Cấu hình credentials "googleSheetsTriggerOAuth2Api"
   - Đảm bảo file Google Sheets mẫu đã được chia sẻ với tài khoản này

2. **OpenAI**:
   - Cấu hình credentials "openAiApi"
   - Điền API Key từ OpenAI vào credentials này

3. **Fal.AI**:
   - Cập nhật API Key trong các node HTTP Request:
     - "Submit Request to generate video"
     - "Check video status"
     - "Get video url"
   - Thay thế phần `Key <YOUR_API_KEY>` trong header Authorization bằng API Key thật của bạn

4. **Google Sheets Update**:
   - Cấu hình credentials "googleSheetsOAuth2Api"
   - Đảm bảo tài khoản này có quyền chỉnh sửa file Google Sheets mẫu

#### 3. Kích hoạt ⚡️
1. Thêm một dòng mới vào Google Sheets mẫu với định dạng:
   - Cột A: Ý tưởng video
   - Cột B: Tỉ lệ video (ví dụ: "16:9")
   - Cột C: Có âm thanh hay không (true/false)
2. Lưu lại dòng này
3. Workflow sẽ tự động kích hoạt và bắt đầu quá trình tạo video
4. Theo dõi tiến trình trong Google Sheets - khi video sẵn sàng, URL sẽ được cập nhật tự động

### ✍️ Mẹo & gợi ý nâng cao
- **Tạo nhiều video cùng lúc**: Thêm nhiều dòng vào Google Sheets để tạo nhiều video đồng thời
- **Tích hợp với Slack/Teams**: Kết nối với các công cụ chat để thông báo khi video sẵn sàng
- **Lưu trữ video**: Tự động lưu video vào Google Drive hoặc hệ thống lưu trữ khác
- **Tối ưu chi phí**: Sử dụng video 8 giây (mặc định) thay vì dài hơn để tiết kiệm chi phí

### 📌 Kết luận
Với workflow này, các sếp có thể tự động hóa hoàn toàn quy trình tạo video từ ý tưởng, tiết kiệm thời gian và nâng cao hiệu quả marketing. Hãy thử ngay và trải nghiệm cách làm việc thông minh hơn với n8n!