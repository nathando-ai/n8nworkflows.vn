---
title: "🚀 Tự động gửi email chăm sóc khách hàng mới từ Google Sheets qua Microsoft Outlook"
description: "Hướng dẫn thiết lập workflow n8n giúp tự động gửi email template cho khách hàng mới từ Google Sheets theo lịch trình và cập nhật trạng thái để tránh gửi lặp."
slug: "tu-dong-gui-email-leads-google-sheets-outlook"
tags: [n8n, automation, google-sheets, microsoft-outlook, email-marketing]
keywords: [n8n workflow, tu dong hoa email, google sheets outlook, chamsoc khach hang, no-code automation]
---

# 🚀 Tự động gửi email chăm sóc khách hàng mới từ Google Sheets qua Microsoft Outlook

Các sếp có đang gặp tình trạng danh sách khách hàng mới (leads) đổ về Google Sheets mỗi ngày nhưng đội ngũ Sales lại phải copy/paste thủ công từng email để gửi? Việc này không chỉ tốn hàng giờ đồng hồ mà còn dễ dẫn đến sai sót, gửi trùng lặp hoặc bỏ sót khách hàng tiềm năng.

Được thiết kế bởi chuyên gia **Robert Breen**, workflow n8n này sẽ giải quyết triệt để nỗi đau đó. Hệ thống sẽ tự động quét danh sách khách hàng mới theo lịch trình, gửi email chăm sóc qua Microsoft Outlook và tự động cập nhật trạng thái "Đã liên hệ" (Contacted) lên Google Sheets để đảm bảo không bao giờ gửi nhầm một khách hàng hai lần!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Không cần động tay copy/paste email, hệ thống tự động chạy ngầm theo lịch hẹn hàng ngày.
- **Cá nhân hóa chuyên nghiệp:** Gửi email outreach với nội dung mẫu chuẩn xác qua tài khoản Microsoft Outlook cá nhân hoặc doanh nghiệp.
- **Kiểm soát chặt chẽ:** Tự động đánh dấu trạng thái "đã liên hệ" vào Google Sheets, loại bỏ hoàn toàn rủi ro gửi trùng lặp cho một khách hàng.
- **Tiết kiệm thời gian:** Giải phóng hàng chục giờ làm việc thủ công mỗi tuần cho đội ngũ kinh doanh để tập trung chốt sale.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn n8n (Cloud hoặc Self-hosted).
- **Google Account:** Có quyền truy cập Google Sheets chứa danh sách khách hàng (chú ý cột `Email` và cột trạng thái `Contacted`).
- **Microsoft Outlook Account:** Tài khoản Microsoft 365 / Outlook để gửi email.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ n8n template (ID: 8095) hoặc copy toàn bộ mã JSON và dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 5 nodes chính cần được cấu hình chuẩn xác:

- **Schedule Trigger:** 
  - Cấu hình tần suất chạy (ví dụ: chạy mỗi ngày 1 lần vào 9:00 sáng) để quét các lead mới phát sinh.
- **Get row(s) in sheet3 (Google Sheets):**
  - Tạo kết nối **Google Sheets (OAuth2)** trong mục Credentials.
  - Chọn đúng file Google Sheets chứa danh sách khách hàng (`Lead Source`) và chọn worksheet phù hợp.
  - Đảm bảo trong sheet của các sếp có ít nhất cột `Email` và cột `Contacted` (để trống đối với khách hàng mới).
- **Filter1:**
  - Bộ lọc sẽ giữ lại các dòng dữ liệu có cột `Contacted` đang trống (chưa được gửi email).
- **Send a message (Microsoft Outlook):**
  - Tạo kết nối **Microsoft Outlook OAuth2**. 
    - *n8n Cloud:* Chỉ cần chọn Connect và đăng nhập tài khoản Microsoft.
    - *Self-hosted:* Cần đăng ký App trên Azure Portal (thêm redirect URL: `https://YOUR_N8N_URL/rest/oauth2-credential/callback`, cấu hình API permissions `Mail.Send`, `User.Read`, `offline_access`).
  - Trong node, trỏ ô `To` tới biến `{{$json.Email}}`.
  - Tùy chỉnh Tiêu đề (`Subject`) và Nội dung (`Body`) email theo chiến dịch của doanh nghiệp.
- **Append or update row in sheet1 (Google Sheets):**
  - Sử dụng lại Credentials Google Sheets.
  - Chọn chế độ operation là `appendOrUpdate`.
  - Cấu hình để cập nhật dòng hiện tại, ghi đè giá trị vào cột `Contacted` (đánh dấu là "Yes" hoặc thời gian đã gửi) để lần chạy sau bộ lọc sẽ bỏ qua lead này.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thử với một vài dữ liệu mẫu xem email có gửi đi và Google Sheets có được cập nhật hay không.
- Sau khi test thành công, bật công tắc **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối thông báo:** Thêm node **Slack** hoặc **Telegram** vào sau bước gửi email thành công để bắn một thông báo nhỏ về nhóm kinh doanh: *"Đã gửi email outreach tự động cho khách hàng: [Email]"*.
- **Theo dõi log lỗi:** Thêm nhánh Error Trigger để nếu tài khoản Outlook gặp lỗi xác thực hoặc hết hạn token, hệ thống sẽ gửi cảnh báo ngay lập tức cho quản lý hệ thống.
- **Chia chiến dịch theo tag:** Mở rộng Google Sheets thêm cột `Campaign_Type` để bộ lọc phân loại và gửi các mẫu email template khác nhau tùy theo dịch vụ khách hàng quan tâm.

### 📌 Kết luận
Việc tự động hóa quy trình chăm sóc khách hàng mới từ Google Sheets sang Outlook không chỉ giúp doanh nghiệp tăng tốc độ phản hồi mà còn chuyên nghiệp hóa quy trình vận hành. Hãy cài đặt ngay workflow này để tối ưu hóa hiệu suất làm việc của đội ngũ ngay hôm nay!