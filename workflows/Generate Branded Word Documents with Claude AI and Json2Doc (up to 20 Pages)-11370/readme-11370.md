---
title: "🚀 Tự động tạo tài liệu Word chuẩn nhận diện thương hiệu với Claude AI và Json2Doc"
description: "Hướng dẫn xây dựng workflow n8n tự động tạo văn bản Word dài tới 20 trang từ prompt và logo nhờ sức mạnh của Claude AI và Json2Doc MCP."
slug: "tao-tai-lieu-word-thuong-hieu-voi-claude-ai-va-json2doc"
tags: [n8n, automation, no-code, ai, claude-ai, json2doc, document-generation]
keywords: [n8n workflow, tạo file word tự động, claude ai, json2doc mcp, tự động hóa tài liệu, n8n viet nam]
---

# 🚀 Tự động tạo tài liệu Word chuẩn nhận diện thương hiệu với Claude AI và Json2Doc

Viết các tài liệu, báo cáo, proposal dài (lên tới 20 trang) thủ công mà vẫn phải đảm bảo đúng font chữ, màu sắc, bố cục nhận diện thương hiệu (branding) là một cơn ác mộng tốn rất nhiều thời gian của các đội ngũ kinh doanh, marketing hay tư vấn. 

Workflow n8n này chính là giải pháp tự động hóa 100% không cần code. Chỉ với một **Prompt** yêu cầu và một **Logo URL**, hệ thống sẽ phối hợp cùng **Claude AI** và **Json2Doc** để biên soạn nội dung chi tiết, định dạng chuyên nghiệp và trả về một file Word hoàn chỉnh mang đậm dấu ấn thương hiệu của doanh nghiệp bạn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Biến một ý tưởng/prompt thô thành văn bản Word dài tới 20 trang chỉ trong vài phút.
- **Chuẩn nhận diện thương hiệu:** Tự động áp dụng font chữ, màu sắc, cỡ chữ, header/footer và style bảng theo đúng styleguide của công ty.
- **AI thông minh:** Sử dụng tư duy phân tích sâu của Claude Sonnet 4.5 để chia nhỏ và tạo nội dung từng phần mạch lạc, chuyên sâu.
- **Vận hành tự động:** Giao diện Form đơn giản, dễ dàng sử dụng cho cả nhân sự không biết kỹ thuật.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Phiên bản hỗ trợ LangChain và MCP).
- **Tài khoản Anthropic (hoặc OpenRouter):** Lấy API Key để kết nối với Claude AI Model.
- **Tài khoản Json2Doc:** Đăng ký tại [app.json2docs.com](https://app.json2docs.com) để lấy API Key sử dụng dịch vụ định dạng và xuất file Word.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể copy mã JSON của workflow từ [n8n Workflow #11370](https://n8n.io/workflows/11370), sau đó dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 11 nodes, trong đó có các cấu hình quan trọng cần lưu ý:

- **On form submission (`formTrigger`):** Node khởi chạy bằng form giao diện. Các sếp có thể tuỳ chỉnh thêm các trường nhập liệu nếu muốn (ví dụ: tên khách hàng, lĩnh vực...).
- **Add Company styleguide (`set`):** Nơi các sếp định nghĩa styleguide của công ty (Font chữ, màu sắc chủ đạo, khoảng cách dòng, style bảng, header/footer). Hãy cấu hình phần này chuẩn xác để file Word xuất ra đúng nhận diện thương hiệu.
- **Anthropic Chat Model / OpenRouter Chat Model (`lmChatAnthropic` / `lmChatOpenRouter`):** Cần cấu hình Credentials với API Key tương ứng. Model mặc định đang dùng là `Claude Sonnet 4.5` (`claude-sonnet-4-5-20250929`) cho chất lượng văn bản xuất sắc nhất.
- **Json2Doc MCP & Các node HTTP Request (`Json2Doc MCP`, `HTTP Request`, `Download Docx`):** 
  Sử dụng chung một chuẩn xác thực **Header Auth**:
  1. **Header Name:** `x-api-key`
  2. **Header Value:** *API Key lấy từ [app.json2docs.com](https://app.json2docs.com)*
- **Wait for Document Generation (`wait`) & is Completed? (`if`):** Cơ chế chờ đồng bộ để đảm bảo AI và hệ thống render xong file nặng (lên tới 20 trang) trước khi kích hoạt lệnh tải xuống.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và điền thử thông tin vào Form để kiểm tra quá trình sinh văn bản từ AI đến khi tải file Word về máy.
- Sau khi test thành công, bật trạng thái **Active** để đưa vào sử dụng chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node Telegram hoặc Slack ở cuối workflow để khi file Word được tạo xong, hệ thống sẽ tự động bắn thông báo kèm file về nhóm chat cho các sếp.
- **Lưu trữ đám mây:** Thay vì chỉ tải về máy thông qua trình duyệt, có thể kết nối thêm node Google Drive hoặc OneDrive để lưu trữ tự động toàn bộ tài liệu tạo ra vào thư mục chung của công ty.
- **Mở rộng nguồn dữ liệu:** Kết hợp với các node Vector Store hoặc Google Docs để AI đọc thêm tài liệu nội dung cũ trước khi viết báo cáo mới.

### 📌 Kết luận
Việc tạo ra các bộ tài liệu, báo cáo hàng chục trang chưa bao giờ dễ dàng và chuyên nghiệp đến thế. Hãy áp dụng ngay workflow này vào quy trình làm việc của doanh nghiệp để giải phóng sức lao động cho đội ngũ nhân sự ngay hôm nay!