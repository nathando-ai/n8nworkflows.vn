---
title: "🚀 Hướng dẫn học Code Node JavaScript trong n8n qua Workshop Tương tác Thực chiến"
description: "Khám phá cách làm chủ JavaScript Code Node trong n8n từ cơ bản đến nâng cao với workflow hướng dẫn tương tác trực quan, giúp bạn tự tin xử lý dữ liệu phức tạp."
slug: "huong-dan-hoc-code-node-javascript-trong-n8n"
tags: [n8n, javascript, code-node, automation, tutorial, backend]
keywords: [n8n code node, javascript trong n8n, hoc n8n nang cao, lap trinh n8n, xu ly du lieu n8n]
---

# 🚀 Hướng dẫn học Code Node JavaScript trong n8n qua Workshop Tương tác Thực chiến

Nhiều anh chị em khi làm tự động hóa với n8n thường gặp "nỗi sợ" khi phải động đến các đoạn code JavaScript phức tạp, hoặc lúng túng không biết cách xử lý mảng dữ liệu, gọi API trong code hay xuất file binary. 

Workflow này do chuyên gia **Lucas Peyrin** xây dựng chính là "cứu cánh" tuyệt vời. Nó hoạt động như một lớp học tương tác trực quan ngay bên trong n8n, giúp các sếp nắm vững tư duy và cách viết Code Node từ con số không đến chuyên gia mà không cần tìm kiếm tài liệu rời rạc bên ngoài!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Hiểu bản chất:** Phân biệt rõ ràng giữa hai chế độ chạy của Code Node: *"Run Once for Each Item"* và *"Run Once for All Items"*.
- **Kỹ năng thực chiến:** Biết cách truy xuất dữ liệu (`$input.item.json`, `$items()`), gọi API trực tiếp bằng hàm hỗ trợ (`this.helpers.httpRequest`), và xử lý dữ liệu bất đồng bộ (`async/await`).
- **Tự tay làm file:** Học được cách tạo file binary (như file CSV) ngay từ dữ liệu dạng chữ thuần túy bằng JavaScript.
- **Tiết kiệm thời gian:** Không cần tra cứu cú pháp rườm rà, có ngay các mẫu code chuẩn chỉnh để áp dụng vào các dự án tự động hóa thực tế.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance **n8n** (Cloud hoặc Self-hosted phiên bản bất kỳ).
- Không cần chuẩn bị API key bên ngoài vì workflow sử dụng dữ liệu mẫu và các API công khai có sẵn.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Copy mã nguồn JSON của workflow hoặc tải file JSON từ kho lưu trữ n8n.
- Vào giao diện n8n của các sếp, chọn **Workflows** -> **Import from File / Clipboard** và dán vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này được thiết kế theo dạng bài học từng bước (Step-by-step tutorial). Các sếp hãy đi qua từng node để hiểu rõ cách vận hành:

- **Node `1. Sample Data` (Set node):** Nơi khởi tạo danh sách người dùng mẫu. Các sếp có thể thay đổi tên, tuổi hoặc thêm bớt dữ liệu tùy ý để thử nghiệm.
- **Node `2. Split Out Users` (Split Out node):** Chia nhỏ mảng dữ liệu người dùng thành các item độc lập để các Code Node phía sau có thể xử lý từng người một.
- **Node `3. Process Each User` (Code node - Bài học 1):** Chạy ở chế độ **"Run Once for Each Item"**. Node này dùng để làm giàu dữ liệu cho từng user. 
  * *Mẹo:* Quan sát cách sử dụng `$input.item.json` và cấu trúc `return { ...user, fullName: ... }` để giữ lại dữ liệu cũ và thêm dữ liệu mới.
- **Node `4. Fetch External Data (Advanced)` (Code node - Bài học 2):** Nâng cao hơn với việc gọi API bên ngoài từ trong code sử dụng `await this.helpers.httpRequest()`.
- **Node `5. Calculate Average Age` (Code node - Bài học 3):** Chuyển sang chế độ **"Run Once for All Items"**. Học cách gom toàn bộ dữ liệu sử dụng `$items()` để tính toán tổng số lượng và tuổi trung bình.
- **Node `6. Create a Binary File (Expert)` (Code node - Bài học bài 4):** Chuyên gia xử lý file. Học cách sử dụng `Buffer` và `this.helpers.prepareBinaryData` để biến một chuỗi text thành file CSV thực thụ có thể tải xuống.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** tại node `Start Tutorial` (Manual Trigger) để chạy thử nghiệm toàn bộ chuỗi bài học.
- Kiểm tra kết quả đầu ra ở từng node để thấy sự biến đổi kỳ diệu của dữ liệu qua từng đoạn mã JavaScript.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thực tế:** Sau khi đã hiểu cách viết code, các sếp có thể thay thế node `1. Sample Data` bằng node **Webhook** hoặc **Google Sheets** để lấy dữ liệu thực tế từ khách hàng của mình.
- **Lưu file tự động:** Kết nối node tạo file binary (Node số 6) vào các node lưu trữ như **Google Drive** hoặc gửi thẳng qua **Telegram / Slack** để báo cáo định kỳ.
- **Xử lý lỗi (Error Handling):** Thêm các khối `try...catch` vào trong các Code Node gọi API ngoại vi để workflow không bị dừng đột ngột khi API bên ngoài gặp sự cố.

### 📌 Kết luận
Code Node chính là "vũ khí bí mật" giúp n8n trở nên cực kỳ mạnh mẽ vượt qua giới hạn của các node có sẵn. Hãy chạy thử workflow tương tác này ngay hôm nay để tự tin viết code JavaScript cho mọi bài toán tự động hóa phức tạp nhất!