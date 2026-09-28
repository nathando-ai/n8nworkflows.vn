---
title: "🩺 Tự động hóa báo cáo y tế bằng Ollama AI và hệ thống gửi email"
description: "Hướng dẫn tự động hóa xử lý báo cáo y tế từ PDF qua email đến báo cáo đơn giản hóa bằng Ollama AI và gửi lại qua email"
slug: "tu-dong-hoa-bao-cao-y-te-voi-ollama-ai-va-email"
tags: [n8n, automation, no-code, y-te, ai, ollama]
keywords: [n8n workflow, tự động hóa y tế, Ollama AI, xử lý PDF, báo cáo y tế]
---

# 🩺 Tự động hóa báo cáo y tế bằng Ollama AI và hệ thống gửi email

[Đoạn mở đầu: Phân tích nỗi đau thực tế của bệnh viện/phòng khám khi xử lý thủ công hàng nghìn báo cáo y tế hàng ngày. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 80% thời gian xử lý báo cáo y tế
- Giảm sai sót trong việc dịch thuật y khoa
- Tự động hóa hoàn toàn quy trình xử lý PDF
- Đảm bảo an toàn dữ liệu theo tiêu chuẩn HIPAA
- Tạo báo cáo y tế đơn giản hóa cho bệnh nhân
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản email IMAP để theo dõi báo cáo y tế đến
- Dịch vụ Ollama AI đã được cấu hình với model `llama3.2-16000:latest`
- Tài khoản SMTP để gửi báo cáo đã đơn giản hóa
- Thư viện xử lý PDF (nếu cần) trong node "Extract PDF Content"
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/7274)
2. Click vào nút "Copy JSON" để sao chép cấu hình workflow
3. Trong n8n Editor, click vào "Import from Clipboard" và dán JSON đã sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Lab Report Email Trigger"**:
   - Cấu hình credentials IMAP với thông tin tài khoản email nhận báo cáo
   - Đặt bộ lọc email để chỉ xử lý các báo cáo y tế (ví dụ: chủ đề chứa "Lab Report")

2. **Node "Medical AI Model"**:
   - Cấu hình credentials Ollama API với thông tin kết nối đến dịch vụ AI
   - Đảm bảo model `llama3.2-16000:latest` đã được tải về và sẵn sàng sử dụng

3. **Node "Extract PDF Content"**:
   - Nếu cần, thêm thư viện xử lý PDF như pdf-lib hoặc pdf-parse
   - Kiểm tra mã code để đảm bảo nó có thể trích xuất nội dung từ file PDF

4. **Node "AI Report Simplifier"**:
   - Cấu hình prompt cho AI để đảm bảo nó hiểu ngữ cảnh y khoa
   - Thêm các hướng dẫn cụ thể cho AI về cách đơn giản hóa báo cáo

5. **Node "Format Report Response"**:
   - Kiểm tra mã code định dạng để đảm bảo báo cáo đầu ra đẹp mắt và chuyên nghiệp
   - Thêm các phần như lời khuyên phòng ngừa, hướng dẫn theo dõi sau khi điều trị

6. **Node "Send Simplified Report"**:
   - Cấu hình credentials SMTP với thông tin tài khoản email gửi báo cáo
   - Đặt chủ đề email phù hợp (ví dụ: "Simplified Lab Report")

#### 3. Kích hoạt ⚡️
1. Chạy test với một báo cáo y tế mẫu để kiểm tra toàn bộ quy trình
2. Kiểm tra email để đảm bảo báo cáo đã được gửi đúng định dạng
3. Bật Active workflow để bắt đầu xử lý tự động các báo cáo y tế đến

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node Slack/Telegram để thông báo khi có báo cáo mới được xử lý
- Lưu log các báo cáo đã xử lý vào Google Sheets để theo dõi
- Tự động gửi báo cáo định kỳ cho các bệnh nhân quan tâm
- Kết hợp với hệ thống quản lý bệnh nhân để tự động cập nhật thông tin

### 📌 Kết luận
Workflow này giúp tự động hóa hoàn toàn quy trình xử lý báo cáo y tế từ nhận email đến gửi báo cáo đơn giản hóa, giúp các cơ sở y tế tiết kiệm thời gian và giảm sai sót trong quá trình dịch thuật y khoa. Hãy thử ngay để trải nghiệm sự tiện lợi và hiệu quả của tự động hóa!