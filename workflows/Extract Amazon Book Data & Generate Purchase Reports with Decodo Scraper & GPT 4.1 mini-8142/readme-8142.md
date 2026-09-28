---
title: "🚀 Tự động trích xuất dữ liệu sách Amazon & tạo báo cáo mua hàng với Decodo Scraper & GPT-4.1 mini"
description: "Hướng dẫn xây dựng workflow n8n tự động cào dữ liệu từ trang sách Amazon, phân tích bằng AI và xuất báo cáo PDF chuyên nghiệp gửi thẳng lên Google Drive và Slack."
slug: "tu-dong-trich-xuat-du-lieu-amazon-tao-bao-cao-voi-decodo-va-gpt"
tags: [n8n, automation, decodo, openai, gpt-4, google-drive, slack]
keywords: [n8n workflow, trích xuất dữ liệu amazon, decodo scraper api, tự động hóa báo cáo, ai agent n8n]
---

# 🚀 Tự động trích xuất dữ liệu sách Amazon & tạo báo cáo mua hàng với Decodo Scraper & GPT-4.1 mini

Chào các sếp! Việc cào dữ liệu (scraping) các trang thương mại điện tử lớn như Amazon bằng tay hoặc các công cụ truyền thống thường gặp rất nhiều khó khăn do cơ chế chống bot, nội dung tải bằng JavaScript (headless JS) hoặc cấu trúc HTML phức tạp. Chưa kể việc ngồi tổng hợp dữ liệu đó thành một báo cáo hoàn chỉnh để gửi cho cấp trên hay team vận hành tốn hàng giờ đồng hồ.

Workflow n8n này sẽ giải quyết triệt để nỗi đau đó bằng cách tự động hóa 100% quy trình: **Cào dữ liệu web thông minh** qua Decodo API ➔ **Trích xuất dữ liệu cấu trúc** bằng GPT-4.1 mini ➔ **Tự động biên soạn báo cáo** ➔ **Xuất file Google Doc/PDF** và **gửi thẳng lên Slack**. Các sếp không cần phải code một dòng nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Biến việc nghiên cứu thị trường, cào sản phẩm và làm báo cáo thủ công thành một cú click chuột.
- **Dữ liệu chuẩn xác, sạch sẽ:** Kết hợp Decodo Scraper API vượt qua các rào cản kỹ thuật và LLM để làm sạch, trích xuất đúng schema mong muốn.
- **Báo cáo chuyên nghiệp tự động:** Tự động tạo Google Doc, chuyển đổi sang PDF và phân phối ngay lập tức cho các bên liên quan.
- **Hoạt động linh hoạt:** Dễ dàng thay đổi URL mục tiêu, thiết bị giả lập (mobile/desktop) và tiêu chí lọc sản phẩm.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động mượt mà, các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **Hệ thống n8n:** (Self-hosted hoặc n8n Cloud)
- **Decodo Scraper API Key:** Để cào dữ liệu trang web công khai.
- **OpenAI API Key:** Cho Model GPT-4.1 mini xử lý và phân tích sản phẩm.
- **Google Drive / Google Docs Credentials (OAuth2):** Để tạo file Doc và xuất PDF.
- **Slack Bot Token:** Với quyền `files:write` và `chat:write` để gửi báo cáo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ kho lưu trữ n8n (Template ID: `8142`), sau đó vào giao diện n8n chọn **Add workflow** -> **Import from File** (hoặc paste trực tiếp mã JSON vào Editor).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 12 nodes chính, các sếp cần chú ý cấu hình kỹ các điểm sau:

- **When clicking ‘Execute workflow’ (Manual Trigger):** Nơi bắt đầu quy trình chạy thủ công.
- **Edit Fields (Set node):** Nơi các sếp cấu hình các thông số đầu vào như `targetUrl` (link danh mục/sản phẩm Amazon), `deviceType` (`desktop`, `mobile` hoặc `tablet`), cùng các thông tin tiêu đề báo cáo, người phụ trách (`reportOwner`).
- **Scraper API Request (HTTP Request):** Cấu hình gửi POST request đến Decodo Scraper API với API key cá nhân để cào mã nguồn HTML của trang đích.
- **HTML Response Parser (Code node):** Node này nhận chuỗi HTML thô từ Decodo, tiến hành làm sạch (loại bỏ script, style thừa, thu gọn khoảng trắng) để chuẩn bị cho AI xử lý.
- **Product Analyzer Agent & OpenAI Chat Model:** Chọn credential OpenAI, cấu hình model là `gpt-4.1-mini`. Kết hợp với **Structured Output Parser** để ép AI trả về dữ liệu JSON theo đúng định dạng sách (tiêu đề, tác giả, giá, đánh giá, ASIN...).
- **Build 📚 Book Purchase Report (Code node):** Chuyển đổi dữ liệu JSON đã trích xuất thành báo cáo dạng Markdown/HTML gọn gàng (có tóm tắt điều hành, bảng danh sách sách, gợi ý mua hàng).
- **Configure Google Drive Folder & Create Document File & Convert document to PDF:** Kết nối tài khoản Google Drive (OAuth2), trỏ tới thư mục lưu trữ báo cáo mong muốn để tự động tạo Google Doc và xuất ra file PDF.
- **Upload report to Slack (Slack node):** Chọn channel Slack nhận thông báo và cấu hình gửi kèm file PDF báo cáo cùng tóm tắt nội dung.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** chạy thử với URL mẫu để kiểm tra toàn bộ luồng từ cào dữ liệu đến tạo file PDF gửi Slack.
- Sau khi test thành công, bật nút **Active** để chính thức đưa vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng nguồn dữ liệu:** Không chỉ Amazon, các sếp có thể đổi `targetUrl` sang bất kỳ trang thương mại điện tử hoặc trang tin tức công khai nào khác.
- **Tự động hóa theo lịch:** Thay thế node Manual Trigger bằng node **Schedule (Cron)** để tự động chạy báo cáo hàng tuần hoặc hàng tháng.
- **Đa dạng kênh nhận tin:** Ngoài Slack, các sếp có thể cấu hình thêm node gửi email qua Gmail/SMTP, hoặc đẩy dữ liệu vào Telegram, Notion, Google Sheets để lưu trữ dài hạn.
- **Tùy chỉnh schema trích xuất:** Thêm các trường dữ liệu như phần trăm giảm giá (`discount_percent`), huy hiệu best-seller vào Structured Output Parser để báo cáo chi tiết hơn.

### 📌 Kết luận
Với workflow này, việc thu thập dữ liệu sản phẩm từ Amazon và tổng hợp thành báo cáo chuyên nghiệp không còn là gánh nặng tốn kém thời gian. Hãy áp dụng ngay vào hệ thống của các sếp để tối ưu hóa năng suất và ra quyết định kinh doanh dựa trên dữ liệu thực tế!