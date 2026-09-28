---
title: "🧹 Tự Động Dọn Dẹp Discord: Xóa Tin Nhắn Cũ Hàng Đêm"
description: "Workflow n8n tự động quét và xóa tin nhắn cũ hơn 7 ngày trên Discord mỗi tối, giúp server luôn gọn gàng và tuân thủ chính sách dữ liệu mà không cần code."
slug: "tu-dong-don-dep-discord-xoa-tin-nhan-cu"
tags: [n8n, automation, discord, no-code, data-management]
keywords: [n8n workflow discord, tự động xóa tin nhắn discord, dọn dẹp server discord, n8n discord cleanup]
---

# 🧹 Tự Động Dọn Dẹp Discord: Xóa Tin Nhắn Cũ Hàng Đêm

Quản lý một cộng đồng Discord lớn không chỉ là điều hành nội dung mà còn là bài toán về **bảo mật dữ liệu** và **trải nghiệm người dùng**. Khi tin nhắn tích tụ hàng ngày, server trở nên lộn xộn, khó tìm kiếm thông tin quan trọng, và quan trọng hơn, bạn có thể vi phạm các chính sách về quyền riêng tư (GDPR) hoặc quy định nội bộ về thời gian lưu trữ dữ liệu (retention policy).

Làm thủ công việc này là bất khả thi: bạn không thể vào từng kênh, cuộn lên tìm tin nhắn cũ hơn 7 ngày và xóa chúng mỗi ngày. Đây chính là lúc **n8n** phát huy sức mạnh. Workflow này hoạt động như một "người dọn dẹp" tự động, chạy vào lúc 21:00 mỗi tối, quét toàn bộ các kênh, lọc ra những tin nhắn cũ và xóa chúng một cách an toàn, tuân thủ nghiêm ngặt các giới hạn tốc độ API (rate limits) của Discord.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tuân thủ chính sách dữ liệu:** Đảm bảo tin nhắn chỉ được lưu trữ đúng số ngày quy định (mặc định 7 ngày trong workflow này).
- **Server luôn gọn gàng:** Người dùng mới tham gia sẽ thấy kênh sạch sẽ, dễ theo dõi, không bị "chôn vùi" bởi hàng nghìn tin nhắn cũ.
- **Tiết kiệm 100% thời gian quản trị:** Không cần nhân viên điều hành phải dành thời gian dọn dẹp thủ công mỗi ngày.
- **An toàn cho API:** Workflow được thiết kế với các bước "Cool down" (nghỉ ngơi) để tránh bị Discord khóa tài khoản do gọi API quá nhanh.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Đã cài đặt và chạy (Cloud hoặc Self-hosted).
- **Tài khoản Discord:** Có quyền quản trị (Administrator hoặc Manage Channels) trên server cần dọn dẹp.
- **Discord Bot Token / OAuth2:** Workflow sử dụng kết nối Discord. Các sếp cần tạo một Bot hoặc sử dụng tài khoản người dùng (User Account) đã được cấp quyền. *Lưu ý: Sử dụng Bot thường ổn định và an toàn hơn về mặt API.*
- **Kiến thức cơ bản về n8n:** Biết cách import workflow và cấu hình credentials.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải xuống file JSON của workflow từ [link gốc](https://n8n.io/workflows/2980) hoặc copy toàn bộ mã JSON.
2. Mở n8n Editor, vào menu **Workflows** -> **Import from File** (hoặc **Import from URL**).
3. Chọn file JSON vừa tải hoặc dán mã JSON vào ô nhập liệu.
4. Nhấn **Import**. Workflow sẽ xuất hiện trong danh sách.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Đây là phần quan trọng nhất. Workflow gốc có 10 nodes, các sếp cần chú ý cấu hình các node sau:

**A. Cấu hình Credentials (Thông tin xác thực)**
- Tìm các node có biểu tượng Discord (màu xanh dương).
- Nhấn vào node, chọn **Credentials**.
- Nếu chưa có, tạo mới một **Discord Account**.
  - *Gợi ý:* Chọn **OAuth2** nếu dùng tài khoản người dùng, hoặc **Bot Token** nếu dùng Bot.
  - Điền **Bot Token** hoặc thông tin OAuth2 tương ứng.
  - Chọn **Server ID** (ID của server Discord cần dọn dẹp) trong phần cấu hình của node. *Mẹo: Bật Developer Mode trong Discord, chuột phải vào tên server -> Copy ID.*

**B. Chỉnh sửa Logic Lọc (Filter Node)**
- Tìm node tên là **`Filter Messages older than 7 days`**.
- Mặc định workflow xóa tin nhắn cũ hơn 7 ngày.
- Nếu các sếp muốn giữ tin nhắn lâu hơn (ví dụ: 30 ngày), hãy chỉnh lại điều kiện trong node này.
  - Đảm bảo tham số `date` so sánh với `now() - 7 days` (hoặc số ngày mong muốn).

**C. Kiểm tra các Node "Cool down" (Wait Nodes)**
Workflow có 3 node `Wait` để tránh bị Discord rate-limit (giới hạn tốc độ gọi API):
1. `Cool down Discord API rate limits`: Chạy sau khi lấy danh sách kênh.
2. `Cool down Get messages API rate limits`: Chạy sau khi lấy tin nhắn từ một kênh.
3. `Cool down Message deletion API rate limits`: Chạy sau khi xóa một loạt tin nhắn.
- **Lưu ý:** Nếu server của các sếp rất lớn (hàng nghìn kênh/tin nhắn), hãy tăng thời gian chờ (ví dụ từ 1 giây lên 2-5 giây) để đảm bảo an toàn tuyệt đối cho tài khoản.

**D. Cấu hình Lịch Chạy (Schedule Trigger)**
- Node **`Every day at 9pm`** mặc định chạy lúc 21:00.
- Các sếp có thể đổi giờ chạy bất kỳ, ví dụ: 02:00 sáng (khi server ít người hoạt động nhất) để tránh gây nhiễu.

#### 3. Kích hoạt ⚡️
1. Nhấn nút **Test Workflow** (hoặc chạy thử từng node) để đảm bảo không có lỗi credentials hay quyền truy cập.
   - *Mẹo:* Chạy thử ở chế độ "Execute Workflow" và kiểm tra xem nó có lấy được danh sách kênh và tin nhắn không.
2. Nếu mọi thứ ổn, nhấn nút **Active** (góc trên bên phải) để bật workflow.
3. Workflow sẽ tự động chạy vào khung giờ đã định.

### ✍️ Mẹo & gợi ý nâng cao
- **Gửi báo cáo qua Telegram/Slack:** Thêm một node `Telegram` hoặc `Slack` ở cuối workflow để gửi thông báo: *"Đã dọn dẹp xong! Đã xóa X tin nhắn từ Y kênh."* Giúp các sếp nắm bắt tình hình mà không cần vào n8n kiểm tra.
- **Lọc theo Kênh cụ thể:** Thay vì xóa toàn bộ server, các sếp có thể thêm một node `Filter` ngay sau `Get all Discord channels` để chỉ xóa tin nhắn ở các kênh công khai (public channels), giữ nguyên tin nhắn ở kênh riêng tư (private channels) hoặc kênh quan trọng.
- **Lưu Log:** Thêm node `Google Sheets` hoặc `Postgres` để ghi lại lịch sử xóa (kênh nào, bao nhiêu tin, thời gian). Rất hữu ích cho việc kiểm toán dữ liệu.
- **Xử lý Lỗi (Error Workflow):** Như ghi chú trong workflow gốc, hãy tạo một **Error Workflow** riêng. Khi workflow chính gặp lỗi (ví dụ: mất kết nối mạng, Discord bị bảo trì), nó sẽ gửi thông báo lỗi đến email hoặc Telegram của các sếp để kịp thời xử lý.

### 📌 Kết luận
Việc duy trì một server Discord sạch sẽ và tuân thủ quy định không nên là gánh nặng cho đội ngũ quản trị. Với workflow **Nightly Discord Channel Cleanup** này, các sếp đã tự động hóa hoàn toàn quy trình dọn dẹp dữ liệu cũ. Chỉ mất 5 phút để cấu hình, các sếp sẽ có một "người dọn dẹp" làm việc chăm chỉ mỗi đêm, giúp server luôn chuyên nghiệp và an toàn.

Hãy import ngay và trải nghiệm sự khác biệt! 🚀