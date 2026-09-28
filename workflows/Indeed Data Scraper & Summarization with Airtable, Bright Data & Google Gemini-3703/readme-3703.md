---
title: "🚀 Tự Động Cào Dữ Liệu Việc Làm Indeed và Tóm Tắt Bằng AI Agent & Google Gemini"
description: "Hướng dẫn tự động hóa cào dữ liệu công ty từ Indeed sử dụng Bright Data, trích xuất thông tin thông minh với Google Gemini AI và lưu trữ kết quả lên Airtable."
slug: "tu-dong-cao-du-lieu-indeed-ai-gemini-airtable"
tags: [n8n, automation, ai-agent, google-gemini, bright-data, airtable]
keywords: [n8n workflow, cào dữ liệu indeed, bright data web unlocker, google gemini ai n8n, airtable automation, tóm tắt dữ liệu ai]
---

# 🚀 Tự Động Cào Dữ Liệu Việc Làm Indeed và Tóm Tắt Bằng AI Agent & Google Gemini

Các sếp làm trong ngành nhân sự (HR), marketing hoặc nghiên cứu thị trường chắc hẳn đã rất đau đầu với việc phải truy cập thủ công vào từng trang tuyển dụng, công ty trên Indeed để thu thập thông tin, đánh giá đối thủ hoặc tìm kiếm insight tuyển dụng. Quá trình này không chỉ tốn hàng giờ đồng hồ copy-paste mà còn cực kỳ nhàm chán.

Đừng lo nữa các sếp! Bài viết này sẽ hướng dẫn các sếp thiết lập một **n8n workflow tự động hóa 100% không cần code**, kết hợp sức mạnh của **Bright Data Web Unlocker**, **Google Gemini AI** và **Airtable** để cào, phân tích và tóm tắt toàn bộ dữ liệu từ Indeed trong chớp mắt.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Đọc danh sách link công ty từ Airtable, tự động cào dữ liệu qua Bright Data mà không sợ bị chặn (anti-bot).
- **Trí tuệ nhân tạo đỉnh cao**: Sử dụng Google Gemini AI và AI Agent để đọc hiểu, trích xuất dữ liệu thô từ dạng Markdown thành định dạng có cấu trúc.
- **Tóm tắt thông minh**: Tự động tạo bản tóm tắt chi tiết về thông tin công ty và kết quả tìm kiếm.
- **Đồng bộ hóa mượt mà**: Toàn bộ quy trình diễn ra tự động, giúp tiết kiệm 95% thời gian so với làm thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản Airtable**: Đã tạo Base chứa các liên kết Indeed cần cào.
- **Bright Data Account**: Cần cấu hình Zone để sử dụng Web Unlocker API (hoặc HTTP Header Auth tương ứng).
- **Google Gemini API Key**: Dùng cho các node LangChain Google Gemini Chat Model.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này (hoặc tải file JSON từ nguồn n8n) và dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà không báo lỗi, các sếp chú ý cấu hình kỹ các node sau:

- **Node `Airtable`**: Kết nối với tài khoản Airtable của sếp. Đảm bảo cấu hình Base và Table Name là **"Indeed"** (hoặc tùy chỉnh lại theo ý muốn), với cấu trúc bảng chứa cột `Tab` (tên công ty) và cột `Link` (đường dẫn Indeed cần cào, ví dụ mẫu: `https://www.indeed.com/cmp/Starbucks`).
- **Node `Set Bright Data Zone`**: Cấu hình các thông số Zone và API Key của dịch vụ Bright Data Web Unlocker để vượt qua lớp bảo mật của Indeed.
- **Node `Perform Indeed Web Request`**: Kiểm tra lại phần `credentials` (`httpHeaderAuth`) để đảm bảo yêu cầu HTTP được gửi đi với đúng định dạng xác thực của Bright Data.
- **Các node Google Gemini (`Google Gemini Chat Model For Summarization`, `Google Gemini Chat Model`, `Google Gemini Chat Model for AI Agent`)**: Điền `Google Palm API Key` (hoặc Gemini API Key) hợp lệ để AI có thể xử lý ngữ nghĩa, trích xuất dữ liệu Markdown và chạy AI Agent.
- **Node `Initiate a Webhook Notification for Markdown to HTML Response` (HTTP Request)**: Cập nhật lại Webhook Notification URL nếu các sếp muốn gửi kết quả HTML đã chuyển đổi sang một hệ thống bên thứ ba khác (hoặc Slack/Telegram).

#### 3. Kích hoạt ⚡️
- Nhấn **Test workflow** để chạy thử với dữ liệu mẫu từ Airtable.
- Kiểm tra kết quả trả về ở các nhánh `Indeed Summarizer` và `Indeed Expert AI Agent`.
- Nếu mọi thứ xanh mướt (success), các sếp hãy bật công tắc **Active** để workflow tự động chạy ngầm theo lịch trình hoặc sự kiện.

---

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng thông báo**: Kết hợp thêm node Telegram hoặc Slack ở cuối workflow để nhận ngay bản tóm tắt thông tin công ty ngay khi AI xử lý xong.
- **Lưu lịch sử**: Thay vì chỉ gọi webhook, các sếp có thể cấu hình thêm một hành động ghi ngược lại kết quả tóm tắt của AI vào một cột `Summary` mới trong chính bảng Airtable đó.
- **Tùy chỉnh Prompt cho AI Agent**: Các sếp có thể tinh chỉnh system prompt bên trong `Indeed Expert AI Agent` để yêu cầu AI trích xuất các thông tin cụ thể hơn như: số lượng nhân viên, phúc lợi, đánh giá văn hóa công ty,...

---

### 📌 Kết luận
Với sự kết hợp hoàn hảo giữa **n8n**, **Bright Data** và **Google Gemini AI**, việc thu thập và phân tích dữ liệu từ Indeed nay đã trở nên dễ dàng hơn bao giờ hết. Hãy áp dụng ngay vào quy trình của các sếp để tối ưu hóa hiệu suất công việc ngay hôm nay!