---
title: "🚀 Tự động tạo mô tả sản phẩm đa ngôn ngữ cho Shopify với Google Gemini AI"
description: "Hướng dẫn chi tiết cách sử dụng n8n và Google Gemini AI để tự động phân tích hình ảnh, tạo nội dung mô tả sản phẩm đa ngôn ngữ chất lượng cao cho cửa hàng Shopify và lưu trữ vào Google Sheets."
slug: "tao-mo-ta-san-pham-shopify-da-ngon-ngu-voi-gemini-ai"
tags: [n8n, automation, shopify, google-gemini, ai-agent, e-commerce, ai]
keywords: [n8n workflow, shopify automation, gemini ai, tao mo ta san pham, thuong mai dien tu, google sheets]
output_format: markdown
---

# 🚀 Tự động tạo mô tả sản phẩm đa ngôn ngữ cho Shopify với Google Gemini AI

Viết mô tả sản phẩm chuẩn SEO, hấp dẫn và đặc biệt là hỗ trợ **đa ngôn ngữ** cho hàng trăm, hàng nghìn sản phẩm trên Shopify luôn là một "cơn ác mộng" tốn nhiều thời gian và công sức của các chủ doanh nghiệp Thương mại điện tử. Việc thuê nhân sự viết content thủ công vừa đắt đỏ lại không đảm bảo tiến độ.

Đừng lo, workflow n8n này sẽ giúp các sếp giải quyết triệt để bài toán trên bằng cách kết hợp sức mạnh của **Shopify**, **Google Gemini Vision AI** và **LangChain Agent** để tự động phân tích hình ảnh sản phẩm, sinh nội dung mô tả chuẩn SEO bằng nhiều ngôn ngữ khác nhau và lưu trữ gọn gàng vào Google Sheets chỉ trong vòng một nốt nhạc!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Tự động hóa hoàn toàn quy trình lấy sản phẩm từ Shopify và viết nội dung hàng loạt.
- **Đa ngôn ngữ thông minh:** Tự động dịch và bản địa hóa nội dung mô tả sản phẩm sang nhiều ngôn ngữ mục tiêu.
- **AI Vision thông minh:** Node `Analyze image` kết hợp Gemini AI sẽ "nhìn" hình ảnh sản phẩm để viết mô tả cực kỳ chân thực, đúng trọng tâm.
- **Quản lý tập trung:** Toàn bộ kết quả được tự động lưu vào Google Sheets (`Append row in sheet`) giúp các sếp dễ dàng kiểm duyệt trước khi đồng bộ ngược lại Shopify.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và credentials sau:
- **Tài khoản n8n** (Self-hosted hoặc n8n Cloud).
- **Cửa hàng Shopify** kèm Custom App hoặc API Access Token để kết nối node `Get many products`.
- **Google Cloud / Gemini API Key** (Google Palm API credentials) để kết nối các node AI.
- **Google Sheets** đã tạo sẵn một file chứa các cột nhận dữ liệu (Tên sản phẩm, mô tả các ngôn ngữ, hình ảnh...).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ kho lưu trữ n8n (Link gốc: [Workflow #8179](https://n8n.io/workflows/8179)) hoặc copy mã nguồn JSON và paste trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node quan trọng sau:
- **Get many products (Shopify):** Chọn đúng `Credentials` Shopify Access Token của cửa hàng các sếp, cấu hình resource là `product` và operation là `getAll`.
- **Analyze image & Google Gemini Chat Model1:** Điền `Google Palm API` credentials hợp lệ. Node này đóng vai trò phân tích thị giác hình ảnh sản phẩm.
- **AI Agent & Structured Output Parser:** Cấu hình prompt để hướng dẫn AI cách tạo nội dung, định dạng đầu ra chuẩn cấu trúc mong muốn (ví dụ: tiêu đề, mô tả ngắn, mô tả chi tiết, các bullet points nổi bật).
- **Expand Languages & Sanitize (Code Node):** Kiểm tra và chỉnh sửa đoạn mã JavaScript trong node này để khai báo danh sách các ngôn ngữ mà các sếp muốn dịch (Ví dụ: Tiếng Anh, Tiếng Tây Ban Nha, Tiếng Pháp, Tiếng Việt...).
- **Append row in sheet (Google Sheets):** Kết nối tài khoản Google, chọn đúng File Spreadsheet và Sheet Name để lưu kết quả trả về từ AI Agent.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** (với trigger `When clicking ‘Execute workflow’`) để test thử với một vài sản phẩm mẫu.
- Kiểm tra kết quả trả về trên Google Sheets xem đã đúng định dạng chưa.
- Sau khi mọi thứ hoàn hảo, bật nút **Active** để workflow sẵn sàng hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tự động hóa qua Webhook:** Thay vì dùng `Manual Trigger`, các sếp có thể đổi thành `Shopify Webhook` (khi có sản phẩm mới được tạo) để AI tự động viết mô tả ngay lập tức.
- **Gửi thông báo qua Telegram/Slack:** Thêm một node thông báo sau khi hoàn thành để đội ngũ Marketing nhận được link Google Sheets kiểm duyệt nội dung nhanh chóng.
- **Cập nhật ngược lại Shopify:** Nối thêm một node Shopify Update Product để tự động đẩy mô tả đa ngôn ngữ vừa tạo vào cửa hàng mà không cần copy-paste thủ công.

### 📌 Kết luận
Workflow **Generate Multilingual Shopify Product Descriptions with Gemini 2.5 Vision AI** là một giải pháp đỉnh cao giúp tối ưu hóa vận hành cửa hàng Shopify bằng sức mạnh của AI đa phương thức. Hãy cài đặt ngay hôm nay để tiết kiệm thời gian và bứt phá doanh số cùng n8n các sếp nhé!