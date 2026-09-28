---
title: "🚀 Tự động lấy danh sách Release từ Sentry bằng n8n cực kỳ nhanh chóng"
description: "Hướng dẫn tự động hóa quy trình quản lý và trích xuất toàn bộ thông tin release từ Sentry.io vào hệ thống của bạn một cách dễ dàng với n8n."
slug: "tu-dong-lay-danh-sach-release-tu-sentry-bang-n8n"
tags: [n8n, automation, no-code, sentry, devops, engineering]
keywords: [n8n workflow, sentry automation, lay release sentry, quan ly release sentry, n8n sentry integration]
keywords: [n8n workflow, tự động hóa, sentry.io, devops automation]
---

# 🚀 Tự động lấy danh sách Release từ Sentry bằng n8n

Việc theo dõi các phiên bản (releases) phần mềm trên Sentry thủ công thường tốn nhiều thời gian của các kỹ sư DevOps và Tech Lead, đặc biệt khi cần tổng hợp báo cáo hoặc đồng bộ dữ liệu sang các nền tảng khác. 

Workflow n8n này sẽ giúp các sếp tự động hóa toàn bộ quy trình: vừa có thể tạo release mới, vừa dễ dàng lấy toàn bộ danh sách các release hiện có từ Sentry.io chỉ bằng một cú click hoặc kích hoạt tự động mà không cần viết code phức tạp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian:** Tự động hóa việc truy xuất dữ liệu release từ Sentry thay vì tra cứu thủ công trên giao diện web.
- **Đồng bộ liền mạch:** Dễ dàng chuyển dữ liệu release sang các công cụ quản lý dự án, Google Sheets, hoặc gửi thông báo.
- **Hoạt động linh hoạt:** Có thể kích hoạt thủ công khi cần kiểm tra hoặc tích hợp vào các pipeline CI/CD lớn hơn.
:::

### ❌ Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Đã cài đặt n8n (Self-hosted hoặc n8n Cloud).
- Tài khoản Sentry.io và quyền truy cập API.
- **Sentry API Credentials** (`sentryIoApi`) để kết nối n8n với tài khoản Sentry của các sếp.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Copy mã JSON của workflow hoặc tải file JSON từ nguồn cấp.
- Mở n8n Editor của các sếp, chọn **Add workflow** -> **Import from File** hoặc dán trực tiếp vào màn hình làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 3 nodes cơ bản sau:

- **On clicking 'execute' (`manualTrigger`):** 
  - Đây là điểm khởi đầu dạng thủ công. Các sếp có thể thay thế node này bằng *Webhook*, *Schedule Trigger (Cron)* hoặc *Schedule interval* nếu muốn tự động chạy định kỳ hàng ngày/hàng tuần.
- **Sentry.io (`sentryIo` - Create Release):** 
  - Node này chịu trách nhiệm tạo một release mới trên Sentry.
  - *Cấu hình:* Chọn đúng Credentials `sentryIoApi`, điền thông tin tổ chức (Organization), dự án (Project) và phiên bản (Version) release cần tạo.
- **Sentry.io1 (`sentryIo` - Get All Releases):** 
  - Node này thực hiện câu lệnh gọi API để lấy toàn bộ danh sách các release hiện có trên Sentry.
  - *Cấu hình:* Kết nối chung `sentryIoApi`, chọn Resource là `release` và Operation là `getAll`. Điền thông tin Organization và Project tương ứng để lọc dữ liệu chính xác.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Test workflow** để chạy thử nghiệm và kiểm tra dữ liệu trả về từ Sentry ở bảng Output bên dưới.
- Sau khi kết quả đã chính xác, bật công tắc **Active** ở góc trên cùng bên phải để workflow sẵn sàng hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối thông báo:** Thêm node **Slack** hoặc **Telegram** sau node lấy danh sách release để gửi thông báo tự động về nhóm chat mỗi khi có bản release mới được ghi nhận trên Sentry.
- **Lưu trữ dữ liệu:** Thêm node **Google Sheets** hoặc **Notion** để lưu trữ toàn bộ lịch sử release phục vụ cho việc kiểm toán và làm báo cáo kỹ thuật định kỳ.
- **Tích hợp CI/CD:** Thay đổi trigger thành Webhook để kích hoạt workflow này ngay sau khi quá trình build/deploy hoàn tất trên GitHub Actions hoặc GitLab CI.

### 📌 Kết luận
Với workflow n8n tích hợp Sentry này, việc quản lý và trích xuất dữ liệu release phần mềm trở nên tự động hóa hoàn toàn, giúp đội ngũ kỹ thuật tập trung vào code thay vì tốn thời gian thao tác thủ công. Hãy áp dụng ngay vào hệ thống của các sếp nhé!