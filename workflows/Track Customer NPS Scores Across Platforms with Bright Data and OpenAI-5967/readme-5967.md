---
title: "🚀 Theo dõi điểm NPS khách hàng trên nhiều nền tảng với Bright Data và OpenAI"
description: "Tự động thu thập đánh giá khách hàng từ các nền tảng như Trustpilot, tính toán điểm NPS và lưu kết quả vào Google Sheets để theo dõi hiệu suất dịch vụ khách hàng hàng tuần."
slug: "theo-doi-diem-nps-khach-hang-voi-bright-data-openai"
tags: [n8n, automation, no-code, Bright Data, OpenAI, Google Sheets]
keywords: [n8n workflow, tự động hóa, điểm NPS, thu thập đánh giá, Bright Data, OpenAI]
---

# 🚀 Theo dõi điểm NPS khách hàng trên nhiều nền tảng với Bright Data và OpenAI

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi phải theo dõi thủ công đánh giá khách hàng từ nhiều nền tảng. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động thu thập và phân tích đánh giá hàng tuần
- Chính xác: Thu thập dữ liệu từ các trang đánh giá có JavaScript
- Cá nhân hóa: Theo dõi hiệu suất dịch vụ trên nhiều nền tảng khác nhau
- Hoạt động liên tục: Nhận báo cáo NPS hàng tuần mà không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Sheets với quyền truy cập API
- API Key từ OpenAI (đã kích hoạt các model như gpt-4o-mini)
- Tài khoản Bright Data với Mobile Carrier Proxy (MCP) đã kích hoạt
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/5967)
2. Click vào nút "Download" để tải file JSON
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "⏰ Run Weekly NPS Tracker"**:
   - Cấu hình lịch chạy hàng tuần (ví dụ: mỗi thứ Hai lúc 10:00 sáng)
   - Thay đổi thời gian theo múi giờ của doanh nghiệp

2. **Node "✏️ Set Survey Page URL"**:
   - Thay đổi URL trang đánh giá (ví dụ: trang Trustpilot của Shopify)
   - Có thể thêm các tham số tùy chọn như số lượng đánh giá, khoảng thời gian

3. **Node "📄 Log NPS to Google Sheet"**:
   - Kết nối với tài khoản Google Sheets của doanh nghiệp
   - Chỉnh sửa tên sheet và phạm vi dữ liệu nếu cần
   - Đảm bảo tài khoản có quyền ghi dữ liệu vào sheet

4. **Node "🎯 Prompt & Guide Agent"**:
   - Kiểm tra và điều chỉnh prompt nếu cần (ví dụ: "Extract customer ratings, comments, and dates from Trustpilot")
   - Đảm bảo prompt phù hợp với ngôn ngữ và định dạng của trang đánh giá

5. **Node "🌐 Execute Web Scrape (Bright Data)"**:
   - Kết nối với tài khoản Bright Data MCP
   - Kiểm tra cấu hình proxy và user-agent để tránh bị chặn

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu:
   - Chạy từng node một để kiểm tra kết quả
   - Đảm bảo dữ liệu đầu ra của mỗi node phù hợp với đầu vào của node tiếp theo
2. Bật Active workflow:
   - Sau khi kiểm tra thành công, bật chế độ tự động chạy workflow

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Teams để nhận thông báo khi điểm NPS xuống dưới ngưỡng mong muốn
- Lưu trữ lịch sử đánh giá để phân tích xu hướng dài hạn
- Thêm node gửi báo cáo định kỳ đến email quản lý
- Tích hợp với các công cụ khác như Google Data Studio để tạo báo cáo trực quan

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa quy trình theo dõi điểm NPS hàng tuần, tiết kiệm thời gian và nguồn lực đáng kể. Bằng cách tích hợp Bright Data và OpenAI, workflow có thể thu thập dữ liệu từ các trang đánh giá có JavaScript một cách đáng tin cậy. Kết quả được lưu vào Google Sheets để theo dõi và phân tích hiệu suất dịch vụ khách hàng một cách dễ dàng.