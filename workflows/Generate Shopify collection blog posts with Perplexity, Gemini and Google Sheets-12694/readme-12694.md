---
title: "🚀 Tự động hóa tạo bài viết Blog Shopify chuẩn SEO với Perplexity, Gemini và Google Sheets"
description: "Xây dựng hệ thống tự động hóa toàn diện giúp chuyển đổi các bộ sưu tập (Collection) trên Shopify thành bài viết blog chuẩn SEO, tự động tạo ảnh bằng AI và đăng tải trực tiếp."
slug: "tu-dong-hoa-tao-blog-shopify-perplexity-gemini"
tags: [n8n, automation, shopify, ai, google-sheets, content-creation]
keywords: [n8n workflow, shopify automation, perplexity ai, google gemini, tu dong hoa blog shopify]
---

# 🚀 Tự động hóa tạo bài viết Blog Shopify chuẩn SEO với Perplexity, Gemini và Google Sheets

Các sếp làm e-commerce trên Shopify chắc chắn hiểu rõ nỗi đau: Việc viết blog thủ công cho từng bộ sưu tập sản phẩm (Collection) vừa tốn thời gian, vừa nhàm chán lại khó duy trì đều đặn để kéo traffic SEO. Việc ngồi nghiên cứu từ khóa, viết nội dung dài, thiết kế ảnh minh họa và đăng lên Shopify chiếm hàng tá thời gian quý báu.

Giải pháp ở đây là gì? Một hệ thống tự động hóa (Automation Pipeline) 100% không cần code sử dụng **n8n**, kết hợp sức mạnh tìm kiếm thời gian thực của **Perplexity**, khả năng sáng tạo nội dung và tạo ảnh đỉnh cao của **Google Gemini**, kết hợp lưu trữ và quản lý qua **Google Sheets**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Lắng nghe sự kiện từ Shopify hoặc chạy định kỳ theo lịch trình để lấy danh sách Collection mới nhất.
- **Nghiên cứu & Viết bài thông minh:** Tích hợp Perplexity AI để research thông tin thị trường và Google Gemini (LangChain Agent) để viết bài blog dài, chuẩn SEO.
- **Tạo ảnh tự động:** AI tự động tạo hình ảnh minh họa độc quyền cho từng bài viết, upload lên Shopify và nhúng trực tiếp vào mã nguồn HTML của bài đăng.
- **Đồng bộ hóa dữ liệu:** Mọi trạng thái (chờ xử lý, đã tạo nội dung, đã đăng bài) đều được cập nhật minh bạch trong Google Sheets.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Shopify Store** với quyền truy cập Admin API (để lấy danh sách collection và đăng bài viết blog).
- **Google Sheets API / OAuth2** để quản lý dữ liệu collection và trạng thái bài viết.
- **Perplexity API Key** phục vụ việc tìm kiếm thông tin ngữ cảnh.
- **Google Gemini API Key** (Google Palm API) phục vụ việc sinh văn bản (Text Generation) và tạo hình ảnh (Image Generation).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ n8n.io (ID: 12694) hoặc copy toàn bộ mã JSON, sau đó dán trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 51 nodes được chia thành các phân đoạn logic rõ ràng. Các sếp cần cấu hình chính xác các điểm sau:
- **Shopify Trigger1 & các HTTP Request nodes (`collection API call`, `article creation7`, v.v.):** Cấu hình `shopifyAccessTokenApi` credentials với quyền đọc/ghi sản phẩm, collection và blog articles của cửa hàng Shopify.
- **Google Sheets nodes (`collection data storing`, `get old collection`, `update content3`, v.v.):** Kết nối tài khoản Google Sheets thông qua `googleSheetsOAuth2Api`. Trỏ tới file Google Sheet quản lý chung và đảm bảo tên các cột tương ứng với dữ liệu trả về từ workflow (ID, Title, Handle, Description, Status, Image Prompt...).
- **AI Agent & LLM nodes (`Gemini2`, `Gemini5`, `web search2`, `content generator2`):** Cấu hình `googlePalmApi` cho các node Gemini và `perplexityApi` cho node Perplexity. Thiết lập prompt hệ thống cho phù hợp với văn phong thương hiệu của các sếp.
- **Node `image creation`:** Sử dụng Gemini model để tạo ảnh dựa trên `image_prompt` được trích xuất từ dữ liệu bài viết.
- **Node `replace img url` & `HTML structuring3` (Code nodes):** Kiểm tra lại logic xử lý HTML để đảm bảo URL hình ảnh được chèn chính xác vào thẻ `<img>` trong bài viết trước khi đẩy lên Shopify.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** chạy thử nghiệm thủ công (`START` / Manual Trigger) với một vài dòng dữ liệu mẫu trong Google Sheets.
- Kiểm tra kết quả trên Google Sheets và Shopify xem bài viết đã được định dạng chuẩn, có ảnh và đăng thành công chưa.
- Bật công tắc **Active** để hệ thống tự động vận hành 24/7 theo `Schedule Trigger` hoặc `Shopify Trigger`.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Thêm node Telegram hoặc Slack ở cuối workflow để nhận thông báo ngay khi hệ thống tạo và đăng thành công một bài blog mới lên Shopify.
- **Kiểm duyệt thủ công (Human-in-the-loop):** Thay vì đăng tự động ngay lập tức, các sếp có thể đặt trạng thái trong Google Sheets là `pending_review`. Sử dụng thêm một trigger thủ công hoặc nút bấm để duyệt trước khi gọi API đăng lên Shopify.
- **Lưu log lỗi:** Thêm các nhánh xử lý lỗi (Error Trigger) để tự động ghi nhận vào một sheet riêng nếu quá trình gọi API Perplexity hoặc Gemini gặp sự cố gián đoạn mạng.

### 📌 Kết luận
Workflow "Generate Shopify collection blog posts with Perplexity, Gemini and Google Sheets" là một cỗ máy tự động hóa hoàn hảo giúp các chủ cửa hàng e-commerce giải phóng hoàn toàn sức lao động trong việc xây dựng nội dung SEO. Hãy thiết lập ngay hôm nay để tối ưu hóa lưu lượng truy cập tự nhiên cho cửa hàng Shopify của các sếp!