---
title: "📧 Tự Động Hóa Email Cá Nhân Hóa (Mail Merge) Từ Google Sheets Sang Gmail - Không Cần Code!"
description: "Học cách tự động hóa việc gửi email cá nhân hóa từ Google Sheets sang Gmail chỉ trong vài phút, tiết kiệm thời gian và tăng hiệu quả marketing cho doanh nghiệp. Workflow này hỗ trợ cả gửi bulk email và gửi email theo điều kiện tự động."
slug: "tieu-dong-hoa-email-canh-nhan-hoa-tu-google-sheets-sang-gmail"
tags: [n8n, automation, no-code, google-sheets, gmail, mail-merge]
keywords: [tự động hóa email, mail merge n8n, gửi email bulk tự động, google sheets gmail automation, tự động hóa marketing]
---

# 🚀 **Tự Động Hóa Email Cá Nhân Hóa Từ Google Sheets Sang Gmail - Không Cần Code!**

Bạn có bao giờ phải mất nhiều giờ để gửi email cá nhân hóa cho khách hàng, đồng nghiệp hay khách hàng tiềm năng? Hay phải copy-paste dữ liệu từ Google Sheets sang Gmail một cách thủ công, dễ mắc lỗi và tốn thời gian? **Workflow này sẽ giải quyết tất cả những vấn đề đó!**

Với **n8n**, bạn có thể **tự động hóa hoàn toàn** việc gửi email cá nhân hóa từ Google Sheets sang Gmail, **không cần viết một dòng code nào**. Workflow này hỗ trợ hai cách gửi email:
1. **Gửi bulk email (Mail Merge)**: Sử dụng dữ liệu từ Google Sheets để gửi email cá nhân hóa cho nhiều người một lúc.
2. **Gửi email theo điều kiện tự động**: Email được gửi tự động khi dữ liệu trong Google Sheets thay đổi (ví dụ: khi cột "Status" được cập nhật thành "Ready to Send").

Kết quả? **Tiết kiệm thời gian, giảm sai sót, và tăng hiệu quả trong việc tương tác với khách hàng!**

---
## 🎯 **Kết quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần copy-paste dữ liệu từ Google Sheets sang Gmail.
- **Cá nhân hóa hoàn toàn**: Email được tự động thay đổi nội dung dựa trên dữ liệu từ Google Sheets (tên, nội dung, liên kết...).
- **Hoạt động liên tục 24/7**: Email được gửi tự động theo lịch trình hoặc khi dữ liệu thay đổi.
- **Giảm sai sót**: Không còn lo lắng về việc quên gửi email hoặc gửi sai nội dung.
- **Tích hợp hoàn hảo**: Sử dụng Google Sheets và Gmail, hai công cụ mà hầu hết doanh nghiệp đã sử dụng.
:::

