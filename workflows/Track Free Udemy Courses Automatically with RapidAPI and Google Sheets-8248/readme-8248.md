---
title: "🚀 Tự động theo dõi khóa học miễn phí Udemy với RapidAPI và Google Sheets"
description: "Hướng dẫn tự động hóa việc theo dõi khóa học miễn phí Udemy hàng giờ và đồng bộ dữ liệu lên Google Sheets, giúp tiết kiệm thời gian và tối ưu hóa việc học tập."
slug: "tu-dong-theo-doi-khoa-hoc-mien-phi-udemy-voi-rapidapi-va-google-sheets"
tags: [n8n, automation, no-code, udemy, google-sheets]
keywords: [n8n workflow, tự động hóa, udemy, google sheets, khóa học miễn phí]
---

# 🚀 Tự động theo dõi khóa học miễn phí Udemy với RapidAPI và Google Sheets

[Khi các sếp thường xuyên tìm kiếm khóa học miễn phí trên Udemy, việc phải truy cập trang web và lọc thủ công các khóa học phù hợp là một công việc tốn thời gian và dễ gây lỗi. Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình này, giúp tiết kiệm thời gian và đảm bảo luôn cập nhật với những khóa học mới nhất.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Không cần phải truy cập trang web Udemy hàng giờ để tìm kiếm khóa học miễn phí.
- Tự động hóa hoàn toàn: Workflow sẽ tự động chạy và cập nhật dữ liệu mỗi giờ.
- Dễ dàng quản lý: Tất cả các khóa học miễn phí sẽ được đồng bộ lên Google Sheets, giúp các sếp dễ dàng quản lý và truy cập.
- Thông báo lỗi: Nếu có lỗi xảy ra trong quá trình lấy dữ liệu, các sếp sẽ nhận được thông báo qua email để khắc phục kịp thời.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google để truy cập Google Sheets.
- Tài khoản email để cấu hình SMTP và nhận thông báo lỗi.
- API Key từ RapidAPI để truy cập dữ liệu từ Udemy.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow, các sếp có thể làm theo các bước sau:
1. Truy cập vào n8n Editor.
2. Nhấn vào nút "Import from URL" và dán link sau: [https://n8n.io/workflows/8248](https://n8n.io/workflows/8248).
3. Hoặc, các sếp có thể tải file JSON từ link trên và import trực tiếp vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Schedule Trigger**: Cấu hình thời gian chạy workflow (mặc định là mỗi giờ).
- **Fetch Udemy Coupons**: Cần cấu hình API Key từ RapidAPI để truy cập dữ liệu từ Udemy.
- **Check API Success**: Không cần cấu hình gì, node này sẽ tự động kiểm tra kết quả từ API.
- **Filter Free Courses**: Không cần cấu hình gì, node này sẽ tự động lọc các khóa học miễn phí.
- **Send Error Notification**: Cấu hình tài khoản email SMTP để nhận thông báo lỗi.
- **Sync Courses to Google Sheet**: Cấu hình tài khoản Google và ID của Google Sheet để đồng bộ dữ liệu.

#### 3. Kích hoạt ⚡️
- Sau khi cấu hình xong, các sếp có thể nhấn vào nút "Activate" để kích hoạt workflow.
- Để kiểm tra workflow, các sếp có thể nhấn vào nút "Execute Workflow" để chạy thử với dữ liệu mẫu.

### ✍️ Mẹo & gợi ý nâng cao
- Các sếp có thể cấu hình workflow để gửi thông báo qua Slack hoặc Telegram thay vì email.
- Có thể thêm node để lưu log các khóa học đã được đồng bộ lên Google Sheets.
- Các sếp có thể cấu hình workflow để gửi báo cáo định kỳ về các khóa học miễn phí mới nhất.

### 📌 Kết luận
Với workflow này, các sếp có thể tự động hóa việc theo dõi khóa học miễn phí Udemy và đồng bộ dữ liệu lên Google Sheets, giúp tiết kiệm thời gian và tối ưu hóa việc học tập. Hãy thử ngay và trải nghiệm sự tiện lợi mà tự động hóa mang lại!