---
title: "🔢 Tự Động Đếm Số Lượng Dữ Liệu Trong n8n: Hướng Dẫn Chi Tiết"
description: "Học cách sử dụng node Set để đếm chính xác số lượng item trả về từ bất kỳ nguồn dữ liệu nào trong n8n, giúp tối ưu hóa quy trình xử lý logic."
slug: "tu-dong-dem-so-luong-du-lieu-trong-n8n"
tags: [n8n, automation, no-code, data-processing, logic]
keywords: [n8n workflow, đếm dữ liệu, n8n set node, xử lý mảng, tự động hóa]
---

# 🔢 Tự Động Đếm Số Lượng Dữ Liệu Trong n8n: Hướng Dẫn Chi Tiết

Trong các quy trình tự động hóa phức tạp, việc biết chính xác "có bao nhiêu dữ liệu" đang được xử lý là yếu tố then chốt để đưa ra các quyết định logic tiếp theo. Ví dụ: Bạn muốn gửi email thông báo chỉ khi có ít hơn 5 khách hàng mới, hoặc muốn dừng quy trình nếu không tìm thấy dữ liệu.

Làm thủ công việc này cực kỳ khó khăn và dễ sai sót. Workflow **"Count the items returned by a node"** do Tom (một chuyên gia hàng đầu của n8n) xây dựng sẽ giải quyết vấn đề này một cách đơn giản, chính xác và không cần viết code. Đây là một "Building Block" (khối xây dựng) cơ bản nhưng cực kỳ hữu ích để các sếp có thể tích hợp vào bất kỳ workflow phức tạp nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Chính xác tuyệt đối:** Loại bỏ sai sót khi đếm thủ công hoặc dùng công thức phức tạp.
- **Tối ưu Logic:** Dễ dàng tạo điều kiện (IF/ELSE) dựa trên số lượng dữ liệu (ví dụ: nếu count > 0 thì gửi báo cáo).
- **Tiết kiệm thời gian phát triển:** Chỉ cần 3 node đơn giản để có một khối chức năng đếm dữ liệu chuẩn mực.
- **Mở rộng dễ dàng:** Có thể áp dụng cho bất kỳ node nào trả về mảng dữ liệu (API, Database, Sheets...).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Cloud hoặc Self-hosted).
- Không cần API key hay credentials bên ngoài (workflow dùng dữ liệu mẫu có sẵn trong n8n training).
- Kiến thức cơ bản về cấu trúc dữ liệu trong n8n (Items).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/1913](https://n8n.io/workflows/1913).
2. Nhấn nút **"Copy JSON"**.
3. Mở n8n Editor của bạn, vào **Import from URL** hoặc **Import from File** (nếu bạn đã lưu file JSON).
4. Hoặc đơn giản nhất: Mở n8n Editor, nhấn tổ hợp phím `Ctrl + V` (hoặc `Cmd + V` trên Mac) để dán JSON trực tiếp vào canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này rất nhẹ nhàng với 3 node chính, nhưng các sếp cần hiểu rõ cách hoạt động của từng phần để áp dụng vào dự án thực tế:

*   **Node 1: `When clicking "Execute Workflow"` (Manual Trigger)**
    *   Đây là nút khởi động thủ công. Trong dự án thực tế, các sếp có thể thay thế bằng **Webhook**, **Cron Schedule** hoặc **Trigger từ Email/Slack** tùy theo nhu cầu.

*   **Node 2: `Customer Datastore (n8n training)`**
    *   **Vai trò:** Đây là nguồn dữ liệu mẫu (Mock Data) được n8n cung cấp sẵn để các sếp test mà không cần kết nối database thật.
    *   **Tham số quan trọng:** `operation` được đặt là `getAllPeople`.
    *   **Lưu ý khi áp dụng thực tế:** Các sếp cần thay thế node này bằng node lấy dữ liệu thực tế của mình (ví dụ: `Google Sheets`, `Postgres`, `HTTP Request`...). Quan trọng là node này phải trả về một mảng các item (dù là 1 hay nhiều).

*   **Node 3: `Set` (Node quan trọng nhất)**
    *   **Vai trò:** Đây là nơi "phép màu" xảy ra. Node Set được cấu hình để tính toán và lưu trữ số lượng item từ node trước đó.
    *   **Cấu hình chi tiết:**
        *   Trong tab **Values**, các sếp sẽ thấy một trường được đặt tên (ví dụ: `count` hoặc `totalItems`).
        *   Giá trị (Value) của trường này thường sử dụng biểu thức: `{{ $input.all().length }}` hoặc `{{ $items.length }}`.
        *   **Giải thích:** `$input.all()` lấy toàn bộ dữ liệu đầu vào, và `.length` là thuộc tính JavaScript chuẩn để đếm số phần tử trong mảng.
    *   **Kết quả:** Sau khi chạy, output của node Set sẽ là một item duy nhất chứa trường `count` với giá trị là số lượng dữ liệu ban đầu.

#### 3. Kích hoạt ⚡️
1. Nhấn nút **Execute Workflow** để chạy thử.
2. Kiểm tra output của node **Set**: Bạn sẽ thấy một object JSON chứa trường `count` (ví dụ: `{"count": 5}`).
3. Nếu kết quả đúng, nhấn nút **Active** ở góc trên bên phải để kích hoạt workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp với Logic IF/ELSE:** Sau node Set, các sếp có thể thêm node **IF**. Ví dụ: Nếu `{{ $json.count }} > 0`, thì gửi thông báo "Đã tìm thấy dữ liệu", ngược lại gửi cảnh báo "Không có dữ liệu".
- **Gửi báo cáo định kỳ:** Thay vì Manual Trigger, dùng **Cron Schedule** để chạy workflow mỗi ngày. Kết hợp với node **Telegram** hoặc **Slack** để gửi tin nhắn: "Hôm nay có {{ $json.count }} đơn hàng mới".
- **Xử lý dữ liệu lớn:** Nếu dữ liệu quá lớn, các sếp có thể thêm node **Code** (Function) sau node Set để thực hiện các phép toán thống kê khác (tổng, trung bình, max, min) dựa trên mảng dữ liệu gốc.
- **Lưu log vào Database:** Thêm node **Postgres** hoặc **MySQL** sau node Set để lưu lại lịch sử số lượng dữ liệu theo thời gian, giúp theo dõi xu hướng (trending) trong dashboard.

### 📌 Kết luận
Việc đếm số lượng dữ liệu nghe có vẻ đơn giản nhưng lại là nền tảng cho rất nhiều logic tự động hóa phức tạp. Với workflow **"Count the items returned by a node"**, các sếp đã có trong tay một công cụ chuẩn mực, dễ hiểu và dễ tùy biến. Hãy thử áp dụng ngay vào dự án hiện tại của bạn để tối ưu hóa quy trình và giảm thiểu lỗi logic!