---
title: "🚀 Quản lý và Tự động hóa Phân tích SMC Screener với n8n Forms & HTTP API"
description: "Hướng dẫn chi tiết cách sử dụng workflow n8n để tự động hóa toàn bộ quy trình quản lý bản ghi SMC Screener thông qua Form và API mà không cần code."
slug: "quan-ly-smc-screener-analyses-voi-n8n"
tags: [n8n, automation, smc-screener, trading-tools, api-integration, no-code]
keywords: [n8n workflow, smc screener api, tự động hóa trading, quản lý phân tích screener, n8n form trigger]
---

# 🚀 Quản lý và Tự động hóa Phân tích SMC Screener với n8n Forms & HTTP API

Các sếp làm trong lĩnh vực giao dịch (trading) hay phân tích kỹ thuật chắc chắn đã quá quen thuộc với việc thao tác thủ công trên nền tảng **SMC Screener**: từ việc tạo mới phân tích, cập nhật metadata, xem danh sách, cho đến việc xóa hay kiểm tra trạng thái hệ thống. Việc lặp đi lặp lại các thao tác này vừa mất thời gian vừa dễ xảy ra sai sót.

Workflow này sinh ra để giải quyết triệt để vấn đề đó! Nó cung cấp một giải pháp tự động hóa 100% không cần code, kết hợp giữa **n8n Form** thân thiện và **SMC Screener API**, giúp các sếp quản lý toàn bộ dữ liệu phân tích chỉ bằng vài cú click.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Quản lý tạo, sửa, xóa, xem danh sách bản ghi phân tích tự động qua giao diện Form hoặc API.
- **Tiết kiệm thời gian:** Thay vì thao tác thủ công từng bước trên web, nay chỉ cần điền form là hệ thống tự xử lý qua API.
- **An toàn và chính xác:** Các hành động nhạy cảm như xóa (Delete) hoặc dọn dẹp dữ liệu (Clear) đều có cơ chế xác thực an toàn (`confirm=true`).
- **Hoạt động liên tục:** Sẵn sàng kết nối và mở rộng với các công cụ khác như Google Sheets, Telegram, hoặc Slack.
:::

### Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **SMC Screener API Key:** Tài khoản SMC Screener và API Key tương ứng với các quyền (scopes) cần thiết như `analyses_read`, `analyses_create`, `analyses_edit`, `analyses_delete`, v.v.
:::

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy toàn bộ mã JSON từ nguồn.
- Mở n8n Editor, chọn **Add workflow** -> Nhấp vào biểu tượng menu (3 chấm) ở góc trên bên phải -> Chọn **Import from File** hoặc **Paste Workflow JSON**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm **25 nodes** được tối ưu hóa để xử lý đa dạng các tác vụ. Các sếp cần chú ý các node cốt lõi sau:

- **Node `SMC_Analysis_Form` (formTrigger):** Điểm vào chính qua giao diện n8n Form. Người dùng sẽ nhập `api_key` và chọn hành động (`action`) tại đây.
- **Node `Manual Test Payload` (code):** Dùng để test thủ công khi các sếp đang trong quá trình xây dựng và gỡ lỗi (debugging). Hãy thay thế `api_key` mẫu bằng API key thực tế của các sếp ở đây nếu chạy thử nghiệm.
- **Các node `HTTP Request` (`GET User Analyses`, `POST Create Analysis`, `PATCH Update Analysis`, `DELETE Analysis`, v.v.):** 
  - Trỏ tới base URL API: `https://api.smcscreener.com/api/v1`
  - Các sếp cần cấu hình Header để truyền API Key vào request (thường thông qua cấu hình Bearer Token hoặc Header tùy chỉnh theo tài liệu API của SMC Screener).
- **Node `Input Valid?` & `Action Router` (switch):** Đóng vai trò định tuyến luồng dữ liệu dựa trên hành động mà người dùng chọn trên Form (List, Get, Create, Update, Reanalyze, Clear, Delete, Runtime Status).

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng cách điền thông tin vào `Manual Test Payload` hoặc truy cập URL của `SMC_Analysis_Form`.
- Kiểm tra kết quả trả về ở các node tóm tắt (như `Build Create Summary`, `Build Analyses List Summary`,...).
- Sau khi test thành công, chuyển công tắc sang **Active** để đưa workflow vào vận hành chính thức 24/7.

---

### ✍️ Mẹo & gợi ý nâng cao
Để khai thác tối đa sức mạnh của workflow này, các sếp có thể mở rộng thêm:
1. **Tích hợp Telegram/Slack Bot:** Nhận thông báo trực tiếp mỗi khi một bản ghi phân tích được tạo thành công hoặc khi trạng thái runtime có sự thay đổi.
2. **Đồng bộ với Google Sheets:** Thay vì chỉ dùng Form, các sếp có thể kết nối thêm Google Sheets trigger để tự động tạo hàng loạt phân tích từ bảng tính.
3. **Quản lý Log lỗi:** Thêm node Error Trigger để bắt các lỗi API (ví dụ: `analysisnotfound` hoặc lỗi thiếu quyền hạn) và gửi cảnh báo về email hoặc nhóm chat.

---

### 📌 Kết luận
Workflow **Manage SMC Screener analyses with n8n forms and HTTP API** là một cỗ máy tự động hóa cực kỳ gọn gàng và mạnh mẽ cho cộng đồng trader và automation builder. Hãy áp dụng ngay để tối ưu hóa quy trình làm việc với SMC Screener của các sếp!