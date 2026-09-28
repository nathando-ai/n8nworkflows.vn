---
title: "🚀 Tự động giám sát SLA phản hồi ứng viên qua Gmail và cảnh báo Slack với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động kiểm tra email tuyển dụng từ Gmail, phát hiện vi phạm SLA phản hồi và thông báo thông minh qua Slack."
slug: "tu-dong-giam-sat-sla-phan-hoi-ung-vien-gmail-slack"
tags: [n8n, automation, hr, gmail, slack, no-code]
keywords: [n8n workflow, tự động hóa nhân sự, giám sát SLA email, cảnh báo Slack, quản lý tuyển dụng]
---

# 🚀 Tự động giám sát SLA phản hồi ứng viên qua Gmail và cảnh báo Slack

Trong quy trình tuyển dụng (HR), việc phản hồi email của ứng viên chậm trễ (vi phạm SLA) sẽ làm giảm trải nghiệm ứng viên và vô tình bỏ lỡ nhân tài. Tuy nhiên, việc kiểm tra hòm thư thủ công mỗi ngày là một cực hình đối với đội ngũ tuyển dụng. 

Workflow n8n này chính là giải pháp tự động hóa 100% không cần code, giúp doanh nghiệp tự động quét email từ Gmail, kiểm tra xem Recruiter đã phản hồi hay chưa, và tự động gọi tên (mention) nhân sự đang online trên Slack để xử lý ngay lập tức!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Không bỏ sót email ứng viên:** Tự động rà soát toàn bộ email đến trong 24 giờ qua.
- **Kiểm soát SLA chặt chẽ:** Tự động phát hiện các luồng email (thread) chưa có nhân sự nào phản hồi.
- **Phân công thông minh trên Slack:** Tự động kiểm tra trạng thái hoạt động (online/away) của các thành viên trong kênh Slack để assign người xử lý, ưu tiên người đang online hoặc chọn ngẫu nhiên nếu tất cả đều bận.
- **Vận hành 24/7:** Chạy tự động định kỳ mà không cần con người can thiệp thủ công.
:::

### 📦 Các thành phần chính trong Workflow
Workflow gồm 12 nodes được chia thành 4 giai đoạn logic rõ rệt:
1. **Email Intake & Initial Filtering:** `Scheduler – Every 5 min` ➔ `Fetch Recent Emails` ➔ `Filter Candidate Emails Only`
2. **Thread Analysis & SLA Evaluation:** `Get Thread Details` ➔ `Reply Detection` ➔ `Check – Has Recruiter Replied?`
3. **Slack User Selection Logic:** `Get Channel Members` ➔ `Get User Presence` ➔ `Merge Presence Data` ➔ `Select – Active/Random User`
4. **Alert Preparation & Notification:** `Merge Assign User Data` ➔ `Send SLA Alert`

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản **n8n** (Cloud hoặc Self-hosted).
- Tài khoản **Gmail** (với quyền kết nối Gmail OAuth2).
- Workspace **Slack** (với quyền bot để đọc thông tin channel, user presence và gửi tin nhắn).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tạo một workflow mới trên n8n Editor, sau đó copy toàn bộ mã JSON của workflow này (hoặc import file JSON) vào không gian làm việc của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Scheduler – Every 5 min:** Cài đặt tần suất chạy mong muốn (mặc định là cứ mỗi 5 phút quét một lần).
- **Fetch Recent Emails & Get Thread Details:** Kết nối tài khoản **Gmail** (Credentials: `gmailOAuth2`). Cấu hình bộ lọc thời gian (ví dụ: email trong 24h qua) và điều kiện truy vấn để lấy đúng email.
- **Filter Candidate Emails Only & Reply Detection:** Kiểm tra đoạn code JavaScript bên trong để tùy chỉnh từ khóa nhận diện email ứng viên (ví dụ: tiêu đề chứa "Job Application", "CV", "Ứng tuyển"...) và logic check phản hồi của Recruiter.
- **Get Channel Members, Get User Presence & Send SLA Alert:** Kết nối tài khoản **Slack** (Credentials: `slackApi`). Chọn đúng kênh Slack (Channel ID) nhận thông báo cảnh báo SLA.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** để chạy thử nghiệm (Test Run) với dữ liệu thực tế gần nhất.
- Kiểm tra các nhánh dữ liệu để đảm bảo luồng chạy mượt mà.
- Bật công tắc **Active** ở góc trên cùng bên phải để workflow chính thức tự động vận hành.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp bảng theo dõi:** Kết nối thêm node Google Sheets hoặc Airtable sau bước phát hiện vi phạm SLA để lưu lại lịch sử vi phạm phục vụ báo cáo hiệu suất tuyển dụng hàng tháng.
- **Đa kênh thông báo:** Ngoài Slack, có thể bổ sung thêm nhánh gửi tin nhắn qua Telegram Bot hoặc Zalo ZNS nếu đội ngũ làm việc trên nền tảng khác.
- **Nâng cấp logic phân công:** Tùy chỉnh code node `Select – Active/Random User` để chia đều công việc theo round-robin cho team tuyển dụng thay vì chọn ngẫu nhiên.

### 📌 Kết luận
Việc tự động hóa cảnh báo SLA phản hồi ứng viên giúp nâng cao chuyên nghiệp hóa bộ phận nhân sự, đảm bảo không một ứng viên tiềm năng nào bị bỏ quên. Hãy áp dụng ngay workflow này để tối ưu hóa hiệu suất tuyển dụng cho doanh nghiệp của các sếp!