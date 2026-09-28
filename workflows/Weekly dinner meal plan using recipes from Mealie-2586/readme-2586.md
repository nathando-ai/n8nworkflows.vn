---
title: "🍽️ Tự động hóa kế hoạch bữa ăn hàng tuần với Mealie - Giải pháp tiết kiệm thời gian cho gia đình"
description: "Hướng dẫn chi tiết cách tự động tạo kế hoạch bữa ăn hàng tuần từ danh sách công thức Mealie, tiết kiệm thời gian và đảm bảo sự đa dạng trong thực đơn."
slug: "tu-dong-hoa-ke-hoach-bua-an-hang-tuan-voi-mealie"
tags: [n8n, automation, meal-planning, mealie, no-code]
keywords: [tự động hóa bữa ăn, kế hoạch ăn uống, mealie, n8n workflow, tự động hóa gia đình]
---

# 🍽️ Tự động hóa kế hoạch bữa ăn hàng tuần với Mealie - Giải pháp tiết kiệm thời gian cho gia đình

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các gia đình khi lên kế hoạch bữa ăn hàng tuần. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian lên kế hoạch bữa ăn hàng tuần
- Đảm bảo sự đa dạng trong thực đơn hàng tuần
- Tự động hóa hoàn toàn quá trình lên kế hoạch
- Tích hợp dễ dàng với hệ thống Mealie hiện có
- Hoạt động liên tục theo lịch trình đã đặt
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Mealie đã cài đặt và hoạt động
- API token từ Mealie để truy cập dữ liệu
- Danh sách công thức đã nhập trong Mealie
- Tài khoản n8n đã cài đặt và cấu hình
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Hướng dẫn import từ file JSON hoặc copy/paste JSON vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:
- **Friday 8pm**: Node scheduleTrigger để đặt lịch chạy workflow hàng tuần vào lúc 8pm thứ Sáu.
  - Cấu hình: Chọn ngày và giờ chạy (thường là thứ Sáu 8pm).
- **Create Meal Plan**: Node httpRequest để tạo kế hoạch bữa ăn mới.
  - Cấu hình: Điền URL cơ sở của Mealie instance và cấu hình các tham số khác trong node Config.
- **When clicking "Test workflow"**: Node manualTrigger để kiểm tra workflow.
  - Cấu hình: Không cần thay đổi gì, chỉ cần nhấn nút "Test workflow" khi cần kiểm tra.
- **Get Recipes**: Node httpRequest để lấy danh sách công thức từ Mealie.
  - Cấu hình: Điền URL cơ sở của Mealie instance và cấu hình các tham số khác trong node Config.
- **Config**: Node set để cấu hình các tham số cho workflow.
  - Cấu hình:
    - Base URL của Mealie instance
    - Số lượng công thức cần tạo
    - Số ngày offset (0 sẽ bắt đầu từ ngày hôm nay)
    - ID danh mục (nếu có)
- **Generate Random Items**: Node code để tạo danh sách công thức ngẫu nhiên.
  - Cấu hình: Không cần thay đổi gì, node này sẽ tự động tạo danh sách công thức ngẫu nhiên dựa trên các tham số đã cấu hình.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để thông báo kế hoạch bữa ăn hàng tuần.
- Lưu log các kế hoạch đã tạo để theo dõi lịch sử.
- Gửi báo cáo định kỳ về các công thức đã sử dụng và chưa sử dụng.
- Tích hợp với các dịch vụ khác như Google Calendar để tạo sự kiện nhắc nhở bữa ăn.

### 📌 Kết luận
Workflow này giúp các gia đình tiết kiệm thời gian và đảm bảo sự đa dạng trong thực đơn hàng tuần. Với việc tự động hóa hoàn toàn quá trình lên kế hoạch, các sếp có thể tập trung vào việc chuẩn bị bữa ăn thay vì phải tốn thời gian lên kế hoạch. Hãy áp dụng ngay để trải nghiệm sự tiện lợi và hiệu quả của tự động hóa!