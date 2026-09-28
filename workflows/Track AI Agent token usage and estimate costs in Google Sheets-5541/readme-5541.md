---
title: "💰 Theo dõi sử dụng token AI và ước tính chi phí trong Google Sheets"
description: "Hướng dẫn tự động hóa theo dõi token sử dụng của các mô hình AI (OpenAI, Anthropic, Gemini) và ước tính chi phí trong Google Sheets bằng n8n"
slug: "theo-doi-token-ai-va-uoc-tinh-chi-phi-trong-google-sheets"
tags: [n8n, automation, no-code, ai, google-sheets]
keywords: [n8n workflow, tự động hóa, theo dõi token AI, ước tính chi phí, Google Sheets]
---

# 💰 Theo dõi sử dụng token AI và ước tính chi phí trong Google Sheets

[Các sếp đang gặp khó khăn khi quản lý chi phí sử dụng các mô hình AI như OpenAI, Anthropic và Google Gemini. Với workflow này, các sếp có thể tự động theo dõi lượng token sử dụng và ước tính chi phí thực tế trong Google Sheets một cách dễ dàng.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Theo dõi lượng token sử dụng của các mô hình AI (OpenAI, Anthropic, Gemini)
- Tự động cập nhật dữ liệu vào Google Sheets
- Ước tính chi phí thực tế dựa trên lượng token sử dụng
- Quản lý chi phí AI một cách hiệu quả và minh bạch
- Tích hợp dễ dàng với các hệ thống khác thông qua Google Sheets
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản API của các nhà cung cấp AI (OpenAI, Anthropic, Google Gemini)
- Tài khoản Google Drive và Google Sheets
- API key của instance n8n
- Tạo bản sao của [Google Sheets Template](https://docs.google.com/spreadsheets/d/1c9CeePI6ebNnIKogyJKHUpDWT6UEowpH9OwVtViadyE/edit?usp=sharing)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/5541](https://n8n.io/workflows/5541)
2. Nhấn nút "Copy to clipboard" để sao chép JSON workflow
3. Trong n8n Editor, nhấn vào "Import from Clipboard" và dán JSON đã sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "When clicking ‘Test workflow’"**:
   - Không cần cấu hình gì thêm

2. **Node "AI Agent"**:
   - Thay thế bằng agent của bạn (nếu cần)
   - Đảm bảo agent của bạn đã được cấu hình đúng

3. **Node "Call sub-workflow"**:
   - Đảm bảo sub-workflow đã được cấu hình đúng
   - Thay đổi `{{ $workflow.id }}` nếu sub-workflow của bạn ở trong file khác

4. **Node "Think"**:
   - Không cần cấu hình gì thêm

5. **Node "Extract token usage data"**:
   - Cấu hình các trường dữ liệu cần trích xuất từ token usage
   - Điều chỉnh nếu bạn sử dụng nhà cung cấp AI khác ngoài OpenAI, Anthropic, Google Gemini

6. **Node "Get execution data"**:
   - Cấu hình credentials "n8nApi" với API key của instance n8n
   - Đảm bảo API key có quyền truy cập đầy đủ

7. **Node "When Executed by Another Workflow"**:
   - Không cần cấu hình gì thêm

8. **Node "Split Out"**:
   - Không cần cấu hình gì thêm

9. **Node "Sum Token Totals - aggregate by model"**:
   - Không cần cấu hình gì thêm

10. **Node "Record token usage"**:
    - Cấu hình credentials "googleSheetsOAuth2Api"
    - Chọn Spreadsheet ID từ Google Sheets Template đã tạo
    - Đặt tên Sheet là "Executions"
    - Đảm bảo các cột dữ liệu khớp với template

11. **Node "Gemini"**:
    - Cấu hình credentials "googlePalmApi"
    - Đảm bảo API key có quyền truy cập đầy đủ

12. **Node "OpenAI"**:
    - Cấu hình credentials "openAiApi"
    - Chọn model phù hợp (mặc định là "gpt-4o-mini")
    - Đảm bảo API key có quyền truy cập đầy đủ

13. **Node "Anthropic"**:
    - Cấu hình credentials "anthropicApi"
    - Chọn model phù hợp (mặc định là "claude-3-haiku-20240307")
    - Đảm bảo API key có quyền truy cập đầy đủ

#### 3. Kích hoạt ⚡️
1. Nhấn nút "Test workflow" để kiểm tra dữ liệu mẫu
2. Sau khi kiểm tra thành công, nhấn "Activate workflow" để kích hoạt

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp với Slack/Telegram**: Thêm node gửi thông báo khi chi phí vượt ngưỡng
2. **Lưu log chi tiết**: Thêm node lưu log chi tiết vào Google Sheets
3. **Gửi báo cáo định kỳ**: Tạo workflow con để gửi báo cáo chi phí hàng tuần
4. **Cảnh báo khi token sắp hết**: Thiết lập cảnh báo khi token sắp hết hạn

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa việc theo dõi và quản lý chi phí sử dụng AI một cách hiệu quả. Bằng cách tích hợp với Google Sheets, các sếp có thể dễ dàng quản lý và phân tích dữ liệu chi phí AI. Hãy áp dụng ngay để tiết kiệm thời gian và giảm thiểu rủi ro về chi phí không cần thiết.