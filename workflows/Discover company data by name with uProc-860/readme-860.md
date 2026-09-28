---
title: "🚀 Tự Động Tra Cứu Thông Tin Công Ty Bằng Tên Với uProc trong n8n"
description: "Hướng dẫn chi tiết cách xây dựng workflow n8n tự động hóa việc tìm kiếm, tra cứu và xác thực dữ liệu doanh nghiệp từ tên công ty sử dụng dịch vụ uProc."
slug: "tu-dong-tra-cuu-thong-tin-cong-ty-voi-uproc-trong-n8n"
tags: [n8n, automation, no-code, sales, data-enrichment, uproc]
keywords: [n8n workflow, tra cứu thông tin công ty, uProc n8n, data enrichment, tự động hóa bán hàng]
---

# 🚀 Tự Động Tra Cứu Thông Tin Công Ty Bằng Tên Với uProc

Các sếp làm trong lĩnh vực Sales, B2B hay Marketing chắc hẳn đã quá quen thuộc với nỗi đau: Có trong tay một danh sách dài tên công ty, nhưng lại thiếu hoàn toàn các thông tin chi tiết như website, quy mô, địa chỉ hay mã số thuế để tiếp cận. Việc ngồi tra cứu thủ công từng công ty trên Google vừa tốn hàng tá thời gian, vừa dễ xảy ra sai sót.

Giải pháp là gì? Hãy để n8n và uProc "gánh" thay các sếp! Workflow này sẽ tự động hóa hoàn toàn quy trình nhận diện và làm giàu dữ liệu doanh nghiệp (Data Enrichment) chỉ bằng một cái tên đơn giản.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không còn cảnh tra cứu thủ công từng công ty một cách mệt mỏi.
- **Dữ liệu chính xác cao:** Khai thác thông tin doanh nghiệp chuẩn xác từ hệ thống tích hợp uProc.
- **Tự động phân loại:** Dễ dàng kiểm tra xem thông tin công ty có tồn tại hay không để có hướng xử lý tiếp theo trong luồng làm việc.
- **Vận hành linh hoạt:** Dễ dàng tích hợp tiếp vào CRM, Google Sheets hoặc gửi thông báo qua Slack/Telegram.
:::

### 📦 Các Nodes sử dụng trong Workflow
Workflow tinh gọn này chỉ bao gồm 4 nodes chính được tối ưu hóa:
1. **On clicking 'execute' (`manualTrigger`):** Khởi chạy thủ công để test dữ liệu hoặc bắt đầu quy trình.
2. **Create Company Item (`functionItem`):** Chuẩn bị và định dạng tên công ty đầu vào để gửi đi truy vấn.
3. **Get Company by Name (`uproc`):** Gọi API uProc để tìm kiếm và trích xuất dữ liệu chi tiết của doanh nghiệp.
4. **Company Found? (`if`):** Kiểm tra xem uProc có tìm thấy kết quả phù hợp hay không để rẽ nhánh xử lý.

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống n8n đang hoạt động (Cloud hoặc Self-hosted).
- Tài khoản [uProc](https://uproc.io/) và API Key tương ứng để cấu hình credentials (`uprocApi`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Sao chép mã JSON của workflow hoặc tải file JSON từ nguồn gốc.
- Trong giao diện n8n Editor, chọn **Add workflow** -> Nhấp vào biểu tượng menu (3 chấm) ở góc trên bên phải -> **Import from File** hoặc **Import from Clipboard** và dán mã JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node `Create Company Item` (`functionItem`):** 
  - Tại đây, các sếp cần cấu hình tên công ty đầu vào mà mình muốn tra cứu (ví dụ: thay đổi giá trị biến công ty thành tên công ty thực tế cần tìm).
- **Node `Get Company by Name` (`uproc`):** 
  - Cần kết nối tài khoản uProc bằng cách thêm **Credentials** (`uprocApi`). Lấy API Key từ tài khoản uProc của các sếp và dán vào n8n.
  - Chọn đúng phương thức/dịch vụ tìm kiếm công ty theo tên trong cấu hình node.
- **Node `Company Found?` (`if`):** 
  - Kiểm tra điều kiện logic trả về từ uProc (ví dụ: `{{ $json.found }}` hoặc `{{ $json.name }}` có tồn tại hay không) để chuyển hướng luồng dữ liệu sang nhánh "True" (Đã tìm thấy) hoặc "False" (Không tìm thấy).

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** để chạy thử nghiệm với dữ liệu mẫu và kiểm tra kết quả trả về ở từng node.
- Nếu mọi thứ hoạt động trơn tru, hãy chuyển trạng thái workflow sang **Active** để sẵn sàng đưa vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa quy trình kinh doanh, các sếp có thể mở rộng workflow này bằng cách:
- **Kết nối Google Sheets / Airtable:** Tự động đọc danh sách tên công ty từ file Google Sheets và ghi ngược lại thông tin chi tiết (website, địa chỉ, lĩnh vực) sau khi uProc trả về kết quả.
- **Tích hợp CRM:** Đẩy thẳng dữ liệu công ty tìm được vào HubSpot, Pipedrive hoặc Salesforce để đội ngũ Sales tiến hành outreach ngay lập tức.
- **Xử lý nhánh lỗi (False):** Thêm node gửi thông báo qua Telegram hoặc Slack khi hệ thống không tìm thấy thông tin công ty để nhân sự kiểm tra lại tên đầu vào.

### 📌 Kết luận
Tự động hóa việc tra cứu dữ liệu doanh nghiệp chưa bao giờ dễ dàng đến thế với sự kết hợp giữa n8n và uProc. Hãy áp dụng ngay vào quy trình của các sếp để giải phóng sức lao động thủ công và bứt phá doanh số ngay hôm nay!