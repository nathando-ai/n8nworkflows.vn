---
title: "🚀 Tự động giám sát chất lượng danh sách Klaviyo, chấm điểm suy giảm & lọc tương tác với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động kiểm tra danh sách Klaviyo hàng ngày, phân loại mức độ suy giảm tương tác, lưu trữ vào Postgres và tự động hủy đăng ký (suppress) các tài khoản không hoạt động lâu ngày để bảo vệ uy tín gửi email."
slug: "tu-dong-giam-sat-chat-luong-danh-sach-klaviyo-n8n"
tags: [n8n, automation, no-code, klaviyo, postgres, email-marketing]
keywords: [n8n workflow, klaviyo list decay, tu dong hoa email marketing, quan ly danh sach klaviyo, n8n postgres gmail]
---

# 🚀 Tự động giám sát chất lượng danh sách Klaviyo, chấm điểm suy giảm & lọc tương tác

Các sếp làm email marketing chắc chắn hiểu rõ nỗi đau: danh sách subscriber (thuê bao) ngày càng phình to nhưng tỷ lệ mở (open rate) và click lại èo uột, thậm chí tệ hơn là email bắt đầu rơi vào mục Spam. Nguyên nhân lớn nhất là do các tài khoản "ma", không còn tương tác suốt nhiều tháng trời làm "bẩn" uy tín tên miền gửi (sender reputation).

Việc kiểm tra và lọc thủ công hàng ngàn profile trên Klaviyo là cơn ác mộng tốn thời gian. Giải pháp ở đây là để **n8n** tự động hóa toàn bộ quy trình này: định kỳ hàng đêm, hệ thống sẽ quét toàn bộ danh sách, chấm điểm mức độ suy giảm tương tác (list decay), lưu log lịch sử vào Postgres, gửi báo cáo qua Gmail và đặc biệt là **tự động vô hiệu hóa (suppress)** các profile "ngủ đông" trên 90 ngày để bảo vệ danh hiệu nhà gửi email uy tín của các sếp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Bảo vệ Sender Reputation:** Tự động phát hiện và dọn dẹp các email không tương tác quá 90 ngày, giúp tỷ lệ vào Inbox luôn ở mức cao nhất.
- **Tiết kiệm chi phí Klaviyo:** Loại bỏ các contact "rác" giúp tối ưu hóa chi phí gói cước Klaviyo hàng tháng.
- **Báo cáo trực quan mỗi sáng:** Nhận bản báo cáo HTML chi tiết qua Gmail ngay khi thức dậy với đầy đủ số liệu phân hóa theo tầng suy giảm.
- **Kiểm toán dữ liệu minh bạch:** Mọi profile và lịch sử chạy đều được lưu trữ cẩn thận vào cơ sở dữ liệu Postgres để tiện tra cứu về sau.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **Klaviyo Account:** API Key có quyền đọc Profiles và ghi Bulk Suppressions.
- **PostgreSQL Database:** Đã tạo sẵn database để lưu log.
- **Gmail Account:** Đã cấu hình OAuth2 để gửi báo cáo và cảnh báo lỗi.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này và import trực tiếp vào giao diện n8n Editor của các sếp, hoặc tạo mới một workflow và copy/paste toàn bộ cấu trúc nodes vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru, các sếp cần chú ý cấu hình kỹ các phần sau:

- **Klaviyo API Key & HTTP Request:** 
  - Tạo credential kiểu *HTTP Header Auth*. Tên Header là `Authorization`, giá trị là `Klaviyo-API-Key <YOUR_KEY>`. Áp dụng credential này cho node **Get All Profiles**.
  - Thêm biến môi trường `KLAVIYO_API_KEY` vào cài đặt n8n của các sếp để node **Suppress Critical in Batches** có thể gọi API hàng loạt.
- **PostgreSQL Database:** 
  - Kết nối thông tin database của các sếp vào các node: **Log Profiles to DB**, **Insert Run Summary**, và **Log Error to DB**.
  - *Lưu ý quan trọng:* Các sếp phải tạo sẵn 2 bảng sau trong Postgres trước khi bật workflow:
    1. `klaviyo_decay_log` (Lưu từng profile theo mỗi lần chạy): các cột gồm `profile_id`, `email`, `days_since_active`, `tier`, `engagement_score`, `action_taken`, `run_id`.
    2. `klaviyo_run_summary` (Lưu tổng kết mỗi lần chạy): các cột gồm `run_id`, `run_start`, `run_end`, `total_profiles`, `active_count`, `moderate_count`, `high_count`, `critical_count`, `suppressed_count`, `status`, `error_message`.
- **Gmail Credentials:** 
  - Cấu hình tài khoản Gmail (OAuth2) cho node **Send a message** (gửi báo cáo hàng ngày) và **Send Error Alert** (gửi cảnh báo nếu có lỗi).
  - Cập nhật địa chỉ email nhận báo cáo và nhận cảnh báo lỗi thành email của các sếp.

#### 3. Các phân đoạn chính trong Workflow ⚡️
- **Trigger & Initialize (`Schedule: Daily 2AM` & `Set: Initialize Run`):** Chạy tự động lúc 2 giờ sáng mỗi ngày và khởi tạo metadata cho phiên chạy.
- **Fetch & Score (`Get All Profiles`, `Extract Profile Items`, `Score Profiles`):** Lấy toàn bộ profile từ Klaviyo, bóc tách dữ liệu phân trang và chấm điểm số ngày không hoạt động.
- **Phân loại Decay Tiers:**
  - 🟢 **Active** (< 30 ngày): Bình thường.
  - 🟡 **Moderate Decay** (30–60 ngày): Chỉ ghi log.
  - 🟠 **High Decay** (60–90 ngày): Chỉ ghi log.
  - 🔴 **Critical** (90+ ngày): Tự động gom nhóm 100 profile/lần để gửi sang Klaviyo Bulk Suppression API vô hiệu hóa.
- **Báo cáo & Xử lý lỗi (`Build Email HTML`, `Send a message`, nhánh `Error Trigger`):** Tổng hợp số liệu thành file HTML đẹp mắt gửi qua Gmail và tự động ghi log kèm email thông báo ngay lập tức nếu xảy ra sự cố bất ngờ.

#### 4. Kích hoạt ⚡️
- Chạy thử công khai (Test run) một lần để kiểm tra xem dữ liệu có đẩy vào Postgres và Klaviyo chính xác không.
- Bật công tắc **Active** để workflow tự động hoạt động hàng đêm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack/Telegram:** Thay vì chỉ nhận email, các sếp có thể nối thêm node Slack hoặc Telegram vào nhánh báo cáo tổng kết để team marketing nắm thông tin nhanh chóng trên chatwork.
- **Tùy chỉnh ngưỡng thời gian:** Nếu ngách sản phẩm của các sếp có chu kỳ mua hàng dài hơn, hãy chỉnh sửa logic tính điểm trong các node Code (ví dụ: đổi mốc Critical từ 90 ngày lên 120 ngày).
- **Lưu trữ Dashboard:** Kết nối cơ sở dữ liệu Postgres với Metabase hoặc Google Looker Studio để vẽ biểu đồ theo dõi sức khỏe danh sách subscriber theo thời gian thực.

### 📌 Kết luận
Việc duy trì một danh sách email "sạch" là chìa khóa sống còn của bất kỳ chiến dịch Email Marketing nào. Với workflow n8n này, các sếp hoàn toàn có thể tự động hóa toàn bộ quy trình chăm sóc và dọn dẹp danh sách Klaviyo mà không tốn một phút nhân lực thủ công nào. Triển khai ngay thôi các sếp ơi!