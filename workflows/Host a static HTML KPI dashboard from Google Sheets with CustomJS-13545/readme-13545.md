---
title: "🚀 Tự động hóa tạo và host Static HTML KPI Dashboard từ Google Sheets bằng n8n & CustomJS"
description: "Hướng dẫn cấu hình workflow n8n giúp tự động lấy dữ liệu KPI từ Google Sheets, biên dịch thành trang HTML tĩnh trực quan và host trực tiếp lên CustomJS."
slug: "host-static-html-kpi-dashboard-google-sheets-customjs"
tags: [n8n, automation, customjs, google-sheets, dashboard, no-code]
keywords: [n8n workflow, kpi dashboard google sheets, customjs html host, tự động hóa kpi, n8n viet nam]
keywords: [n8n workflow, kpi dashboard google sheets, customjs html host, tự động hóa kpi, n8n viet nam]
---

# 🚀 Tự động hóa tạo và host Static HTML KPI Dashboard từ Google Sheets bằng n8n & CustomJS

Các sếp có bao giờ cảm thấy mệt mỏi mỗi tuần phải thủ công copy dữ liệu từ Google Sheets, vẽ biểu đồ báo cáo KPI rồi gửi qua email hay chat? Việc này không chỉ tốn thời gian mà còn dễ sai sót, thiếu đi sự chuyên nghiệp khi sếp lớn hoặc khách hàng cần theo dõi số liệu real-time.

Giải pháp là đây! Workflow n8n này sẽ tự động hóa từ A-Z: lấy dữ liệu từ Google Sheets, biến nó thành một trang Dashboard HTML tĩnh cực kỳ bắt mắt (có biểu đồ Chart.js, thẻ KPI cards) và host trực tiếp lên [CustomJS](https://www.customjs.space) để tạo thành một trang web live có thể chia sẻ ngay lập tức. Không cần code, không cần đau đầu setup server phức tạp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 100%:** Hàng tuần số liệu tự làm mới mà không cần chạm tay vào.
- **Dashboard chuyên nghiệp:** Biến các con số khô khan trong bảng tính thành biểu đồ trực quan, sinh động.
- **Chia sẻ dễ dàng:** Có ngay một link web tĩnh (Live URL) để gửi cho team hoặc cấp trên xem bất cứ lúc nào.
- **Tiết kiệm chi phí:** Tận dụng CustomJS để host miễn phí/giá rẻ mà không cần mua hosting riêng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n (Self-hosted khuyến nghị).
- Tài khoản và API Key từ [CustomJS](https://www.customjs.space).
- Google Sheets chứa dữ liệu KPI (được chia sẻ công khai hoặc cấp quyền cho n8n).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow này, vào n8n editor, chọn **New Workflow**, nhấn tổ hợp `Ctrl + V` (hoặc `Cmd + V`) để dán toàn bộ các node vào màn hình làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần chú ý cấu hình các node cốt lõi sau:

- **Schedule Trigger / When clicking ‘Execute workflow’**: Quyết định thời gian tự động chạy (ví dụ: Chạy hàng tuần vào sáng thứ Hai) hoặc chạy thủ công bằng cơm.
- **Get Data From Sheet (HTTP Request / Google Sheets)**: 
  - Kết nối tới file Google Sheets mẫu [tại đây](https://docs.google.com/spreadsheets/d/10mj6hngkPTg1_A6bVNn8QfKujap6j-Lrt_LwAkY2d7Q/edit?usp=sharing).
  - Đảm bảo endpoint hoặc credential lấy dữ liệu từ sheet trả về cấu trúc JSON chuẩn dạng:
    ```json
    [
      {"Date":"2026-02-01","Channel":"Google Ads","Visitors":1200,"Leads":95,"Demo Booked":40,"Proposal Sent":22,"Won":9},
      {"Date":"2026-02-01","Channel":"LinkedIn","Visitors":800,"Leads":70,"Demo Booked":28,"Proposal Sent":16,"Won":7}
    ]
    ```
- **HTML (Node)**: Xử lý template HTML, nhúng dữ liệu JSON vào các thành phần giao diện, biểu đồ (Chart.js) để tạo nên một Dashboard hoàn chỉnh.
- **Upload new HTML Page / Get HTML Pages / Update existing HTML Page (CustomJS PDF Toolkit)**:
  - Chọn hoặc tạo mới **Credentials** cho `customJsApi`.
  - Nhập API Key của sếp vào đây để n8n có quyền đẩy (push) trang HTML lên hệ thống lưu trữ của CustomJS.
- **Convert HTML to PDF & Extract from File / Filter / If / Aggregate**: Các node phụ trợ dùng để lọc dữ liệu, xử lý logic điều kiện (nếu trang đã tồn tại thì update, chưa có thì tạo mới) hoặc tùy chọn xuất file PDF báo cáo dự phòng.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Test Step** hoặc **Execute Workflow** ở từng node để kiểm tra xem dữ liệu có chảy qua mượt mà hay không.
- Sau khi test thành công, gạt công tắc **Active** ở góc trên bên phải để n8n tự động vận hành theo lịch hẹn.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node Telegram hoặc Slack ở cuối workflow để bắn ngay link trang Dashboard vừa update vào nhóm chat cho team cùng nắm tình hình.
- **Lưu trữ lịch sử:** Kết hợp thêm node Google Drive hoặc một database riêng để lưu trữ các bản backup HTML theo từng tuần phục vụ việc so sánh xu hướng (historical trends).
- **Custom Domain:** Trỏ một tên miền riêng của công ty vào CustomJS để Dashboard trông chuyên nghiệp và uy tín hơn nữa.

### 📌 Kết luận
Việc tự động hóa báo cáo KPI chưa bao giờ dễ dàng và chuyên nghiệp đến thế. Chỉ với vài bước cấu hình trên n8n kết hợp cùng CustomJS, các sếp đã có ngay một hệ thống dashboard tĩnh xịn sò chạy tự động hoàn toàn. Lên đồ và áp dụng ngay cho doanh nghiệp của mình thôi nào các sếp ơi!