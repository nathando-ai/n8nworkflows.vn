---
title: "📊 Tự động hóa truy vấn SQL với OpenAI và Quickchart.io - Workflow n8n hoàn chỉnh"
description: "Hướng dẫn chi tiết cách tự động hóa truy vấn SQL, tạo biểu đồ từ dữ liệu và tích hợp với OpenAI trong n8n. Giải pháp toàn diện cho phân tích dữ liệu không cần code."
slug: "tu-dong-hoa-truy-van-sql-voi-openai-quickchart-n8n"
tags: [n8n, automation, no-code, AI, data visualization, SQL]
keywords: [n8n workflow, tự động hóa dữ liệu, AI phân tích, SQL Agent, Quickchart.io, OpenAI]
---

# 📊 Tự động hóa truy vấn SQL với OpenAI và Quickchart.io - Workflow n8n hoàn chỉnh

[Các sếp đang gặp khó khăn khi phải phân tích dữ liệu SQL thủ công và tạo biểu đồ để trình bày kết quả? Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình từ truy vấn đến tạo biểu đồ chỉ với vài bước cấu hình đơn giản trong n8n.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công khi truy vấn và tạo biểu đồ.
- **Tiết kiệm thời gian**: Giảm thời gian phân tích dữ liệu từ vài giờ xuống còn vài phút.
- **Chính xác cao**: Sử dụng AI của OpenAI để đảm bảo dữ liệu và biểu đồ được tạo chính xác.
- **Tích hợp dễ dàng**: Kết nối liền mạch với các công cụ phân tích dữ liệu khác.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản OpenAI với API key (để sử dụng mô hình GPT-4o).
- Tài khoản cơ sở dữ liệu (PostgreSQL, MySQL hoặc SQLite).
- Dữ liệu mẫu (có thể sử dụng [bộ dữ liệu này từ Kaggle](https://www.kaggle.com/datasets/ihelon/coffee-sales/versions/15?resource=download)).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [trang workflow gốc](https://n8n.io/workflows/2559).
2. Click vào nút "Copy JSON" để sao chép cấu hình workflow.
3. Trong n8n Editor, click vào "Import from Clipboard" và dán JSON đã sao chép.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "OpenAI Chat Model" và "OpenAI Chat Model Classifier"**:
   - Chọn credentials "openAiApi".
   - Đảm bảo đã cấu hình đúng API key trong credentials này.

2. **Node "AI Agent"**:
   - Cấu hình credentials cho cơ sở dữ liệu (PostgreSQL, MySQL hoặc SQLite).
   - Điều chỉnh `Prefix Prompt` nếu cần (ví dụ: để truy vấn cơ sở dữ liệu Supabase).

3. **Node "OpenAI - Generate Chart definition with Structured Output"**:
   - Đảm bảo đã cấu hình đúng API key trong credentials "openAiApi".
   - Kiểm tra định dạng JSON đầu ra của OpenAI để đảm bảo tương thích với Quickchart.io.

4. **Node "Execute Workflow"**:
   - Đảm bảo workflow con "Generate a chart" đã được cấu hình đúng.

#### 3. Kích hoạt ⚡️
1. Test run với dữ liệu mẫu để kiểm tra kết quả.
2. Bật Active workflow để bắt đầu sử dụng.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Thêm node để gửi kết quả phân tích dữ liệu trực tiếp đến các kênh chat.
- **Lưu log truy vấn**: Thêm node để lưu lịch sử truy vấn và kết quả để theo dõi.
- **Tự động hóa báo cáo**: Kết hợp với các công cụ tạo báo cáo để gửi báo cáo định kỳ.
- **Tối ưu hóa biểu đồ**: Thử nghiệm với các loại biểu đồ khác nhau để tìm ra cách trình bày dữ liệu hiệu quả nhất.

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc tự động hóa truy vấn SQL và tạo biểu đồ từ dữ liệu. Với sự kết hợp của OpenAI và Quickchart.io, các sếp có thể tiết kiệm thời gian và công sức trong việc phân tích dữ liệu. Hãy thử ngay và trải nghiệm sự tiện lợi mà workflow này mang lại!