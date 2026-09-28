---
title: "🍽️ Tự Động Hóa Thực Đơn Tuần & Danh Sách Mua Sắm Thông Minh Với Mealie"
description: "Workflow n8n tự động tạo lịch ăn uống 7 ngày, gửi email xác nhận và sinh danh sách mua sắm thông minh trên Mealie, giúp tiết kiệm hàng giờ mỗi tuần."
slug: "tu-dong-hoa-thuc-don-tuan-mealie"
tags: [n8n, automation, no-code, mealie, productivity, email-automation]
keywords: [n8n workflow, tự động hóa thực đơn, mealie api, danh sách mua sắm, quản lý bữa ăn]
---

# 🍽️ Tự Động Hóa Thực Đơn Tuần & Danh Sách Mua Sắm Thông Minh Với Mealie

Các sếp có bao giờ cảm thấy mệt mỏi khi phải ngồi suy nghĩ "Hôm nay ăn gì?" hay "Tuần này nấu những món gì?" không? Việc lên thực đơn cho cả gia đình thường tốn rất nhiều thời gian, chưa kể đến việc phải đối chiếu lại xem trong tủ lạnh còn nguyên liệu gì, thiếu gì để đi chợ.

Workflow này là giải pháp hoàn hảo để giải quyết nỗi đau đó. Nó tự động hóa toàn bộ quy trình: từ việc tạo lịch ăn uống ngẫu nhiên cho 7 ngày tới, gửi email để các sếp duyệt/xóa món, cho đến việc tự động tổng hợp danh sách nguyên liệu cần mua trên ứng dụng Mealie. Tất cả diễn ra trong im lặng, không cần các sếp phải đụng tay vào bất kỳ dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, đặc biệt là với các tác vụ định kỳ (Schedule Trigger), các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian:** Loại bỏ hoàn toàn công đoạn lên thực đơn thủ công mỗi tuần.
- **Chính xác tuyệt đối:** Danh sách mua sắm được tổng hợp tự động từ công thức nấu ăn, tránh sót nguyên liệu.
- **Tương tác linh hoạt:** Gửi email để xác nhận hoặc loại bỏ món ăn không mong muốn trước khi chốt danh sách mua.
- **Tích hợp liền mạch:** Kết nối trực tiếp với Mealie, nền tảng quản lý công thức nấu ăn mã nguồn mở hàng đầu.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Mealie:** Cài đặt và chạy Mealie (có thể self-host hoặc dùng bản cloud).
2. **Mealie API Key:** Lấy token Bearer Auth từ cài đặt Mealie.
3. **Tài khoản Gmail:** Để gửi và nhận email xác nhận thực đơn.
4. **n8n Instance:** Chạy trên VPS hoặc local.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ [link gốc](https://n8n.io/workflows/14095) hoặc copy toàn bộ code JSON bên dưới và dán vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này sử dụng 14 nodes chính, tập trung vào việc gọi API Mealie và xử lý dữ liệu. Dưới đây là các điểm cần cấu hình:

**A. Cấu hình Trigger & Lịch trình**
- **Node:** `Weekly Schedule Trigger`
- **Hành động:** Click vào node này.
- **Cấu hình:**
    - Chọn `Cron` hoặc `Interval`.
    - Thiết lập thời gian chạy (ví dụ: 18:00 thứ 6 hàng tuần).
    - **Quan trọng:** Chọn đúng Timezone (ví dụ: `Asia/Ho_Chi_Minh`) để đảm bảo email gửi đi đúng giờ.

**B. Cấu hình Mealie API (Quan trọng nhất)**
Workflow sử dụng nhiều node `httpRequest` để giao tiếp với Mealie. Các sếp cần tạo một **Credential** mới trong n8n:
1. Vào `Credentials` -> `New` -> Chọn `HTTP Request` -> `Generic Credential` (hoặc `Bearer Auth` tùy phiên bản n8n).
2. Điền thông tin:
   - **URL/Host:** Địa chỉ IP hoặc Domain của server Mealie (ví dụ: `http://192.168.1.100:3000`).
   - **Authentication:** Chọn `Bearer Auth`.
   - **Token:** Dán Mealie API Key của các sếp vào đây.
3. **Áp dụng credential này vào các node sau:**
   - `Fetch Current Week Meal Plans`
   - `Generate Random Meal Plan`
   - `Delete Random Meal Plan`
   - `Fetch Recipe By Slug`
   - `Create Shopping List in Mealie`
   - `Add Ingredients To Shopping List`

**C. Cấu hình Gmail**
- **Node:** `Send Meal Plan Email`
- **Hành động:** Chọn credential Gmail của các sếp.
- **Cấu hình:**
    - **To:** Địa chỉ email nhận thực đơn.
    - **Subject:** Tiêu đề email (có thể giữ nguyên hoặc sửa cho phù hợp).
    - **Body:** Nội dung email sẽ được sinh động từ node `Prepare Meal Plan Email Data`. Các sếp có thể chỉnh sửa template HTML trong node Code này nếu muốn thay đổi giao diện email.

**D. Logic Xử lý Dữ liệu (Code Nodes)**
- **Node:** `Generate Upcoming Week`
    - Node này tính toán 7 ngày tới. Nếu các sếp muốn thay đổi logic (ví dụ: chỉ tính ngày làm việc, hoặc bắt đầu từ thứ 2), hãy mở node Code này và chỉnh sửa phần tính toán ngày tháng.
- **Node:** `Normalize Recipe Data` & `Normalize User Response`
    - Các node này xử lý dữ liệu thô từ API Mealie và phản hồi từ email. Thường không cần chỉnh sửa trừ khi Mealie thay đổi cấu trúc API.

#### 3. Kích hoạt ⚡️
1. **Test Run:**
   - Click vào nút `Execute Workflow` (hoặc `Test`).
   - Kiểm tra xem email có được gửi đi không.
   - Phản hồi email (nếu workflow thiết kế để chờ phản hồi) hoặc kiểm tra Mealie xem có danh sách mua sắm mới được tạo không.
2. **Bật Active:**
   - Sau khi test thành công, bật công tắc `Active` ở góc trên bên phải n8n.
   - Workflow sẽ tự động chạy theo lịch đã đặt.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram/Slack:** Thay vì gửi email, các sếp có thể thay node `Send Meal Plan Email` bằng node `Telegram` hoặc `Slack` để nhận thông báo nhanh hơn trên điện thoại.
- **Cá nhân hóa món ăn:** Trong node `Generate Random Meal Plan`, các sếp có thể thêm tham số để lọc công thức dựa trên chế độ ăn (Vegan, Keto, Low-carb) nếu Mealie hỗ trợ tag.
- **Lưu Log Lịch sử:** Thêm một node `Google Sheets` hoặc `Postgres` để lưu lại lịch sử thực đơn các tuần trước, giúp tránh lặp lại món ăn quá thường xuyên.
- **Tự động Mua Sắm Online:** Nếu các sếp dùng dịch vụ giao hàng (như GrabMart, ShopeeFood), có thể mở rộng workflow để tự động thêm sản phẩm vào giỏ hàng dựa trên danh sách mua sắm.

### 📌 Kết luận
Việc lên thực đơn và đi chợ là những việc vặt nhưng lại tốn rất nhiều "băng thông" não bộ. Với workflow n8n kết hợp Mealie này, các sếp có thể tự động hóa hoàn toàn quy trình này, chỉ cần một cú click để duyệt email và để hệ thống lo phần còn lại. Hãy thử ngay hôm nay để trải nghiệm sự tiện lợi của việc "ăn uống thông minh" mà không cần suy nghĩ!