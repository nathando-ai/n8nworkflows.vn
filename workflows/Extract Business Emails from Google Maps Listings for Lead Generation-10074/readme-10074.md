---
title: "🚀 Tự động trích xuất Email doanh nghiệp từ Google Maps bằng n8n (Lead Generation)"
description: "Hướng dẫn xây dựng workflow n8n tự động cào dữ liệu Google Maps, truy cập website doanh nghiệp và trích xuất email chất lượng cao vào Google Sheets."
slug: "trich-xuat-email-doanh-nghiep-google-maps-n8n"
tags: [n8n, automation, no-code, lead-generation, google-maps, web-scraping, google-sheets]
keywords: [n8n workflow, trích xuất email google maps, lead generation tự động, cào email doanh nghiệp, no-code automation]
---

# 🚀 Tự động trích xuất Email doanh nghiệp từ Google Maps cho chiến dịch Lead Generation

Việc tìm kiếm khách hàng tiềm năng (Lead Generation) theo phương pháp thủ công bằng cách tìm kiếm trên Google Maps, click vào từng website và mò mẫm tìm địa chỉ email là một công việc cực kỳ tốn thời gian, nhàm chán và không thể mở rộng quy mô. 

Đừng để đội ngũ sales của bạn lãng phí thời gian vào những việc chân tay đó nữa! Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ mạnh mẽ do **Jose Castillo** phát triển, giúp tự động hóa toàn bộ quy trình: từ tìm kiếm địa điểm trên Google Maps, lọc website, truy cập từng trang, trích xuất email và lưu thẳng vào Google Sheets. Tất cả diễn ra tự động 100% mà không cần viết một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Tự động hóa hoàn toàn quy trình tìm kiếm và thu thập danh sách email doanh nghiệp.
- **Dữ liệu sạch & chính xác:** Tự động loại bỏ các liên kết rác từ Google, lọc bỏ các bản ghi trùng lặp (duplicates) trước khi lưu trữ.
- **Cá nhân hóa nguồn Lead:** Dễ dàng quét theo khu vực, ngành nghề (ngách) cụ thể để phục vụ cho các chiến dịch Email Marketing hoặc Sales Outreach.
- **Lưu trữ tập trung:** Toàn bộ thông tin email thu thập được sẽ được đồng bộ thẳng vào Google Sheets để team sales dễ dàng khai thác.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống **n8n** đang hoạt động (Self-hosted hoặc n8n Cloud).
- Tài khoản **Google Sheets** để lưu trữ danh sách email trích xuất được.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này hoặc copy toàn bộ mã JSON từ nguồn gốc.
- Trong giao diện n8n Editor, chọn **Add workflow** -> Click vào menu ba chấm (...) ở góc trên bên phải -> Chọn **Import from File** hoặc **Import from Clipboard** và dán mã JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động mượt mà theo đúng nhu cầu, các sếp cần chú ý cấu hình các node cốt lõi sau:

- **When clicking ‘Test workflow’ (`manualTrigger`):** Node kích hoạt thủ công. Các sếp có thể thay thế bằng *Schedule Trigger* nếu muốn chạy tự động định kỳ hàng ngày/hàng tuần.
- **Scrape Google Maps (`httpRequest`):** Node này thực hiện việc lấy HTML từ kết quả tìm kiếm Google Maps. Các sếp cần cấu hình URL tìm kiếm (chứa từ khóa ngành nghề và khu vực mong muốn).
- **Extract URLs & Extract Emails (`code`):** Các node JavaScript có sẵn trong workflow giúp xử lý logic bóc tách URL website và tìm các chuỗi email có cấu trúc hợp lệ từ mã nguồn trang. Không cần chỉnh sửa code trừ khi các sếp muốn tùy chỉnh regex lọc email.
- **Filter Google URLs, Remove Duplicates, Limit (`filter`, `removeDuplicates`, `limit`):** Các node này giúp làm sạch dữ liệu. Mặc định node `Limit` đang giới hạn 100 kết quả cho mỗi lần chạy để đảm bảo an toàn và tránh bị chặn. Các sếp có thể điều chỉnh con số này tùy theo nhu cầu.
- **Loop Over Items, Wait1, Scrape Site, Wait (`splitInBatches`, `wait`, `httpRequest`):** Khối xử lý vòng lặp để truy cập từng website một cách từ tốn (có kèm thời gian chờ `Wait` để tránh việc gửi quá nhiều request cùng lúc khiến website mục tiêu chặn IP).
- **Add to Sheet (`googleSheets`):** 
  - Kết nối tài khoản Google thông qua **Credentials** (`googleSheetsOAuth2Api`).
  - Chọn file Spreadsheet và Sheet cụ thể nơi các sếp muốn lưu danh sách email doanh nghiệp.

#### 3. Kích hoạt ⚡️
- Click vào nút **Test workflow** để chạy thử với một từ khóa mẫu và kiểm tra kết quả trả về trong Google Sheets.
- Sau khi test thành công, gạt công tắc **Active** ở góc trên cùng bên phải để bật workflow chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo Telegram/Slack:** Thêm một node Telegram hoặc Slack ở cuối workflow để bắn thông báo ngay về điện thoại mỗi khi quét xong một danh sách lead mới.
- **Tự động gửi Email chào hàng (Cold Email):** Nối tiếp workflow này bằng một bước gửi email tự động thông qua Gmail hoặc SMTP node để tiếp cận ngay lập tức với các email vừa thu thập được.
- **Mở rộng nguồn quét:** Có thể kết hợp thêm các node AI (như OpenAI) để tự động phân loại ngành nghề hoặc chấm điểm chất lượng lead (Lead Scoring) trước khi lưu vào Google Sheets.

### 📌 Kết luận
Workflow trích xuất email doanh nghiệp từ Google Maps này là một "vũ khí bí mật" giúp tối ưu hóa chi phí và thời gian cho các đội ngũ Marketing và Sales. Hãy triển khai ngay trên hệ thống n8n của các sếp để tạo ra một nguồn tài nguyên khách hàng tiềm năng dồi dào mỗi ngày!