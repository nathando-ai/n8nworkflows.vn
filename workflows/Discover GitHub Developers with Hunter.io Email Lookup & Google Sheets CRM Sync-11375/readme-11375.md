---
title: "🚀 Tự động săn lập trình viên trên GitHub, lấy Email qua Hunter.io và đồng bộ Google Sheets CRM"
description: "Khám phá workflow n8n giúp tự động tìm kiếm lập trình viên trên GitHub theo từ khóa/địa điểm, làm giàu dữ liệu email qua Hunter.io và lọc trùng đẩy thẳng vào CRM Google Sheets."
slug: "tu-dong-san-lap-trinh-vien-github-hunterio-google-sheets"
tags: [n8n, automation, lead-generation, github, hunter-io, google-sheets]
keywords: [n8n workflow, github scraper, hunter.io email lookup, google sheets crm, tu dong hoa lead generation]
---

# 🚀 Tự động săn lập trình viên trên GitHub, làm giàu dữ liệu Email và đồng bộ CRM

Việc tìm kiếm và tiếp cận nhân tài công nghệ (Tech Talent) hoặc khách hàng tiềm năng là lập trình viên trên GitHub thường ngốn rất nhiều thời gian thủ công. Các sếp phải tự tay search từng từ khóa, lọc profile, mò mẫm tìm email và copy-paste vào file Excel quản lý. 

Quá trình thủ công này không chỉ chậm chạp mà còn dễ bỏ sót những profile chất lượng cao. Giờ đây, với workflow n8n **Discover GitHub Developers with Hunter.io Email Lookup & Google Sheets CRM Sync** do tác giả *Gilbert Onyebuchi* thiết kế, toàn bộ quy trình từ quét dữ liệu GitHub, tra cứu email qua Hunter.io cho đến lọc trùng và đẩy vào Google Sheets CRM sẽ được tự động hóa 100%.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Định kỳ quét GitHub tìm kiếm lập trình viên theo vị trí, ngôn ngữ lập trình hoặc kỹ năng mong muốn mà không cần thao tác tay.
- **Làm giàu dữ liệu thông minh:** Tự động gọi API Hunter.io để tìm và xác thực email chuyên nghiệp của developer nếu profile công khai không có sẵn.
- **Quản lý CRM sạch sẽ:** Tự động kiểm tra trùng lặp dữ liệu (Check For Duplicates) trước khi thêm mới vào Google Sheets, giúp database luôn gọn gàng, không bị rác.
- **Tiết kiệm hàng chục giờ:** Thay vì tốn hàng ngày để săn lead thủ công, hệ thống xử lý hàng loạt chỉ trong vài phút chạy.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **GitHub Personal Access Token:** Để gọi API tìm kiếm và lấy thông tin chi tiết user trên GitHub.
- **Hunter.io API Key:** Dùng cho node tra cứu email (Email Lookup).
- **Google Sheets Account:** Kết nối tài khoản Google để đồng bộ CRM (sử dụng OAuth2).
- **Template Google Sheets:** Chuẩn bị sẵn file database theo mẫu [tại đây](https://docs.google.com/spreadsheets/d/1HyoSj2HncMgap96eNxkzLEMxt1DjO6J4uOj8CHrYkFc/edit?usp=sharing).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow này, vào n8n Editor, chọn **New Workflow** -> Bấm dấu `...` (Options ở góc trên bên phải) -> **Import from Clipboard** và dán vào là xong.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình kỹ các node sau:
- **Schedule Trigger:** Cấu hình khoảng thời gian chạy định kỳ (ví dụ: mỗi ngày một lần hoặc mỗi tuần).
- **Define Developer Searches (Code Node):** Tùy chỉnh từ khóa tìm kiếm lập trình viên, địa điểm (location), ngôn ngữ lập trình theo đúng nhu cầu tuyển dụng hoặc chiến dịch outreach của doanh nghiệp.
- **Search GitHub Users & Get User Details (HTTP Request Nodes):** 
  - Thêm Credentials loại `Header Auth` chứa GitHub Personal Access Token của các sếp để vượt qua giới hạn rate limit của GitHub API.
- **Hunter.io Email Lookup (HTTP Request Node):** 
  - Nhập Hunter.io API Key vào phần cấu hình request để hệ thống tự động quét email dựa trên tên miền công ty hoặc tên của lập trình viên.
- **Check For Duplicates & Add to Lead Database (Google Sheets Nodes):**
  - Kết nối tài khoản Google Sheets của các sếp (OAuth2).
  - Trỏ đường dẫn đến file Google Sheets mẫu đã chuẩn bị sẵn ở phần yêu cầu.
  - Đảm bảo các cột map dữ liệu giữa node `Format For Database` và Google Sheets khớp nhau hoàn toàn.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** để chạy thử nghiệm (Test Run) với dữ liệu mẫu xem dòng chảy dữ liệu có đi qua các nhánh `Need Email Enrichment?`, `Filter Duplicates` và vào Google Sheets mượt mà không.
- Nếu không có lỗi xuất hiện, các sếp gạt công tắc sang **Active** để hệ thống tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh thông báo:** Nối thêm một node Telegram hoặc Slack ở cuối luồng để nhận thông báo tức thì mỗi khi hệ thống tìm được một lập trình viên chất lượng mới.
- **Tự động gửi Email Outreach:** Kết hợp thêm node Gmail hoặc Resend ngay sau bước lưu vào Google Sheets để tự động gửi email chào mừng/giới thiệu công việc đến các lập trình viên vừa tìm được.
- **Mở rộng nguồn tìm kiếm:** Ngoài GitHub, có thể tùy biến node Code đầu vào để kết hợp quét thêm từ LinkedIn hoặc GitLab.

### 📌 Kết luận
Workflow **Discover GitHub Developers with Hunter.io & Google Sheets CRM Sync** là một "vũ khí" cực kỳ lợi hại cho các team tuyển dụng (Tech Recruiter) hoặc các agency muốn tiếp cận tệp khách hàng lập trình viên. Hãy cài đặt ngay hôm nay để tự động hóa toàn bộ quy trình săn nhân tài công nghệ của doanh nghiệp các sếp nhé!