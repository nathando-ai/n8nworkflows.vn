---
title: "🚀 Tổng hợp và phân tích tin tức đa nguồn tự động với Mistral AI trên n8n"
description: "Tự động hóa hoàn toàn quy trình thu thập tin tức từ RSS, Custom Feed, phân tích tóm tắt bằng Mistral AI và gửi kết quả qua Telegram, WhatsApp hoặc Email."
slug: "tong-hop-phan-tich-tin-tuc-da-nguồn-mistral-ai-n8n"
tags: [n8n, automation, ai, mistral-ai, rss, telegram, content-creation]
keywords: [n8n workflow, tổng hợp tin tức tự động, Mistral AI n8n, RSS feed automation, AI summarization, tự động hóa marketing]
---

# 🚀 Tổng hợp và phân tích tin tức đa nguồn tự động với Mistral AI

Các sếp làm nội dung, Marketing hay quản trị doanh nghiệp chắc hẳn luôn đau đầu với việc phải cập nhật tin tức hàng ngày từ hàng tá nguồn khác nhau (RSS, website, video feed...). Việc đọc thủ công, tóm tắt và lên lịch chia sẻ ngốn vô số thời gian và dễ bỏ sót thông tin quan trọng. 

Workflow n8n tuyệt vời này từ tác giả **Hybroht** sinh ra để giải quyết triệt để vấn đề đó! Hệ thống sẽ tự động quét tin tức từ nhiều nguồn, sử dụng **Mistral AI** để phân tích, lọc trùng lặp, tóm tắt thông minh và phân phối trực tiếp đến các kênh tùy chỉnh như Telegram, WhatsApp hoặc Email mà không cần tốn một phút làm thủ công nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Tự động gom nhặt tin tức từ hàng loạt nguồn RSS, Custom Feed và Google News thay vì lướt web thủ công.
- **Tóm tắt sắc bén bằng AI:** Ứng dụng sức mạnh của **Mistral Cloud Chat Model** để phân tích, trích xuất ý chính và QA chất lượng nội dung trước khi xuất bản.
- **Đa kênh phân phối linh hoạt:** Tự động đẩy bản tin hoàn chỉnh đến Telegram, WhatsApp, Email hoặc lưu trực tiếp vào ổ đĩa.
- **Hoạt động tự động 24/7:** Chạy định kỳ nhờ `Schedule Trigger` hoặc kích hoạt theo yêu cầu qua Webhook và Email IMAP.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (phiên bản hỗ trợ LangChain và các AI Agent).
- **Mistral AI API Key:** Để cấu hình node `Mistral Cloud Chat Model`.
- **SerpApi Key:** Cho node `Google_news search` (nếu muốn tìm kiếm tin tức qua từ khóa/video).
- **Credentials kênh nhận tin:** Token bot Telegram, tài khoản WhatsApp, hoặc thông tin SMTP/IMAP để gửi/nhận email.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ nguồn cấp hoặc copy toàn bộ mã JSON.
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File** (hoặc dán trực tiếp bằng phím tắt `Ctrl+V` / `Cmd+V`).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Khi đưa vào vận hành thực tế, các sếp cần chú ý cấu hình các node trọng điểm sau:
- **Mistral Cloud Chat Model:** Thêm Credentials API Key của Mistral AI để các Agent (`News Analyzer`, `Website Summarizer`, `Quality Assurance`, `Content Translator`) có "não" để hoạt động.
- **Schedule:** Tần suất chạy workflow (ví dụ: chạy mỗi sáng lúc 7:00 AM để tổng hợp tin tức điểm tin ngày mới).
- **Google_news search (SerpApi):** Cấu hình khóa API SerpApi nếu muốn cào dữ liệu tìm kiếm tin tức theo từ khóa.
- **Telegram / WhatsApp / Email (Send email):** Kết nối tài khoản cá nhân/bot của các sếp để hệ thống biết chính xác gửi bản tin tổng hợp về đâu.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** để chạy thử một vòng (Test run) với dữ liệu mẫu xem các bước AI phân tích và lọc trùng (`Remove Duplicates`) hoạt động trơn tru chưa.
- Sau khi test thành công, bật công tắc **Active** góc trên cùng bên phải để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm bước lưu Google Sheets:** Nối thêm node Google Sheets ở cuối chuỗi xử lý để lưu lại lịch sử tất cả các bản tin AI đã tổng hợp, tiện cho việc tra cứu sau này.
- **Tích hợp Slack:** Thêm node Slack để gửi bản tin tóm tắt vào các kênh nội bộ công ty, giúp đội ngũ cập nhật tin tức thị trường nhanh chóng.
- **Đa ngôn ngữ tự động:** Tận dụng node `Content Translator` có sẵn trong workflow để dịch các bản tin tiếng Anh hot nhất sang tiếng Việt một cách mượt mà.

### 📌 Kết luận
Workflow **Multi-Source News Curator with Mistral AI** là một "vũ khí tối tân" giúp cá nhân và doanh nghiệp tự động hóa hoàn toàn quy trình điểm tin, nghiên cứu thị trường và sáng tạo nội dung. Hãy import ngay vào hệ thống n8n của các sếp và tận hưởng sức mạnh của tự động hóa AI ngay hôm nay!