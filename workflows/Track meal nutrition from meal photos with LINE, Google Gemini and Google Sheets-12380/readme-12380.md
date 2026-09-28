---
title: "🍽️ Tự động theo dõi dinh dưỡng từ ảnh món ăn bằng LINE, Google Gemini và Google Sheets"
description: "Hướng dẫn chi tiết cách tự động phân tích dinh dưỡng từ ảnh món ăn gửi qua LINE, lưu kết quả vào Google Sheets và Google Drive với công nghệ AI của Google Gemini"
slug: "tu-dong-theo-doi-dinh-duong-tu-anh-mon-an"
tags: [n8n, automation, no-code, LINE, Google Gemini, Google Sheets, Google Drive]
keywords: [n8n workflow, tự động hóa, theo dõi dinh dưỡng, AI phân tích ảnh, Google Gemini, LINE bot]
---

# 🍽️ Tự động theo dõi dinh dưỡng từ ảnh món ăn bằng LINE, Google Gemini và Google Sheets

[Các sếp] có biết không? Theo dõi dinh dưỡng hàng ngày là một trong những thói quen quan trọng nhất để duy trì sức khỏe. Tuy nhiên, việc ghi chép thông tin dinh dưỡng từ ảnh món ăn truyền thống lại tốn thời gian và dễ gây lỗi. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình này chỉ trong vài bước đơn giản!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động phân tích ảnh món ăn trong vài giây thay vì phải ghi chép thủ công.
- **Chính xác cao**: Sử dụng công nghệ AI của Google Gemini để phân tích chính xác dinh dưỡng.
- **Lưu trữ an toàn**: Tự động lưu ảnh và dữ liệu vào Google Drive và Google Sheets.
- **Cá nhân hóa**: Nhận lời khuyên dinh dưỡng cá nhân hóa dựa trên dữ liệu phân tích.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản LINE Messaging API (Channel Access Token)
- Google Sheets với các cột: Ngày, Giờ, Loại bữa ăn, Món ăn, Calo, Protein, Carbs, Fat, Fiber, Điểm sức khỏe, Lời khuyên
- Thư mục Google Drive để lưu ảnh món ăn
- API Key của Google Gemini
- Credentials cho Google Sheets và Google Drive
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/12380)
2. Click vào nút "Import" và chọn "Import from URL"
3. Dán link workflow vào ô nhập liệu và nhấn "Import"

Hoặc có thể copy/paste JSON sau vào n8n Editor:

```json
{
  "nodes": [
    {
      "parameters": {
        "path": "/MealTracker",
        "httpMethod": "POST"
      },
      "name": "LINE Webhook",
      "type": "n8n-nodes-base.webhook",
      "typeVersion": 1,
      "position": [
        250,
        300
      ]
    },
    // ... (các node khác từ workflow gốc)
  ],
  "connections": [
    // ... (các kết nối giữa nodes)
  ],
  "settings": {
    "saveDataErrorExecution": "all",
    "saveDataSuccessExecution": "all",
    "saveManualExecutions": true,
    "executionTimeout": 3600,
    "timezone": ""
  },
  "name": "Track meal nutrition from meal photos with LINE, Google Gemini and Google Sheets"
}
```

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **LINE Webhook**:
   - Đảm bảo đã tạo LINE Messaging API channel và có Channel Access Token
   - Cấu hình webhook URL trong LINE Developer Console trỏ đến địa chỉ của bạn (ví dụ: `https://your-n8n-domain.com/webhook/MealTracker`)

2. **Config**:
   - Thêm các credentials cần thiết:
     - `googlePalmApi` cho Google Gemini
     - `googleDriveOAuth2Api` cho Google Drive
     - `googleSheetsOAuth2Api` cho Google Sheets
   - Cấu hình các tham số:
     - `lineChannelAccessToken`: Token truy cập của LINE
     - `googleDriveFolderId`: ID thư mục Google Drive để lưu ảnh
     - `googleSheetId`: ID của Google Sheet để lưu dữ liệu
     - `googleSheetName`: Tên sheet trong Google Sheet

3. **Google Gemini Chat Model**:
   - Đảm bảo đã kích hoạt Google Gemini API và có API Key
   - Cấu hình các tham số:
     - `model`: Chọn model phù hợp (ví dụ: `gemini-pro-vision`)
     - `temperature`: Đặt giá trị từ 0.0 đến 1.0 để điều chỉnh tính sáng tạo của kết quả

4. **Analyze Meal with AI**:
   - Cấu hình prompt để phân tích ảnh món ăn. Ví dụ:
     ```
     Analyze this food image and provide the following information in JSON format:
     {
       "foodItems": ["item1", "item2"],
       "nutrition": {
         "calories": value,
         "protein": value,
         "carbs": value,
         "fat": value,
         "fiber": value
       },
       "healthScore": value,
       "advice": "personalized advice"
     }
     ```

5. **Save to Google Sheets**:
   - Đảm bảo Google Sheet đã có các cột cần thiết
   - Cấu hình các tham số:
     - `spreadsheetId`: ID của Google Sheet
     - `range`: Phạm vi dữ liệu (ví dụ: `Sheet1!A:K`)

#### 3. Kích hoạt ⚡️
1. Test run workflow với dữ liệu mẫu để đảm bảo mọi thứ hoạt động đúng
2. Bật Active workflow để bắt đầu theo dõi dinh dưỡng hàng ngày

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Telegram**: Thay thế LINE bằng các nền tảng khác bằng cách thay đổi node webhook và node gửi phản hồi.
2. **Lưu log hoạt động**: Thêm node để lưu log các hoạt động vào Google Sheets hoặc cơ sở dữ liệu.
3. **Gửi báo cáo định kỳ**: Tạo một workflow phụ để gửi báo cáo dinh dưỡng hàng tuần hoặc hàng tháng.
4. **Tích hợp với các ứng dụng khác**: Kết nối với các ứng dụng khác như MyFitnessPal, Strava để có dữ liệu toàn diện hơn.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quá trình theo dõi dinh dưỡng từ ảnh món ăn chỉ trong vài bước đơn giản. Với công nghệ AI tiên tiến của Google Gemini, các sếp có thể nhận được thông tin dinh dưỡng chính xác và lời khuyên cá nhân hóa. Hãy thử ngay và nâng cao sức khỏe của mình với công nghệ tự động hóa!