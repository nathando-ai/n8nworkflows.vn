---
title: "🚀 Tự động hóa đăng tuyển dụng từ ATS lên Google Calendar, ClickUp và LinkedIn với GPT-4o"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa toàn bộ quy trình tuyển dụng: đồng bộ lịch hẹn, tạo task quản lý và viết bài PR LinkedIn bằng AI."
slug: "tu-dong-hoa-tuyen-dung-ats-google-calendar-clickup-linkedin-gpt4o"
tags: [n8n, automation, ai, openai, clickup, linkedin, google-calendar, hr-automation]
keywords: [n8n workflow, tự động hóa tuyển dụng, ATS integration, GPT-4o marketing, ClickUp task, LinkedIn automation]
---

# 🚀 Tự động hóa đăng tuyển dụng từ ATS lên Google Calendar, ClickUp và LinkedIn với GPT-4o

Các nhà tuyển dụng (HR) và bộ phận Nhân sự thường xuyên phải đối mặt với một đống công việc thủ công lặp đi lặp lại khi có vị trí tuyển dụng mới: tạo lịch hẹn SLA, hạn chót trên lịch, tạo task quản lý trên công cụ quản lý dự án, và quan trọng nhất là viết bài đăng tuyển dụng thu hút trên mạng xã hội như LinkedIn. Quá trình này vừa tốn thời gian, vừa dễ thiếu sót.

Workflow n8n này chính là giải pháp tự động hóa 100% không cần code, giúp các sếp kết nối hệ thống ATS (Applicant Tracking System) trực tiếp với Google Calendar, ClickUp và sử dụng sức mạnh của GPT-4o để tự động viết bài PR đăng lên LinkedIn một cách mượt mà!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Chuyển đổi từ dữ liệu thô trên ATS thành lịch trình, task quản lý và bài viết marketing chỉ trong vài giây.
- **Quản lý thời gian chính xác:** Tự động tạo sự kiện SLA và Ngày hết hạn (Expiration) trên Google Calendar kèm link truy cập nhanh.
- **Tối ưu hóa tuyển dụng đa kênh:** GPT-4o tự động viết bài tuyển dụng cực kỳ cuốn hút dựa trên mô tả công việc và đăng trực tiếp lên LinkedIn.
- **Theo dõi liền mạch:** Tự động cập nhật log, bình luận kết quả lên task ClickUp để đội ngũ dễ dàng theo dõi tiến độ.
:::

### 🍜 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và credentials sau:
- **Hệ thống ATS (Recrutei hoặc tương đương):** Nơi bắn Webhook chứa thông tin vị trí tuyển dụng.
- **Google Calendar Credentials:** Tài khoản Google để tạo các sự kiện lịch.
- **ClickUp API Key / OAuth2:** Để tự động tạo task và comment báo cáo.
- **OpenAI API Key:** Sử dụng mô hình GPT-4o để viết nội dung marketing.
- **LinkedIn Account / Page Credentials:** Để đăng bài tuyển dụng tự động.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể copy mã JSON của workflow này và dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm **12 nodes** chính phối hợp nhịp nhàng với nhau. Các sếp chú ý cấu hình kỹ các điểm sau:
- **Webhook:** Cấu hình đường dẫn endpoint (`calendar-trello-webhook`) để nhận dữ liệu POST từ hệ thống ATS của công ty.
- **Arranging data & Code nodes (`Arranging data`, `Generating vacancy ATS's URL`, `Recover vacancy data`):** Xử lý định dạng dữ liệu, chuyển đổi chuỗi ngày tháng (ví dụ: định dạng DD/MM/YYYY) sang chuẩn ISO và tính toán thời lượng 24h cho các sự kiện trên lịch.
- **Create event for the SLA & Create event for the expired date (`googleCalendar`):** Chọn đúng bộ lịch (Calendar ID) của đội ngũ nhân sự để hệ thống tự động đánh dấu các mốc thời gian quan trọng.
- **Create a task for the vacancy (`clickUp`):** Map chính xác Team, Space, và List nơi các task tuyển dụng sẽ được khởi tạo.
- **Message a model (`openAi`):** Chọn model `GPT-4o` và kiểm tra cấu hình Prompt được tạo bởi node `Generates a prompt with the vacancy data`.
- **Create a post (`linkedIn`):** Kết nối tài khoản cá nhân hoặc Trang doanh nghiệp (Company Page) để hệ thống tự động xuất bản bài viết tuyển dụng.
- **Create a comment in vacancy task (`clickUp`):** Đảm bảo node này trỏ đúng vào task ID vừa được tạo để để lại bình luận xác nhận bài đăng LinkedIn đã được xuất bản thành công.

#### 3. Kích hoạt ⚡️
- Thực hiện một lượt chạy thử (**Test Run**) bằng cách gửi một payload mẫu qua Webhook để kiểm tra lịch, task ClickUp và bài viết nháp trên LinkedIn.
- Sau khi mọi thứ chạy trơn tru, hãy bật công tắc **Active workflow** để hệ thống tự động vận hành 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo nội bộ:** Thêm một node Telegram hoặc Slack vào sau khi bài viết được đăng lên LinkedIn để thông báo cho toàn bộ team HR vào chung vui.
- **Lưu log vào Google Sheets:** Thêm bước lưu trữ lịch sử các vị trí đã tuyển dụng vào Google Sheets để làm báo cáo hiệu suất (HR Dashboard) hàng tháng.
- **Kiểm duyệt thủ công (Human-in-the-loop):** Thay vì đăng thẳng lên LinkedIn, các sếp có thể đổi node LinkedIn thành lưu bản nháp hoặc gửi thông báo chờ duyệt trước khi xuất bản chính thức.

### 📌 Kết luận
Workflow này là một minh chứng tuyệt vời cho việc ứng dụng AI và Low-code vào quy trình nhân sự thực chiến. Hãy cài đặt ngay hôm nay để giải phóng đội ngũ HR khỏi những tác vụ thủ công nhàm chán và tập trung vào việc tìm kiếm nhân tài!