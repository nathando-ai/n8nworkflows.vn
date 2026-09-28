---
title: "🚀 Tự động tạo mô tả sản phẩm Shopify với GPT-4o Vision, Claude 3.5 và phân tích doanh số"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa hoàn toàn việc lấy sản phẩm Shopify, phân tích hình ảnh bằng GPT-4o Vision, viết mô tả chuẩn SEO bằng Claude 3.5 và tổng hợp báo cáo doanh số."
slug: "tao-mo-ta-san-pham-shopify-ai-phan-tich-doanh-so"
tags: [n8n, automation, shopify, ai-agent, claude, openai, google-sheets]
keywords: [n8n workflow, shopify automation, gpt-4o vision, claude 3.5 sonnet, tao mo ta san pham ai, phan tich doanh so shopify]
---

# 🚀 Tự động tạo mô tả sản phẩm Shopify với GPT-4o Vision, Claude 3.5 và phân tích doanh số

Các sếp đang sở hữu cửa hàng Shopify chắc chắn hiểu rõ nỗi đau khi phải viết hàng trăm mô tả sản phẩm thủ công, vừa tốn thời gian, vừa nhàm chán lại khó đảm bảo chuẩn SEO. Việc quản lý hình ảnh, cập nhật dữ liệu lên Google Sheets và theo dõi báo cáo doanh số mỗi ngày càng ngốn nhiều tài nguyên của đội ngũ vận hành.

Workflow n8n đỉnh cao này do chuyên gia **Kumar Shivam** thiết kế sẽ giải quyết triệt để bài toán trên. Hệ thống kết hợp sức mạnh đa phương thức (Multimodal AI) giữa **GPT-4o Vision** (phân tích hình ảnh sản phẩm) và **Claude 3.5 Sonnet** thông qua OpenRouter (viết mô tả chuyên nghiệp, chuẩn định dạng thị trường), kết hợp tự động lấy dữ liệu Shopify và phân tích báo cáo doanh số.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Tự động quét sản phẩm mới từ Shopify theo lịch trình (Schedule/Cron).
- **AI Đa phương thức thông minh:** Sử dụng GPT-4o Vision để "nhìn" và phân tích ảnh sản phẩm, sau đó giao cho Claude 3.5 Sonnet viết mô tả cuốn hút, chuẩn SEO.
- **Xử lý phân trang thông minh (Pagination):** Lưu trữ tiến độ và tự động tiếp tục ở các lần chạy sau mà không sợ sót sản phẩm.
- **Báo cáo doanh số tự động:** Tích hợp các node Google Sheets để ghi nhận và tổng hợp số liệu kinh doanh hàng ngày.
- **Cơ chế cảnh báo lỗi (Error Trigger):** Tự động bắt lỗi API hoặc server và gửi thông báo chi tiết để xử lý kịp thời.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị các tài khoản và API Keys sau:
- **n8n Instance** (phiên bản Cloud hoặc Self-hosted).
- **Shopify Store & Access Token** (để lấy thông tin sản phẩm và đơn hàng).
- **OpenAI API Key** (cho node GPT-4o Vision phân tích ảnh).
- **OpenRouter API Key** (để sử dụng các mô hình Claude 3.5 Sonnet).
- **Perplexity API Key** (cho các công cụ tra cứu thông tin bổ trợ trong AI Agent).
- **Google Sheets Account** (để lưu trữ dữ liệu sản phẩm, nhật ký chạy và báo cáo doanh số).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy trực tiếp mã nguồn JSON.
- Trong giao diện n8n Editor, chọn **Add workflow** -> Nhấn dấu `...` ở góc trên bên phải -> Chọn **Import from File** hoặc **Import from Clipboard** và dán mã JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các credentials và tham số tại các node quan trọng sau:
- **Fetch Shopify Products** & **HTTP Request1**: Kết nối tài khoản **Shopify Access Token API** của cửa hàng các sếp. Đảm bảo Store URL được cấu hình đúng endpoint lấy sản phẩm/đơn hàng.
- **Analyze image**: Chọn credentials **OpenAI API** và kiểm tra resource/operation (`image` / `analyze`) để đảm bảo GPT-4o Vision nhận được hình ảnh từ Shopify.
- **OpenRouter Chat Model / OpenRouter Chat Model1 / OpenRouter Chat Model2**: Cấu hình credentials **OpenRouter API** và chọn model chính xác (ví dụ: `anthropic/claude-3.5-sonnet`).
- **Message a model in Perplexity / Perplexity1**: Cấu hình credentials **Perplexity API** cho các tool tìm kiếm thông tin của Agent.
- **Google Sheets Nodes** (*Get row(s) in sheet1/2, Update row, Append row...*): Kết nối tài khoản **Google Sheets OAuth2 API**, trỏ đến file Google Sheet quản lý sản phẩm và báo cáo doanh số của doanh nghiệp các sếp.
- **Code5 & Code1**: Các node xử lý logic code (lọc sản phẩm theo điều kiện `body_html`, `CurrSeas:SS2025` hoặc có hình ảnh, xử lý phân trang URL) - kiểm tra kỹ các biến đầu vào nếu thay đổi cấu trúc dữ liệu.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** chạy thử thủ công với một vài sản phẩm mẫu để kiểm tra luồng dữ liệu qua từng node (đặc biệt là khâu gọi AI và ghi vào Google Sheets).
- Sau khi test thành công, chuyển công tắc sang **Active** để hệ thống tự động chạy ngầm theo lịch trình đã cài đặt (Schedule/Cron).

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo Slack/Telegram:** Thêm node gửi tin nhắn vào kênh Slack hoặc Telegram mỗi khi AI tạo xong mô tả sản phẩm mới hoặc khi có cảnh báo lỗi từ Error Trigger.
- **Mở rộng bộ nhớ Agent:** Tận dụng các node `Session Memory2` hoặc `Simple Memory` để AI duy trì ngữ cảnh tốt hơn khi xử lý các chuỗi sản phẩm phức tạp.
- **Tự động đăng ngược lại Shopify:** Sau khi AI tạo mô tả hoàn chỉnh và lưu vào Google Sheets, có thể bổ sung node Shopify Update để tự động đẩy mô tả chuẩn SEO đó trực tiếp lên website Shopify của các sếp.

### 📌 Kết luận
Workflow này là một "vũ khí tối thượng" giúp tự động hóa toàn bộ quy trình sáng tạo nội dung sản phẩm và quản trị dữ liệu bán hàng cho các nhà bán lẻ trên nền tảng Shopify. Hãy triển khai ngay hôm nay để tiết kiệm hàng chục giờ làm việc thủ công mỗi tuần và tăng tốc doanh thu cùng AI!