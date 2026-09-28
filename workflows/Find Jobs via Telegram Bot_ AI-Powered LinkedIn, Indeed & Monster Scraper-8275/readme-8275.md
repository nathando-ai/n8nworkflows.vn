---
title: "🚀 Tìm kiếm việc làm tự động qua Telegram Bot với AI: Tích hợp LinkedIn, Indeed & Monster"
description: "Xây dựng trợ lý tìm việc thông minh trên Telegram sử dụng n8n, tự động quét tin tuyển dụng từ LinkedIn, Indeed và Monster, phân tích và trả kết quả trực tiếp cho bạn."
slug: "tim-kiem-viec-lam-tu-dong-telegram-bot-ai-linkedin-indeed-monster"
tags: [n8n, automation, no-code, telegram-bot, ai-scraper, job-search]
keywords: [n8n workflow, telegram bot tìm việc, linkedin scraper, indeed scraper, tự động hóa n8n]
---

# 🚀 Tự động hóa tìm kiếm việc làm đỉnh cao với Telegram Bot và AI

Việc lướt qua hàng trăm tin tuyển dụng thủ công mỗi ngày trên LinkedIn, Indeed hay Monster để tìm ra công việc phù hợp thực sự là một "cực hình" ngốn rất nhiều thời gian của các ứng viên hay nhà tuyển dụng. Thay vì tốn hàng giờ cào dữ liệu thủ công, tại sao các sếp không tự động hóa toàn bộ quy trình này?

Bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n cực kỳ mạnh mẽ: Biến **Telegram Bot** thành một trợ lý AI thông minh, tự động nhận lệnh tìm việc, quét dữ liệu từ các nền tảng việc làm lớn nhất, đồng thời lưu trữ vào Google Sheets/Airtable một cách gọn gàng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần mở nhiều tab trình duyệt, chỉ cần chat với Telegram Bot để nhận danh sách việc làm cô đọng.
- **Quét đa nền tảng:** Tự động lấy dữ liệu đồng thời từ LinkedIn, Indeed và Monster trong tích tắc.
- **Lưu trữ thông minh:** Tự động đồng bộ dữ liệu việc làm vào Google Sheets hoặc Airtable để dễ dàng theo dõi tiến độ ứng tuyển.
- **Hoạt động 24/7:** Bot luôn sẵn sàng nhận lệnh bất cứ khi nào các sếp cần tìm kiếm cơ hội mới.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** (Self-hosted hoặc n8n Cloud).
- **Telegram Bot Token:** Tạo qua `@BotFather` trên Telegram để làm cổng giao tiếp.
- **Google Sheets hoặc Airtable:** Nơi lưu trữ danh sách các công việc tìm được.
- **API truy xuất dữ liệu việc làm (HTTP Request):** Các nguồn scraper tương ứng cho LinkedIn, Indeed, Monster.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này và dán trực tiếp vào n8n Editor của mình, hoặc import file JSON thông qua giao diện n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru, các sếp cần cấu hình chính xác các node quan trọng sau:

- **Telegram Bot Trigger & Các node Telegram (`Send Welcome Message`, `Send Search Status`, `Send Job Results`):**
  - Tạo kết nối (`Credentials`) bằng **Telegram API Token** lấy từ BotFather.
  - Đảm bảo bot đã được kích hoạt và khởi chạy (gửi lệnh `/start`).
- **Command Filter & Job Search Filter:**
  - Kiểm tra điều kiện lọc tin nhắn từ người dùng để phân loại lệnh tìm việc hoặc lệnh chào mừng.
- **Parse Job Command & Code Nodes (`Process Jobs for Telegram`, `Format Jobs Message`):**
  - Các node mã nguồn JavaScript này xử lý chuỗi tìm kiếm (vị trí công việc, địa điểm) do người dùng nhập vào và định dạng lại hiển thị cho đẹp mắt trên Telegram.
- **LinkedIn Jobs Scraper, Indeed Jobs Scraper & Monster Jobs Scraper (`httpRequest`):**
  - Cấu hình endpoint API hoặc dịch vụ scraper tương ứng mà các sếp sử dụng để cào dữ liệu từ 3 nền tảng trên.
- **Save to Google Sheets & Save to Airtable:**
  - Kết nối tài khoản Google/Airtable tương ứng.
  - Chọn đúng File, Sheet Name (đối với Google Sheets) hoặc Base/Table (đối với Airtable) để dữ liệu đổ về đúng chỗ.
- **Log Usage Analytics (`httpRequest`):**
  - Node này dùng để ghi nhận log hệ thống hoặc gửi thống kê sử dụng (có thể tắt đi nếu không cần thiết).

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và thử nhắn tin cho Telegram Bot với cú pháp tìm việc để test dữ liệu trả về.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để bot chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp AI (OpenAI / Claude):** Thêm một node AI để phân tích mức độ phù hợp (matching score) giữa JD công việc và CV của các sếp trước khi gửi về Telegram.
- **Gửi thông báo qua Slack/Discord:** Ngoài Telegram, có thể cấu hình để bot bắn tin nhắn vào kênh tuyển dụng riêng của team.
- **Báo cáo định kỳ:** Tạo thêm một nhánh cron-job để tổng hợp các công việc tìm được trong tuần và gửi báo cáo tổng kết vào mỗi sáng thứ Hai.

### 📌 Kết luận
Việc tự động hóa quy trình tìm kiếm việc làm bằng Telegram Bot kết hợp n8n không chỉ giúp tiết kiệm thời gian tối đa mà còn mở ra khả năng xây dựng các ứng dụng AI/Automation cực kỳ thiết thực. Hãy "lên đồ" ngay hôm nay và tối ưu hóa quy trình của các sếp nhé!