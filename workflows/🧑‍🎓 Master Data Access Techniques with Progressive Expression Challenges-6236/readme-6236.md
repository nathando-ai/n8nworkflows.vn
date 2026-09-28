---
title: "🧑‍🎓 Hướng dẫn Thực hành Truy cập Dữ liệu trong n8n qua Thử thách Biểu thức Tiến bộ"
description: "Học cách truy cập dữ liệu JSON cơ bản, mảng, đối tượng lồng nhau, mảng đối tượng và hàm JavaScript bằng biểu thức n8n qua các bài test tương tác."
slug: "huong-dan-thuc-hanh-truy-cap-du-lieu-n8n-bieu-thuc"
tags: [n8n, automation, no-code, expressions, data manipulation, javascript]
keywords: [n8n workflow, tự động hóa, n8n expressions, truy cập JSON, học n8n]
---

# 🧑‍🎓 Hướng dẫn Thực hành Truy cập Dữ liệu trong n8n qua Thử thách Biểu thức Tiến bộ

Bạn thường cảm thấy “bị mắc” khi phải viết biểu thức (`{{ }}`) để lấy giá trị từ một đối JSON lồng nhau trong n8n? Workflow **Master Data Access Techniques with Progressive Expression Challenges** của Lucas Peyrin là một bài tập thực hành tương tác giúp bạn rèn luyện kỹ năng truy cập dữ liệu qua các mức độ khó tăng dần: từ truy cập trường đơn giản, mảng, đối tượng lồng nhau, mảng đối tượng cho tới việc kết hợp với hàm JavaScript. Sau khi hoàn thành, bạn sẽ viết biểu thức n8n một cách tự tin và áp dụng ngay vào các workflow tự động hoá thực tế.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Thành thạo biểu thức n8n**: biết cách truy cập trường, phần tử mảng, đối tượng lồng nhau và mảng đối tượng.
- **Áp dụng hàm JavaScript trong biểu thức**: ví dụ `.toUpperCase()`, `.slice()`, v.v.
- **Giảm thời gian debug**: mỗi bước có phản hồi ngay (xanh = đúng, đỏ = sai) giúp bạn tự sửa lỗi nhanh.
- **Nền tảng cho các workflow phức tạp**: sau khi thành thạo, bạn có thể tự tin xử lý dữ liệu từ API, webhook, Google Sheets… mà không cần node Function phức tạp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n (self‑hosted hoặc n8n.cloud) đã được cài đặt và có thể truy cập Editor.
- **Không cần credentials bên ngoài** vì workflow chỉ sử dụng các node nội bộ (Manual Trigger, Set, IF, NoOp, StopAndError, HTML, Sticky Note).
- Mở trình duyệt và truy cập vào workflow đã import để bắt đầu thực hành.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Sao chép toàn bộ JSON workflow từ trang gốc (https://n8n.io/workflows/6236) hoặc tải file JSON nếu có.
2. Trong n8n Editor, nhấn vào nút **Import** (góc trên bên phải) → chọn **Paste JSON** hoặc **Upload file** → dán JSON → nhấn **Import**.
3. Workflow sẽ xuất hiện với tên **🧑‍🎓 Master Data Access Techniques with Progressive Expression Challenges**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow được thiết kế để bạn tự chỉnh các node **Test - …** bằng biểu thức đúng. Dưới đây là hướng dẫn chi tiết cho mỗi bước, kèm gợi ý expression (bạn có thể tham khảo các node **Answer - …** nếu bị mắc).

| Node cần chỉnh | Trường cần tạo | Mô tả nhiệm vụ | Gợi ý expression (tham khảo) |
|---|---|---|---|
| **Test - Basic Access** | `user_city` | Lấy `city` từ **Source Data** | `{{ $('Source Data').item.json.city }}` |
| **Test - Array Access** | `third_tool` | Lấy phần tử thứ 3 (index 2) của mảng `tools` | `{{ $('Source Data').item.json.tools[2] }}` |
| **Test - Nested Object** | `street_address` | Lấy `street` bên trong đối tượng `address` | `{{ $('Source Data').item.json.address.street }}` |
| **Test - Array of Objects** | `second_task_name` | Lấy `name` của đối tượng thứ 2 (index 1) trong mảng `tasks` | `{{ $('Source Data').item.json.tasks[1].name }}` |
| **Test - JS Function** | `uppercase_name` | Lấy `name` và chuyển thành HOA | `{{ $('Source Data').item.json.name.toUpperCase() }}` |
| **Test - Final** | `summary` | Tạo chuỗi: `The status of task 'Review PR' is Pending.` (kết hợp text tĩnh và expression) | `{{ "The status of task '" + $('Source Data').item.json.tasks[0].name + "' is " + $('Source Data').item.json.tasks[0].status + "." }}` |

> **Lưu ý:**  
> - Mỗi node **Test - …** là loại **Set**. Nhấn vào node → trong tab **Fields** → **Add Field** → đặt tên trường như bảng trên → trong ô **Value** bấm vào biểu tượng `{}` (expression) và dán expression tương ứng.  
> - Sau khi nhập expression, nhấn **Execute Workflow** (nút màu xanh lá ở góc trên bên phải). Nếu đường đi từ node **Test - …** tới node **Check - …** turns **xanh**, nghĩa là bạn đã đúng. Nếu đỏ, đọc gợi ý ở node **❌ Incorrect.** hoặc tham khảo node **Answer - …** tương ứng.

#### 3. Kích hoạt ⚡️
- Sau khi tất cả các Test node đều trả về đường xanh (tức là bạn đã vượt qua mọi bước), workflow sẽ dẫn tới node **🎉 SUCCESS 🎉** (node HTML hiển thị gif chúc mừng).  
- Bạn có thể deixar workflow ở trạng thái **Inactive** vì nó chỉ cần chạy thủ công khi bạn muốn luyện tập. Nếu muốn chạy tự động, bật toggle **Active** và sử dụng nút **Execute Workflow** mỗi khi muốn bắt đầu lại một lượt test mới.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo kết quả qua Slack/Telegram**: sau node **🎉 SUCCESS 🎉**, thêm node **Slack** hoặc **Telegram** để gửi thông báo “Bạn đã hoàn thành bài test truy cập dữ liệu!” khi hoàn thành.
- **Lưu log vào Google Sheets**: mỗi lần chạy workflow, thêm node **Google Sheets** để ghi lại thời gian bắt đầu, kết quả (pass/fail) và các giá trị bạn đã lấy ra – giúp bạn theo dõi tiến độ học tập.
- **Tạo phiên bản mở rộng**: sao chép workflow này và thay đổi **Source Data** bằng JSON thực tế từ API (ví dụ: danh sách người dùng từ GitHub) để luyện tập trên dữ liệu có cấu trúc phức tạp hơn.
- **Kết hợp với Node Function**: sau khi thành thạo biểu thức, thử chuyển một số logic phức tạp sang node **Function** để tối ưu hóa hiệu năng khi xử lý lớn.

### 📌 Kết luận
Workflow **Master Data Access Techniques with Progressive Expression Challenges** là một công cụ thực hành tuyệt vời để bạn nắm vững cách truy cập và xử lý dữ liệu JSON trong n8n mà không cần viết code phức tạp. Sau khi hoàn thành tất cả các thử thách, bạn sẽ có khả năng xây dựng các workflow tự động hoá mạnh mẽ, từ xử lý webhook, đồng bộ CRM, tới tạo báo cáo tự động – tất cả đều dựa trên nền tảng biểu thức mà bạn vừa rèn luyện.

Hãy import ngay, thử thách bản thân và chia sẻ thành tích với cộng đồng n8n nhé! 🚀