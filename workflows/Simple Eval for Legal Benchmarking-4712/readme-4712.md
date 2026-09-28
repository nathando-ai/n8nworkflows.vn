---
title: "🚀 Tự động đánh giá LLM với Google Sheets & OpenRouter - Workflow n8n đơn giản"
description: "Hướng dẫn tự động hóa đánh giá hiệu suất LLM (Large Language Model) bằng workflow n8n kết hợp Google Sheets và OpenRouter. Tiết kiệm thời gian, nâng cao độ chính xác đánh giá."
slug: "tu-dong-danh-gia-llm-voi-google-sheets-openrouter"
tags: [n8n, automation, no-code, AI, LLM, Google Sheets, OpenRouter]
keywords: [n8n workflow, tự động hóa, đánh giá LLM, Google Sheets, OpenRouter, AI automation]
---

# 🚀 Tự động đánh giá LLM với Google Sheets & OpenRouter - Workflow n8n đơn giản

[Các sếp] có bao giờ phải đánh giá hiệu suất của các mô hình ngôn ngữ lớn (LLM) một cách thủ công không? Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình đánh giá, từ lấy dữ liệu đến cập nhật kết quả - mà không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa toàn bộ quy trình đánh giá LLM
- **Độ chính xác cao**: Sử dụng LLM để đánh giá LLM khác
- **Dễ theo dõi**: Kết quả được lưu trực tiếp vào Google Sheets
- **Tùy chỉnh linh hoạt**: Dễ dàng thay đổi mô hình LLM hoặc điều chỉnh prompt
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với Google Sheets API đã kích hoạt
- API Key từ OpenRouter
- File Google Sheets mẫu đã được chia sẻ: [Tests Sheet](https://docs.google.com/spreadsheets/d/10l_gMtPsge00eTTltGrgvAo54qhh3_twEDsETrQLAGU/edit?usp=sharing)
- Các file PDF cần đánh giá đã được upload lên Google Drive
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/4712](https://n8n.io/workflows/4712)
2. Click vào nút "Import" ở góc trên bên phải
3. Trong n8n Editor, chọn "Import from URL" và dán link trên
4. Hoặc copy toàn bộ JSON workflow và paste vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Get Tests"**:
   - Chọn credentials Google Sheets OAuth2
   - Điền ID của Google Sheet chứa test cases (mặc định là `10l_gMtPsge00eTTltGrgvAo54qhh3_twEDsETrQLAGU`)
   - Đảm bảo Sheet có các cột: ID, Test No., AI Platform, Relevant Source, URL, Input, Output

2. **Node "Google Drive"**:
   - Chọn credentials Google Drive OAuth2
   - Đảm bảo các file PDF cần đánh giá đã được chia sẻ với tài khoản này

3. **Node "OpenRouter Chat Model"**:
   - Chọn credentials OpenRouter API
   - Đảm bảo đã có API Key từ OpenRouter
   - Mặc định sử dụng mô hình `openai/gpt-4.1`

4. **Node "Update Results"**:
   - Chọn credentials Google Sheets OAuth2
   - Điền ID của Google Sheet để lưu kết quả
   - Đảm bảo Sheet có các cột tương ứng với dữ liệu đầu vào và kết quả đánh giá

#### 3. Kích hoạt ⚡️
1. Click vào nút "Test workflow" để chạy thử với dữ liệu mẫu
2. Kiểm tra kết quả trong Google Sheet đã chỉ định
3. Bật "Active" workflow để chạy tự động khi có dữ liệu mới

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Teams**: Thêm node gửi thông báo khi workflow hoàn thành
2. **Lưu log**: Thêm node lưu log vào Google Sheets hoặc cơ sở dữ liệu
3. **Gửi báo cáo định kỳ**: Thiết lập workflow chạy hàng ngày và gửi báo cáo qua email
4. **Tối ưu hóa mô hình**: Thử nghiệm với các mô hình khác từ OpenRouter để tìm ra mô hình phù hợp nhất

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quá trình đánh giá hiệu suất LLM, từ lấy dữ liệu đến cập nhật kết quả - mà không cần viết code. Với khả năng tùy chỉnh linh hoạt và tích hợp dễ dàng với các công cụ khác, workflow này sẽ là công cụ hữu ích cho bất kỳ ai làm việc với AI và tự động hóa. Hãy thử ngay và tiết kiệm thời gian quý giá của các sếp!