---
## 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
- **Tài khoản Google** (để sử dụng Google Sheets và Gmail).
- **Google Sheets template** (bạn có thể sao chép từ [đây](https://docs.google.com/spreadsheets/d/1fWg_GOU0m_2cQpah7foDiz1WqTRKjCbJJCLBGCvJlXc/edit?usp=sharing)).
- **API Key hoặc OAuth 2.0** cho Google Sheets và Gmail (n8n sẽ tự động tạo khi kết nối).
- **Dữ liệu trong Google Sheets** phải có các cột như: `Email`, `Name`, `Subject`, `Body`, và `Scheduled for send` (để điều khiển khi gửi email).
:::

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### 1. **Import Workflow 📥**
Bước 1: Tải workflow từ [n8n.io](https://n8n.io/workflows/8149) hoặc sao chép JSON từ trang này.
Bước 2: Mở **n8n Editor** và chọn **Import Workflow** (hoặc paste JSON vào ô Import Workflow).

:::note[LƯU Ý]
- Nếu bạn **self-hosted n8n**, hãy đảm bảo đã cài đặt các **credentials** cần thiết (Google Sheets OAuth 2.0 và Gmail).
- Nếu bạn dùng **n8n Cloud**, chỉ cần đăng nhập và import workflow.
:::

### 2. **Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **7 node chính**, và các sếp cần chú ý đến các bước sau:

#### **A. Cấu Hình Google Sheets**
1. **Node "Read Google Sheets data"**:
   - Chọn **credentials**: `googleSheetsOAuth2Api` (n8n sẽ tự động tạo khi kết nối đầu tiên).
   - Điền **Spreadsheet ID** (tìm trong URL của Google Sheets của bạn, ví dụ: `1fWg_GOU0m_2cQpah7foDiz1WqTRKjCbJJCLBGCvJlXc`).
   - Chọn **Sheet Name** (tên tab trong Google Sheets).
   - Chọn **Range** (ví dụ: `Sheet1!A:Z` để đọc toàn bộ dữ liệu).

#### **B. Cấu Hình Lịch Trình (Schedule Trigger)**
1. **Node "Schedule Trigger"**:
   - Chọn **cron expression** để xác định thời gian gửi email (ví dụ: `0 0 * * *` để gửi hàng ngày lúc 00:00).
   - Hoặc để **manual trigger** (gửi khi bạn kích hoạt thủ công).

#### **C. Lọc Email Theo Điều Kiện**
1. **Node "Pass on 'Scheduled for send'"**:
   - Chọn **filter condition**: `jsonpath("$.Scheduled for send")` == `true` (để chỉ gửi email khi cột này là `true`).
   - Nếu muốn gửi email theo ngày cụ thể, thay đổi điều kiện thành `jsonpath("$.Scheduled for send") == "2024-05-20"`.

#### **D. Gửi Email Cá Nhân Hóa**
1. **Node "Send an email"**:
   - Chọn **credentials**: `gmailOAuth2Api`.
   - Điền **Subject** và **Body** (sử dụng **variables** từ Google Sheets, ví dụ: `{{ $jsonpath("$.Name") }}` để hiển thị tên người nhận).
   - Chọn **To** từ cột `Email` trong Google Sheets (`{{ $jsonpath("$.Email") }}`).

#### **E. Cập Nhật Trạng Thái Email**
1. **Node "Update Status email column"**:
   - Chọn **credentials**: `googleSheetsOAuth2Api`.
   - Điền **Spreadsheet ID** và **Sheet Name** tương tự như node đọc dữ liệu.
   - Chọn **Range** (ví dụ: `Sheet1!D:D` để cập nhật cột `Status`).
   - Đặt **Value** thành `"Sent"` (để đánh dấu email đã được gửi).

---
### 3. **Kích Hoạt ⚡️**
1. **Test Run**:
   - Chọn **Run Workflow** và kiểm tra email đã được gửi chưa.
   - Kiểm tra Google Sheets để đảm bảo cột `Status` được cập nhật thành `"Sent"`.
2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active**.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[TIẾP CẬN HƠN]
- **Gửi email theo nhóm**: Sử dụng **Google Sheets Filter** để chia dữ liệu thành các nhóm (ví dụ: khách hàng mới, khách hàng cũ) và gửi email riêng cho mỗi nhóm.
- **Kết hợp với Slack/Telegram**: Sử dụng **Slack Node** để thông báo khi email đã được gửi thành công.
- **Lưu log gửi email**: Sử dụng **Set Node** để lưu dữ liệu gửi email vào một **Google Sheet khác** để theo dõi.
- **Gửi email theo thời gian cụ thể**: Sử dụng **Schedule Trigger** với cron expression phức tạp (ví dụ: gửi email vào thứ 2 và thứ 4 hàng tuần).
- **Tự động hóa từ nhiều nguồn**: Kết hợp với **Zapier** hoặc **Make (Integromat)** để lấy dữ liệu từ các ứng dụng khác (CRM, Shopify...) và tự động gửi email.
:::

---
## 📌 **Kết Luận**
Với **n8n**, bạn đã có một **công cụ tự động hóa email cá nhân hóa** mạnh mẽ, không cần code. **Workflow này giúp tiết kiệm thời gian, tăng hiệu quả và giảm sai sót** trong việc gửi email bulk hoặc theo điều kiện tự động.

**Hãy thử ngay và tự động hóa email của mình trong vài phút!** Nếu có bất kỳ câu hỏi nào, hãy để lại comment bên dưới. 🚀

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::