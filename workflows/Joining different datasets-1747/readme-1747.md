---
title: "🚀 Hướng dẫn kết hợp dữ liệu thông minh trong n8n với Merge Node (Dataset Joining)"
description: "Khám phá cách sử dụng Merge Node trong n8n để kết hợp, hợp nhất và lọc dữ liệu từ nhiều nguồn khác nhau tương tự như các câu lệnh SQL Joins."
slug: "ket-hop-du-lieu-trong-n8n-merge-node"
tags: [n8n, automation, no-code, data-integration, merge-node, sql-joins]
keywords: [n8n workflow, kết hợp dữ liệu, merge node n8n, sql join trong n8n, tự động hóa dữ liệu]
---

# 🚀 Hướng dẫn kết hợp dữ liệu thông minh trong n8n với Merge Node

Các sếp có bao giờ gặp khó khăn khi phải lấy dữ liệu từ hai nguồn khác nhau (như Database, Google Sheets, API) rồi hì hục viết code hoặc dùng Excel phức tạp để ghép nối chúng lại không? Việc xử lý dữ liệu thủ công này không chỉ tốn thời gian mà còn dễ dẫn đến sai sót, nhầm lẫn thông tin.

Giải pháp ở đây chính là **n8n Workflow: Joining different datasets** do tác giả Jonathan xây dựng. Workflow này sẽ giúp các sếp làm chủ hoàn toàn **Merge Node** – một trong những node mạnh mẽ nhất của n8n, hoạt động linh hoạt hệt như các câu lệnh **SQL Joins** (Inner Join, Left Join, Union All) nhưng hoàn toàn không cần viết code phức tạp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Nắm vững kỹ thuật xử lý dữ liệu nâng cao:** Hiểu rõ cách dùng Merge Node để kết hợp, làm giàu và lọc dữ liệu.
- **Mô phỏng SQL Joins trực quan:** Dễ dàng áp dụng các logic Left Join, Inner Join, Union All mà không cần biết lập trình cơ sở dữ liệu.
- **Tối ưu hóa quy trình tự động hóa:** Giúp các luồng tích hợp dữ liệu đa nguồn chạy mượt mà, chính xác và tự động 100%.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống **n8n** đang hoạt động (phiên bản Cloud hoặc Self-hosted).
- Workflow này hoàn toàn chạy độc lập bằng dữ liệu mẫu (mock data) thông qua các node `Code` và `Manual Trigger`, không đòi hỏi kết nối API hay tài khoản bên thứ ba nào phức tạp.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này hoặc copy toàn bộ mã JSON từ [link nguồn chính thức](https://n8n.io/workflows/1747).
- Trong giao diện n8n Editor, tạo một workflow mới, chọn mục menu và dán (Paste) đoạn JSON vào, hoặc import trực tiếp file.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này được thiết kế dưới dạng một "phòng thí nghiệm" trực quan để các sếp khám phá 3 cách kết hợp dữ liệu phổ biến nhất thông qua các node sau:

- **Left Join (Enriching Data):** 
  - Sử dụng các node: `A. Ingredients`, `B. Recipe quantities` và `Merge recipe`.
  - **Tác dụng:** Thêm số lượng cần thiết vào từng nguyên liệu trong công thức (tương tự SQL Left Join), giữ lại toàn bộ dữ liệu từ nhánh A và bổ sung thông tin khớp từ nhánh B.
- **Inner Join (Filtering Data):** 
  - Sử dụng các node: `A. Ingredients Needed`, `B. Ingredients in stock` và `Ingredients in stock from recipe`.
  - **Tác dụng:** Chỉ giữ lại các nguyên liệu cần thiết mà hiện đang có sẵn trong kho (tương tự SQL Inner Join).
- **Union All (Combining Datasets):** 
  - Sử dụng các node: `A. Queen`, `B. Led Zeppelin` và `Super Band`.
  - **Tác dụng:** Ghép nối hai tập dữ liệu (danh sách nhạc sĩ/ban nhạc) lại với nhau (tương tự SQL Union All, nhưng linh hoạt hơn vì không bắt buộc các trường dữ liệu phải hoàn toàn giống hệt nhau).

#### 3. Kích hoạt ⚡️
- Nhấp vào nút **`Execute Workflow`** trên giao diện n8n để chạy thử nghiệm thủ công.
- Nhấp đúp vào từng node `Merge` và các node kết quả để quan sát dữ liệu đầu vào (Input) và đầu ra (Output), từ đó hiểu rõ cách các tập dữ liệu được hòa trộn với nhau.

### ✍️ Mẹo & gợi ý nâng cao
- **Ứng dụng thực tế vào Database/Google Sheets:** Thay thế các node `Code` chứa dữ liệu mẫu bằng các node truy vấn cơ sở dữ liệu thực tế (PostgreSQL, MySQL) hoặc Google Sheets để tự động hóa việc đối soát kho hàng, báo cáo doanh thu.
- **Kết hợp thông báo:** Sau bước Merge, các sếp có thể nối thêm node Telegram hoặc Slack để gửi cảnh báo tự động (ví dụ: cảnh báo nguyên liệu nào trong kho sắp hết).
- **Lưu trữ lịch sử:** Đưa dữ liệu sau khi merge vào một bảng tổng hợp trên Airtable hoặc Google Drive để tiện theo dõi định kỳ.

### 📌 Kết luận
Merge Node chính là chìa khóa giúp các sếp giải quyết mọi bài toán phức tạp về tổng hợp và xử lý dữ liệu đa nguồn trong n8n. Hãy import workflow này ngay hôm nay để thử nghiệm và áp dụng vào các dự án tự động hóa thực tế của doanh nghiệp!