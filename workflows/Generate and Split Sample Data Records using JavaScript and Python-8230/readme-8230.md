---
title: "🚀 Tạo và Tách Dữ Liệu Mẫu trong n8n bằng JavaScript và Python cực dễ"
description: "Hướng dẫn sử dụng workflow n8n để tự động tạo 20 bản ghi mẫu bằng code JavaScript/Python và tách thành các item riêng biệt phục vụ testing và prototyping."
slug: "tao-va-tach-du-lieu-mau-trong-n8n-bang-javascript-va-python"
tags: [n8n, automation, no-code, javascript, python, workflow-template]
keywords: [n8n workflow, tao du lieu mau n8n, code node n8n, split out n8n, javascript python n8n]
---

# 🚀 Tạo và Tách Dữ Liệu Mẫu trong n8n bằng JavaScript và Python

Các sếp có bao giờ gặp khó khăn khi cần test các workflow phức tạp trong n8n nhưng lại chưa có sẵn nguồn dữ liệu thực tế từ database hay API chưa? Việc ngồi tạo thủ công từng bản ghi hoặc viết code từ đầu cho các bước test thường rất tốn thời gian và làm gián đoạn tiến độ công việc.

Workflow này do chuyên gia **Robert Breen** thiết kế chính là "vị cứu tinh". Template cung cấp sẵn các đoạn code mẫu bằng cả **JavaScript** và **Python** để tạo ngay tập dữ liệu giả lập, kết hợp với node **Split Out** để tách chúng thành các item độc lập. Các sếp có thể dùng ngay lập tức để kiểm thử các node phía sau, xử lý phân trang (pagination) hoặc dựng nguyên mẫu (prototyping) mà không cần kết nối nguồn dữ liệu thật.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tạo dữ liệu nhanh chóng**: Tự động sinh ra 20 bản ghi mẫu chứa các trường `index`, `num`, và `test` chỉ trong một nốt nhạc.
- **Linh hoạt ngôn ngữ**: Tích hợp sẵn cả 2 phiên bản bằng **JavaScript** và **Python** tùy theo sở thích và thế mạnh của các sếp.
- **Tách item thông minh**: Sử dụng node **Split Out** để chuyển mảng dữ liệu thành các item riêng biệt, sẵn sàng truyền vào các node xử lý tiếp theo.
- **Tiết kiệm thời gian test**: Không cần phụ thuộc vào API bên ngoài hay database thật khi đang trong giai đoạn xây dựng và kiểm thử workflow.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance **n8n** đang hoạt động (Cloud hoặc Self-hosted).
- Không cần cấu hình Credentials hay API Key phức tạp nào vì workflow thuần túy sử dụng logic Code bên trong n8n!
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Copy mã JSON của workflow hoặc tải file JSON từ thư viện n8n.
- Tại giao diện n8n Editor, chọn **Add workflow** -> **Import from File** hoặc dán trực tiếp JSON vào màn hình làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm các node chính sau đây:
- **Start Workflow (`manualTrigger`)**: Node khởi chạy thủ công để test nhanh. Các sếp có thể thay thế bằng Webhook, Schedule Trigger hoặc bất kỳ trigger nào khác tùy nhu cầu thực tế.
- **Generate Data Javascript (`code`)**: Chứa đoạn code JavaScript tạo sẵn 20 bản ghi mẫu và gán vào `item.json.barr`. Các sếp có thể chỉnh sửa lại số lượng bản ghi hoặc cấu trúc các trường dữ liệu trực tiếp trong node này nếu muốn.
- **Generate Data Python (`code`)**: Phiên bản tương tự viết bằng Python dành cho các sếp thích xử lý dữ liệu bằng Python. (Lưu ý: n8n cần hỗ trợ môi trường Python được cấu hình trên server nếu chạy self-host).
- **Split Out Javascript & Split Out Python (`splitOut`)**: Nhận mảng dữ liệu từ các node Code phía trước và "fan out" thành các item riêng lẻ để các node tiếp theo trong chuỗi có thể xử lý độc lập từng dòng.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Test workflow** trên giao diện n8n để kiểm tra kết quả trả về ở các node `Split Out`.
- Sau khi kiểm tra dữ liệu hiển thị chính xác, các sếp có thể tuỳ chỉnh lại cấu trúc dữ liệu theo ý muốn và bắt đầu tích hợp vào các kịch bản tự động hóa lớn hơn.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kịch bản**: Kết nối output của các node `Split Out` với các node như **Google Sheets**, **Airtable** hoặc **Slack** để kiểm thử việc đẩy dữ liệu hàng loạt.
- **Tùy biến dữ liệu giả**: Chỉnh sửa đoạn code JavaScript/Python để sinh ra dữ liệu động phức tạp hơn như tên khách hàng, email giả lập, hoặc số tiền ngẫu nhiên phục vụ việc test báo cáo.
- **Tự động hóa báo cáo**: Thiết lập Schedule Trigger chạy định kỳ kết hợp workflow này để test các cơ chế nhận dữ liệu tự động.

### 📌 Kết luận
Workflow "Generate and Start Sample Data" là một công cụ cực kỳ hữu ích trong bộ đồ nghề của bất kỳ kỹ sư tự động hóa nào. Hãy áp dụng ngay template này để tiết kiệm thời gian dựng khung dữ liệu và tăng tốc độ triển khai các dự án n8n của các sếp!