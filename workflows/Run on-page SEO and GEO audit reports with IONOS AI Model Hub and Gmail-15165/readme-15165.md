---
title: "🚀 Tự động tạo báo cáo SEO & GEO trên trang với IONOS AI Model Hub + Gmail"
description: "Workflow n8n thu thập dữ liệu SEO, phân tích bằng AI Mistral‑Nemo và gửi báo cáo chi tiết qua Gmail chỉ trong vài giây."
slug: "run-onpage-seo-geo-audit-ionos-gmail"
tags: [n8n, automation, no-code, seo, ai, email]
keywords: [n8n workflow, tự động hóa, SEO audit, AI summarization, IONOS AI Model Hub]
---

# 🚀 Tự động tạo báo cáo SEO & GEO trên trang với IONOS AI Model Hub + Gmail

Bạn đã từng phải **điền tay** vào các công cụ SEO, sao chép‑dán dữ liệu, rồi lại viết báo cáo cho khách hàng?  
Quá trình này tốn **giờ đồng** và dễ **sai sót**, đặc biệt khi phải kiểm tra đồng thời các yếu tố GEO (E‑E‑A‑T, nội dung đáp ứng địa phương).  

**Workflow này** sẽ **tự động**:
1. Nhận URL, loại crawler và email từ form.
2. Thu thập dữ liệu SEO bằng **HTTP** hoặc **Headless Browser**.
3. Trích xuất tiêu đề, meta, schema, từ‑khóa, số từ…
4. Gửi dữ liệu tới **IONOS AI Model Hub** (model Mistral‑Nemo) để phân tích SEO + GEO.
5. Chuyển kết quả Markdown thành HTML.
6. Gửi báo cáo qua **Gmail** ngay tới hộp thư của người yêu cầu.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài phút xuống còn **giây** để có báo cáo hoàn chỉnh.  
- **Độ chính xác cao**: AI phân tích dựa trên mô hình Mistral‑Nemo, giảm thiểu lỗi con người.  
- **Báo cáo cá nhân hoá**: Gửi trực tiếp tới email người yêu cầu, kèm HTML đẹp mắt.  
- **Hoạt động liên tục**: Không cần can thiệp, workflow chạy 24/7 trên server của bạn.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản IONOS Cloud** với **API Key** (để dùng IONOS AI Model Hub).  
- **Tài khoản Gmail** và **OAuth2 credentials** (để gửi email).  
- **Apify API token** (nếu muốn dùng **Headless Browser Crawl** cho các site SPA).  
- **n8n** đã cài đặt (đề nghị chạy trên VPS như trên).  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Đăng nhập vào n8n Dashboard.  
2. Chọn **Workflows → Import**.  
3. Tải file JSON của workflow (hoặc copy/paste nội dung JSON) và nhấn **Import**.  
4. Đặt tên cho workflow (mặc định: *Run on-page SEO and GEO audit reports with IONOS AI Model Hub and Gmail*).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Mô tả | Cấu hình cần chỉnh |
|------|------|-------------------|
| **Form Trigger** | Thu thập **URL**, **Crawler type** (HTTP / Headless) và **Email** từ người dùng. | Không cần credentials. Đảm bảo các trường **URL**, **Crawler**, **Email** được bật. |
| **Choose Crawler** (Switch) | Điều hướng luồng dựa trên giá trị **Crawler** từ form. | Kiểm tra **Expression**: `{{$json["crawler"]}}` (hoặc tên trường thực tế). |
| **Simple HTTP Crawl** (HTTP Request) | Gửi GET tới URL để lấy HTML tĩnh. | **URL**: `{{$json["url"]}}` <br> **Response Format**: `String`. |
| **Headless Browser Crawl** (HTTP Request) | Gọi API Apify để chạy Playwright Chrome, trả về HTML đã render. | **URL**: `https://api.apify.com/v2/actor-runs` (hoặc endpoint Apify). <br> **Headers**: `Authorization: Bearer <YOUR_APIFY_TOKEN>` <br> **Body**: JSON chứa `url: {{$json["url"]}}`. |
| **Extract SEO Data** (Code) | JavaScript trích xuất **title, meta description, meta keywords, H1, word count, schema.org**… | Không cần credentials. Kiểm tra biến `items` và `return` để phù hợp với output của node trước. |
| **SEO + GEO Audit** (IONOS AI Model Hub) | Gửi dữ liệu SEO tới model **Mistral‑Nemo** để phân tích SEO & GEO. | **Credentials**: chọn `ionosCloudApi`. <br> **Resource**: `openai`. <br> **Model**: `mistralai/Mistral-Nemo-Instruct-2407`. <br> **Prompt**: tùy chỉnh nếu muốn, mặc định đã có prompt chuẩn. |
| **Markdown** (Markdown) | Chuyển kết quả AI (JSON) thành **Markdown** báo cáo. | Đảm bảo **Input** là output của node **SEO + GEO Audit**. |
| **Gmail** (Gmail) | Gửi email báo cáo. | **Credentials**: chọn `gmailOAuth2`. <br> **To**: `{{$json["email"]}}` (địa chỉ từ Form). <br> **Subject**: “Báo cáo SEO & GEO cho {{$json["url"]}}”. <br> **HTML**: `{{$node["Markdown"].json["html"]}}` (hoặc output HTML). |

> **Lưu ý:**  
> - Nếu sử dụng **Headless**, hãy **đảm bảo token Apify** còn hạn và có đủ credit.  
> - Kiểm tra lại **các trường JSON** (ví dụ `url`, `email`) sao cho khớp với tên trường trong Form Trigger.  
> - Khi test, dùng URL **đơn giản** (ví dụ https://example.com) để xác nhận luồng chạy đúng.

#### 3. Kích hoạt ⚡️
1. Nhấn **Execute Workflow** với dữ liệu mẫu để kiểm tra.  
2. Nếu mọi thứ ổn, bật **Active** (nút chuyển đổi ở góc trên bên phải).  
3. Đặt **Cron** (nếu muốn chạy định kỳ) hoặc để **trigger** chỉ qua Form.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối Slack/Telegram**: Thêm node Slack hoặc Telegram để nhận thông báo khi báo cáo đã được gửi.  
- **Lưu log vào Google Sheets**: Dùng node Google Sheets để ghi lại ngày, URL, thời gian chạy, kết quả audit.  
- **Báo cáo định kỳ**: Dùng **Cron** để tự động audit danh sách URL (đọc từ Google Sheet) mỗi tuần.  
- **Tùy chỉnh Prompt**: Thêm các tiêu chí SEO địa phương (ví dụ “kiểm tra schema địa chỉ”) vào prompt của IONOS AI để có báo cáo chi tiết hơn.  
- **Kiểm tra lỗi**: Thêm node **Error Trigger** để gửi email cảnh báo khi bất kỳ node nào thất bại.

### 📌 Kết luận
Với workflow này, các sếp có thể **tự động hoá toàn bộ quy trình audit SEO & GEO** chỉ bằng một cú click, giảm thiểu công sức và tăng độ tin cậy của báo cáo. Hãy **import**, **cấu hình credentials**, **bật chạy** và để AI làm phần còn lại – khách hàng sẽ nhận được báo cáo chuyên nghiệp trong tích tắc! 🚀