---
title: "🚀 Tự động trích xuất thông tin website & phân loại URL Thương mại điện tử với Gemini & Firecrawl"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa việc cào dữ liệu website, phân tích bằng Google Gemini và lưu trữ phân loại chi tiết vào Google Sheets."
slug: "trich-xuat-website-phan-loai-url-gemini-firecrawl-google-sheets"
tags: [n8n, automation, ai, gemini, firecrawl, google-sheets, ecommerce, market-research]
keywords: [n8n workflow, tự động hóa website, firecrawl n8n, google gemini ai, trích xuất dữ liệu thương mại điện tử, google sheets automation]
---

# 🚀 Tự động trích xuất thông tin website & phân loại URL Thương mại điện tử với Gemini & Firecrawl

Việc nghiên cứu thị trường, thu thập dữ liệu đối thủ hay phân tích cấu trúc website của các sàn thương mại điện tử (E-commerce) theo cách thủ công thường ngốn rất nhiều thời gian. Các sếp sẽ phải mở hàng chục tab, copy danh mục sản phẩm, phân loại URL thủ công vào Excel cực kỳ mệt mỏi và dễ sai sót. 

Giải pháp là đây! Workflow n8n này sẽ tự động hóa 100% quy trình: Nhận diện URL từ form đăng ký, sử dụng **Firecrawl** để map toàn bộ website, cào nội dung, nhờ sức mạnh AI của **Google Gemini** để phân loại thông minh, và cuối cùng tự động đổ toàn bộ dữ liệu sạch sẽ vào **Google Sheets**. Không cần viết code phức tạp, mọi thứ đã được đóng gói gọn gàng!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Thay vì mất hàng giờ cào và phân loại thủ công, AI và Firecrawl sẽ xử lý hàng trăm URL chỉ trong vài phút.
- **Phân loại thông minh bằng AI:** Google Gemini tự động nhận diện và phân chia URL thành các nhóm: Danh mục (Categories), Sản phẩm (Products), và Khác (Others) với độ chính xác cao.
- **Đồng bộ hóa dữ liệu thời gian thực:** Mọi thông tin công ty, metadata và URL phân loại được lưu trữ ngăn nắp trực tiếp lên Google Sheets.
- **Hoạt động tự động 24/7:** Kích hoạt dễ dàng thông qua Form Submission và tự động chạy ngầm theo kịch bản có sẵn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và credentials sau:
1. **Tài khoản n8n** (Cloud hoặc Self-hosted).
2. **Firecrawl API Key**: Dùng cho node cào và map website.
3. **Google Gemini API Key**: Dùng cho các AI Agent phân tích và phân loại dữ liệu.
4. **Google Sheets Account**: Đã tạo sẵn file Google Sheets để lưu trữ thông tin doanh nghiệp, danh mục và sản phẩm.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này từ kho lưu trữ n8n hoặc copy trực tiếp đoạn mã JSON, sau đó paste vào giao diện n8n Editor của các sếp qua tính năng **Import from JSON**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node sau:

- **Form Submission (`formTrigger`)**: 
  - Cấu hình form để người dùng nhập vào URL website cần phân tích.
- **Map a website and get urls (`@mendable/n8n-nodes-firecrawl.firecrawl`)**: 
  - Kết nối Firecrawl API Credentials.
  - Thiết lập domain mục tiêu dựa trên dữ liệu đầu vào từ Form.
- **Categorising AI Agent & Company Info Agent (`googleGemini`)**: 
  - Chọn credentials Google Gemini.
  - Tinh chỉnh Prompt (nếu cần) để yêu cầu Gemini phân loại chính xác các URL thành Product, Category hay Others theo ý muốn doanh nghiệp.
- **Update Domain Scraper Sheet, Append Categories, Append Products, Append Others (`googleSheets`)**: 
  - Kết nối tài khoản Google Drive/Sheets.
  - Chọn đúng file Google Sheets và tương ứng với từng Sheet Name (ví dụ: *Domain Info*, *Categories*, *Products*, *Others*) để dữ liệu đổ về đúng chỗ.
- **Các node Code xử lý dữ liệu (Clean HTML Content, Parse JSON Data, Parse URLs with MetaData, Parse Array URLs, v.v.)**: 
  - Giữ nguyên cấu trúc code JavaScript đã được tối ưu sẵn trong template, chỉ cần kiểm tra xem tên trường (key) có khớp với Google Sheets của các sếp hay không.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng một URL thương mại điện tử mẫu thông qua Form.
- Kiểm tra kết quả trả về trên Google Sheets xem dữ liệu đã được phân tách chuẩn xác chưa.
- Sau khi mọi thứ xanh mướt, hãy bật công tắc **Active** để đưa workflow vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Thêm node **Telegram** hoặc **Slack** ở cuối luồng để gửi thông báo về group chat ngay khi workflow cào và phân tích xong một website.
- **Lưu log lỗi:** Sử dụng nhánh *Error Trigger* để bắt lỗi nếu Firecrawl không truy cập được website, giúp các sếp dễ dàng debug.
- **Mở rộng định dạng xuất:** Ngoài Google Sheets, các sếp có thể đẩy dữ liệu trực tiếp vào các hệ thống CRM như HubSpot hoặc Notion bằng cách thay thế các node ghi dữ liệu cuối cùng.

### 📌 Kết luận
Workflow tích hợp giữa **Firecrawl** và **Google Gemini** là một "vũ khí tối thượng" cho các đội ngũ làm Growth Marketing, SEO hay nghiên cứu thị trường E-commerce. Hãy triển khai ngay hôm nay để tối ưu hóa năng suất làm việc và để AI gánh vác những công việc lặp đi lặp lại thay cho các sếp!