---
title: "🚀 Tự động hóa quét dữ liệu tuyển dụng từ LinkedIn và Indeed với n8n và Bright Data"
description: "Hướng dẫn xây dựng workflow n8n tự động cào dữ liệu việc làm từ LinkedIn và Indeed thông qua Bright Data API, sau đó tổng hợp và lưu trữ trực tiếp vào Google Sheets."
slug: "tu-dong-hoa-quet-du-lieu-tuyen-dung-linkedin-indeed-n8n"
tags: [n8n, automation, no-code, hr, scraping, bright-data, google-sheets]
keywords: [n8n workflow, cào dữ liệu việc làm, tuyển dụng tự động, linkedin scraping, indeed scraping, bright data, google sheets automation]
---

# 🚀 Tự động hóa quét dữ liệu tuyển dụng từ LinkedIn và Indeed với n8n

Việc nghiên cứu thị trường lao động, tổng hợp dữ liệu tuyển dụng cho các chiến dịch Headhunting, hoặc phân tích xu hướng nghề nghiệp thủ công đang ngốn rất nhiều thời gian của các HR team. Các sếp thường phải mất hàng giờ lướt LinkedIn hay Indeed, copy-paste thông tin vào file Excel một cách nhàm chán.

Giải pháp là đây! Workflow n8n này sẽ tự động hóa toàn bộ quy trình: nhận yêu cầu tìm kiếm từ biểu mẫu (Form), kích hoạt cào dữ liệu đa nền tảng (LinkedIn & Indeed) thông qua **Bright Data API**, kiểm tra trạng thái xử lý bất đồng bộ, gộp kết quả và lưu trữ gọn gàng vào **Google Sheets**. Mọi thứ diễn ra hoàn toàn tự động 100% không cần code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa đa nền tảng:** Thu thập dữ liệu việc làm đồng thời từ cả hai "ông lớn" LinkedIn và Indeed chỉ với một cú click gửi form.
- **Xử lý bất đồng bộ thông minh:** Sử dụng cơ chế Check Status & Wait thông minh để đảm bảo dữ liệu từ API bên thứ ba được trả về đầy đủ trước khi tiến hành bước tiếp theo.
- **Tập trung một nơi:** Tự động hợp nhất (Merge) kết quả và đổ thẳng vào Google Sheets theo định dạng chuẩn, sẵn sàng để phân tích hoặc báo cáo.
- **Tiết kiệm 95% thời gian:** Giải phóng đội ngũ nhân sự khỏi các tác vụ tay chân lặp đi lặp lại.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản Bright Data:** Cần có API Key và cấu hình Dataset/Scraper cho Indeed và LinkedIn.
- **Google Sheets:** Tài khoản Google kết nối qua OAuth2 để lưu trữ dữ liệu việc làm.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này hoặc tải file JSON từ n8n.io (ID: 6371), sau đó dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 16 nodes hoạt động nhịp nhàng, các sếp cần lưu ý cấu hình kỹ các điểm sau:
- **Triggers workflow from job search form (`formTrigger`):** Tạo form đầu vào để người dùng điền các thông tin tìm kiếm như Chức danh (Job Title), Thành phố (City), Quốc gia (Country), Loại công việc (Job Type).
- **Formats form input for Bright Data Indeed API1 (`code`):** Node code JavaScript này giúp chuẩn hóa định dạng dữ liệu đầu vào từ Form thành payload chuẩn mà Bright Data API yêu cầu.
- **Triggers job scraping on Indeed/LinkedIn (`httpRequest`):** Cần cấu hình Header chứa API Token/Key của dịch vụ **Bright Data** cho các node gọi API cào dữ liệu.
- **Checks if Bright Data has completed... (`httpRequest` & `if` & `wait`):** Các node này tạo vòng lặp kiểm tra trạng thái snapshot từ Bright Data. Nếu dữ liệu chưa sẵn sàng (`Is Indeed/LinkedIn data ready?` trả về false), workflow sẽ tạm dừng 1 phút (`wait`) rồi kiểm tra lại.
- **Combines Indeed + LinkedIn job results (`merge`):** Gộp dữ liệu công việc từ hai nguồn lại với nhau.
- **Saves final job list to Google Sheet (`googleSheets`):** 
  - Kết nối tài khoản Google Sheets thông qua `googleSheetsOAuth2Api`.
  - Sử dụng template Google Sheets chuẩn tại đây để tránh lỗi khớp cột: [Make A Copy Of This Sheet](https://docs.google.com/spreadsheets/d/1FmjpyNjus0tdN9hU9e-EsFcKl-W4EdWq1PYfIvGu8Ws/edit?gid=0#gid=0).
  - Chọn đúng Sheet đích (mặc định là tab "Compare") và chọn operation là **Append**.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng cách điền form mẫu để kiểm tra toàn bộ luồng dữ liệu chạy từ đầu đến cuối.
- Sau khi test thành công, bật công tắc **Active** ở góc trên cùng bên phải để đưa workflow vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Thêm node Telegram hoặc Slack vào cuối luồng để bắn thông báo ngay về nhóm chat khi quét xong danh sách việc làm mới.
- **Lọc dữ liệu thông minh:** Thêm node `IF` hoặc `Code` sau bước Merge để lọc bớt các job trùng lặp hoặc không đạt yêu cầu trước khi đẩy vào Google Sheets.
- **Lên lịch định kỳ:** Thay vì dùng Form Trigger, các sếp có thể đổi thành `Schedule Trigger` để hệ thống tự động cào dữ liệu thị trường việc làm mỗi tuần/mỗi tháng một cách tự động.

### 📌 Kết luận
Với workflow n8n kết hợp Bright Data này, việc thu thập dữ liệu tuyển dụng quy mô lớn chưa bao giờ dễ dàng đến thế. Hãy triển khai ngay hôm nay để tối ưu hóa quy trình làm việc cho team HR của các sếp nhé!