---
title: "🚀 Tự động nhận thông báo khi đối thủ đổi giá với Airtop và Slack qua n8n"
description: "Hướng dẫn cài đặt workflow n8n tự động cào và phân tích giá sản phẩm của đối thủ cạnh tranh bằng Airtop AI, lưu vào Google Sheets và gửi cảnh báo tức thì qua Slack."
slug: "tu-dong-thong-bao-gia-doi-thu-airtop-slack"
tags: [n8n, automation, no-code, airtop, slack, google-sheets, competitor-analysis]
keywords: [n8n workflow, theo dõi giá đối thủ, airtop ai, slack automation, tự động hóa marketing, cạnh tranh giá]
keywords: [n8n workflow, theo dõi giá đối thủ, airtop ai, slack automation, tự động hóa marketing, cạnh tranh giá]
---

# 🚀 Tự động nhận thông báo khi đối thủ đổi giá với Airtop và Slack

Các sếp có đang tốn hàng giờ mỗi tuần chỉ để truy cập website của đối thủ kiểm tra xem họ có tăng giá, giảm giá hay tung ra gói sản phẩm mới nào không? Việc theo dõi thủ công này không chỉ nhàm chán, dễ bỏ sót mà còn khiến doanh nghiệp phản ứng chậm chân trên thị trường.

Giải pháp là đây! Workflow n8n này sẽ tự động hóa 100% quy trình: Đọc danh sách URL đối thủ từ Google Sheets, sử dụng sức mạnh AI của **Airtop** để trượt vào trang giá, phân tích và so sánh với dữ liệu cũ, sau đó nếu phát hiện thay đổi sẽ cập nhật lại Sheets và bắn tin nhắn cảnh báo ngay lập tức vào **Slack**. Không cần code, hoạt động bền bỉ!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Bắt mạch đối thủ tức thì:** Nhận thông báo qua Slack ngay khi đối thủ thay đổi biểu phí hoặc tính năng gói cước.
- **Tiết kiệm 99% thời gian:** Không cần nhân sự đi "soi" giá thủ công hàng tuần.
- **Dữ liệu luôn đồng bộ:** Tự động ghi nhận và lưu trữ lịch sử thay đổi giá vào Google Sheets một cách ngăn nắp.
- **AI thông minh phân tích:** Tận dụng Airtop AI để trích xuất dữ liệu giá phức tạp từ website đối thủ cực kỳ chính xác.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị sẵn các tài khoản sau:
1. **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
2. **Google Sheets:** Một file Google Sheet chứa danh sách URL trang giá của đối thủ và cột lưu trữ dữ liệu giá cũ.
3. **Airtop AI Account:** Tài khoản và API Key để sử dụng node trích xuất web thông minh.
4. **Slack Workspace:** Đã tạo Bot hoặc Webhook để gửi tin nhắn thông báo vào kênh (channel) chỉ định.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ thư viện n8n (Link gốc: [n8n.io/workflows/3480](https://n8n.io/workflows/3480)) hoặc sử dụng mã nguồn JSON tương đương để dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 8 nodes chính. Các sếp cần cấu hình lần lượt các điểm mấu chốt sau:

- **Get Pricing URLs (Google Sheets):** 
  - Kết nối tài khoản Google Sheets của các sếp qua `googleSheetsOAuth2Api`.
  - Chọn đúng file Spreadsheet và Sheet chứa danh sách URL trang giá của đối thủ.
- **Check pricing (Airtop):** 
  - Thêm Credentials cho `airtopApi`.
  - Node này dùng prompt AI sẵn có để cào dữ liệu, tóm tắt các gói cước, liệt kê giá và 3 tính năng top đầu, sau đó đối chiếu với dữ liệu cũ (`{{ $json.Pricing }}`). Các sếp có thể tinh chỉnh prompt nếu muốn AI tập trung vào các trường dữ liệu đặc thù hơn.
- **Parse response (Code):** 
  - Node này chạy mã JavaScript nhẹ nhàng để bóc tách kết quả trả về từ Airtop, chuẩn hóa định dạng dữ liệu trước khi so sánh.
- **Merge & Filter out similar (Merge & Filter):** 
  - Node Filter sẽ đóng vai trò "gác cổng": chỉ cho phép các luồng dữ liệu có sự **thay đổi thực sự** so với dữ liệu cũ đi tiếp. Tránh việc bắn spam thông báo khi giá không đổi.
- **Update pricing (Google Sheets):** 
  - Kết nối lại Google Sheets để cập nhật dòng dữ liệu mới nhất (giá mới, thời điểm cập nhật) vào bảng tính.
- **Notify pricing change (Slack):** 
  - Cấu hình `slackApi`, chọn kênh Slack (Channel) muốn nhận thông báo và soạn nội dung tin nhắn đính kèm thông tin thay đổi giá của đối thủ.

#### 3. Kích hoạt ⚡️
- Bấm nút **‘Test workflow’** (hoặc dùng `When clicking ‘Test workflow’` trigger thủ công) để chạy thử với 1-2 dòng dữ liệu mẫu xem các node có truyền nhận dữ liệu mượt mà không.
- Sau khi kiểm tra mọi thứ chạy xanh mướt, hãy gạt công tắc sang **Active** để workflow chạy tự động theo lịch (có thể gắn thêm Schedule Trigger thay vì Manual Trigger ở bước đầu).

### ✍️ Mẹo & gợi ý nâng cao
- **Đổi sang Schedule Trigger:** Thay thế node `When clicking ‘Test workflow’` bằng node **Schedule Trigger** để hệ thống tự động quét giá đối thủ mỗi tuần một lần (ví dụ: Thứ Hai hàng tuần).
- **Mở rộng kênh thông báo:** Kết hợp thêm node Telegram hoặc Email để gửi báo cáo tổng hợp cho sếp lớn hoặc đội ngũ Sales/Marketing.
- **Lưu log chi tiết:** Lưu trữ toàn bộ lịch sử thay đổi giá vào một tab riêng trên Google Sheets để vẽ biểu đồ biến động giá thị trường theo thời gian.

### 📌 Kết luận
Việc theo dõi đối thủ chưa bao giờ dễ dàng đến thế nhờ sự kết hợp giữa n8n, AI thông minh và Slack. Hãy thiết lập ngay workflow này để luôn đi trước một bước trong cuộc chiến cạnh tranh về giá trên thị trường nhé các sếp!