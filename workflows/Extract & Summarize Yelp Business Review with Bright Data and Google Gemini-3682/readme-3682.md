---
title: "🚀 Tự động trích xuất và tóm tắt đánh giá Yelp với Bright Data và Google Gemini"
description: "Hướng dẫn xây dựng workflow n8n tự động cào dữ liệu đánh giá doanh nghiệp trên Yelp bằng Bright Data, sau đó phân tích và tóm tắt thông minh bằng AI Google Gemini."
slug: "tu-dong-trich-xuat-tom-tat-danh-gia-yelp-bright-data-google-gemini"
tags: [n8n, automation, ai, bright-data, google-gemini, web-scraping]
keywords: [n8n workflow, cào đánh giá yelp, bright data yelp, google gemini n8n, tự động hóa marketing, trích xuất dữ liệu ai]
---

# 🚀 Tự động trích xuất và tóm tắt đánh giá Yelp với Bright Data và Google Gemini

Việc phân tích hàng trăm đánh giá của khách hàng trên Yelp để tìm ra điểm mạnh, điểm yếu của đối thủ hoặc chính doanh nghiệp mình là một công việc cực kỳ tốn thời gian nếu làm thủ công. Các nhà quản lý và đội ngũ marketing thường "ngợp" trước dữ liệu dạng văn bản thô và thiếu cấu trúc.

Giải pháp? Workflow n8n này sẽ tự động hóa toàn bộ quy trình: cào dữ liệu đánh giá từ Yelp thông qua **Bright Data**, sau đó tận dụng sức mạnh AI của **Google Gemini** để trích xuất dữ liệu có cấu trúc và tạo ra bản tóm tắt sắc bén chỉ trong vài giây, hoàn toàn không cần viết code!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần copy-paste hay đọc thủ công từng review trên Yelp.
- **Dữ liệu chuẩn hóa:** Chuyển đổi các bài đánh giá dạng text thô thành dữ liệu có cấu trúc rõ ràng (JSON/Object).
- **Insight tức thì:** AI tự động tổng hợp, tóm tắt các phản hồi cốt lõi của khách hàng (pain points, khen ngợi...).
- **Tự động hóa toàn diện:** Dễ dàng tích hợp kết quả gửi thẳng về Webhook, Slack, Telegram hoặc Google Sheets.
:::

### Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Bright Data Account:** Tài khoản Bright Data để cấu hình Web Scraper/Zone lấy dữ liệu Yelp.
- **Google Gemini API Key:** API Key từ Google AI Studio để kết nối với các mô hình Gemini.
- **Webhook Endpoint (Tùy chọn):** URL nhận kết quả trả về (nếu muốn đẩy dữ liệu sang hệ thống khác như Make, Zapier, Slack...).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này từ kho lưu trữ n8n hoặc copy trực tiếp đoạn mã JSON, sau đó mở n8n Editor chọn **Add workflow** -> **Import from File / Clipboard** và dán vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần chú ý cấu hình các node cốt lõi sau:

- **Set Yelp URL with the Bright Data Zone (`set`):** 
  - Cần cập nhật lại URL doanh nghiệp trên Yelp mà các sếp muốn cào dữ liệu.
  - Cấu hình endpoint hoặc API token của Bright Data Zone tương ứng vào node này.
- **HTTP Request to fetch the Yelp Business Reviews (`httpRequest`):**
  - Kiểm tra lại phần Headers (`httpHeaderAuth`) để đảm bảo kết nối thành công với API/Proxy của Bright Data.
- **Google Gemini Chat Model & Google Gemini Chat Model for Summarization (`lmChatGoogleGemini`):**
  - Nhập **Google Gemini API Key** của các sếp vào phần credentials (`googlePalmApi`).
  - Khuyến nghị sử dụng các model mới như `Google Gemini Flash Exp` để tối ưu tốc độ và chi phí.
- **Webhook Notifier for the merged response (`httpRequest`):**
  - Cập nhật URL Webhook nhận dữ liệu (ví dụ: webhook của Slack, Zapier, hoặc hệ thống nội bộ) hoặc thay thế bằng node Telegram/Slack chính thức của n8n.

#### 3. Kích hoạt ⚡️
- Nhấn **Test workflow** để chạy thử với dữ liệu mẫu xem hệ thống phản hồi thế nào.
- Kiểm tra các node trích xuất cấu trúc (`Structured Data Extractor`) và tóm tắt (`Summarization Chain`) xem kết quả trả về đã đúng ý chưa.
- Sau khi mọi thứ mượt mà, gạt công tắc sang **Active** để bật chế độ chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu trữ tự động:** Thay thế hoặc bổ sung node Webhook bằng **Google Sheets** hoặc **Airtable** node để tự động lưu lại toàn bộ các bản tóm tắt đánh giá theo ngày.
- **Cảnh báo khủng hoảng truyền thông:** Kết hợp thêm điều kiện (If node), nếu điểm đánh giá trung bình thấp hoặc có review tiêu cực nghiêm trọng, hãy bắn thông báo khẩn cấp lên **Telegram/Slack**.
- **Định kỳ quét đối thủ:** Đặt lịch chạy tự động (Schedule Trigger) hàng tuần để theo dõi biến động review của đối thủ cạnh tranh trên Yelp.

### 📌 Kết luận
Workflow "Extract & Summarize Yelp Business Review with Bright Data and Google Gemini" là một cỗ máy tự động hóa cực mạnh mẽ giúp khai thác dữ liệu thị trường và tiếng nói khách hàng (Voice of Customer) một cách thông minh. Hãy "lên đồ" ngay cho hệ thống n8n của các sếp để tối ưu hóa công tác nghiên cứu thị trường!