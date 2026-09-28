---
title: "🚀 Hướng dẫn xử lý dữ liệu JavaScript trong n8n với Code Node: Lọc, Phân tích & Xuất dữ liệu"
description: "Khám phá cách làm chủ JavaScript trong n8n Code Node để lọc dữ liệu, tính toán thống kê và định dạng xuất file cực kỳ mạnh mẽ qua ví dụ thực chiến."
slug: "xu-ly-du-lieu-javascript-trong-n8n-code-node"
tags: [n8n, automation, javascript, code-node, data-processing, no-code]
keywords: [n8n workflow, n8n code node, xử lý dữ liệu javascript, lọc dữ liệu n8n, tính toán thống kê n8n]
---

# 🚀 Hướng dẫn xử lý dữ liệu JavaScript trong n8n với Code Node: Lọc, Phân tích & Xuất dữ liệu

Các sếp có bao giờ gặp khó khăn khi các node mặc định của n8n không đủ sức xử lý các logic phức tạp như tính toán nâng cao, lọc dữ liệu đa điều kiện hay biến đổi cấu trúc JSON lằng nhằng chưa? Việc phải xoay sở bằng các công cụ kéo thả đôi khi biến thành "cực hình" khi gặp bài toán dữ liệu lớn. Giải pháp tuyệt vời nhất chính là kết hợp **JavaScript** trực tiếp vào **n8n Code Node**!

Workflow này do chuyên gia **David Olusola** thiết kế, sẽ dẫn dắt các sếp đi từ cơ bản đến nâng cao cách dùng JavaScript trong n8n để giải quyết gọn gàng mọi bài toán xử lý dữ liệu thực tế mà không cần viết code từ đầu.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Nắm vững Code Node:** Hiểu rõ cách truy xuất, biến đổi và trả về dữ liệu chuẩn cú pháp n8n (`items`, `json`).
- **Tự động hóa lọc & phân tích:** Tự tay viết code lọc danh sách khách hàng, phân khúc dữ liệu và tính toán các chỉ số thống kê (KPIs, tổng, trung bình).
- **Chuẩn bị dữ liệu xuất:** Định dạng dữ liệu linh hoạt thành CSV, payload API hoặc danh sách email sẵn sàng đẩy sang các hệ thống bên thứ ba.
- **Nâng cao hiệu suất:** Giảm thiểu số lượng node rườm rà, gom logic phức tạp vào một Code Node duy nhất giúp workflow tinh gọn, dễ bảo trì.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (phiên bản Cloud hoặc Self-hosted đều được).
- **Kiến thức cơ bản:** Biết sơ qua về JavaScript (mảng `Array`, hàm `.map()`, `.filter()`, `.reduce()`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy đoạn JSON gốc.
- Mở n8n Editor, chọn **New Workflow** -> Bấm vào dấu `...` ở góc trên bên phải -> Chọn **Import from File / Clipboard** và dán dữ liệu vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 5 nodes được thiết kế chuẩn xác để hướng dẫn từng bước:
- **When clicking ‘Execute workflow’ (`manualTrigger`):** Node kích hoạt thủ công, dùng để test chạy thử bất cứ lúc nào.
- **Set Sample Data (`set`):** Node khởi tạo bộ dữ liệu mẫu (danh sách người dùng, tuổi, lương, team...). Các sếp có thể thay đổi dữ liệu tại đây để thử nghiệm.
- **Code: Filter & Transform (`code`):** 
  - *Nhiệm vụ:* Lọc người dùng trên 18 tuổi, tính thêm tiền thưởng (10% lương), tạo email định dạng chuẩn và xuất ra thành từng item riêng lẻ.
  - *Cú pháp cốt lõi:* Sử dụng `items[0].json` để lấy dữ liệu đầu vào và dùng `.map()` để tách mảng thành các item độc lập.
- **Code: Calculate Stats (`code`):**
  - *Nhiệm vụ:* Gom nhóm dữ liệu team, tính toán các chỉ số trung bình, tổng tiền lương và phân phối dữ liệu để tạo báo cáo tổng hợp.
- **Code: Format for Export (`code`):**
  - *Nhiệm vụ:* Đóng gói lại dữ liệu thành các định dạng chuẩn phục vụ cho API payload, danh sách gửi email hàng loạt hoặc xuất file kèm metadata/timestamp.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** để chạy thử nghiệm thủ công và kiểm tra kết quả trả về ở từng Code Node.
- Quan sát cửa sổ Output của n8n để hiểu cách dữ liệu biến đổi qua từng bước code JavaScript.

### ✍️ Mẹo & gợi ý nâng cao
- **Debug dễ dàng:** Luôn tận dụng `console.log("Dữ liệu:", data);` bên trong Code Node và xem kết quả tại tab *Execution Log* của n8n.
- **Mở rộng thông báo:** Kết nối node `Code: Format for Export` trực tiếp với các node **Slack** hoặc **Telegram** để tự động gửi báo cáo thống kê định kỳ về điện thoại/nhóm chat.
- **Xử lý lỗi (Edge Cases):** Luôn kiểm tra dữ liệu `null` hoặc `undefined` bằng toán tử optional chaining (`?.`) để tránh việc workflow bị crash giữa chừng.

### 📌 Kết luận
Việc làm chủ JavaScript trong n8n Code Node sẽ mở ra một cấp độ tự động hóa hoàn toàn mới, giúp các sếp giải quyết mọi bài toán "khó nhằn" mà các node kéo thả thông thường phải đầu hàng. Hãy import workflow ngay hôm nay và bắt đầu thử nghiệm các đoạn code của riêng mình!