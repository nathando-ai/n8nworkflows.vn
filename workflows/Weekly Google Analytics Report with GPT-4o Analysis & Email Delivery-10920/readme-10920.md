---
title: "📊 Tự động hóa báo cáo Google Analytics hàng tuần với AI GPT-4o và gửi email"
description: "Hướng dẫn tự động hóa báo cáo Google Analytics hàng tuần với AI phân tích và gửi email tự động, tiết kiệm thời gian và nâng cao hiệu quả quản lý"
slug: "tu-dong-hoa-bao-cao-google-analytics-hang-tuan-voi-ai-gpt-4o"
tags: [n8n, automation, no-code, google-analytics, ai-summarization]
keywords: [n8n workflow, tự động hóa báo cáo, google analytics, ai phân tích, báo cáo hàng tuần]
---

# 📊 Tự động hóa báo cáo Google Analytics hàng tuần với AI GPT-4o và gửi email

[Các sếp] có bao giờ phải tốn thời gian hàng giờ để tổng hợp dữ liệu từ Google Analytics, so sánh các chỉ số tuần này với tuần trước, và viết báo cáo tóm tắt không? Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình này chỉ trong vài phút, nhận báo cáo hàng tuần đầy đủ và chuyên nghiệp chỉ với một cú nhấp chuột.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động thu thập và phân tích dữ liệu từ Google Analytics hàng tuần
- **Chính xác cao**: So sánh tự động các chỉ số giữa tuần này và tuần trước
- **Báo cáo chuyên nghiệp**: Sử dụng AI GPT-4o để tạo tóm tắt thông minh và báo cáo đầy đủ
- **Tự động hóa hoàn toàn**: Gửi báo cáo PDF qua email tự động đến người quản lý
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Cloud với các API đã kích hoạt:
  - Gmail API
  - Google Analytics Admin API
  - Google Analytics Data API
- API key từ HTML to PDF service (PDFmunk)
- Tài khoản OpenAI để sử dụng GPT-4o
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/10920](https://n8n.io/workflows/10920)
2. Nhấn nút "Import" trên trang workflow
3. Hoặc copy toàn bộ JSON workflow và paste vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Schedule Trigger**:
   - Cấu hình lịch chạy hàng tuần (thường là mỗi Chủ Nhật)
   - Thiết lập múi giờ phù hợp với doanh nghiệp

2. **Google Analytics Nodes (GA This Week & GA Last Week)**:
   - Tạo và cấu hình credentials cho Google Analytics OAuth2
   - Thiết lập View ID của tài khoản Google Analytics
   - Cấu hình ngày bắt đầu và kết thúc cho tuần này và tuần trước

3. **OpenAI Node (Message a model1)**:
   - Tạo và cấu hình credentials cho OpenAI API
   - Thiết lập model là GPT-4o
   - Cấu hình prompt phù hợp với báo cáo của doanh nghiệp

4. **HTML to PDF Node**:
   - Tạo và cấu hình credentials cho HTML to PDF API
   - Thiết lập các tham số PDF như tên file, kích thước trang,...

5. **Gmail Node (Send a message)**:
   - Tạo và cấu hình credentials cho Gmail OAuth2
   - Thiết lập địa chỉ email người nhận
   - Cấu hình tiêu đề và nội dung email

#### 3. Kích hoạt ⚡️
1. Chạy test với dữ liệu mẫu để kiểm tra toàn bộ workflow
2. Kích hoạt workflow sau khi đã kiểm tra và cấu hình đầy đủ
3. Kiểm tra email để đảm bảo báo cáo được gửi đúng định dạng

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Teams**: Thêm node để gửi báo cáo đến kênh Slack/Teams của nhóm
2. **Lưu log hoạt động**: Thêm node để lưu log các lần chạy workflow
3. **Tùy chỉnh báo cáo**: Sửa đổi template HTML để phù hợp với nhu cầu báo cáo cụ thể của doanh nghiệp
4. **Thêm biểu đồ tương tác**: Sử dụng các công cụ như Chart.js để tạo biểu đồ tương tác trong báo cáo

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quy trình báo cáo hàng tuần từ Google Analytics, từ thu thập dữ liệu đến gửi báo cáo PDF qua email. Với sự trợ giúp của AI GPT-4o, báo cáo trở nên thông minh hơn, chuyên nghiệp hơn và tiết kiệm được hàng giờ lao động mỗi tuần. Hãy áp dụng ngay để nâng cao hiệu quả quản lý và tối ưu hóa nguồn lực cho doanh nghiệp!