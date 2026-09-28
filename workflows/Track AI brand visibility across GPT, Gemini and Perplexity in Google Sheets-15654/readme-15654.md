---
title: "🚀 Theo dõi sự hiện diện thương hiệu AI trên GPT, Gemini và Perplexity trong Google Sheets"
description: "Hướng dẫn tự động hóa theo dõi và phân tích sự hiện diện thương hiệu AI trên các nền tảng GPT, Gemini và Perplexity bằng n8n, lưu kết quả vào Google Sheets"
slug: "theo-doi-su-hien-dien-thuong-hieu-ai-tren-gpt-gemini-perplexity"
tags: [n8n, automation, no-code, ai, google-sheets]
keywords: [n8n workflow, tự động hóa, phân tích AI, thương hiệu, Google Sheets]
---

# 🚀 Theo dõi sự hiện diện thương hiệu AI trên GPT, Gemini và Perplexity trong Google Sheets

[Các sếp đang gặp khó khăn khi phải theo dõi sự hiện diện thương hiệu AI trên nhiều nền tảng khác nhau một cách thủ công. Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình theo dõi và phân tích trên GPT, Gemini và Perplexity, lưu kết quả vào Google Sheets một cách liền mạch.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đáng kể trong việc theo dõi thủ công
- Nhận được dữ liệu thống nhất từ 3 nền tảng AI hàng đầu
- Phân tích tự động và lưu trữ kết quả trong Google Sheets
- Theo dõi sự thay đổi của thương hiệu AI theo thời gian
- Tự động hóa toàn bộ quy trình phân tích AI
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Cloud với quyền truy cập Google Sheets API
- API Key cho OpenAI, Google Gemini và Perplexity
- Google Sheet mẫu đã được chuẩn bị (có thể sử dụng [Google Sheet mẫu](https://docs.google.com/spreadsheets/d/1q9-LcZ_BNQ7PTEKuJ6T4j3HffYn23Co_mO5R-c8C0XY/edit))
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/15654](https://n8n.io/workflows/15654)
2. Nhấn nút "Import" để tải workflow về máy
3. Trong n8n Editor, nhấn vào "Import from File" và chọn file JSON đã tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Manual Trigger Execute Workflow**:
   - Không cần cấu hình gì, chỉ cần kích hoạt khi cần chạy workflow

2. **Read Prompts from Sheets**:
   - Cấu hình credentials: `googleSheetsOAuth2Api`
   - Thiết lập tham số:
     - Spreadsheet ID: ID của Google Sheet chứa prompts
     - Range: Phạm vi dữ liệu chứa prompts (ví dụ: "Sheet1!A1:B100")

3. **Read Criteria from Sheets**:
   - Cấu hình credentials: `googleSheetsOAuth2Api`
   - Thiết lập tham số:
     - Spreadsheet ID: ID của Google Sheet chứa criteria
     - Range: Phạm vi dữ liệu chứa criteria (ví dụ: "Sheet2!A1:B10")

4. **OpenAI GPT Model Request**:
   - Cấu hình credentials: `openAiApi`
   - Thiết lập tham số:
     - Model: Chọn model phù hợp (ví dụ: gpt-3.5-turbo)

5. **Google Gemini Model Request**:
   - Cấu hình credentials: `googlePalmApi`
   - Thiết lập tham số:
     - Model: Chọn model phù hợp (ví dụ: gemini-pro)

6. **Post to Perplexity API**:
   - Cấu hình endpoint: `https://api.perplexity.ai/chat/completions`
   - Thiết lập headers:
     - Authorization: `Bearer <API_KEY>`
     - Content-Type: `application/json`

7. **Write Gemini Results to Sheets**:
   - Cấu hình credentials: `googleSheetsOAuth2Api`
   - Thiết lập tham số:
     - Spreadsheet ID: ID của Google Sheet lưu kết quả
     - Range: Phạm vi để ghi kết quả (ví dụ: "Results!A1")

8. **Write GPT Results to Sheets**:
   - Cấu hình credentials: `googleSheetsOAuth2Api`
   - Thiết lập tham số:
     - Spreadsheet ID: ID của Google Sheet lưu kết quả
     - Range: Phạm vi để ghi kết quả (ví dụ: "Results!B1")

9. **Write Perplexity Results to Sheets**:
   - Cấu hình credentials: `googleSheetsOAuth2Api`
   - Thiết lập tham số:
     - Spreadsheet ID: ID của Google Sheet lưu kết quả
     - Range: Phạm vi để ghi kết quả (ví dụ: "Results!C1")

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node, nhấn vào nút "Execute Workflow" để test chạy dữ liệu mẫu
2. Kiểm tra kết quả trong Google Sheets đã cấu hình
3. Nếu mọi thứ hoạt động tốt, nhấn vào nút "Activate" để kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
1. **Lập lịch tự động chạy**: Cấu hình workflow chạy định kỳ hàng ngày hoặc hàng tuần để theo dõi sự thay đổi của thương hiệu AI
2. **Thêm cảnh báo**: Kết nối với Slack hoặc Email để nhận thông báo khi phát hiện sự thay đổi đáng kể
3. **Phân tích sâu hơn**: Sử dụng các node phân tích dữ liệu khác để tạo báo cáo chi tiết hơn
4. **Kết hợp với các công cụ khác**: Kết nối với các công cụ khác như Zapier hoặc Make để mở rộng khả năng tự động hóa

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quá trình theo dõi và phân tích sự hiện diện thương hiệu AI trên các nền tảng GPT, Gemini và Perplexity. Kết quả được lưu trữ trong Google Sheets, giúp việc theo dõi và báo cáo trở nên dễ dàng hơn bao giờ hết. Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao hiệu quả kinh doanh!