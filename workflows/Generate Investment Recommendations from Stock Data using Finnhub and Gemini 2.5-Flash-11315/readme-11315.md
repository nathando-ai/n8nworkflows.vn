---
title: "🚀 Tự động hóa phân tích cổ phiếu và tạo khuyến nghị đầu tư với Finnhub & Google Gemini"
description: "Xây dựng hệ thống AI tự động thu thập dữ liệu tài chính từ Finnhub, tính toán chỉ số và sử dụng Google Gemini để đưa ra báo cáo khuyến nghị đầu tư chuyên sâu chỉ trong vài giây."
slug: "tu-dong-hoa-phan-tich-co-phieu-finnhub-gemini"
tags: [n8n, automation, ai-agent, finnhub, gemini, stock-analysis, finance]
keywords: [n8n workflow, phân tích cổ phiếu tự động, finnhub api, google gemini ai, AI stock analyst, đầu tư tài chính no-code]
---

# 🚀 Tự động hóa phân tích cổ phiếu và tạo khuyến nghị đầu tư với Finnhub & Google Gemini

Các sếp có bao giờ cảm thấy ngợp trước hàng tá báo cáo tài chính, bảng cân đối kế toán, hay các chỉ số P/E, EPS, CAGR phức tạp mỗi khi muốn nghiên cứu một mã cổ phiếu mới? Việc thu thập dữ liệu thủ công rồi ngồi phân tích tốn rất nhiều thời gian và dễ bỏ lỡ cơ hội vàng.

Đừng lo, workflow n8n này sinh ra để giải quyết triệt để vấn đề đó cho các sếp! Bằng cách kết hợp sức mạnh của **Finnhub API** (cung cấp dữ liệu tài chính thời gian thực) và **Google Gemini AI** (AI Agent thông minh), hệ thống sẽ tự động hóa 100% quy trình từ khâu cào dữ liệu, tính toán các mô hình dự báo đến việc xuất ra một báo cáo khuyến nghị đầu tư cực kỳ chi tiết dưới dạng HTML hoặc file dữ liệu.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Không cần copy-paste dữ liệu thủ công từ nhiều nguồn khác nhau.
- **Phân tích chuẩn chuyên gia:** AI Agent đóng vai trò như một chuyên gia phân tích chứng khoán thực thụ, đánh giá dựa trên số liệu thực tế (Báo cáo quý hoặc Báo cáo năm).
- **Tính toán thông minh:** Hệ thống tự động lọc các chỉ số quan trọng, tính toán TTM (Trailing Twelve Months), CAGR và các mô hình dự báo tăng trưởng.
- **Báo cáo trực quan:** Xuất kết quả thành file HTML hoặc file dữ liệu sẵn sàng để lưu trữ hoặc gửi cho khách hàng/đội ngũ.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (phiên bản hỗ trợ LangChain nodes).
- **Finnhub API Key:** Tài khoản miễn phí hoặc trả phí tại [Finnhub Stock API](https://finnhub.io/) để lấy dữ liệu Quote, Financials, Ratios và MarketCap.
- **Google Gemini API Key:** Để cấu hình các node AI Chat Model (Gemini 2.5-Flash).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần tải file JSON của workflow này từ n8n.io hoặc copy toàn bộ mã JSON, sau đó paste trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần lưu ý cấu hình các node quan trọng sau:

- **Trigger Nodes (`Use if most recent company filing is quarterly report` & `Use if most recent filing is annual report`):** 
  Đây là 2 node `formTrigger` để kích hoạt workflow dựa trên kỳ báo cáo gần nhất của công ty mà các sếp muốn phân tích (Quý hay Năm). Hãy nhập mã cổ phiếu (Ticker symbol) vào form khi trigger.
- **HTTP Request Nodes (`Financials`, `Quote`, `Ratios`, `MarketCap`, v.v.):** 
  Các node này dùng để gọi API đến Finnhub. Các sếp cần thiết lập **Credentials** cho Finnhub API Key (thường dưới dạng Header Authentication `X-Finnhub-Token`).
- **Code Nodes (`Filter Important Ratios`, `Calculate TTM`, `Calculate CAGR/Prediction Models`):** 
  Các node xử lý JavaScript này thực hiện nhiệm vụ bóc tách, lọc dữ liệu thô và tính toán các chỉ số tài chính quan trọng. Các sếp có thể tùy chỉnh logic tính toán nếu muốn thay đổi công thức định giá riêng.
- **AI Agent Nodes (`Executive Stock Analyst`, `Executive Stock Analyst`):** 
  Nơi AI tiếp nhận dữ liệu đã qua xử lý. Các sếp cần liên kết chúng với các node **Google Gemini Chat Model** / **Google Gemini Chat Model1** và điền Gemini API Key hợp lệ.
- **File Nodes (`Save to Computer`, `Save to Computer1`, `Convert to Data`):** 
  Xác định đường dẫn lưu trữ trên server/máy tính để lưu file HTML báo cáo hoặc file dữ liệu xuất ra.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và nhập thử một mã cổ phiếu (ví dụ: `AAPL`, `GOOGL`) vào form trigger để test run.
- Kiểm tra kết quả trả về ở các node AI và file được lưu.
- Nếu mọi thứ chạy trơn tru, hãy gạt công tắc sang **Active** để đưa hệ thống vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Thay vì chỉ lưu file vào máy tính, các sếp có thể nối thêm node Telegram hoặc Slack để gửi bản tóm tắt khuyến nghị ngay vào điện thoại.
- **Lưu trữ đám mây:** Thay thế node lưu file cục bộ bằng Google Sheets hoặc Notion để tạo kho lưu trữ lịch sử các mã cổ phiếu đã phân tích.
- **Lên lịch định kỳ (Cron):** Thay form trigger bằng `Schedule Trigger` để hệ thống tự động quét danh sách các cổ phiếu tiềm năng mỗi tuần.

### 📌 Kết luận
Với workflow n8n kết hợp giữa Finnhub và Google Gemini này, các sếp đã sở hữu ngay một "chợ trợ lý AI tài chính" hoạt động 24/7 với chi phí gần như bằng không. Hãy triển khai ngay hôm nay để tối ưu hóa quy trình đầu tư của mình nhé!