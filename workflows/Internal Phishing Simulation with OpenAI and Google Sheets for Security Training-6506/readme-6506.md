---
title: "🚀 Tự động hóa Mô phỏng Phishing nội bộ bằng OpenAI và Google Sheets"
description: "Xây dựng hệ thống đào tạo nhận thức an ninh mạng tự động 100%, kết hợp AI tạo email giả mạo cá nhân hóa và theo dõi lượt click thời gian thực."
slug: "tu-dong-hoa-mo-phong-phishing-noi-bo-openai-google-sheets"
tags: [n8n, automation, secops, openai, google-sheets, security-training]
keywords: [n8n workflow, phishing simulation, bảo mật nội bộ, openai automation, tự động hóa secops]
keywords: [n8n workflow, phishing simulation, bảo mật nội bộ, openai automation, tự động hóa secops]
---

# 🚀 Tự động hóa Mô phỏng Phishing nội bộ bằng OpenAI và Google Sheets

Việc tổ chức các bài kiểm tra nhận thức an ninh mạng (Phishing Simulation) định kỳ cho nhân viên thường ngốn rất nhiều thời gian của đội ngũ IT và SecOps. Từ việc nghĩ kịch bản, viết nội dung email cho đến việc theo dõi ai đã "sập bẫy" đều phải làm thủ công.

Giải pháp? Workflow n8n này sẽ tự động hóa toàn bộ quy trình: sử dụng **OpenAI AI Agent** để tạo nội dung email lừa đảo tinh vi, gửi qua **Gmail**, tự động ghi log vào **Google Sheets**, và tích hợp **Webhook** để theo dõi chính xác nhân viên nào đã click vào liên kết độc hại nhằm phục vụ cho việc đào tạo bổ sung.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Từ khâu sinh nội dung email, gửi đi đến tracking kết quả mà không cần thao tác tay.
- **Cá nhân hóa cao:** AI tạo ra các kịch bản phishing đa dạng, phù hợp với từng phòng ban hoặc đối tượng mục tiêu.
- **Theo dõi thời gian thực:** Nắm bắt ngay lập tức nhân viên nào click vào link mô phỏng thông qua Webhook Tracker.
- **Nâng cao văn hóa bảo mật:** Giúp doanh nghiệp chủ động phát hiện lỗ hổng con người trước khi các cuộc tấn công thực tế xảy ra.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt và hoạt động ổn định (Self-hosted hoặc Cloud).
- **Tài khoản OpenAI:** API Key để kết nối với LangChain Agent.
- **Google Sheets:** File chứa danh sách mục tiêu (Target List) và bảng để ghi log lịch sử gửi/click.
- **Tài khoản Gmail:** Đã cấu hình Credentials để gửi email mô phỏng.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể copy mã JSON của workflow từ nguồn cấp hoặc sử dụng trực tiếp bản thiết kế tiêu chuẩn, sau đó paste vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống vận hành trơn tru, các sếp cần cấu hình chính xác các node sau:
- **`GetTargetList` (Google Sheets):** Kết nối tài khoản Google của các sếp, chọn đúng file Sheet và Range chứa danh sách email/tên nhân viên mục tiêu.
- **`🤖 Generate Phishing Email` & `OpenAI Chat Model`:** Nhập OpenAI API Key, cấu hình prompt cho AI Agent để định hình phong cách email lừa đảo (ví dụ: thông báo thay đổi lương, phúc lợi cuối năm...).
- **`Gmail`:** Chọn Credentials Gmail được cấp quyền gửi thư để hệ thống bắt đầu bắn email mô phỏng tới danh sách.
- **`🧾 Log Sent Email` (Google Sheets):** Trỏ tới bảng tính lưu lịch sử gửi email (thời gian, người nhận, nội dung).
- **`🎯 Click Tracker` (Webhook):** Đảm bảo URL của Webhook là Public (nếu dùng self-host cần có SSL và domain trỏ về n8n) để khi nhân viên click vào link trong email, webhook sẽ ghi nhận sự kiện.
- **`🧾 Record Click` (Google Sheets):** Cập nhật trạng thái "Đã Click" vào dòng tương ứng của nhân viên đó trong Google Sheets.

#### 3. Kích hoạt ⚡️
- Nhấn **`When clicking ‘Execute workflow’`** hoặc nút **Execute Workflow** để chạy thử với 1 dòng dữ liệu mẫu xem email có gửi đi và tracking có hoạt động không.
- Sau khi test thành công, bật công tắc **Active** để workflow sẵn sàng hoạt động tự động theo lịch định kỳ (có thể gắn thêm Schedule Trigger nếu muốn).

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack/Telegram:** Thêm node thông báo về kênh chat nội bộ ngay khi phát hiện có nhân viên click vào link phishing để đội ngũ SecOps nắm bắt.
- **Trang đích cảnh báo (Landing Page):** Thay vì chỉ ghi nhận click, hãy redirect họ về một trang Google Site hoặc trang nội bộ thông báo: *"Bạn vừa sập bẫy phishing, hãy tham gia khóa đào tạo ngắn tại đây!"*.
- **Báo cáo định kỳ:** Kết hợp thêm node Google Sheets/Email để tự động tổng kết tỷ lệ click theo phòng ban vào cuối mỗi chiến dịch.

### 📌 Kết luận
Mô phỏng Phishing là bước đi cốt lõi trong chiến lược xây dựng "phòng tuyến con người" cho doanh nghiệp. Với workflow n8n này, các sếp hoàn toàn có thể tự dựng một hệ thống Red Teaming nội bộ tự động, chuyên nghiệp và tiết kiệm hàng đống chi phí. Lên đồ và trải nghiệm ngay thôi!