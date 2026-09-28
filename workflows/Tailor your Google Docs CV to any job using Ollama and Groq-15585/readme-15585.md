---
title: "🚀 Tự động hóa CV với Ollama & Groq: Tối ưu hồ sơ ứng tuyển chỉ trong 5 phút"
description: "Hướng dẫn tự động hóa tối ưu CV theo công việc mong muốn bằng n8n, Ollama và Groq. Tiết kiệm 80% thời gian chỉnh sửa thủ công với AI."
slug: "tu-dong-hoa-cv-voi-ollama-groq"
tags: [n8n, automation, no-code, AI, Google Docs]
keywords: [n8n workflow, tự động hóa CV, tối ưu hồ sơ, Ollama, Groq]
---

# 🚀 Tự động hóa CV với Ollama & Groq: Tối ưu hồ sơ ứng tuyển chỉ trong 5 phút

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 80% thời gian chỉnh sửa CV thủ công
- Tối ưu hồ sơ theo từng vị trí tuyển dụng
- Tự động trích xuất và áp dụng từ khóa quan trọng
- Tạo bản sao CV gốc để bảo toàn thông tin gốc
- Nhận báo cáo chi tiết các thay đổi được thực hiện
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Cloud với API Drive và Docs đã kích hoạt
- API Key từ Groq (https://console.groq.com/home)
- Docker để chạy Ollama local (cài đặt và chạy lệnh: `docker run -d --name ollama -p 11434:11434 -v ollama_data:/root/.ollama --restart unless-stopped ollama/ollama`)
- Pull model Llama 3.1:8b (`docker exec ollama ollama pull llama3.1:8b`)
- CV gốc dưới dạng Google Docs (không phải .docx)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/15585)
2. Click "Download" để tải file JSON
3. Trong n8n Editor, chọn "Import from File" và chọn file JSON vừa tải

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node "CV Input Form"**: Đảm bảo đường dẫn (`path`) duy nhất trong hệ thống của bạn
- **Node "Read CV from Google Docs"**: Cấu hình credentials Google Docs OAuth2
- **Node "Scrape Job Page"**: Có thể cần cấu hình headers tùy theo trang tuyển dụng
- **Node "Ollama Chat Model"**: Đảm bảo Ollama đang chạy local và model đã được pull
- **Node "Groq Chat Model"**: Cấu hình credentials Groq API
- **Node "Copy Original CV"**: Cấu hình credentials Google Drive OAuth2
- **Node "Apply Replacements to Copy"**: Đảm bảo Google Docs API đã được kích hoạt

#### 3. Kích hoạt ⚡️
1. Test run với dữ liệu mẫu:
   - Link Google Docs CV của bạn
   - Link công việc hoặc mô tả công việc
2. Kiểm tra kết quả:
   - Bản sao CV đã được tối ưu
   - Báo cáo thay đổi chi tiết
3. Bật Active workflow sau khi xác nhận hoạt động ổn định

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Teams để thông báo khi CV đã sẵn sàng
- Lưu log các phiên tối ưu CV để theo dõi tiến trình
- Tạo báo cáo định kỳ về hiệu suất tối ưu CV
- Kết hợp với workflow khác để tự động gửi CV đã tối ưu đến nhà tuyển dụng

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian quý giá trong việc tối ưu CV theo từng vị trí tuyển dụng. Bằng cách kết hợp Ollama và Groq, chúng ta có thể tự động hóa toàn bộ quá trình từ trích xuất thông tin đến áp dụng thay đổi, mang lại hồ sơ ứng tuyển chuyên nghiệp và phù hợp hơn. Hãy thử ngay và nâng cao cơ hội tuyển dụng của mình!