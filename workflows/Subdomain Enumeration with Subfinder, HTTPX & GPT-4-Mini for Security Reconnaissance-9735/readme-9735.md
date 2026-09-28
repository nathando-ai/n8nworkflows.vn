---
title: "🚀 Tự động hóa Thăm dò Thông tin Bảo mật với Subfinder, HTTPX & GPT-4-Mini"
description: "Hướng dẫn chi tiết cách tự động hóa quá trình tìm kiếm subdomain và phân tích bảo mật bằng công cụ Subfinder, HTTPX và trí tuệ nhân tạo GPT-4-Mini trong n8n"
slug: "tu-dong-hoa-tham-do-thong-tin-bao-mat-voi-subfinder-httpx-gpt4-mini"
tags: [n8n, automation, no-code, security, bug bounty, passive reconnaissance]
keywords: [n8n workflow, tự động hóa bảo mật, tìm kiếm subdomain, GPT-4-Mini, HTTPX, Subfinder]
---

# 🚀 Tự động hóa Thăm dò Thông tin Bảo mật với Subfinder, HTTPX & GPT-4-Mini

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các chuyên gia bảo mật khi phải thực hiện thủ công quá trình tìm kiếm subdomain và phân tích bảo mật. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian lên tới 90% so với phương pháp thủ công
- Tăng độ phủ của quá trình thăm dò lên tới 20,000 subdomain
- Phát hiện các điểm yếu bảo mật tiềm ẩn mà các công cụ truyền thống bỏ qua
- Tự động hóa toàn bộ quá trình từ tìm kiếm đến phân tích kết quả
- Tích hợp trí tuệ nhân tạo để tối ưu hóa kết quả tìm kiếm
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản OpenAI với API key (để sử dụng GPT-4-Mini)
- Máy chủ Linux (VPS) với các công cụ đã cài đặt: Subfinder, Assetfinder, HTTPX
- Tài khoản SSH với quyền root (hoặc tài khoản có đủ quyền thực thi các công cụ trên)
- File chứa danh sách domain cần kiểm tra (định dạng .txt)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào [n8n.io/workflows/9735](https://n8n.io/workflows/9735)
2. Nhấn nút "Import" để tải workflow về máy
3. Hoặc copy nội dung JSON của workflow và paste vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Webhook Node**:
   - Đảm bảo đường dẫn webhook là duy nhất (đã được tạo sẵn trong workflow)
   - Ví dụ: `e0a62a2b-6669-4f09-bd16-e548ae1386cb`

2. **SSH Nodes** (SSH Subfinder, SSH Assetfinder, SSH HTTPX, v.v.):
   - Cấu hình credentials SSH với thông tin máy chủ của bạn
   - Đảm bảo máy chủ có các công cụ đã được cài đặt: Subfinder, Assetfinder, HTTPX
   - Đường dẫn thư mục lưu trữ kết quả: `/tmp/reconAI`

3. **OpenAI Node** (Subdomain Generator AI):
   - Cấu hình credentials OpenAI với API key của bạn
   - Đảm bảo tài khoản OpenAI có đủ credit để sử dụng GPT-4-Mini

4. **HTTP Request Nodes** (WayBack Machine, crt.sh):
   - Không cần cấu hình đặc biệt, các node này đã được cấu hình sẵn

5. **Code Nodes** (Filter Subdomains, Subdomain Format Validation, v.v.):
   - Các node này chứa logic xử lý dữ liệu, không cần thay đổi trừ khi bạn muốn tùy chỉnh logic

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu:
   - Tạo file .txt chứa danh sách domain cần kiểm tra
   - Sử dụng curl hoặc Python script để gửi file đến webhook
   - Ví dụ với curl:
     ```bash
     curl -X POST -F "file=@/path/to/your/domains.txt" http://your-n8n-server:5678/webhook-test/e0a62a2b-6669-4f09-bd16-e548ae1386cb
     ```

2. Bật Active workflow sau khi đã kiểm tra và cấu hình đầy đủ

### ✍️ Mẹo & gợi ý nâng cao
- **Tối ưu hóa chi phí**: Theo dõi số lượng token sử dụng và điều chỉnh số lượng subdomain được xử lý mỗi lần chạy để tiết kiệm chi phí
- **Kết hợp với Slack/Telegram**: Thêm node để gửi kết quả qua Slack hoặc Telegram sau khi hoàn thành quá trình
- **Lưu log**: Thêm node để lưu log các kết quả quan trọng vào Google Sheets hoặc cơ sở dữ liệu
- **Tự động hóa báo cáo**: Tạo báo cáo định kỳ từ kết quả thu thập được

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho quá trình thăm dò thông tin bảo mật, kết hợp sức mạnh của các công cụ truyền thống với trí tuệ nhân tạo. Bằng cách tự động hóa toàn bộ quá trình, các chuyên gia bảo mật có thể tiết kiệm thời gian và tăng độ phủ của quá trình kiểm tra, từ đó phát hiện các điểm yếu bảo mật tiềm ẩn một cách hiệu quả hơn. Hãy áp dụng ngay để nâng cao khả năng phát hiện lỗ hổng trong các chương trình bug bounty của bạn!