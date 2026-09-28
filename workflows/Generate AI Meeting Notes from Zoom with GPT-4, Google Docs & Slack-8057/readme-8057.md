---
title: "🚀 Tự Động Tạo Biên Bản Cuộc Họp Từ Zoom Bằng GPT-4, Google Docs & Slack"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình ghi chép cuộc họp từ Zoom, tóm tắt bằng GPT-4, lưu vào Google Docs và thông báo lên Slack."
slug: "tu-dong-tao-bien-ban-cuoc-hop-zoom-gpt-4-google-docs-slack"
tags: [n8n, automation, ai-summarization, zoom, openai, google-docs, slack]
keywords: [n8n workflow, tóm tắt cuộc họp zoom, ai meeting notes, gpt-4 n8n, tự động hóa google docs slack]
---

# 🚀 Tự Động Tạo Biên Bản Cuộc Họp Từ Zoom Bằng GPT-4, Google Docs & Slack

Các sếp có bao giờ cảm thấy mệt mỏi khi phải vừa tham gia họp, vừa tất bật ghi chép từng ý chính, sau đó lại mất thêm cả tiếng đồng hồ để tổng hợp biên bản (Meeting Notes) gửi cho team? Việc này không chỉ tốn thời gian mà còn dễ bỏ sót các action items quan trọng.

Đừng lo, workflow n8n này sẽ giúp các sếp giải quyết triệt để bài toán trên. Hệ thống sẽ tự động bắt sự kiện khi cuộc họp Zoom kết thúc, sử dụng sức mạnh của **GPT-4** để phân tích, tóm tắt, sau đó tự động lưu thành liệu trên **Google Docs** và bắn thông báo gọn gàng lên kênh **Slack** của team. 100% tự động, không cần đụng tay!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn cảnh ngồi nghe bản ghi âm dài dằng dặc để viết báo cáo.
- **Biên bản chuyên nghiệp:** GPT-4 giúp cô đọng ý chính, làm nổi bật các quyết định và giao việc rõ ràng (Action Items).
- **Lưu trữ khoa học:** Tự động tạo file trên Google Docs, dễ dàng tìm kiếm và chia sẻ.
- **Minh bạch thông tin:** Team nhận ngay thông báo kèm tóm tắt và link tài liệu trực tiếp trên Slack ngay khi cuộc họp vừa khép lại.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và thông tin sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Zoom Developer Account** (Để cấu hình Webhook sự kiện `meeting.ended`).
- **OpenAI API Key** (Đã nạp tiền để sử dụng mô hình GPT-4).
- **Tài khoản Google** (Kết nối Google Docs).
- **Tài khoản Slack** (Đã tạo sẵn kênh nhận thông báo, ví dụ: `#team-meetings`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow và dán trực tiếp vào giao diện n8n Editor của mình, hoặc import file JSON theo hướng dẫn thông thường.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 5 nodes chính, các sếp cần cấu hình kỹ các điểm sau:

- **Zoom Meeting Webhook (`webhook`):**
  - Cấu hình phương thức `POST` và lấy đường dẫn Webhook URL từ n8n để dán vào **Zoom Developer Console** (tạo App mới và bật sự kiện **`meeting.ended`**).
- **Normalize Data (`code`):**
  - Node này dùng mã Javascript để làm sạch dữ liệu đầu vào từ Zoom (thông tin bản ghi, nội dung transcript hoặc metadata cuộc họp). Thường không cần sửa code trừ khi cấu trúc payload của Zoom thay đổi.
- **Generate AI Notes (`openAi`):**
  - Chọn Credentials OpenAI của các sếp.
  - Chọn Resource: `Chat`, Operation: `Create`.
  - Cấu hình Prompt truyền vào để GPT-4 tiến hành tóm tắt nội dung cuộc họp theo ý muốn (ví dụ: yêu cầu tách rõ phần Tóm tắt, Ý kiến đóng góp và Action Items).
- **Save to Google Docs (`googleDocs`):**
  - Kết nối tài khoản Google OAuth trong n8n.
  - Thiết lập thư mục lưu trữ trên Google Drive và tiêu đề tự động cho tài liệu (có thể kết hợp tên cuộc họp và ngày tháng).
- **Post to Slack (`slack`):**
  - Kết nối Slack OAuth.
  - Chọn kênh nhận thông báo (ví dụ thay thế bằng kênh `#team-meetings` của công ty).
  - Định dạng nội dung tin nhắn gửi đi kèm đường dẫn (link) tới Google Doc vừa tạo.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và thực hiện một cuộc họp test trên Zoom để kiểm tra luồng dữ liệu.
- Khi dữ liệu chạy mượt mà không lỗi, gạt công tắc sang **Active** để hệ thống tự động vận hành 24/7.

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống xịn sò hơn nữa, các sếp có thể mở rộng workflow này với các ý tưởng sau:
- **Gửi Email tự động:** Thêm một node Email (Gmail/SMTP) để gửi biên bản họp đến những người vắng mặt hoặc khách hàng bên ngoài.
- **Lưu Database:** Lưu lịch sử tóm tắt cuộc họp vào Google Sheets hoặc Notion để dễ dàng tra cứu KPI, tiến độ công việc theo tuần/tháng.
- **Phân loại theo dự án:** Dùng thêm node điều kiện (If/Switch) để dựa vào tên cuộc họp hoặc tên phòng ban trên Zoom mà định tuyến gửi tin nhắn tới các kênh Slack khác nhau (ví dụ: team Tech, team Marketing...).

### 📌 Kết luận
Tự động hóa biên bản cuộc họp bằng AI không chỉ giúp giải phóng sức lao động cho đội ngũ quản lý và nhân sự, mà còn nâng cao tính minh bạch, chuyên nghiệp trong vận hành doanh nghiệp. Hãy cài đặt ngay workflow này để tối ưu hóa thời gian họp hành của team các sếp nhé!