---
title: "🚀 Tự động trích xuất hóa đơn vào Google Sheets bằng Ainoflow và ChatGPT"
description: "Hướng dẫn xây dựng workflow n8n tự động đọc hóa đơn từ Gmail, phân tích bằng AI (OpenAI/OpenRouter + Ainoflow) và lưu trữ dữ liệu vào Google Sheets 100% không cần code."
slug: "tu-dong-trich-xuat-hoa-don-google-sheets-ainoflow-chatgpt"
tags: [n8n, automation, invoice-processing, openai, google-sheets, ai]
keywords: [n8n workflow, tự động hóa hóa đơn, trích xuất hóa đơn ai, google sheets automation, ainoflow chatgpt]
---

# 🚀 Tự động trích xuất hóa đơn vào Google Sheets bằng Ainoflow và ChatGPT

Các sếp có đang mệt mỏi mỗi cuối tháng khi phải ngồi "soi" từng tờ hóa đơn PDF gửi qua email, gõ thủ công từng con số, tên công ty, tiền thuế vào file Excel hay Google Sheets không? Công việc nhàm chán này không chỉ ngốn hàng giờ đồng hồ mà còn rất dễ dẫn đến sai sót số liệu.

Đừng lo, bài viết này sẽ hướng dẫn các sếp cách "lên đồ" một workflow n8n cực kỳ xịn sò giúp tự động hóa từ A-Z quy trình xử lý hóa đơn: Tự động quét Gmail, dùng AI (Ainoflow kết hợp ChatGPT) đọc hiểu hóa đơn, trích xuất dữ liệu chuẩn chỉnh và tự động lưu vào Google Sheets, đồng thời gửi thông báo kết quả. Tất cả diễn ra tự động 100% mà không tốn một giọt mồ hôi thủ công nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn cảnh nhập liệu thủ công, AI sẽ lo phần đọc hiểu hóa đơn trong vài giây.
- **Độ chính xác cao:** Tránh tối đa các lỗi do con người đánh máy nhầm số tiền, mã số thuế.
- **Tự động hóa toàn diện:** Từ lúc hóa đơn chui vào Gmail đến khi nằm gọn trong Google Sheets và gửi email thông báo đều chạy ngầm tự động.
- **Quản lý thông minh:** Dữ liệu được đồng bộ hóa tập trung, dễ dàng tra cứu báo cáo tài chính bất cứ lúc nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **Tài khoản Google:** Google Sheets (đã tạo sẵn file lưu hóa đơn) và Gmail API credentials.
- **Ainoflow Account:** Tài khoản dịch vụ Ainoflow để xử lý chuyển đổi tài liệu (`@ainoflow/n8n-nodes-ainoflow.ainoflowConvert`).
- **AI API Keys:** OpenAI API Key hoặc OpenRouter API Key để cấp quyền cho các model AI phân tích dữ liệu hóa đơn.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow (hoặc tải file từ nguồn gốc) và dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 20 nodes phối hợp nhịp nhàng. Các sếp cần chú ý cấu hình kỹ các điểm sau:

- **Schedule Trigger:** Cấu hình lịch chạy tự động quét email (ví dụ: chạy mỗi giờ hoặc mỗi ngày một lần tùy nhu cầu).
- **Get invoice & Send a message / Invoice Repeat / Success / Move invoice / Remove label (Gmail Nodes):** Kết nối tài khoản Gmail của sếp. Cấu hình nhãn (Label) hoặc từ khóa tìm kiếm email chứa hóa đơn, cũng như thiết lập email gửi thông báo khi xử lý thành công hoặc thất bại.
- **Convert (`@ainoflow/n8n-nodes-ainoflow.ainoflowConvert`):** Kết nối tài khoản Ainoflow để chuyển đổi định dạng tệp hóa đơn đầu vào (PDF/ảnh) sang dạng dữ liệu tối ưu cho AI đọc.
- **OpenAI Chat Model / OpenRouter Chat Model & Invoice to JSON (Agent):** Nhập API Key hợp lệ. Viết prompt hướng dẫn AI trong Agent node cách nhận diện các trường thông tin trên hóa đơn (như Tổng tiền, Mã số thuế, Tên nhà cung cấp, Ngày tháng...).
- **Get row(s) in sheet & Append row in sheet (Google Sheets):** Kết nối tài khoản Google của sếp, chọn đúng file Spreadsheet và Sheet name để ghi dữ liệu đã trích xuất vào bảng tính.
- **Stop and Error:** Thiết lập hành động khi workflow gặp sự cố (ví dụ: hóa đơn mờ không đọc được) để hệ thống gửi email báo lỗi hoặc dừng an toàn.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** với một email hóa đơn mẫu để test xem dữ liệu có chạy xuyên suốt từ Gmail qua AI và nhảy đẹp đẽ vào Google Sheets hay không.
- Nếu mọi thứ mượt mà, hãy gạt công tắc sang **Active** để hệ thống tự động chạy 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Thay vì chỉ gửi email qua Gmail node, các sếp có thể nối thêm node Telegram hoặc Slack để nhận thông báo tức thì ngay trên điện thoại mỗi khi có hóa đơn mới được xử lý thành công.
- **Lưu log lỗi thông minh:** Kết nối nhánh lỗi (`Stop and Error`) vào một bảng Google Sheets riêng biệt để dễ dàng kiểm tra lại các hóa đơn bị lỗi định dạng hoặc AI không đọc được.
- **Tự động phân loại thư mục:** Sử dụng các Gmail node bổ sung để tự động chuyển hóa đơn đã xử lý sang một nhãn (Label) "Đã thanh toán" hoặc "Đã lưu trữ" trong Gmail giúp hòm thư luôn gọn gàng.

### 📌 Kết luận
Việc tự động hóa quy trình xử lý hóa đơn với n8n, Ainoflow và ChatGPT chính là bước tiến đầu tiên giúp doanh nghiệp của các sếp tiến lên thời kỳ chuyển đổi số tinh gọn, tiết kiệm chi phí nhân sự tối đa. Lên đồ ngay thôi các sếp ơi!