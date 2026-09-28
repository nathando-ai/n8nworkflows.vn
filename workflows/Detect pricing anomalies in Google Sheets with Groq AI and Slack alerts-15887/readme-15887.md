---
title: "🚀 Tự động phát hiện biến động giá bất thường trong Google Sheets với Groq AI và Slack"
description: "Hướng dẫn xây dựng workflow n8n tự động kiểm tra dữ liệu giá trên Google Sheets, phát hiện lỗi hoặc biến động sốc bằng Groq AI và gửi cảnh báo tức thì qua Slack."
slug: "phat-hien-bien-dong-gia-google-sheets-groq-ai-slack"
tags: [n8n, automation, no-code, google-sheets, groq-ai, slack, ai-summarization]
keywords: [n8n workflow, tự động hóa giá, phát hiện bất thường, google sheets groq ai, slack alert n8n]
---

# 🚀 Tự động phát hiện biến động giá bất thường trong Google Sheets với Groq AI và Slack

Các sếp có đang đau đầu vì bảng giá sản phẩm trên Google Sheets bị lỗi nhập liệu, thiếu sót hoặc biến động bất thường mà nhân viên quên kiểm tra? Việc dò thủ công hàng ngàn dòng dữ liệu tốn rất nhiều thời gian và dễ bỏ sót lỗi nghiêm trọng.

Giải pháp là đây! Workflow n8n này sẽ tự động hóa 100% quy trình kiểm tra chất lượng dữ liệu giá. Hệ thống sẽ đọc từng dòng, phối hợp cùng **Groq AI** để phân tích nguyên nhân biến động, tự động cập nhật trạng thái vào Google Sheets và bắn cảnh báo ngay lập tức lên **Slack** khi phát hiện bất thường. Không cần code phức tạp, các sếp chỉ cần "lắp ráp" và chạy!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tuyệt đối:** Thay vì rà soát thủ công hàng ngàn dòng, n8n quét xong chỉ trong vài giây.
- **Phát hiện thông minh bằng AI:** Groq AI không chỉ bắt lỗi mà còn tự động viết lý do chi tiết cho từng sự cố về giá.
- **Đồng bộ dữ liệu thời gian thực:** Tự động gắn nhãn "FLAGGED" (Cảnh báo) hoặc "OK" trực tiếp vào Google Sheets.
- **Cảnh báo tức thì:** Đội ngũ kinh doanh hoặc vận hành nhận ngay thông báo qua Slack để xử lý kịp thời trước khi khách hàng thấy giá sai.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Cloud hoặc Self-hosted).
- Tài khoản **Google Sheets** có sẵn bảng dữ liệu giá.
- Tài khoản **Groq AI** (lấy API Key miễn phí để dùng mô hình siêu tốc).
- Kênh **Slack** kèm Bot Token hoặc Webhook để nhận thông báo cảnh báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow này, vào n8n editor, chọn **Import from JSON** và dán vào là xong.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy trơn tru, các sếp cần cấu hình chính xác các node sau:

- **Chuẩn bị Google Sheet:** Đảm bảo bảng tính của các sếp có các cột: `price`, `previous_price`, `status`, `reason`, `row_number`.
- **Node `Get Pricing Data` & các node Google Sheets (`Update Flagged Row`, `Update Normal Row`):** 
  - Chọn kết nối `googleSheetsOAuth2Api`.
  - Trỏ đúng đến file Spreadsheet và Sheet Name chứa bảng giá của các sếp.
- **Node `Groq Chat Model` & `Generate Issue Reason` (Agent):** 
  - Kết nối tài khoản với `groqApi` (nhập Groq API Key).
  - Chọn model phù hợp (mặc định cấu hình `openai/gpt-oss-safeguard-20b` hoặc các model LLM nhanh của Groq).
- **Node `Check Price Issues` (Code):** Node này chứa logic JavaScript đơn giản để quét lỗi thiếu dữ liệu hoặc lệch giá đột ngột giữa `price` và `previous_price`.
- **Node `Send Slack Alert`:** 
  - Chọn kết nối `slackApi`.
  - Chọn channel nhận thông báo cảnh báo giá bất thường.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** chạy thử thủ công (thông qua node `Start Data Check` dạng Manual Trigger) với vài dòng dữ liệu mẫu để kiểm tra kết quả trên Google Sheets và Slack.
- Nếu mọi thứ mượt mà, gạt nút **Active** để workflow tự động hoạt động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Telegram/Zalo:** Ngoài Slack, các sếp có thể nối thêm node Telegram để bắn tin nhắn trực tiếp vào nhóm chat riêng của bộ phận Sale/Pricing.
- **Lên lịch chạy định động:** Thay thế node `Manual Trigger` bằng `Schedule Trigger` để n8n tự động quét bảng giá mỗi sáng lúc 8:00 hoặc định kỳ mỗi giờ.
- **Mở rộng bộ lọc:** Tùy chỉnh đoạn code trong node `Check Price Issues` để thiết lập biên độ biến động giá cho phép (ví dụ: biến động trên 20% mới báo động).

### 📌 Kết luận
Một workflow cực kỳ thiết thực cho các doanh nghiệp E-commerce, bán lẻ hoặc quản lý tài chính giúp kiểm soát chặt chẽ rủi ro sai sót về giá. Hãy áp dụng ngay vào hệ thống của các sếp để tối ưu hóa vận hành ngay hôm nay!