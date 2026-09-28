---
title: "📈 Theo dõi sự chuyển động của các ngành trong thị trường chứng khoán với Google Sheets, Yahoo Finance, Groq và Gmail"
description: "Tự động hóa phân tích thị trường chứng khoán với workflow n8n: Theo dõi sự chuyển động của các ngành, tính toán hiệu suất, phát hiện tín hiệu giao dịch và nhận thông báo AI"
slug: "theo-doi-chuyen-dong-nganh-chung-khoan"
tags: [n8n, automation, no-code, chứng khoán, AI, LangChain]
keywords: [n8n workflow, tự động hóa, phân tích thị trường, AI chứng khoán, Groq, Google Sheets]
---

# 📈 Theo dõi sự chuyển động của các ngành trong thị trường chứng khoán với Google Sheets, Yahoo Finance, Groq và Gmail

[Các sếp] có bao giờ cảm thấy mệt mỏi khi phải theo dõi thủ công các ngành trong thị trường chứng khoán? Khi phải tính toán hiệu suất từng cổ phiếu, phân tích sự chuyển động của các ngành và chờ đợi tín hiệu giao dịch từ các chuyên gia? Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình này một cách hoàn toàn không cần code!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa toàn bộ quá trình phân tích thị trường
- **Chính xác cao**: Tính toán hiệu suất và phát hiện tín hiệu giao dịch một cách chính xác
- **Cá nhân hóa**: Nhận thông báo chỉ khi có tín hiệu giao dịch mạnh mẽ
- **Hoạt động liên tục**: Theo dõi thị trường 24/7 mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với Google Sheets đã được chia sẻ cho n8n
- Tài khoản Gmail để nhận thông báo
- API Key từ Groq để sử dụng mô hình AI Llama 3
- Danh sách cổ phiếu đang theo dõi trong Google Sheets (Sheet1)
- Bảng dữ liệu lịch sử trong Google Sheets (Sheet2)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/15068)
2. Nhấn nút "Copy" để sao chép JSON workflow
3. Trong n8n Editor, nhấn vào "Import from Clipboard" và dán JSON đã sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Fetch Active Stocks"**:
   - Chọn credentials Google Sheets OAuth2
   - Điền Sheet ID và tên Sheet chứa danh sách cổ phiếu đang theo dõi (Sheet1)

2. **Node "Fetch Historic Data"**:
   - Chọn credentials Google Sheets OAuth2
   - Điền Sheet ID và tên Sheet chứa dữ liệu lịch sử (Sheet2)

3. **Node "Insights from Model"**:
   - Chọn credentials Groq API
   - Đảm bảo đã chọn model "llama-3.3-70b-versatile"

4. **Node "Send Email Alert"**:
   - Chọn credentials Gmail OAuth2
   - Điền địa chỉ email nhận thông báo

#### 3. Kích hoạt ⚡️
1. Chạy test với dữ liệu mẫu để đảm bảo workflow hoạt động đúng
2. Bật Active workflow để chạy tự động hàng ngày

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node Slack để nhận thông báo cùng lúc với email
- Lưu log hoạt động vào Google Sheets để theo dõi lịch sử phân tích
- Kết hợp với workflow khác để tự động mua/bán cổ phiếu khi nhận tín hiệu giao dịch mạnh
- Thiết lập lịch chạy workflow vào cuối ngày giao dịch để nhận thông tin mới nhất

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quá trình phân tích thị trường chứng khoán, từ việc thu thập dữ liệu đến phát hiện tín hiệu giao dịch và nhận thông báo. Với sự hỗ trợ của AI Llama 3, các sếp có thể nhận được phân tích chuyên sâu và quyết định giao dịch thông minh hơn. Hãy áp dụng ngay để tiết kiệm thời gian và tối ưu hóa chiến lược giao dịch của mình!