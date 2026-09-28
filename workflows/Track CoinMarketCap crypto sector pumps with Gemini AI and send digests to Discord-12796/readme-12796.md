---
title: "🚀 Theo dõi xu hướng thị trường crypto với Gemini AI và gửi báo cáo lên Discord"
description: "Tự động hóa theo dõi các xu hướng thị trường crypto, phân tích bằng AI và gửi báo cáo định kỳ lên Discord - Giúp các trader phát hiện sớm các cơ hội giao dịch tiềm năng"
slug: "theo-doi-xu-huong-crypto-voi-gemini-ai-va-discord"
tags: [n8n, automation, no-code, crypto, ai]
keywords: [n8n workflow, tự động hóa, crypto trading, Gemini AI, Discord]
---

# 🚀 Theo dõi xu hướng thị trường crypto với Gemini AI và gửi báo cáo lên Discord

[Các sếp] có thể đang mất cơ hội giao dịch khi phải theo dõi thủ công hàng trăm đồng tiền ảo mỗi ngày. Workflow này sẽ tự động hóa toàn bộ quy trình từ thu thập dữ liệu đến phân tích bằng AI và gửi báo cáo lên Discord, giúp các trader phát hiện sớm các cơ hội giao dịch tiềm năng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phát hiện sớm xu hướng**: Tự động theo dõi và phân tích các sector crypto đang tăng trưởng mạnh
- **Tiết kiệm thời gian**: Không cần theo dõi thủ công hàng trăm đồng tiền ảo mỗi ngày
- **Phân tích chuyên sâu**: Sử dụng sức mạnh của Gemini AI để hiểu lý do đằng sau các xu hướng
- **Tích hợp Discord**: Nhận báo cáo định kỳ trên kênh Discord của team
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản CoinMarketCap API (free tier: 10K credits/month)
- Tài khoản Google AI Studio (để lấy API key cho Gemini)
- Discord webhook URL (tạo trong server của các sếp)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/12796](https://n8n.io/workflows/12796)
2. Click "Import" và chọn "Import from URL"
3. Hoặc copy toàn bộ JSON workflow và paste vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Fetch Top 200 Gainers from CMC**:
   - Tạo credentials mới cho CoinMarketCap API
   - Điền API key vào credentials
   - Kết nối credentials với node này

2. **Gemini Sector Research**:
   - Tạo credentials mới cho Google Gemini
   - Điền API key vào credentials
   - Kết nối credentials với node này

3. **Send to Discord**:
   - Tạo Discord webhook trong server của các sếp
   - Copy webhook URL và paste vào node này
   - Chọn channel để gửi báo cáo

4. **Filter Top Gainers (40% gain, $10M MC, $1M vol)**:
   - Có thể điều chỉnh các tham số lọc trong code node:
     ```javascript
     const MIN_PERCENT_CHANGE = 40; // % tăng trưởng tối thiểu
     const MIN_MARKET_CAP = 10000000; // $10M market cap tối thiểu
     const MIN_VOLUME = 1000000; // $1M volume tối thiểu
     ```

5. **Group Tokens by Sector**:
   - Có thể điều chỉnh mapping sector trong code node nếu cần

#### 3. Kích hoạt ⚡️
1. Click "Execute Node" để test từng node từ đầu đến cuối
2. Kiểm tra kết quả ở mỗi node để đảm bảo dữ liệu được xử lý đúng
3. Sau khi tất cả node hoạt động ổn, bật "Active" workflow

### ✍️ Mẹo & gợi ý nâng cao
1. **Thêm cảnh báo Discord**: Có thể cấu hình để gửi cảnh báo ngay khi phát hiện sector mới nổi bật
2. **Lưu log phân tích**: Thêm node để lưu log các phân tích vào Google Sheets hoặc Notion
3. **Kết hợp với các bot khác**: Có thể kết nối với các bot khác như TradingView để tạo tín hiệu giao dịch tự động
4. **Tùy chỉnh báo cáo**: Điều chỉnh template báo cáo trong node "Create Narrative Digest Report" để phù hợp với phong cách của team

### 📌 Kết luận
Workflow này sẽ giúp các trader crypto tiết kiệm thời gian quý giá và phát hiện sớm các cơ hội giao dịch tiềm năng. Bằng cách kết hợp sức mạnh của dữ liệu thị trường và trí tuệ nhân tạo, các sếp có thể đưa ra quyết định thông minh hơn và tăng khả năng thành công trong thị trường crypto ngày càng cạnh tranh này. Hãy thử ngay và bắt đầu theo dõi xu hướng thị trường crypto một cách thông minh hơn!