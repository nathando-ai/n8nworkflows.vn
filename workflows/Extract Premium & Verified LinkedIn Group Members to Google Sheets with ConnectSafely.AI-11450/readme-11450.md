---
title: "🚀 Tự Động Trích Xuất Thành Viên LinkedIn Premium & Verified Vào Google Sheets với n8n"
description: "Hướng dẫn chi tiết cách sử dụng workflow n8n kết hợp ConnectSafely.AI để tự động cào và lọc thành viên LinkedIn chất lượng cao, lưu trực tiếp vào Google Sheets."
slug: "trich-xuat-thanh-vien-linkedin-vao-google-sheets-n8n"
tags: [n8n, automation, lead-generation, linkedin, google-sheets]
keywords: [n8n workflow, trích xuất thành viên linkedin, connect safely ai, google sheets automation, cào dữ liệu linkedin]
---

# 🚀 Tự Động Trích Xuất Thành Viên LinkedIn Premium & Verified Vào Google Sheets

Các sếp có đang mệt mỏi với việc tìm kiếm khách hàng tiềm năng trên LinkedIn bằng cơm? Việc đi từng nhóm, lọc thủ công các tài khoản có tích xanh (Verified) hay tài khoản trả phí (Premium) để tiếp cận tốn hàng giờ đồng hồ mỗi ngày mà hiệu quả lại thấp? 

Đừng lo nữa! Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ mạnh mẽ, giúp tự động hóa toàn bộ quá trình trích xuất thành viên từ bất kỳ nhóm LinkedIn nào, lọc ra những profile chất lượng cao nhất và đồng bộ thẳng vào Google Sheets chạy ngầm 24/7.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 không bị gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Lọc leads chất lượng:** Tự động nhận diện tài khoản Premium và Verified (tích xanh) để tập trung vào đúng tệp khách hàng có tiền.
- **Tiết kiệm 90% thời gian:** Không cần copy-paste thủ công, hệ thống tự động gom hàng trăm profile mỗi phút.
- **Phân trang thông minh (Pagination):** Xử lý mượt mà cả những hội nhóm LinkedIn khủng có hàng chục ngàn thành viên.
- **Đồng bộ real-time:** Dữ liệu chi tiết từ Headline, URL profile, số lượng follower được đẩy thẳng vào Google Sheets gọn gàng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản ConnectSafely.ai:** Lấy API Token từ nền tảng này để gọi API cào dữ liệu nhóm LinkedIn.
- **Google Sheets:** Một trang tính (Spreadsheet) trống để lưu trữ dữ liệu khách hàng.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này hoặc copy đoạn mã JSON.
- Mở giao diện n8n Editor, chọn **Add workflow** -> **Import from File** (hoặc dán trực tiếp JSON vào màn hình làm việc).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy trơn tru, các sếp cần cấu hình chính xác các node sau:

- **Node `Initialize Pagination` (Code):** 
  - Mở node này và tìm biến `groupId`. Mặc định đang để ID `9357376` (Nhóm Product Hunt Promotion). 
  - Các sếp hãy thay thế bằng ID nhóm LinkedIn mục tiêu của mình.
- **Node `Fetch Group Members` (HTTP Request):**
  - Cấu hình Credentials loại **HTTP Bearer Auth** với token từ ConnectSafely.ai (`ConnectSafelyAI Token`).
  - Endpoint sử dụng: `https://api.connectsafely.ai/linkedin/groups/members`.
- **Node `Process & Filter Members` (Code):**
  - Node này đã viết sẵn logic để lọc các thành viên thỏa mãn điều kiện `isPremium === true`, `isVerified === true` hoặc có chứa badge tương ứng.
- **Node `Append to Google Sheets` (Google Sheets):**
  - Kết nối tài khoản **Google Sheets OAuth2**.
  - Chọn file Google Sheet và Sheet Name phù hợp. Đảm bảo các cột khớp với dữ liệu trả về: *Profile ID, First Name, Last Name, Headline, Profile URL, Follower Count, Is Premium, Is Verified*.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** chạy thử bằng nút **Start Workflow** (`manualTrigger`) để kiểm tra dữ liệu đổ về Google Sheets.
- Nếu mọi thứ xanh mướt, hãy gạt công tắc sang **Active** để hệ thống sẵn sàng hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node **Slack** hoặc **Telegram** vào sau node `✅ Workflow Complete` để nhận thông báo ngay về điện thoại mỗi khi cào xong một nhóm.
- **Tự động hóa định kỳ:** Thay thế node `Manual Trigger` bằng **Schedule Trigger** để hệ thống tự quét nhóm LinkedIn hàng tuần/hàng tháng cập nhật leads mới.
- **Nuôi dưỡng Lead:** Kết hợp dữ liệu từ Google Sheets này với các workflow gửi kết bạn/nhắn tin tự động tiếp theo để tối ưu chuyển đổi inbound.

### 📌 Kết luận
Việc khai thác khách hàng tiềm năng trên LinkedIn chưa bao giờ dễ dàng đến thế khi kết hợp sức mạnh của n8n và ConnectSafely.AI. Hãy thiết lập ngay hôm nay để biến hội nhóm LinkedIn thành cỗ máy hút leads tự động 24/7 cho doanh nghiệp của các sếp!