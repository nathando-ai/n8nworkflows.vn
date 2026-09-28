---
title: "🚀 Tự động cảnh báo biến động khối lượng giao dịch Crypto (5-20%) lên Discord qua CoinGecko"
description: "Theo dõi top 1000 đồng coin trên CoinGecko, tự động phát hiện và gửi cảnh báo biến động volume (5%, 10%, 20%) phân loại theo vốn hóa lên kênh Discord."
slug: "crypto-volume-change-discord-alerts-coingecko"
tags: [n8n, automation, crypto, trading, discord, coingecko]
keywords: [n8n workflow, crypto volume alert, coingecko api discord, bot cảnh báo crypto, tự động hóa trading]
keywords: [n8n workflow, crypto volume alert, coingecko api discord, bot cảnh báo crypto, tự động hóa trading]
---

# 🚀 Tự động cảnh báo biến động khối lượng giao dịch Crypto (5-20%) lên Discord qua CoinGecko

Các anh em trader trường phái "Volume precedes price" (Khối lượng đi trước giá) chắc chắn hiểu được tầm quan trọng của việc theo dõi dòng tiền. Tuy nhiên, việc "cắm mặt" 24/7 vào biểu đồ của hàng trăm đồng coin là điều bất khả thi và cực kỳ mệt mỏi. 

Đừng lo, workflow n8n này sinh ra để giải phóng các sếp! Hệ thống sẽ tự động quét top 1000 đồng coin trên CoinGecko định kỳ, so sánh sự biến động khối lượng giao dịch (từ 5%, 10% đến 20%), phân loại vốn hóa (Large, Mid, Small Cap) và bắn tin nhắn cảnh báo trực tiếp về kênh Discord ngay lập tức. Toàn bộ tự động 100%, không tốn một xu tiền thuê coder!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không sợ sập, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Bắt sóng dòng tiền sớm:** Phát hiện ngay các đồng coin có volume tăng vọt từ 5%, 10%, đến 20% trước khi giá kịp bùng nổ.
- **Phân loại thông minh:** Chia rõ nhóm vốn hóa (Large Cap, Mid Cap, Small Cap) giúp các sếp dễ dàng phân bổ chiến lược giao dịch.
- **Thông báo trực quan:** Gửi báo cáo chi tiết, gọn gàng thẳng vào kênh Discord cá nhân hoặc nhóm Discord của hội nhóm trading.
- **Hoạt động 24/7 tự động:** Chạy ngầm liên tục theo lịch trình (Schedule Trigger) mà không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **CoinGecko API:** Không bắt buộc key cho bản miễn phí cơ bản, nhưng nên chuẩn bị nếu quét tần suất cao.
- **Discord Webhook URL:** Tạo sẵn một Webhook trên kênh Discord để bot gửi tin nhắn cảnh báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này từ kho lưu trữ n8n hoặc copy toàn bộ mã nguồn JSON, sau đó paste trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow có cấu trúc khá hoành tráng với 38 nodes, tập trung vào việc fetch dữ liệu từ nhiều trang, xử lý qua Code nodes và lưu trữ/so sánh bằng n8n DataTable. Các sếp cần chú ý các điểm sau:

- **Schedule Trigger:** Cài đặt khoảng thời gian quét dữ liệu (ví dụ: chạy mỗi 1 tiếng hoặc 30 phút một lần tùy nhu cầu).
- **Các node `Fetch Page...` (HTTP Request):** Kiểm tra lại endpoint gọi API tới CoinGecko để đảm bảo lấy đủ dữ liệu Top 1000 coin (thường chia thành nhiều trang request như `Fetch Page 1`, `Fetch Page 2`,... đến `Fetch Page 10`).
- **Các node Code xử lý dữ liệu (`Data Processing`, `Compare Volume & Calculate Changes...`, `Top 20 volume movers...`):** Các sếp có thể giữ nguyên logic JavaScript có sẵn trong node vì tác giả đã viết rất tối ưu để lọc các mức biến động >5%, >10%, >20%.
- **Các node DataTable (`Get rows`, `Insert row`, `Delete row(s)`):** Sử dụng n8n DataTable nội bộ để lưu trữ dữ liệu volume của chu kỳ trước nhằm so sánh với chu kỳ hiện tại. Hãy kiểm tra xem bảng dữ liệu đã được khởi tạo đúng Schema chưa.
- **Các node gửi Discord (`Send Large Cap Alerts to Discord`, `Send Mid Caps Alerts to Discord`, `Send Large Caps Alerts to Discord` - HTTP Request):** Dán **Discord Webhook URL** của các sếp vào phần Body/URL của các node này để bot có quyền bắn tin nhắn vào kênh.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử nghiệm thủ công xem dữ liệu có trả về mượt mà qua các bước Code và Discord hay không.
- Nếu không có lỗi đỏ xuất hiện, hãy bật nút **Active** ở góc trên cùng bên phải để workflow chính thức tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa kênh thông báo:** Ngoài Discord, các sếp có thể nhân bản nhánh cuối để bắn thêm tin nhắn vào **Telegram Bot** hoặc **Slack** để tiện theo dõi trên điện thoại.
- **Tùy chỉnh biên độ sóng:** Có thể can thiệp vào các code node `Compare Volume` để đổi mức % cảnh báo từ (5-20%) thành các con số khác tùy thuộc vào khẩu vị rủi ro (ví dụ: quét cá mập volume tăng >50%).
- **Lưu lịch sử vào Google Sheets:** Thay thế hoặc kết hợp n8n DataTable với Google Sheets node nếu các sếp muốn lưu trữ dữ liệu lịch sử để backtest sau này.

### 📌 Kết luận
Một trợ lý ảo cảnh báo volume crypto hoàn toàn miễn phí và tự động đã nằm trong tầm tay. Hãy nhanh tay "lên đồ" cài đặt ngay để không bỏ lỡ bất kỳ con sóng nào trên thị trường crypto nhé các sếp! Chúc các sếp giao dịch thắng lớn!