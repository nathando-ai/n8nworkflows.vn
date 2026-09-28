---
title: "🚀 Tự động ghép nối học bổng thông minh cho sinh viên bằng Claude AI, Airtable & n8n"
description: "Xây dựng hệ thống tự động hóa 100% quy trình đánh giá hồ sơ sinh viên, chấm điểm điều kiện và gợi ý học bổng phù hợp bằng Claude AI kết hợp Airtable và Google Sheets."
slug: "tu-dong-ghep-noi-hoc-bong-sinh-vien-claude-ai-airtable"
tags: [n8n, automation, ai-agent, claude-ai, airtable, google-sheets, education]
keywords: [n8n workflow, tu dong hoa hoc bong, claude ai n8n, airtable automation, ai scoring student]
---

# 🚀 Tự động hóa ghép nối học bổng cho sinh viên bằng Claude AI & n8n

Việc quản lý và xét duyệt hàng trăm hồ sơ sinh viên để tìm ra các chương trình học bổng phù hợp thường ngốn rất nhiều thời gian và công sức của các phòng ban học vụ. Việc dò xét từng điều kiện (GPA, ngành học, hoàn cảnh, năng lực ngoại khóa...) thủ công dễ dẫn đến sai sót và bỏ lỡ cơ hội của sinh viên.

Workflow n8n mạnh mẽ này do **Oneclick AI Squad** phát triển sẽ giải quyết triệt để bài toán trên. Hệ thống tự động tiếp nhận hồ sơ, đối chiếu với danh mục học bổng, sử dụng sức mạnh của **Claude AI** để chấm điểm mức độ phù hợp, gửi email cá nhân hóa cho sinh viên và đồng thời cập nhật dữ liệu lên Airtable lẫn Google Sheets một cách mượt mà.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Tự động hóa toàn bộ từ khâu nộp hồ sơ, chấm điểm AI cho đến gửi kết quả.
- **Độ chính xác cao nhờ AI:** Claude AI phân tích đa tiêu chí (GPA, chuyên ngành, tài chính, năng lực đặc biệt) cực kỳ thông minh.
- **Cá nhân hóa trải nghiệm:** Sinh viên nhận được email thông báo chi tiết kèm danh sách các học bổng phù hợp nhất.
- **Đồng bộ đa nền tảng:** Cập nhật ngay trạng thái vào CRM Airtable, lưu vết minh bạch tại Google Sheets và cảnh báo cố vấn học tập qua Slack.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Anthropic API Key:** Để kết nối với mô hình Claude AI (Claude Sonnet).
- **Airtable Account:** Quản lý bảng dữ liệu sinh viên (Student Profiles) và danh mục học bổng (Scholarship Catalogue).
- **Google Sheets Account:** Lưu trữ file log kiểm toán (Audit Trail).
- **SMTP / Email Provider:** Gửi email thông báo tự động tới sinh viên.
- **Slack Workspace:** Nhận cảnh báo cho cố vấn học tập (Academic Advisor).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ nguồn hoặc sao chép toàn bộ mã JSON, sau đó dán trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các node quan trọng sau đây:
- **Load Student Profiles & Load Scholarship Catalogue (Airtable):** Kết nối tài khoản Airtable của sếp, sau đó trỏ đúng vào `Base ID` và `Table Name` chứa dữ liệu sinh viên và học bổng.
- **Claude AI Model (lmChatAnthropic):** Điền `Anthropic API Key` và chọn model phù hợp (mặc định là `=claude-sonnet-4-20250514`) để AI thực hiện chấm điểm tiêu chí.
- **Filter Qualified Matches:** Thiết lập ngưỡng điểm phù hợp (Match Threshold, mặc định là 70 điểm) để lọc ra các học bổng đạt chất lượng cao.
- **Send Scholarship Email to Student (emailSend):** Cấu hình thông tin SMTP để gửi email thông báo học bổng với giao diện cá nhân hóa.
- **Notify Academic Advisor on Slack (httpRequest):** Cấu hình OAuth Slack và điền ID kênh thông báo cho cố vấn học tập.
- **Write Match Audit Log (Google Sheets):** Chọn file Google Sheets và sheet tương ứng để hệ thống tự động ghi nhật ký toàn bộ kết quả ghép nối.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test workflow**) với payload mẫu để kiểm tra dữ liệu đầu ra ở từng bước.
- Bật công tắc **Active** để workflow sẵn sàng hoạt động tự động 24/7 qua Webhook hoặc lịch chạy hàng ngày (`Nightly Batch Schedule`).

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram/Zalo:** Thay thế hoặc bổ sung thông báo qua Telegram bot thay vì chỉ dùng Slack giúp sinh viên hoặc cố vấn dễ dàng theo dõi trên điện thoại.
- **Dashboard phân tích:** Kết nối Google Sheets log với Google Looker Studio để tạo biểu đồ trực quan về tỷ lệ nhận học bổng của sinh viên theo khoa/ngành.
- **Hệ thống nhắc nhở deadline:** Mở rộng thêm nhánh kiểm tra hạn chót nộp hồ sơ để tự động gửi tin nhắn giục sinh viên trước 3 ngày đóng cổng.

### 📌 Kết luận
Workflow tự động hóa ghép nối học bổng bằng Claude AI và Airtable là giải pháp tuyệt vời giúp nâng tầm chuyên nghiệp cho các trường đại học, tổ chức giáo dục hoặc các trung tâm tư vấn du học. Áp dụng ngay để tối ưu hóa nguồn lực và mang lại trải nghiệm tuyệt vời cho học viên!