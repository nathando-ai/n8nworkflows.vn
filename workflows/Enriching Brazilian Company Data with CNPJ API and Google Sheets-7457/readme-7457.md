---
title: "🚀 Tự động làm giàu dữ liệu doanh nghiệp Brazil bằng CNPJ API và Google Sheets"
description: "Hướng dẫn xây dựng workflow n8n tự động lấy dữ liệu hơn 40 trường thông tin doanh nghiệp Brazil từ mã CNPJ qua MinhaReceita API và cập nhật trực tiếp vào Google Sheets."
slug: "tu-dong-lam-giau-du-lieu-doanh-nghiep-brazil-cnpj-api-google-sheets"
tags: [n8n, automation, google-sheets, api, lead-generation]
keywords: [n8n workflow, tự động hóa dữ liệu, CNPJ API, Google Sheets automation, MinhaReceita]
---

# 🚀 Tự động làm giàu dữ liệu doanh nghiệp Brazil bằng CNPJ API và Google Sheets

Các sếp làm trong lĩnh vực B2B hay Sales tại thị trường Brazil chắc chắn hiểu rõ nỗi đau khi phải tra cứu thủ công từng mã số thuế (CNPJ) trên trang của Cơ quan Thuế liên bang. Việc này không chỉ tốn hàng giờ đồng hồ copy-paste mà còn cực kỳ dễ nhầm lẫn, khiến đội ngũ sales chậm trễ trong việc tiếp cận khách hàng tiềm năng.

Đừng lo, bài toán này sẽ được giải quyết 100% tự động với workflow n8n siêu việt này! Workflow giúp tự động quét danh sách mã CNPJ từ Google Sheets, gọi API lấy toàn bộ hơn 40 trường thông tin chính thức (bao gồm trạng thái hoạt động, mã IBGE, ngành nghề...) và tự động điền ngược lại Google Sheets, sau đó gửi thông báo qua Telegram khi hoàn tất.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Xử lý hàng loạt hàng trăm mã CNPJ chỉ trong vài phút mà không cần thao tác tay.
- **Dữ liệu chính xác, cập nhật:** Lấy nguồn dữ liệu chính thống qua API `MinhaReceita.org` hoàn toàn miễn phí, không cần key xác thực phức tạp.
- **Cập nhật thông minh:** Chỉ quét và xử lý các dòng còn trống cột `razao_social`, tránh gọi API trùng lặp.
- **Theo dõi thời gian thực:** Nhận thông báo tự động qua Telegram ngay khi tiến trình hoàn tất.
:::

### Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Cloud hoặc Self-hosted).
- Google Sheets chứa sẵn danh sách mã CNPJ cần làm giàu dữ liệu.
- Tài khoản Telegram và Bot Token để nhận thông báo (tùy chọn).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể lấy mã JSON của workflow từ nguồn gốc (ID: 7457) trên trang n8n workflows, sau đó copy và paste trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần chú ý cấu hình các node sau:
- **Node `Settings` (Set):** Cấu hình lại biến `Telegram ID` và kiểm tra `API URL` (đã được trỏ sẵn đến `MinhaReceita.org`).
- **Node `Get All CNPJs in Sheet` & `Update CNPJ Info in Sheet` (Google Sheets):** 
  - Kết nối tài khoản Google Sheets thông qua `Google Sheets OAuth2 API`.
  - Trỏ đúng đến file Google Sheet và Sheet Name của các sếp. Đảm bảo có cột chứa mã CNPJ và cột `razao_social` để bộ lọc hoạt động.
- **Node `Send API Request` (HTTP Request):** API `minhaReceita.org/{cnpj}` hoàn toàn miễn phí và không yêu cầu xác thực, các sếp chỉ cần map đúng biến CNPJ vào đường dẫn.
- **Node `Notify When Finish` (Telegram):** Kết nối `Telegram API` (Bot Token) và điền đúng Chat ID của các sếp để nhận thông báo báo cáo kết quả.

#### 3. Kích hoạt ⚡️
- Bấm nút **Execute Workflow Manually** để chạy thử với vài dòng dữ liệu mẫu đầu tiên.
- Kiểm tra kết quả trên Google Sheets và Telegram.
- Sau khi mọi thứ chạy trơn tru, hãy bật công tắc **Active** để workflow tự động hóa hoạt động.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng thông báo:** Thay vì chỉ báo cáo khi hoàn thành, các sếp có thể tích hợp thêm Slack hoặc Discord để team Sales cùng theo dõi tiến độ lead được làm giàu.
- **Lưu Log lỗi:** Thêm nhánh xử lý lỗi (Error Trigger) để ghi nhận các mã CNPJ không hợp lệ hoặc lỗi kết nối API vào một sheet riêng biệt.
- **Tự động hóa theo lịch:** Thay thế node `Execute Workflow Manually` bằng `Schedule Trigger` để hệ thống tự động quét và cập nhật dữ liệu hàng tuần/hàng tháng.

### 📌 Kết luận
Việc làm giàu dữ liệu doanh nghiệp chưa bao giờ dễ dàng và tiết kiệm chi phí đến thế. Hãy áp dụng ngay template này vào quy trình Sales & Marketing của các sếp để tối ưu hóa hiệu suất làm việc ngay hôm nay!