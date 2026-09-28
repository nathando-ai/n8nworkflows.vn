---
title: "🚀 Tự động làm giàu và phân loại danh sách khách hàng tiềm năng với Crawl4AI và Google Gemini trong n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động cào dữ liệu website doanh nghiệp qua Crawl4AI, sử dụng Google Gemini AI để phân tích và cập nhật kết quả vào Google Sheets."
slug: "tu-dong-lam-giàu-va-phan-loai-lead-crawl4ai-gemini-n8n"
tags: [n8n, automation, lead-generation, google-sheets, ai, gemini, crawl4ai]
keywords: [n8n workflow, làm giàu dữ liệu lead, crawl4ai, google gemini, tự động hóa google sheets, ai summarization]
---

# 🚀 Tự động làm giàu và phân loại danh sách khách hàng tiềm năng với Crawl4AI và Google Gemini

Các sếp có đang gặp tình trạng tốn hàng giờ đồng hồ để tra cứu thông tin từng doanh nghiệp, tìm mã số thuế, địa chỉ, mạng xã hội hay phân loại lĩnh vực hoạt động từ một danh sách email thô? Việc làm thủ công này không chỉ cực kỳ tẻ nhạt mà còn làm giảm năng suất đội ngũ Sales. 

Giải pháp ở đây là gì? Workflow n8n siêu việt được phát triển bởi **Davide Boizza** sẽ tự động hóa 100% quy trình này: từ việc đọc danh sách lead, cào nội dung website, sử dụng AI (Google Gemini) để trích xuất thông tin cấu trúc, cho đến việc tự động cập nhật ngược lại Google Sheets.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Chuyển đổi danh sách email thô thành hồ sơ doanh nghiệp chi tiết chỉ trong vài phút.
- **Dữ liệu cấu trúc chính xác:** Google Gemini AI tự động trích xuất tên công ty, mã số thuế (VAT), địa chỉ, số điện thoại, mạng xã hội và phân loại lĩnh vực (sector).
- **Xử lý thông minh theo lô (Batching):** Chia nhỏ dữ liệu thành các batch 10 lead kèm độ trễ (delay) giúp tránh tình trạng quá tải API hoặc dính rate limit.
- **Đồng bộ hóa mượt mà:** Tự động đánh dấu trạng thái "đã xử lý" trực tiếp trên Google Sheets sau khi hoàn tất.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google Sheets Credentials** (OAuth2) để đọc và ghi dữ liệu.
- **Google Gemini API Key** (Google Palm API) cấu hình cho các node LangChain.
- **Dịch vụ Crawl4AI** (hoặc API cào web tương thích được kết nối qua node `Post Crawling Request`).
- Bản sao Google Sheets mẫu: 👉 [Clone Google Sheet tại đây](https://docs.google.com/spreadsheets/d/1J-fP0oiryKG7bSejLLyvJhNQ3iHztDmVc-0fFd0CZZI/edit?usp=sharing)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Copy đoạn mã JSON của workflow hoặc tải file JSON từ nguồn gốc.
- Trong giao diện n8n Editor, chọn **Add workflow** -> Nhấp vào biểu tượng menu (3 chấm) -> Chọn **Import from File** hoặc dán trực tiếp JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru, các sếp cần chú ý cấu hình các node sau:
- **Read Leads from Sheets & Update Row in Sheet & Update Lead in Sheets**: Kết nối với tài khoản Google Sheets của các sếp, trỏ tới file Google Sheet mẫu đã clone ở trên, cấu hình đúng tên Sheet và các cột tương ứng (Email, URL, Status...).
- **Post Crawling Request (HTTP Request)**: Đảm bảo Endpoint URL và phương thức gửi request tới dịch vụ Crawl4AI của các sếp được thiết lập chính xác để lấy về định dạng HTML và Markdown của website doanh nghiệp.
- **Use Google Gemini Chat / Gemini Chat HTML**: Điền **Google Palm API Key** vào phần credentials của các node LLM.
- **Process in Batches of 10 & Wait 60 Seconds**: Các sếp có thể điều chỉnh số lượng batch và thời gian chờ (delay) tùy thuộc vào hạn mức (rate limit) của API Gemini và dịch vụ crawl mà các sếp đang sử dụng.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** chạy thử thủ công với một vài dòng dữ liệu mẫu để kiểm tra kết quả trả về trong Google Sheets.
- Sau khi test thành công, bật công tắc **Active** để workflow hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Thêm node Telegram hoặc Slack vào cuối quy trình để nhận thông báo tổng kết mỗi khi workflow chạy xong một lô lead.
- **Xử lý lỗi (Error Handling):** Thêm Error Trigger để bắt các lỗi kết nối mạng hoặc lỗi website không tồn tại, tránh làm dừng toàn bộ tiến trình.
- **Mở rộng bộ lọc:** Kết hợp thêm các điều kiện (If Node) để lọc các email có đuôi miễn phí (như gmail.com, yahoo.com) trước khi tiến hành cào website công ty.

### 📌 Kết luận
Workflow "Enrich and classify company leads with Crawl4AI and Gemini" là một cỗ máy tự động hóa cực kỳ mạnh mẽ giúp đội ngũ Sales và Marketing tiết kiệm hàng chục giờ làm việc thủ công mỗi tuần. Hãy triển khai ngay hôm nay để tối ưu hóa quy trình khai thác khách hàng tiềm năng của doanh nghiệp!