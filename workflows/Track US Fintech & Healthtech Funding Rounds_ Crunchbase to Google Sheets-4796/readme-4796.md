---
title: "💰 Theo dõi vòng gọi vốn Fintech & Healthtech Mỹ: Crunchbase → Google Sheets"
description: "Tự động hóa việc theo dõi các vòng gọi vốn mới nhất của các công ty Fintech và Healthtech Mỹ từ Crunchbase và lưu trữ dữ liệu vào Google Sheets hàng ngày."
slug: "theo-doi-vong-goi-von-fintech-healthtech-my"
tags: [n8n, automation, no-code, fintech, healthtech, crunchbase, google-sheets]
keywords: [n8n workflow, tự động hóa, theo dõi vòng gọi vốn, fintech, healthtech, crunchbase, google sheets]
---

# 💰 Theo dõi vòng gọi vốn Fintech & Healthtech Mỹ: Crunchbase → Google Sheets

[Các sếp đang làm việc trong lĩnh vực Fintech và Healthtech Mỹ chắc hẳn đã biết rằng việc theo dõi các vòng gọi vốn mới nhất là một công việc cực kỳ quan trọng. Tuy nhiên, việc làm thủ công này tốn thời gian và dễ gây lỗi. Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình theo dõi và lưu trữ dữ liệu vào Google Sheets hàng ngày.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa toàn bộ quá trình theo dõi và lưu trữ dữ liệu.
- **Chính xác**: Dữ liệu được cập nhật hàng ngày và lưu trữ một cách chính xác.
- **Cá nhân hóa**: Các sếp có thể tùy chỉnh dữ liệu theo nhu cầu của mình.
- **Hoạt động liên tục**: Workflow chạy tự động hàng ngày mà không cần can thiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Crunchbase với quyền truy cập API.
- Tài khoản Google với quyền truy cập Google Sheets.
- API Key từ Crunchbase.
- Thiết lập Google Sheets với các cột: `Date`, `Company`, `Funding Round`, `Amount`, `Lead Investors`, `Location`, `Sector`, `Industry`, `Funding Type`, `Funding Stage`, `Funding Status`, `Funding Date`, `Funding URL`.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor.
2. Nhấn vào nút `Import from URL`.
3. Dán link sau vào ô nhập liệu: `https://n8n.io/workflows/4796`.
4. Nhấn `Import`.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node "Daily Check for New Funding Rounds"**:
  - Thiết lập lịch chạy hàng ngày.
  - Chọn thời gian chạy phù hợp với nhu cầu của các sếp.

- **Node "Fetch Crunchbase Funding Rounds"**:
  - Thiết lập API Key từ Crunchbase.
  - Cấu hình URL để lấy dữ liệu từ Crunchbase.

- **Node "Extract & Format Funding Data"**:
  - Kiểm tra và chỉnh sửa mã JavaScript để trích xuất và định dạng dữ liệu theo nhu cầu.
  - Đảm bảo dữ liệu được trích xuất đúng với các cột trong Google Sheets.

- **Node "Save to Google Sheets"**:
  - Thiết lập tài khoản Google và Google Sheets.
  - Chọn Google Sheets và bảng tính cần lưu trữ dữ liệu.
  - Đảm bảo các cột trong Google Sheets đã được thiết lập đúng với dữ liệu được trích xuất.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Các sếp có thể nhận thông báo ngay khi có vòng gọi vốn mới.
- **Lưu log**: Các sếp có thể lưu log để theo dõi lịch sử các vòng gọi vốn.
- **Gửi báo cáo định kỳ**: Các sếp có thể gửi báo cáo định kỳ về các vòng gọi vốn mới nhất.

### 📌 Kết luận
Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình theo dõi và lưu trữ dữ liệu về các vòng gọi vốn mới nhất của các công ty Fintech và Healthtech Mỹ. Hãy áp dụng ngay để tiết kiệm thời gian và tăng hiệu quả công việc!