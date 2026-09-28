---
title: "🚀 Tự động phân loại email và tổng hợp báo cáo sáng với AI cục bộ Ollama"
description: "Hướng dẫn tự động hóa phân loại email, xử lý ưu tiên và tổng hợp báo cáo sáng bằng Ollama LLM - giải pháp tiết kiệm thời gian 100% không cần code"
slug: "tu-dong-phan-loai-email-voi-ollama-llm"
tags: [n8n, automation, no-code, AI, email-processing]
keywords: [n8n workflow, tự động hóa email, Ollama LLM, phân loại email, báo cáo sáng]
---

# 🚀 Tự động phân loại email và tổng hợp báo cáo sáng với AI cục bộ Ollama

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi xử lý hàng trăm email hàng ngày. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động phân loại email thành 3 loại: **Ưu tiên cao**, **Thông thường**, **Không quan trọng**
- Tạo báo cáo sáng tổng hợp tự động với nội dung được tóm tắt bởi AI
- Xử lý email ưu tiên ngay lập tức với thông báo rõ ràng
- Tiết kiệm 2-3 giờ mỗi ngày cho công việc thủ công
- Hoạt động liên tục 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n đã cài đặt và chạy
- Ollama đã cài đặt và chạy cục bộ với model `gemma4:e4b`
- API key Ollama (nếu sử dụng phiên bản cloud)
- Tài khoản email (IMAP) để lấy email thực tế (tùy chọn)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/15913](https://n8n.io/workflows/15913)
2. Click "Import" và chọn "Import from URL"
3. Dán URL workflow vào và hoàn tất import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Ollama AI Model** (Node 4):
   - Chọn credentials `ollamaApi`
   - Đảm bảo model được đặt là `gemma4:e4b`
   - Cấu hình URL Ollama (thường là `http://localhost:11434` nếu chạy cục bộ)

2. **Simulate Email Input** (Node 2):
   - Nếu muốn sử dụng email thực tế, thay thế node này bằng node **IMAP** để lấy email từ hộp thư
   - Cấu hình credentials IMAP với thông tin đăng nhập email

3. **Parse Email Categories** (Node 5):
   - Kiểm tra và điều chỉnh logic phân loại email nếu cần
   - Đảm bảo output phù hợp với định dạng mong muốn

4. **Create Urgent Email Alert** (Node 7):
   - Cấu hình thông báo cho email ưu tiên (có thể gửi qua email, Slack, Teams...)

5. **Compile Morning Email Digest** (Node 9):
   - Điều chỉnh template báo cáo sáng theo nhu cầu
   - Thêm các thông tin cần thiết vào báo cáo

#### 3. Kích hoạt ⚡️
1. Chạy test với dữ liệu mẫu để kiểm tra workflow
2. Sau khi kiểm tra thành công, bật chế độ **Active** cho workflow
3. Đặt lịch chạy hàng ngày (nếu muốn tự động hóa hoàn toàn)

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết nối Slack/Teams**: Thêm node gửi thông báo đến Slack/Teams sau khi xử lý email ưu tiên
2. **Lưu log hoạt động**: Thêm node lưu log hoạt động vào Google Sheets hoặc cơ sở dữ liệu
3. **Tự động gửi báo cáo**: Thiết lập gửi báo cáo sáng tự động đến email hoặc Slack
4. **Mở rộng phân loại**: Thêm các tiêu chí phân loại email phức tạp hơn (ví dụ: theo dự án, theo người nhận...)

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong việc xử lý email hàng ngày. Với khả năng phân loại tự động và tổng hợp báo cáo sáng, các sếp có thể tập trung vào những công việc quan trọng nhất. Hãy thử ngay và trải nghiệm sự khác biệt của tự động hóa!