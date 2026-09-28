---
title: "🚀 Theo dõi các khoản trợ cấp chính phủ với AI, RSS, Google Sheets & Gmail"
description: "Tự động hóa việc theo dõi các khoản trợ cấp chính phủ từ nguồn tin RSS, phân loại và trích xuất thông tin bằng AI, lưu vào Google Sheets và gửi báo cáo qua email - hoàn toàn không cần code."
slug: "theo-doi-tro-cap-chinh-phu-voi-ai-rss-google-sheets-gmail"
tags: [n8n, automation, no-code, ai, google-sheets, gmail]
keywords: [n8n workflow, tự động hóa, theo dõi trợ cấp, AI trích xuất, Google Sheets, Gmail]
---

# 🚀 Theo dõi các khoản trợ cấp chính phủ với AI, RSS, Google Sheets & Gmail

[Các sếp] có bao giờ cảm thấy mệt mỏi khi phải theo dõi thủ công các khoản trợ cấp chính phủ từ nhiều nguồn tin khác nhau? Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình: từ thu thập thông tin đến phân tích và báo cáo - chỉ trong vài phút mỗi ngày!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động thu thập và xử lý thông tin từ nhiều nguồn trong một lần chạy.
- **Chính xác cao**: AI phân loại và trích xuất thông tin một cách nhất quán.
- **Cá nhân hóa**: Báo cáo được tùy chỉnh theo nhu cầu của từng doanh nghiệp.
- **Hoạt động liên tục**: Nhận báo cáo hàng ngày mà không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Cloud với API Google Sheets và Gmail được kích hoạt.
- API key từ OpenRouter cho các dịch vụ AI.
- Danh sách email người nhận báo cáo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/10424](https://n8n.io/workflows/10424)
2. Click "Import" và chọn "Import from URL"
3. Dán URL vào ô nhập liệu và nhấn "Import"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Schedule Trigger**:
   - Cấu hình tần suất chạy workflow (ví dụ: hàng ngày lúc 8h sáng).

2. **RSS Feed Reader**:
   - Thêm các nguồn tin RSS khác nếu cần (ví dụ: RSS của các cơ quan chính phủ khác).
   - Cấu hình URL nguồn tin: `https://www.mhlw.go.jp/stf/seisakunitsuite/bunya/koyou_roudou/grants/rss.xml`

3. **Text Classifier**:
   - Cấu hình mô hình phân loại (ví dụ: sử dụng mô hình `text-embedding-ada-002`).
   - Thiết lập các nhãn phân loại (ví dụ: "Khoa học công nghệ", "Nông nghiệp", "Y tế").

4. **AI Agent**:
   - Chọn mô hình OpenRouter (ví dụ: `mistralai/mistral-7b-instruct`).
   - Cấu hình prompt để trích xuất thông tin cần thiết.

5. **Structured Output Parser**:
   - Cấu hình schema đầu ra mong muốn (ví dụ: `{"title": "string", "deadline": "date", "amount": "number", "url": "string"}`).

6. **Google Sheets**:
   - Cấu hình thông tin xác thực Google Sheets.
   - Thiết lập tên sheet và phạm vi dữ liệu (ví dụ: `Sheet1!A:F`).

7. **Code in JavaScript**:
   - Chỉnh sửa mã JavaScript để tạo bảng HTML phù hợp với dữ liệu đầu ra.

8. **Gmail**:
   - Cấu hình thông tin xác thực Gmail.
   - Thiết lập danh sách email người nhận và chủ đề email.

#### 3. Kích hoạt ⚡️
1. Chạy thử workflow với dữ liệu mẫu.
2. Kiểm tra kết quả trên Google Sheets và hộp thư Gmail.
3. Bật chế độ Active workflow để chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- Thêm các nguồn tin RSS khác để thu thập thông tin từ nhiều nguồn.
- Tùy chỉnh schema đầu ra để phù hợp với nhu cầu cụ thể của doanh nghiệp.
- Kết hợp với Slack để nhận thông báo tức thời.
- Lưu log các lần chạy workflow để theo dõi hiệu suất.
- Tạo báo cáo định kỳ (tuần/tháng) từ dữ liệu đã thu thập.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quy trình theo dõi các khoản trợ cấp chính phủ một cách hiệu quả và chính xác. Với sự kết hợp của AI, Google Sheets và Gmail, các sếp có thể tiết kiệm thời gian và tập trung vào những việc quan trọng hơn. Hãy thử ngay và trải nghiệm sự khác biệt!