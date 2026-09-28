---
title: "🚀 Tự động hóa báo cáo tài chính hàng tháng với Google Gemini AI, SQL và Outlook"
description: "Hướng dẫn xây dựng workflow n8n tự động kết nối cơ sở dữ liệu MySQL, phân tích dữ liệu tài chính bằng Google Gemini AI và gửi báo cáo chuyên nghiệp qua Microsoft Outlook."
slug: "tu-dong-hoa-bao-cao-tai-chinh-hang-thang-gemini-ai-sql-outlook"
tags: [n8n, automation, ai, finance, google-gemini, microsoft-outlook, sql]
keywords: [n8n workflow, tự động hóa tài chính, báo cáo tài chính tự động, google gemini ai, mysql n8n, microsoft outlook automation]
---

# 🚀 Tự động hóa báo cáo tài chính hàng tháng với Google Gemini AI, SQL và Outlook

Việc tổng hợp dữ liệu tài chính, làm báo cáo lãi lỗ (P&L), phân tích chỉ số nhân sự và dự án vào cuối mỗi tháng luôn là "nỗi ám ảnh" tốn rất nhiều thời gian của các bộ phận kế toán và quản lý. Việc làm thủ công rất dễ xảy ra sai sót, chậm trễ trong việc đưa ra quyết định kinh doanh.

Workflow n8n tuyệt vời này do chuyên gia **Amjid Ali** phát triển sẽ giải quyết triệt để bài toán trên bằng cách tự động hóa 100 từ khâu truy vấn dữ liệu cơ sở dữ liệu (MySQL), phân tích đa chiều bằng **Google Gemini AI**, cho đến việc xuất báo cáo HTML và gửi email tự động qua **Microsoft Outlook** vào ngày mùng 5 hàng tháng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Không cần can thiệp thủ công, báo cáo được kích hoạt tự động vào ngày 5 hàng tháng.
- **Phân tích thông minh bằng AI:** Google Gemini AI đóng vai trò như một chuyên gia tài chính (Financial Analyst), tự động viết tóm tắt điều hành (Executive Summary) và đưa ra các khuyến nghị tối ưu chi phí.
- **Báo cáo trực quan, chuyên nghiệp:** Tổng hợp dữ liệu từ nhiều nguồn (P&L, Dự án, Nhân sự) thành một bảng HTML đẹp mắt, sẵn sàng gửi đi.
- **Cá nhân hóa theo từng bộ phận:** Tự động tách và gửi báo cáo riêng biệt cho từng Trung tâm chi phí (Cost Center) hoặc phòng ban.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và thông tin sau:
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **Cơ sở dữ liệu MySQL (hoặc ERP/SQL tương đương):** Chứa dữ liệu kế toán, nhân sự, dự án, ngân sách.
- **Google Gemini API Key:** Để kết nối với node LangChain Google Gemini Chat Model.
- **Tài khoản Microsoft Outlook (OAuth2):** Để cấu hình gửi email báo cáo tự động.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc sao chép mã JSON từ nguồn cấp.
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File** (hoặc dùng tổ hợp phím `Ctrl+V` để dán trực tiếp vào canvas).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 27 nodes được thiết kế mạch lạc, các sếp cần chú ý cấu hình kỹ các điểm sau:
- **Schedule Trigger:** Mặc định được đặt lịch chạy vào ngày mỏng 5 hàng tháng. Các sếp có thể điều chỉnh lại mốc thời gian tùy nhu cầu doanh nghiệp.
- **Các node MySQL (YTD vs Prevoius Month1, Get Cost Centers with Budgets, Employees, Departments, Projects):** 
  - Cần tạo credentials kết nối tới cơ sở dữ liệu MySQL của doanh nghiệp.
  - Điều chỉnh lại cấu trúc câu lệnh SQL nếu bảng dữ liệu (schema) của doanh nghiệp khác với thiết kế gốc (có thể dùng ChatGPT để hỗ trợ viết lại câu lệnh SQL tương ứng).
- **Business Performance AI Agent (Analyst) & Google Gemini Chat Model:** 
  - Nhập Google Gemini API Key vào credentials của node Chat Model.
  - Tinh chỉnh Prompt bên trong Agent nếu muốn AI phân tích theo văn phong hoặc trọng tâm cụ thể của công ty.
- **Microsoft Outlook2:** 
  - Kết nối tài khoản Microsoft Outlook thông qua OAuth2 để cấp quyền gửi email tự động.
  - Cấu hình địa chỉ email nhận (người quản lý, giám đốc tài chính...).

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (**Test Workflow**) bằng cách click vào **Execute Workflow** để kiểm tra dữ liệu từ MySQL chảy qua các node có bị lỗi hay không.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để workflow tự động vận hành.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh thông báo phụ:** Ngoài Microsoft Outlook, các sếp có thể thêm node Telegram hoặc Slack để gửi thông báo nhanh tóm tắt báo cáo về group chat nội bộ công ty.
- **Lưu lịch sử báo cáo:** Bổ sung thêm một node Google Sheets hoặc ghi vào Database lưu lại log của mỗi lần gửi báo cáo để tiện tra cứu về sau.
- **Mở rộng nguồn dữ liệu:** Nếu không dùng MySQL, các sếp hoàn toàn có thể thay thế bằng Google Sheets, Airtable, hoặc file Excel trên Google Drive theo đúng chuẩn cấu trúc dữ liệu đầu ra là chạy mượt mà.

### 📌 Kết luận
Workflow "Generate Monthly Financial Reports with Gemini AI, SQL, and Outlook" là một siêu phẩm tự động hóa giúp giải phóng hoàn toàn sức lao động cho đội ngũ tài chính kế toán. Hãy ứng dụng ngay để nâng tầm chuyên nghiệp và tốc độ ra quyết định dựa trên dữ liệu thời gian thực cho doanh nghiệp của các sếp!