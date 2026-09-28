---
title: "📈 Tự động phân tích thị trường chứng khoán với GPT, Claude & Gemini qua Telegram"
description: "Workflow n8n tự động hóa phân tích thị trường chứng khoán bằng 3 mô hình AI lớn nhất (OpenAI, Anthropic, Google) để tạo báo cáo đầu tư chính xác và đáng tin cậy."
slug: "tu-dong-phan-tich-thi-truong-chung-khoan-voi-gpt-claude-gemini-qua-telegram"
tags: [n8n, automation, no-code, ai, trading, stock-market]
keywords: [n8n workflow, tự động hóa, phân tích thị trường, AI đầu tư, Telegram bot]
---

# 📈 Tự động phân tích thị trường chứng khoán với GPT, Claude & Gemini qua Telegram

[Đoạn mở đầu: Phân tích nỗi đau thực tế của nhà đầu tư khi phải theo dõi hàng chục nguồn thông tin mỗi ngày. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 4-8 giờ nghiên cứu thị trường mỗi ngày
- Nhận báo cáo đầu tư chính xác với 3 mô hình AI lớn nhất
- Giảm rủi ro đầu tư thông qua xác thực đa AI
- Hoạt động liên tục 24/7 mà không cần can thiệp
- Nhận cảnh báo ngay trên Telegram với các gợi ý mua/bán/hold rõ ràng
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- API key từ các dịch vụ:
  - Alpha Vantage hoặc Yahoo Finance (dữ liệu chứng khoán)
  - News API (tin tức thị trường)
  - API từ các nền tảng xã hội (Reddit, Twitter...)
  - OpenAI API key (GPT)
  - Anthropic API key (Claude)
  - Google Gemini API key
  - Telegram bot token
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [trang workflow gốc](https://n8n.io/workflows/10460)
2. Nhấn nút "Download" để tải file JSON
3. Trong n8n Editor, nhấn "Import from File" và chọn file vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Daily Stock Check** (scheduleTrigger):
   - Cấu hình thời gian chạy hàng ngày (ví dụ: 8:00 sáng)

2. **Workflow Configuration** (set):
   - Thiết lập các tham số cơ bản:
     - Danh sách mã chứng khoán theo dõi
     - Ngưỡng xác nhận từ các mô hình AI

3. **Fetch Stock Data** (httpRequest):
   - Chọn API nguồn dữ liệu (Alpha Vantage hoặc Yahoo Finance)
   - Cấu hình API key trong credentials

4. **OpenAI GPT Model** (lmChatOpenAi):
   - Thêm OpenAI API key trong credentials
   - Chọn model "gpt-4.1-mini" (hoặc model khác phù hợp)

5. **Anthropic Claude Model** (lmChatAnthropic):
   - Thêm Anthropic API key trong credentials
   - Chọn model "claude-sonnet-4-20250514"

6. **Send Telegram Alert** (telegram):
   - Tạo bot Telegram mới và lấy token
   - Thêm token vào credentials
   - Nhập chat ID của người nhận cảnh báo

#### 3. Kích hoạt ⚡️
1. Nhấn nút "Test Workflow" để chạy thử với dữ liệu mẫu
2. Kiểm tra các node quan trọng để đảm bảo dữ liệu đầu ra đúng
3. Bật chế độ "Active" để workflow chạy tự động hàng ngày

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp thêm các chỉ số kỹ thuật**: Thêm các node để tính toán RSI, MACD, MACD Histogram
2. **Phân tích tiền điện tử**: Thay đổi dữ liệu đầu vào để theo dõi thị trường tiền điện tử
3. **Theo dõi danh mục đầu tư**: Thêm node để theo dõi hiệu suất của danh mục đầu tư cụ thể
4. **Kết hợp cảnh báo qua email/Slack**: Thêm các node để gửi cảnh báo qua email hoặc Slack
5. **Phân tích theo ngành**: Cấu hình workflow để tập trung vào các ngành cụ thể như công nghệ, tài chính...

### 📌 Kết luận
Workflow này mang lại giải pháp toàn diện cho nhà đầu tư muốn tối ưu hóa quá trình nghiên cứu thị trường. Bằng cách kết hợp sức mạnh của ba mô hình AI lớn nhất cùng với xác thực đa AI, các sếp sẽ nhận được những gợi ý đầu tư chính xác và đáng tin cậy. Hãy áp dụng ngay để tiết kiệm thời gian và giảm rủi ro đầu tư!