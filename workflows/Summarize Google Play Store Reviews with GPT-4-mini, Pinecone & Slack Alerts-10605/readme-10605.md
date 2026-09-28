---
title: "🚀 Tự động hóa tổng hợp đánh giá Google Play Store với GPT-4-mini, Pinecone & Slack Alerts"
description: "Tự động thu thập, phân tích và báo cáo đánh giá ứng dụng trên Google Play Store hàng ngày với công nghệ AI và Slack Alerts - Giảm 90% thời gian đọc đánh giá thủ công"
slug: "tu-dong-hoa-tong-hop-danh-gia-google-play-store-voi-gpt-4-mini-pinecone-slack-alerts"
tags: [n8n, automation, no-code, google-play, ai, slack]
keywords: [n8n workflow, tự động hóa, google play reviews, ai summarization, pinecone, slack alerts]
---

# 🚀 Tự động hóa tổng hợp đánh giá Google Play Store với GPT-4-mini, Pinecone & Slack Alerts

[Các sếp] có bao giờ phải đọc hàng trăm đánh giá trên Google Play Store mỗi ngày không? Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình từ thu thập đánh giá đến tổng hợp và báo cáo trên Slack - tiết kiệm tới 90% thời gian làm việc thủ công!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động thu thập và tổng hợp hàng trăm đánh giá mỗi ngày
- **Phân tích sâu sắc**: Nhận báo cáo hàng ngày với điểm đánh giá trung bình, số lượng đánh giá, và tóm tắt nội dung
- **Hoạt động liên tục**: Theo dõi xu hướng đánh giá 24/7 mà không cần can thiệp thủ công
- **Tích hợp Slack**: Nhận báo cáo ngay trên kênh Slack của team
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Google Service Account**: Để truy cập API Google Play Store
- **Pinecone API Key**: Để lưu trữ và quản lý dữ liệu đánh giá
- **OpenAI API Key**: Để tổng hợp đánh giá bằng AI
- **Slack API Token**: Để gửi báo cáo tự động
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/10605](https://n8n.io/workflows/10605)
2. Click vào nút "Import" trên trang workflow
3. Hoặc copy toàn bộ JSON workflow và paste vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Set the bundle ids"**:
   - Thêm danh sách các Bundle ID của ứng dụng Google Play Store cần theo dõi
   - Bundle ID có thể tìm thấy trong URL của ứng dụng (ví dụ: `com.tripledot.blockbash` trong URL `https://play.google.com/store/apps/details?id=com.tripledot.blockbash`)

2. **Node "HTTP Request"**:
   - Cấu hình Google Service Account credentials
   - Đảm bảo tài khoản có quyền truy cập vào Google Play Developer API

3. **Node "Pinecone Vector Store"**:
   - Cấu hình Pinecone API credentials
   - Tạo namespace riêng cho mỗi ứng dụng (Bundle ID)

4. **Node "OpenAI Chat Model1"**:
   - Cấu hình OpenAI API credentials
   - Đảm bảo sử dụng model phù hợp (gpt-4.1-mini trong workflow)

5. **Node "Send to Slack channel"**:
   - Cấu hình Slack API credentials
   - Chọn kênh Slack để nhận báo cáo

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng
2. Bật Active workflow
3. Đặt lịch chạy hàng ngày (daily trigger) và hàng tuần (weekly trigger)

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh báo cáo**: Chỉnh sửa prompt trong node "OpenAI Chat Model1" để thay đổi định dạng báo cáo
2. **Thêm kênh thông báo**: Kết nối với Telegram hoặc Email để nhận báo cáo
3. **Lưu log đánh giá**: Lưu trữ đánh giá gốc trong Google Sheets hoặc cơ sở dữ liệu
4. **Phân tích nâng cao**: Kết nối với Power BI hoặc Tableau để tạo báo cáo trực quan

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm hàng giờ mỗi ngày trong việc theo dõi đánh giá ứng dụng. Bằng cách tự động hóa toàn bộ quy trình từ thu thập đến tổng hợp và báo cáo, các sếp có thể tập trung vào những việc quan trọng hơn - phát triển sản phẩm và cải thiện trải nghiệm người dùng. Hãy áp dụng ngay để nhận được báo cáo đánh giá hàng ngày một cách tự động và chuyên nghiệp!