---
title: "🚀 Trích xuất Key-Value từ dữ liệu JSON theo Index cực nhanh trong n8n"
description: "Hướng dẫn sử dụng workflow n8n giúp xử lý và bóc tách các cặp khóa-giá trị (Key-Value) từ dữ liệu JSON theo vị trí index một cách tự động, chính xác và không cần code phức tạp."
slug: "trich-xuat-key-value-tu-json-theo-index-trong-n8n"
tags: [n8n, automation, no-code, json, data-processing, weblineindia]
keywords: [n8n workflow, trích xuất json, extract key value, n8n code node, xử lý dữ liệu json tự động]
---

# 🚀 Trích xuất Key-Value từ dữ liệu JSON theo Index cực nhanh trong n8n

Trong quá trình làm việc với các hệ thống API hoặc dữ liệu thô, các sếp chắc chắn sẽ gặp tình trạng dữ liệu JSON trả về có cấu trúc phức tạp hoặc danh sách các thuộc tính mà mình cần bóc tách một cách chính xác theo vị trí (index). Việc xử lý thủ công hoặc viết code dài dòng vừa mất thời gian lại dễ sinh lỗi. 

Đừng lo, bài viết này sẽ hướng dẫn các sếp cách sử dụng một workflow n8n cực kỳ gọn nhẹ do **WeblineIndia** phát triển để tự động hóa hoàn toàn việc bóc tách cặp Key-Value từ JSON theo index một cách nhanh chóng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Bỏ qua thao tác lọc dữ liệu bằng tay, tiết kiệm thời gian xử lý payload JSON lớn.
- **Linh hoạt theo Index:** Dễ dàng nhắm chính xác phần tử Key hoặc Value dựa vào vị trí index mong muốn.
- **Tối ưu hiệu suất:** Sử dụng kết hợp node Set và JavaScript trong Code node giúp xử lý gọn gàng, mượt mà.
- **Dễ dàng tích hợp:** Làm bàn đạp vững chắc để đưa dữ liệu đã trích xuất vào các bước tiếp theo như Google Sheets, Database, hay gửi thông báo.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống **n8n** đang hoạt động (Cloud hoặc Self-hosted).
- Dữ liệu JSON mẫu cần xử lý.
- Không yêu cầu API key phức tạp vì workflow thuần túy xử lý dữ liệu nội bộ.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trong n8n, sau đó copy toàn bộ mã JSON của workflow này (từ nguồn chính thức hoặc file cấu hình) và paste trực tiếp vào giao diện n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 5 nodes chính, các sếp cần chú ý cấu hình các điểm sau để chạy trơn tru:

- **When clicking ‘Test workflow’ (`manualTrigger`):** Node kích hoạt thủ công để kiểm tra dữ liệu mẫu ban đầu. Các sếp có thể thay thế bằng Webhook, Schedule Trigger hoặc node nhận dữ liệu thực tế sau này.
- **Input JSON Node (`set`):** Nơi các sếp định nghĩa hoặc truyền vào đoạn dữ liệu JSON gốc cần bóc tách. Hãy đảm bảo cấu trúc JSON đầu vào đúng định dạng (ví dụ: một object chứa các cặp key-value).
- **Find Key-Value Pair (`code`):** Node sử dụng đoạn mã JavaScript (Node.js) để duyệt qua đối tượng JSON, chuyển đổi thành mảng và tìm kiếm phần tử dựa trên `index` chỉ định. Các sếp có thể mở node này để tùy chỉnh lại vị trí index muốn lấy (ví dụ: lấy phần tử thứ 0, 1, 2...).
- **Key (`set`):** Node nhận kết quả trả về là tên của Khóa (Key) tại vị trí index đã chọn.
- **Value (`set`):** Node nhận kết quả trả về là Giá trị (Value) tương ứng tại vị trí index đã chọn.

#### 3. Kích hoạt ⚡️
- Nhấn **Test workflow** để chạy thử và kiểm tra kết quả đầu ra ở các node `Key` và `Value`.
- Sau khi kiểm tra dữ liệu hiển thị chính xác, các sếp có thể chuyển trạng thái workflow sang **Active** để đưa vào sử dụng thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng dữ liệu:** Thay vì chỉ lấy 1 index cố định, các sếp có thể sửa Code node để vòng lặp (`loop`) qua toàn bộ danh sách JSON và trả về danh sách đầy đủ các cặp Key-Value.
- **Lưu trữ kết quả:** Kết nối node `Key` và `Value` tới Google Sheets hoặc Airtable để lưu lịch sử bóc tách dữ liệu tự động.
- **Cảnh báo lỗi:** Thêm node xử lý lỗi (Error Trigger) để thông báo qua Telegram/Slack nếu cấu trúc JSON đầu vào bị sai định dạng.

### 📌 Kết luận
Workflow "JSON Data Utility: Extract Key-Value Pairs by Index" là một công cụ cực kỳ hữu ích giúp các sếp xử lý nhanh gọn các bài toán liên quan đến bóc tách dữ liệu JSON phức tạp mà không tốn công viết code từ đầu. Hãy áp dụng ngay vào hệ thống tự động hóa của mình nhé!