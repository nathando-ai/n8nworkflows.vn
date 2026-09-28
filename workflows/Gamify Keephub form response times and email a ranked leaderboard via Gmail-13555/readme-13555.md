---
title: "🚀 Gamify Keephub: Tự động hóa bảng xếp hạng tốc độ phản hồi form qua Gmail"
description: "Biến các form Keephub thành cuộc thi tốc độ thú vị, tự động xếp hạng thời gian phản hồi, tổng hợp dữ liệu tổ chức và gửi email báo cáo HTML chuyên nghiệp."
slug: "gamify-keephub-form-response-times-leaderboard"
tags: [n8n, automation, no-code, keephub, hr, gmail, gamification]
keywords: [n8n workflow, keephub automation, gamify form response, tự động hóa hr, gửi email leaderboard]
---

# 🚀 Gamify Keephub: Tự động hóa bảng xếp hạng tốc độ phản hồi form qua Gmail

Việc thu thập phản hồi form nội bộ đôi khi khá nhàm chán và các đội ngũ HR hay Quản lý Đào tạo (L&D) thường gặp khó khăn trong việc khuyến khích nhân viên hoàn thành nhiệm vụ nhanh chóng. Việc đo lường thủ công ai là người nộp form nhanh nhất tốn rất nhiều thời gian và dễ xảy ra sai sót.

Workflow n8n này sẽ giải quyết triệt để vấn đề đó bằng cách biến bất kỳ Keephub form nào thành một cuộc thi tốc độ (gamification) hoàn toàn tự động 100% không cần code. Các sếp chỉ cần nhập Form ID, hệ thống sẽ tự động chấm điểm tốc độ, tổng hợp kết quả và gửi một bảng xếp hạng (leaderboard) đẹp mắt qua Gmail!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Gamification hóa quy trình:** Tạo động lực cho nhân viên hoàn thành form nhanh chóng thông qua các cuộc thi tốc độ có thưởng hoặc vinh danh.
- **Tự động hóa hoàn toàn:** Từ khâu thu thập dữ liệu, tính toán thời gian, tra cứu thông tin phòng ban (org-unit) đến việc gửi báo cáo.
- **Báo cáo chuyên nghiệp:** Tự động tạo bảng xếp hạng HTML (top 10 + phân tích theo đơn vị tổ chức) và gửi thẳng vào hộp thư Gmail của người yêu cầu.
- **Xử lý lỗi thông minh:** Các node được cấu hình tiếp tục chạy ngay cả khi có bản ghi lỗi, đảm bảo báo cáo không bao giờ bị gián đoạn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Self-hosted hoặc Cloud).
- Cài đặt community node **`n8n-nodes-keephub`** (v1.5+) từ phần Cài đặt của n8n.
- Tài khoản và thông tin xác thực (Credentials):
  - **Keephub API Credentials** (Bearer Token & Login API).
  - **Gmail Account** (hoặc SMTP tương đương) để gửi báo cáo.
- **Keephub Form ID** cần lấy dữ liệu.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ kho lưu trữ n8n (Link: `https://n8n.io/workflows/13555`), sau đó chọn **Import from File** hoặc copy và paste trực tiếp đoạn mã JSON vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import thành công, các sếp cần cấu hình các thành phần sau:
- **`🚀 Start here!` (Form Trigger):** Đây là điểm khởi đầu, nơi người dùng nhập Email, Keephub Form ID và thời gian bắt đầu cuộc thi (tùy chọn).
- **Các node Keephub (`Find form submissions by form`, `Get submitter details`, `Calculate response duration`, `Get Orgchart Info`):** Các sếp cần liên kết tài khoản Keephub của mình thông qua `keephubBearerApi` hoặc `keephubLoginApi`. Đảm bảo điền chính xác Form ID từ URL của form Keephub.
- **Code Nodes (`✂️ Split into Items`, `🔗 Enrich with User Data`, `📊 Aggregate Stats & Build Report`):** Các node này dùng để xử lý mảng dữ liệu, tính toán khoảng thời gian phản hồi (dựa trên thời gian tùy chỉnh hoặc thời gian mặc định của Keephub), và gom nhóm theo đơn vị tổ chức. Không cần sửa code bên trong trừ khi muốn tùy chỉnh giao diện HTML của bảng xếp hạng.
- **`📧 Send Competition Report` (Gmail):** Kết nối tài khoản Gmail cá nhân hoặc doanh nghiệp để hệ thống tự động gửi email báo cáo hoàn thành cuộc thi đến người khởi tạo.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Test workflow**, điền các thông tin thử nghiệm vào form n8n và kiểm tra hộp thư đến để xem kết quả.
- Nếu mọi thứ hoạt động trơn tru, hãy bật công tắc **Active workflow** ở góc trên cùng bên phải để hệ thống sẵn sàng hoạt động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh chat:** Thay vì chỉ gửi qua Gmail, các sếp có thể nối thêm node Slack hoặc Telegram để bắn thông báo top 3 người nhanh nhất lên group chung của công ty nhằm tăng tính cạnh tranh.
- **Lưu lịch sử:** Thêm một node Google Sheets ở cuối workflow để lưu trữ toàn bộ lịch sử các cuộc thi và thời gian phản hồi theo thời gian thực phục vụ việc đánh giá KPI định kỳ.
- **Lên lịch định kỳ:** Thay thế Form Trigger bằng Schedule Trigger để tự động chạy báo cáo hàng tuần/hàng tháng cho các form khảo sát nội bộ quan trọng.

### 📌 Kết luận
Workflow này là một "vũ khí" cực kỳ lợi hại cho các đội ngũ HR và quản lý vận hành muốn số hóa và làm sinh động hóa các hoạt động nội bộ. Hãy triển khai ngay hôm nay để tạo ra những cuộc thi tương tác thú vị cho doanh nghiệp của các sếp!