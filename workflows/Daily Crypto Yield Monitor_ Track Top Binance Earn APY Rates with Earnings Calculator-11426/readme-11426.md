---
title: "🚀 Giám sát Lãi suất Crypto Hàng Ngày: Top Binance Earn APY + Tính Thu Nhập"
description: "Tự động lấy dữ liệu APY Binance Earn, lọc 15 đồng có lãi suất cao nhất, tính lợi nhuận giả định $10k và gửi báo cáo email mỗi ngày."
slug: "giamsat-crypto-earn-apy-binh-thu-ngay"
tags: [n8n, automation, no-code, crypto, binance, email]
keywords: [n8n workflow, tự động hóa, Binance Earn, APY, crypto monitoring]
---

# 🚀 Giám sát Lãi suất Crypto Hàng Ngày: Top Binance Earn APY + Tính Thu Nhập

Bạn đã từng phải **đăng nhập Binance, sao chép bảng APY, tính toán lợi nhuận** mỗi sáng để không bỏ lỡ cơ hội sinh lời?  
Công việc này tốn thời gian, dễ sai sót và **không thể tự động hoá** nếu bạn không biết lập trình.  

**Daily Crypto Yield Monitor** là workflow n8n **đầy đủ 100% không code** giúp các sếp:

* **Kết nối an toàn** tới Binance API (ký HMAC‑SHA256).  
* **Lấy dữ liệu Earn** mới nhất, lọc 15 đồng có APY cao nhất.  
* **Tính toán lợi nhuận** giả định cho khoản đầu tư $10.000/ngày.  
* **Gửi báo cáo HTML** qua Gmail mỗi sáng, luôn nhận thông tin kịp thời.

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm thời gian**: Không cần mở Binance, sao chép bảng, tính toán thủ công.  
- **Độ chính xác 100%**: Ký HMAC tự động, không rủi ro lỗi nhập liệu.  
- **Cập nhật liên tục**: Báo cáo được gửi mỗi ngày vào giờ bạn định.  
- **Dễ mở rộng**: Thêm Slack, Telegram, hoặc lưu log vào Google Sheets chỉ trong vài click.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **Tài khoản Binance** với **API Key** và **Secret** (có quyền `Read` để gọi `/sapi/v1/earn/flexible/product/list`).  
- **Tài khoản Gmail** (OAuth2) để gửi email.  
- **n8n** (cài đặt trên VPS hoặc Docker).  
- **Kết nối internet** ổn định để gọi API Binance.  
:::

## 🚀 Cách import & Lên đồ

### 1. Import Workflow 📥
1. **Tải file JSON** của workflow (từ link gốc https://n8n.io/workflows/11426).  
2. Mở n8n Editor → **Import** → **Upload JSON** hoặc **Paste JSON**.  
3. Nhấn **Import** → workflow sẽ xuất hiện trên canvas.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Dưới đây là **điểm danh các node** và **cách cấu hình** chi tiết:

| Node | Loại | Hướng dẫn cấu hình |
|------|------|-------------------|
| **Daily Trigger1** | `scheduleTrigger` | Đặt thời gian chạy hàng ngày (ví dụ: 08:00 UTC). |
| **Prepare Data1** | `code` | Không cần thay đổi, chuẩn bị timestamp cho Binance. |
| **Sign Request1** | `crypto` | Chọn **HMAC‑SHA256**, nhập **Secret** từ Binance API. Output: `signature`. |
| **Get Earn Rates1** | `httpRequest` | - **Method**: GET<br>- **URL**: `https://api.binance.com/sapi/v1/earn/flexible/product/list`<br>- **Query Params**: `timestamp` (từ `Prepare Data1`), `signature` (từ `Sign Request1`).<br>- **Authentication**: Không, dùng query. |
| **Filter & Analyze1** | `code` | Đoạn JavaScript lọc 15 đồng APY cao nhất và tính lợi nhuận giả định. <br>**Tuỳ chỉnh**: Thay `$10,000` thành số tiền bạn muốn mô phỏng. |
| **Split Out1** | `splitOut` | Tách mỗi asset thành một item để xử lý riêng. |
| **Edit Fields1** | `set` | Chọn các trường cần hiển thị trong email (symbol, APY, estimated daily profit…). |
| **Sort1** | `sort` | Sắp xếp theo `APY` giảm dần. |
| **Limit1** | `limit` | Giới hạn kết quả **15** mục. |
| **Set Credentials1** | `set` | **CHỈ** dùng để lưu **Binance API Key** và **Secret** vào workflow (không hiển thị công khai). |
| **Send Email1** | `gmail` | - **Credentials**: Chọn `gmailOAuth2` đã kết nối.<br>- **To**: Địa chỉ email nhận báo cáo.<br>- **Subject**: “📈 Daily Binance Earn APY Report”.<br>- **HTML Body**: Dùng output của `Edit Fields1` (đã được format thành bảng HTML). |

> **Lưu ý quan trọng:**  
> - **Binance API Key** và **Secret** **không** được lưu trong node `httpRequest`; chúng chỉ được dùng trong `Sign Request1` và `Set Credentials1`.  
> - Đảm bảo **đúng timezone** trong `Daily Trigger1` để email tới đúng giờ làm việc.

### 3. Kích hoạt ⚡️
1. **Test run**: Nhấn nút **Execute Workflow** → kiểm tra log ở mỗi node, đặc biệt `Get Earn Rates1` (status 200) và `Send Email1` (email nhận được).  
2. Khi mọi thứ ổn, bật **Active** (nút chuyển đổi góc trên bên phải). Workflow sẽ tự động chạy mỗi ngày.

## ✍️ Mẹo & gợi ý nâng cao
- **Kết nối Slack/Telegram**: Thêm node `Slack` hoặc `Telegram` sau `Send Email1` để nhận thông báo nhanh trên kênh nhóm.  
- **Lưu log vào Google Sheets**: Thêm node `Google Sheets` sau `Limit1` để ghi lại lịch sử APY hàng ngày, dễ dàng phân tích xu hướng.  
- **Báo cáo định kỳ**: Dùng `Cron` (scheduleTrigger) để gửi báo cáo tổng hợp tuần/lần/tháng, kết hợp `Merge` các ngày lại.  
- **Cảnh báo khi APY > X%**: Thêm node `IF` sau `Filter & Analyze1` để gửi email cảnh báo nếu có đồng nào vượt ngưỡng bạn đặt.

## 📌 Kết luận
Với **Daily Crypto Yield Monitor**, các sếp sẽ không còn lo lắng bỏ lỡ cơ hội sinh lời trên Binance Earn. Chỉ cần một lần cấu hình, workflow sẽ tự động **thu thập, phân tích, tính toán và gửi báo cáo** mỗi ngày – giúp bạn tập trung vào quyết định đầu tư, không phải công việc thủ công.  

**Hãy triển khai ngay** để biến dữ liệu Binance thành lợi nhuận thực tế! 🚀