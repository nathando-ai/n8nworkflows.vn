---
title: "🚀 Cách tự động lấy dữ liệu từ Cockpit CMS vào n8n cực kỳ nhanh chóng"
description: "Hướng dẫn chi tiết cách kết nối và lấy danh sách entries từ Cockpit CMS collection tự động bằng n8n, tiết kiệm thời gian quản trị nội dung."
slug: "lay-du-lieu-tu-cockpit-collection-n8n"
tags: [n8n, automation, no-code, cockpit-cms, headless-cms, api-integration]
keywords: [n8n workflow, cockpit cms n8n, lay du lieu cockpit, tu dong hoa cockpit, n8n building blocks]
keywords_additional: [cockpit collection, n8n cockpit integration]
---

# 🚀 Tự động hóa lấy danh sách Entries từ Cockpit CMS Collection trong n8n

Việc quản lý nội dung từ các Headless CMS như Cockpit và đồng bộ dữ liệu sang các nền tảng khác thường tốn nhiều thời gian nếu làm thủ công. Thay vì phải gọi API thủ công mỗi lần cần kiểm tra dữ liệu, các sếp hoàn toàn có thể tự động hóa quy trình này chỉ với 2 nodes cực kỳ đơn giản trên n8n.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%**: Không cần viết code hay gọi API thủ công để truy xuất dữ liệu từ Cockpit CMS.
- **Linh hoạt tích hợp**: Dữ liệu lấy về từ Cockpit collection có thể làm nguồn vào (input) cho các workflow phức tạp tiếp theo như gửi email, đồng bộ Google Sheets, hoặc đẩy lên CRM.
- **Tiết kiệm thời gian**: Giảm thiểu thao tác chuyển đổi giữa các tab quản trị.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống **Cockpit CMS** đang hoạt động.
- **API Token** hoặc thông tin đăng nhập của Cockpit để cấu hình `Cockpit API Credentials` trong n8n.
- Một instance n8n (Cloud hoặc Self-hosted).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trên n8n, sau đó copy cấu trúc gồm 2 nodes (`Manual Trigger` và `Cockpit`) hoặc sử dụng file JSON từ template gốc để import trực tiếp vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này siêu gọn nhẹ, chỉ bao gồm 2 nodes chính cần lưu ý:
- **Node `On clicking 'execute'` (manualTrigger)**: Node này dùng để chạy thủ công khi test. Các sếp có thể thay thế bằng *Schedule Trigger* (chạy định kỳ hàng ngày/hàng giờ) hoặc *Webhook* tùy theo nhu cầu thực tế.
- **Node `Cockpit` (cockpit)**: 
  - Chọn hoặc tạo mới **Credentials** (`cockpitApi`), trong đó điền URL của Cockpit CMS và API Access Token.
  - Cấu hình các tham số để lấy đúng Collection cần thiết (ví dụ: `Collection Name`, phương thức lấy dữ liệu, bộ lọc filter nếu có).

#### 3. Kích hoạt ⚡️
- Nhấn nút **"Execute Workflow"** để test thử xem dữ liệu từ Cockpit collection có đổ về thành công hay không.
- Sau khi kiểm tra dữ liệu trả về chính xác, các sếp có thể thay đổi Trigger theo ý muốn và bật **Active** workflow để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Đồng bộ đa nền tảng**: Nối tiếp node Cockpit với node Google Sheets hoặc Airtable để lưu trữ bản sao dữ liệu tự động.
- **Cảnh báo qua Chat**: Kết hợp thêm node Telegram hoặc Slack để thông báo ngay cho đội ngũ khi có một bài viết/entry mới được tạo trên Cockpit CMS.
- **Chạy định kỳ**: Thay thế Trigger thủ công bằng *Schedule Trigger* để n8n tự động quét collection định kỳ mỗi sáng.

### 📌 Kết luận
Chỉ với vài phút thiết lập cùng 2 nodes cơ bản trong n8n, các sếp đã có thể kết nối mượt mà với Cockpit CMS collection và mở ra vô số kịch bản tự động hóa tuyệt vời khác. Triển khai ngay thôi nào các sếp ơi!