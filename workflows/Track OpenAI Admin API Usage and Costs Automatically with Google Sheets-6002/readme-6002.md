```yaml
---
title: "💰 Theo dõi chi tiết chi phí sử dụng OpenAI Admin API tự động với Google Sheets"
description: "Hướng dẫn tự động hóa việc theo dõi và ghi lại chi phí sử dụng OpenAI Admin API vào Google Sheets hàng ngày, tiết kiệm thời gian và tối ưu hóa ngân sách AI"
slug: "theo-doi-chi-phi-openai-admin-api-voi-google-sheets"
tags: [n8n, automation, no-code, openai, google-sheets]
keywords: [n8n workflow, tự động hóa, openai admin api, theo dõi chi phí, google sheets]
---
```

# 💰 Theo dõi chi tiết chi phí sử dụng OpenAI Admin API tự động với Google Sheets

[Các sếp đang gặp khó khăn khi phải theo dõi chi phí sử dụng OpenAI Admin API thủ công hàng ngày. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình theo dõi và ghi lại dữ liệu vào Google Sheets một cách chính xác và liên tục.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa hoàn toàn quy trình theo dõi chi phí OpenAI Admin API
- Dữ liệu được cập nhật tự động vào Google Sheets hàng ngày
- Tiết kiệm thời gian đáng kể so với phương pháp thủ công
- Dễ dàng theo dõi và phân tích chi phí sử dụng OpenAI
- Hoạt động liên tục 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản OpenAI Admin API với quyền truy cập đầy đủ
- Tài khoản Google Cloud với quyền truy cập Google Sheets API
- API Key và Project ID từ OpenAI Admin
- Google Sheets đã được tạo sẵn để lưu trữ dữ liệu
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào "Import from URL" và dán link workflow: https://n8n.io/workflows/6002
3. Hoặc tải file JSON về và chọn "Import from File"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Schedule Trigger"**:
   - Cấu hình lịch chạy (ví dụ: hàng ngày lúc 9:00 sáng)
   - Chọn múi giờ phù hợp với doanh nghiệp

2. **Node "OpenAI Admin - get token usage" và "OpenAI Admin - Get cost"**:
   - Cấu hình credentials với API Key của OpenAI Admin
   - Đảm bảo API Key có đủ quyền truy cập

3. **Node "Set api_key and project ids"**:
   - Thêm danh sách API Key và Project ID cần theo dõi
   - Định dạng dữ liệu phải là JSON array

4. **Node "Append Usage to GSheets" và "Append Cost to GSheets"**:
   - Cấu hình Google Sheets credentials
   - Chỉ định chính xác Spreadsheet ID và tên Sheet
   - Đảm bảo tài khoản Google có quyền chỉnh sửa sheet này

5. **Node "Set Usage data for Gsheets" và "Set Cost data for Gsheets"**:
   - Kiểm tra và điều chỉnh các trường dữ liệu nếu cần
   - Đảm bảo tên cột trong Google Sheets khớp với dữ liệu đầu ra

#### 3. Kích hoạt ⚡️
1. Chạy test với dữ liệu mẫu để kiểm tra kết quả
2. Sau khi xác nhận kết quả chính xác, bật chế độ Active workflow
3. Kiểm tra Google Sheets sau khi workflow chạy lần đầu để đảm bảo dữ liệu được ghi đúng

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Teams**: Thêm node gửi thông báo khi chi phí vượt ngưỡng
2. **Lưu log chi tiết**: Thêm node lưu log chi tiết vào Google Sheets khác
3. **Báo cáo định kỳ**: Tạo workflow phụ để tổng hợp dữ liệu hàng tháng
4. **Cảnh báo ngân sách**: Thiết lập cảnh báo khi chi phí sắp vượt ngân sách

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn việc theo dõi chi phí sử dụng OpenAI Admin API, tiết kiệm thời gian đáng kể và đảm bảo dữ liệu luôn được cập nhật chính xác. Hãy áp dụng ngay để tối ưu hóa ngân sách AI của doanh nghiệp!