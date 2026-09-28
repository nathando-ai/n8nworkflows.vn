---
title: "🚀 Tự động hóa cảnh báo đánh giá ứng dụng từ Google Play & App Store lên Slack với DataForSEO"
description: "Hướng dẫn chi tiết cách tự động theo dõi và nhận thông báo đánh giá ứng dụng mới từ Google Play và App Store lên Slack hàng ngày bằng n8n và DataForSEO"
slug: "tu-dong-hoa-canh-bao-danh-gia-ung-dung-slack-dataforseo"
tags: [n8n, automation, no-code, DataForSEO, Slack]
keywords: [n8n workflow, tự động hóa, DataForSEO, Slack, đánh giá ứng dụng]
---

# 🚀 Tự động hóa cảnh báo đánh giá ứng dụng từ Google Play & App Store lên Slack với DataForSEO

[Các sếp] có biết không? Theo dõi đánh giá ứng dụng của khách hàng trên Google Play và App Store thường là một công việc tốn thời gian và dễ bị bỏ sót. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình này chỉ trong vài phút, nhận thông báo ngay khi có đánh giá mới xuất hiện.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần theo dõi thủ công mỗi ngày
- **Nhận thông báo tức thì**: Đánh giá mới được gửi ngay lên Slack
- **Quản lý hiệu quả**: Xem tổng quan đánh giá từ cả hai nền tảng trong một nơi
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công sau khi cài đặt
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản DataForSEO với API key (đăng ký tại [DataForSEO](https://app.dataforseo.com/api-access))
- Tài khoản Slack với quyền gửi tin nhắn
- ID ứng dụng trên Google Play và App Store
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/15166](https://n8n.io/workflows/15166)
2. Click vào nút "Import" ở góc trên bên phải
3. Chọn "Import from URL" và dán link trên vào ô nhập liệu
4. Click "Import" để hoàn tất

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Schedule Trigger**:
   - Thiết lập thời gian chạy hàng ngày (ví dụ: 8:00 sáng mỗi ngày)

2. **Get app reviews from Google Play Store**:
   - Tạo credentials cho DataForSEO (sử dụng API login và password từ [DataForSEO](https://app.dataforseo.com/api-access))
   - Nhập App ID của ứng dụng trên Google Play
   - Chọn Location và Language phù hợp

3. **Get app reviews from App Store**:
   - Sử dụng cùng credentials với node Google Play
   - Nhập App ID của ứng dụng trên App Store
   - Chọn Location và Language phù hợp

4. **Send a message (Google Play)**:
   - Tạo credentials cho Slack
   - Chọn channel hoặc người nhận tin nhắn

5. **Send a message (App Store)**:
   - Sử dụng cùng credentials với node Slack Google Play
   - Chọn channel hoặc người nhận tin nhắn

#### 3. Kích hoạt ⚡️
1. Click vào nút "Activate" ở góc trên bên phải
2. Chọn "Save & Activate" để lưu và kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node để lưu log đánh giá vào Google Sheets hoặc cơ sở dữ liệu
- Kết hợp với workflow khác để phân tích cảm xúc của đánh giá
- Thiết lập cảnh báo cho đánh giá có điểm thấp
- Tự động trả lời đánh giá tích cực với nội dung chuẩn

### 📌 Kết luận
Với workflow này, các sếp có thể tự động hóa việc theo dõi đánh giá ứng dụng, nhận thông báo tức thì và quản lý hiệu quả đánh giá từ cả hai nền tảng lớn nhất. Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao trải nghiệm khách hàng!