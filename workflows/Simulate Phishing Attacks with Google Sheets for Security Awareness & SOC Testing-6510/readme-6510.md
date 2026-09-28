---
title: "🎣 [Workflow n8n] Giả lập tấn công lừa đảo qua Google Sheets cho đào tạo nhận thức bảo mật & kiểm tra SOC"
description: "Workflow n8n tự động hóa quá trình giả lập tấn công lừa đảo qua Google Sheets, giúp các tổ chức đào tạo nhận thức bảo mật và kiểm tra hiệu quả của hệ thống SOC."
slug: "gia-lap-tan-cong-lua-dao-google-sheets"
tags: [n8n, automation, no-code, secops, google-sheets]
keywords: [n8n workflow, tự động hóa, secops, đào tạo bảo mật, kiểm tra SOC]
---

# 🎣 Giả lập tấn công lừa đảo qua Google Sheets cho đào tạo nhận thức bảo mật & kiểm tra SOC

[Các sếp đang gặp khó khăn khi phải thủ công tạo và quản lý các chiến dịch giả lập tấn công lừa đảo để đào tạo nhận thức bảo mật cho nhân viên. Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình từ chọn mục tiêu đến ghi log kết quả, giúp tiết kiệm thời gian và đảm bảo tính nhất quán trong các bài kiểm tra bảo mật.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công trong quá trình tạo và quản lý các chiến dịch giả lập.
- **Tiết kiệm thời gian**: Giảm thiểu công việc lặp lại, tập trung vào phân tích kết quả và đào tạo nhân viên.
- **Đảm bảo tính nhất quán**: Các chiến dịch giả lập được tạo ra theo cùng một tiêu chuẩn, giúp đánh giá hiệu quả của hệ thống SOC.
- **Quản lý tập trung**: Tất cả dữ liệu và kết quả được lưu trữ trong Google Sheets, dễ dàng truy cập và phân tích.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google với quyền truy cập vào Google Sheets.
- API Key và Credentials cho Google Sheets.
- Danh sách mục tiêu (targets) được lưu trữ trong Google Sheets.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor.
2. Nhấn vào nút "Import from URL" và dán link sau: [https://n8n.io/workflows/6510](https://n8n.io/workflows/6510).
3. Hoặc tải file JSON từ link trên và import vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node "📄 Get Trap Targets"**: Cần cấu hình Google Sheets credentials và chỉ định Sheet ID và tên Sheet chứa danh sách mục tiêu.
- **Node "🧹 Filter Valid Targets"**: Kiểm tra và điều chỉnh điều kiện lọc để đảm bảo chỉ chọn các mục tiêu hợp lệ.
- **Node "🎯 Generate Trap Link"**: Cấu hình các tham số để tạo liên kết giả lập tấn công phù hợp.
- **Node "🪤 Simulate Credential Submission"**: Cấu hình các tham số để mô phỏng việc gửi thông tin đăng nhập.
- **Node "📄 Append Trap Log"**: Cấu hình Google Sheets credentials và chỉ định Sheet ID và tên Sheet để lưu trữ kết quả.

#### 3. Kích hoạt ⚡️
- Kiểm tra và chạy thử với dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
- Bật Active workflow để bắt đầu chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Thêm các node để gửi thông báo kết quả qua Slack hoặc Telegram.
- **Lưu log chi tiết**: Mở rộng workflow để lưu trữ các thông tin chi tiết hơn về các sự kiện giả lập.
- **Tự động hóa báo cáo**: Tạo các báo cáo tự động từ dữ liệu trong Google Sheets để đánh giá hiệu quả của các chiến dịch đào tạo.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa toàn bộ quá trình giả lập tấn công lừa đảo, từ chọn mục tiêu đến ghi log kết quả, giúp tiết kiệm thời gian và đảm bảo tính nhất quán trong các bài kiểm tra bảo mật. Hãy áp dụng ngay để nâng cao hiệu quả đào tạo nhận thức bảo mật và kiểm tra hiệu quả của hệ thống SOC.