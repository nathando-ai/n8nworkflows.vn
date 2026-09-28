---
title: "🚀 Tự động hóa phân tích cổ phiếu và đưa ra tín hiệu Mua/Bán với GPT-4, Google Sheets và EODHD"
description: "Hướng dẫn cài đặt workflow n8n tự động đọc mã cổ phiếu từ Google Sheets, lấy dữ liệu tài chính & giá từ EODHD, phân tích kỹ thuật bằng AI và lưu kết quả."
slug: "tu-dong-hoa-phan-tich-co-phieu-ai-n8n"
tags: [n8n, automation, ai, openai, google-sheets, finance]
keywords: [n8n workflow, phan tich co phieu ai, eodhd api, openai gpt-4, tu dong hoa dau tu]
---

# 🚀 Tự động hóa phân tích cổ phiếu và đưa ra tín hiệu Mua/Bán với GPT-4, Google Sheets và EODHD

Việc phân tích hàng loạt mã cổ phiếu (stocks) thủ công ngốn rất nhiều thời gian của các nhà đầu tư: từ việc tra cứu báo cáo tài chính, tính toán các chỉ báo kỹ thuật (RSI, SMA, độ biến động...) cho đến việc tổng hợp luận điểm đầu tư (investment thesis). 

Workflow n8n này sẽ giải quyết triệt để vấn đề đó bằng cách xây dựng một đường ống (pipeline) tự động hóa 100% không cần code. Hệ thống sẽ tự động quét danh sách mã cổ phiếu, kéo dữ liệu thị trường thực tế, nhờ AI (GPT-4) phân tích và trả về khuyến nghị Mua/Xem xét/Bán kèm các mức giá cụ thể ngay trong Google Sheets.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Chỉ cần điền mã cổ phiếu vào Google Sheets, hệ thống lo phần còn lại.
- **Phân tích toàn diện:** Kết hợp dữ liệu cơ bản (fundamentals), dữ liệu giá OHLCV và các chỉ báo kỹ thuật tiên tiến.
- **Cố vấn AI thông minh:** Nhận tín hiệu rõ ràng (BUY / WATCH / SELL) cùng mức giá vào lệnh, cắt lỗ (stop-loss), chốt lời (take-profit) và điểm chất lượng cơ bản từ 1-10.
- **Lưu trữ gọn gàng:** Tự động ghi toàn bộ kết quả phân tích vào tab `Signals` trên Google Sheets để tiện theo dõi hoặc làm dashboard.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google Sheets:** Tài khoản kết nối để đọc danh sách mã cổ phiếu và ghi kết quả.
- **EODHD API:** Tài khoản lấy dữ liệu thị trường tài chính (Các sếp có thể nhận ưu đãi giảm 10% tại [EODHD Pricing Special](https://eodhd.com/pricing-special-10?via=kmg&ref1=Meneses)).
- **OpenAI API Key:** Để cấu hình model `gpt-4.1-nano` hoặc các model tương thích thông qua LangChain node trong n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này từ n8n hoặc copy trực tiếp và paste vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các thành phần sau trong workflow:

- **Google Sheets (Input & Output):** 
  - Tại node `Get row(s) in sheet`: Trỏ tới file Google Sheets chứa danh sách mã cổ phiếu. Đảm bảo có cột tên là `ticker` (ví dụ: MSFT, AAPL, AMZN).
  - Tại node `Append row in sheet`: Cấu hình ghi kết quả trả về vào tab `Signals` với các thông tin như Signal, Entry, Stop Loss, Take Profit, và luận điểm đầu tư.
- **EODHD APIs (`Fetch stock fundamentals (EODHD)` & `Fetch OHLC price data (EODHD)`):**
  - Thêm API Token của các sếp vào các HTTP Request nodes theo dạng tham số: `api_token=YOUR_API_KEY`.
- **OpenAI Chat Model (`OpenAI Chat Model`):**
  - Chọn model `gpt-4.1-nano` (hoặc model OpenAI phù hợp) và cấu hình Credentials chứa OpenAI API Key. Node AI Agent sẽ nhận dữ liệu đã được xử lý từ các bước tính toán chỉ báo để đưa ra nhận định chuẩn xác.

#### 3. Kích hoạt ⚡️
- Bấm nút `When clicking ‘Execute workflow’` để chạy thử nghiệm (Test run) với dữ liệu mẫu xem hệ thống hoạt động mượt mà chưa.
- Sau khi test thành công, bật công tắc **Active workflow** để hệ thống sẵn sàng hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node Telegram hoặc Slack ở cuối luồng để nhận ngay cảnh báo (Alert) khi AI phát hiện mã cổ phiếu có tín hiệu `BUY` mạnh.
- **Lên lịch chạy định động (Cron):** Thay thế `Manual Trigger` bằng `Schedule Trigger` để hệ thống tự động quét thị trường vào mỗi sáng trước giờ giao dịch hoặc cuối tuần.
- **Mở rộng dữ liệu:** Tùy biến các đoạn `Code in JavaScript` để tính thêm các chỉ báo kỹ thuật ưa thích khác như MACD, Bollinger Bands.

### 📌 Kết luận
Workflow này là trợ thủ đắc lực giúp các nhà đầu tư tiết kiệm hàng giờ nghiên cứu thủ công mỗi ngày. Hãy áp dụng ngay vào hệ thống của các sếp để tối ưu hóa quy trình đầu tư tài chính với sức mạnh của AI và No-Code!