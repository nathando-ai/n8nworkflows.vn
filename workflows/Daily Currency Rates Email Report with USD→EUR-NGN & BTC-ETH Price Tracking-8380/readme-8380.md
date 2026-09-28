---
title: "🚀 Báo cáo tỷ giá hằng ngày & giá crypto: USD→EUR, USD→NGN, BTC & ETH"
description: "Tự động lấy tỷ giá USD→EUR, USD→NGN và giá Bitcoin, Ethereum mỗi sáng 8h, gửi email báo cáo chuyên nghiệp chỉ trong vài giây."
slug: "bao-cao-ty-gia-hang-ngay-crypto"
tags: [n8n, automation, no-code, finance, crypto, email]
keywords: [n8n workflow, tự động hóa, tỷ giá, crypto, email báo cáo]
---

# 🚀 Báo cáo tỷ giá hằng ngày & giá crypto: USD→EUR, USD→NGN, BTC & ETH

Bạn có bao giờ phải mở nhiều trang web, sao chép‑dán dữ liệu tỷ giá và giá tiền ảo mỗi sáng chỉ để cập nhật báo cáo cho đội ngũ?  
Việc này không chỉ tốn thời gian mà còn dễ gây sai sót, khiến quyết định giao dịch hoặc lập kế hoạch tài chính bị chậm trễ.  

**Daily Currency Rates Email Report** là workflow n8n giúp bạn tự động:

* Lấy tỷ giá USD→EUR và USD→NGN từ ExchangeRate‑API.  
* Lấy giá Bitcoin (BTC) và Ethereum (ETH) so với USD từ CoinGecko.  
* Định dạng dữ liệu thành email HTML đẹp mắt, có màu xanh‑đỏ cho biến động.  
* Gửi báo cáo mỗi sáng 8:00 AM tới hộp thư của bạn – **không cần viết một dòng code nào**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không còn mở 3‑4 trang web mỗi ngày.  
- **Độ chính xác 100 %**: Dữ liệu lấy trực tiếp từ API uy tín, cập nhật liên tục.  
- **Báo cáo chuyên nghiệp**: Email HTML chuẩn mobile, màu mã hoá biến động (+/-).  
- **Hoạt động tự động 24/7**: Chỉ cần một lần thiết lập, workflow chạy mỗi ngày mà không cần can thiệp.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n** (cài trên VPS hoặc Docker).  
- **SMTP credentials** (Gmail, Outlook, hoặc bất kỳ máy chủ SMTP nào).  
- **Địa chỉ email người gửi** và **địa chỉ email người nhận**.  
- Không cần API key cho ExchangeRate‑API & CoinGecko (cả hai đều miễn phí, không đăng ký).  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON của workflow (từ trang gốc https://n8n.io/workflows/8380).  
2. Vào n8n → **Workflows** → **Import** → Chọn file JSON hoặc **Paste JSON** vào ô.  
3. Nhấn **Import** → Workflow sẽ xuất hiện trên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Vai trò | Cấu hình cần chỉnh |
|------|---------|--------------------|
| **Daily 8AM Trigger** | Kích hoạt workflow mỗi ngày lúc 08:00 | Đảm bảo múi giờ (Timezone) phù hợp với địa phương của bạn. |
| **Get Fiat Exchange Rates** | Gọi API ExchangeRate‑API để lấy USD→EUR & USD→NGN | - **Method**: GET <br> - **URL**: `https://v6.exchangerate-api.com/v6/latest/USD` <br> - Không cần credentials. |
| **Get Crypto Prices** | Gọi CoinGecko để lấy giá BTC & ETH (USD) + % thay đổi 24h | - **Method**: GET <br> - **URL**: `https://api.coingecko.com/api/v3/simple/price?ids=bitcoin,ethereum&vs_currencies=usd&include_24hr_change=true` <br> - Không cần credentials. |
| **Merge** | Gộp dữ liệu từ 2 request (fiat & crypto) thành một object | - **Mode**: **Pass‑through** (đảm bảo thứ tự: Fiat → Crypto). |
| **Format Email Content** | JavaScript tạo HTML + plain‑text cho email | - Kiểm tra lại biến `items` (đầu vào từ node Merge). <br> - Nếu muốn thay đổi màu sắc hoặc logo, chỉnh trong đoạn code. |
| **Send Daily Currency Email** | Gửi email báo cáo | - **Credentials**: Chọn **SMTP** đã cấu hình. <br> - **From Email**: `your-email@gmail.com` → thay bằng email gửi thực tế. <br> - **To Email**: `recipient@email.com` → thay bằng email nhận. <br> - **Subject**: `Daily Currency & Crypto Report - {{ $now.format("YYYY-MM-DD") }}` (đảm bảo biến ngày hoạt động). <br> - **HTML**: Dùng output của node **Format Email Content** (field `html`). <br> - **Text**: Dùng output `text`. |
| **Sticky Note** (nếu có) | Ghi chú nội bộ, không ảnh hưởng workflow | Không cần chỉnh. |

> **Lưu ý:** Nếu bạn dùng Gmail làm SMTP, bật **App Password** và để **Port = 587**, **TLS = true**.

#### 3. Kích hoạt ⚡️
1. Nhấn **Execute Workflow** lần đầu để kiểm tra dữ liệu mẫu.  
2. Kiểm tra hộp thư nhận: email phải hiển thị đúng định dạng HTML và chứa tỷ giá/giá crypto.  
3. Khi mọi thứ ổn, bật **Active** (nút chuyển đổi ở góc trên bên phải). Workflow sẽ tự động chạy mỗi ngày 08:00.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm Slack/Telegram**: Sau node `Send Daily Currency Email`, chèn node **Slack** hoặc **Telegram** để gửi thông báo nhanh trên kênh nội bộ.  
- **Lưu log vào Google Sheets**: Thêm node **Google Sheets** sau `Merge` để ghi lại tỷ giá và giá crypto mỗi ngày, tiện cho phân tích xu hướng.  
- **Báo cáo tuần/ tháng**: Dùng **Cron** (scheduleTrigger) với `0 0 * * 0` (Chủ nhật) và thay đổi nội dung email để tổng hợp 7 ngày qua.  
- **Thêm các cặp tiền tệ**: Thay URL ExchangeRate‑API thành `.../latest/USD` và trong code `Format Email Content` thêm các key mới (ví dụ `GBP`, `JPY`).  

### 📌 Kết luận
Với chỉ **6 node** và **không cần viết code**, workflow này giúp các sếp luôn nhận được báo cáo tỷ giá fiat & giá crypto mỗi sáng, giảm thiểu công việc thủ công, tăng độ chính xác và tạo ấn tượng chuyên nghiệp cho đối tác. Hãy triển khai ngay hôm nay, để tập trung vào quyết định kinh doanh chứ không phải việc thu thập dữ liệu!