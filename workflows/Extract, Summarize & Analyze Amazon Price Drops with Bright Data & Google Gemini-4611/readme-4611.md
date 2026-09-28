---
title: "🚀 Tự động Trích xuất, Tóm tắt & Phân tích Giá Giảm Amazon với Bright Data và Google Gemini"
description: "Hướng dẫn cài đặt workflow n8n tự động cào dữ liệu giảm giá thương mại điện tử từ Amazon bằng Bright Data MCP, kết hợp Google Gemini AI để tóm tắt và phân tích sắc thái."
slug: "tu-dong-trich-xuat-tom-tat-phan-tich-gia-amazon-bright-data-gemini"
tags: [n8n, automation, ai, google-gemini, bright-data, e-commerce]
keywords: [n8n workflow, amazon price drop, bright data mcp, google gemini ai, cào dữ liệu amazon tự động]
---

# 🚀 Tự động Trích xuất, Tóm tắt & Phân tích Giá Giảm Amazon với Bright Data và Google Gemini

Việc theo dõi biến động giá cả, các chương trình giảm giá (Price Drops) và đánh giá của khách hàng trên các sàn thương mại điện tử lớn như Amazon theo cách thủ công cực kỳ tốn thời gian và dễ bỏ lỡ cơ hội. Các nhà nghiên cứu thị trường và Marketer thường xuyên phải đối mặt với núi dữ liệu phân mảnh. 

Workflow n8n này chính là giải pháp tự động hóa 100% không cần code (No-code) giúp các sếp giải quyết triệt để bài toán trên. Sự kết hợp giữa **Bright Data MCP Client** và sức mạnh AI của **Google Gemini** sẽ tự động cào dữ liệu, cấu trúc hóa thông tin, tóm tắt nội dung và phân tích sắc thái (Sentiment Analysis) cực kỳ chuyên nghiệp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 (đặc biệt cần thiết cho các tác vụ scraping dữ liệu lớn), các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Cào dữ liệu giảm giá và đánh giá sản phẩm Amazon theo yêu cầu hoặc lịch trình.
- **Phân tích thông minh bằng AI:** Google Gemini tự động tóm tắt nội dung và phân tích sắc thái ý kiến người dùng.
- **Đồng bộ dữ liệu mượt mà:** Tự động cập nhật kết quả vào Google Sheets để dễ dàng theo dõi, báo cáo.
- **Cảnh báo thời gian thực:** Tích hợp Webhook Notification để gửi thông tin biến động giá ngay lập tức.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Self-hosted Instance:** Do workflow sử dụng node cộng đồng `MCP Client`, hệ thống bắt buộc phải chạy trên n8n Self-hosted.
- **Tài khoản Bright Data & API Key:** Để cấu hình `Bright Data MCP Client`.
- **Google Gemini API Key:** Sử dụng cho các model `Google Gemini Chat Model` trong chuỗi LangChain.
- **Google Sheets Credentials:** Để lưu trữ dữ liệu sản phẩm đã trích xuất.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ nguồn cung cấp hoặc copy trực tiếp mã JSON và paste vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần chú ý cấu hình kỹ các node trọng điểm sau đây:
- **Set input fields (`Set input fields`):** Đảm bảo các sếp đã nhập đúng các trường thông tin đầu vào (từ khóa sản phẩm, URL, hoặc danh mục sản phẩm cần quét trên Amazon).
- **Bright Data MCP Client nodes** (`Bright Data MCP Client List Tools`, `MCP Client for Price Drop Data Extract`, `MCP Client for Price Drop Data Extract Within a Loop`): Điền thông tin `mcpClientApi` credentials để kết nối dịch vụ cào dữ liệu của Bright Data.
- **Google Gemini Chat Models** (`Google Gemini Chat Model for Summarize Content`, `Google Gemini Chat Model for Sentiment Analysis`, `Google Gemini Chat Model`): Kết nối tài khoản `googlePalmApi` để AI có thể hoạt động trơn tru.
- **Update Google Sheets (`Update Google Sheets`):** Chọn tài khoản Google Sheets OAuth2, sau đó chỉ định đúng file Google Sheet và Sheet Name để lưu thông tin sản phẩm, giá giảm và kết quả phân tích.
- **Webhook Notification (`Webhook Notification for Price Drop Info`):** Trỏ URL webhook về kênh thông báo của các sếp (Slack, Telegram, hoặc hệ thống nội bộ) nếu muốn nhận cảnh báo biến động giá.

#### 3. Kích hoạt ⚡️
- Nhấn **‘Test workflow’** bằng nút `When clicking ‘Test workflow’` để kiểm tra toàn bộ luồng chạy với dữ liệu mẫu.
- Sau khi test thành công không báo lỗi, bật công tắc **Active** để workflow tự động vận hành.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh chat:** Kết nối thêm node Telegram hoặc Slack vào sau bước `Aggregate` để nhận bản tin tổng hợp giá giảm mỗi sáng.
- **Lưu lịch sử chạy:** Sử dụng thêm node lưu log vào cơ sở dữ liệu (như PostgreSQL hoặc Airtable) để tiện cho việc audit dữ liệu về lâu dài.
- **Định lịch chạy (Cron):** Thay thế `Manual Trigger` bằng `Schedule Trigger` để tự động cào giá Amazon định kỳ hàng ngày/hàng tuần.

### 📌 Kết luận
Workflow này là một "vũ khí" cực kỳ mạnh mẽ giúp tự động hóa toàn bộ quy trình nghiên cứu thị trường thương mại điện tử bằng AI. Hãy cài đặt ngay lên hệ thống n8n self-hosted của các sếp để tối ưu hóa thời gian và gia tăng lợi thế cạnh tranh!