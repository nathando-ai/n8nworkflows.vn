---
title: "🤖 Quản lý Google Calendar bằng Ngôn ngữ tự nhiên với Gemini 1.5 Flash trên n8n"
description: "Hướng dẫn xây dựng trợ lý AI tự động hóa quản lý lịch trình Google Calendar chỉ bằng câu lệnh tự nhiên thông qua n8n và Google Gemini."
slug: "quan-ly-google-calendar-bang-ai-gemini-n8n"
tags: [n8n, automation, ai-agent, google-calendar, gemini]
keywords: [n8n workflow, quan ly lich google bang ai, google gemini n8n, ai agent calendar, tu dong hoa n8n]
---

# 🤖 Quản lý Google Calendar bằng Ngôn ngữ tự nhiên với Gemini 1.5 Flash

Các sếp có bao giờ cảm thấy mệt mỏi khi phải mò mẫm mở Google Calendar, chọn ngày giờ, điền tiêu đề và mô tả thủ công cho từng cuộc họp? Việc này không chỉ tốn thời gian mà đôi khi còn dễ bỏ sót lịch trình. 

Đừng lo, bài viết này sẽ hướng dẫn các sếp tự động hóa toàn bộ quy trình trên bằng một **AI Agent** cực kỳ thông minh trong n8n, kết hợp với sức mạnh của **Google Gemini 1.5 Flash**. Các sếp chỉ cần gõ lệnh như đang nhắn tin với trợ lý thực thụ (ví dụ: *"Đặt lịch họp với team Marketing vào 3 giờ chiều mai"*), AI sẽ tự động lo phần còn lại!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Ra lệnh bằng tiếng Việt tự nhiên:** Không cần nhớ cú pháp phức tạp, thích gì gõ nấy.
- **Tạo và tra cứu lịch tự động:** Trợ lý AI tự động phân tích thời gian, tiêu đề để thêm sự kiện mới hoặc kiểm tra lịch trống.
- **Nhớ ngữ cảnh hội thoại (Memory):** AI có thể hiểu các câu hỏi nối tiếp nhờ bộ nhớ đệm thông minh.
- **Hoạt động 24/7:** Tiết kiệm hàng giờ quản lý thời gian mỗi tuần cho sếp và đội ngũ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google Account** (có quyền truy cập Google Calendar để cấu hình OAuth2 Credentials).
- **Google Gemini API Key** (hoặc cấu hình thông qua Google Gemini Chat Model node).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trên n8n, sau đó copy toàn bộ JSON của workflow từ thư viện n8n (Link gốc: [n8n.io/workflows/5165](https://n8n.io/workflows/5165)) và dán trực tiếp vào giao diện n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 6 nodes chính hoạt động nhịp nhàng với nhau. Các sếp cần chú ý cấu hình các điểm sau:

- **When chat message received (`chatTrigger`)**: Node nhận câu lệnh đầu vào từ người dùng. Các sếp có thể tích hợp widget chat này lên trang web nội bộ hoặc sử dụng giao diện chat mặc định của n8n.
- **AI Agent (`agent`)**: Đây là trung tâm điều phối. Sếp cần viết System Prompt thật rõ ràng trong node này để giới hạn phạm vi hoạt động của AI (ví dụ: *"Bạn là trợ lý lịch trình chuyên nghiệp, chỉ xử lý các vấn đề liên quan đến việc tạo lịch và xem lịch của người dùng"*). Node này cũng chịu trách nhiệm kết nối Gemini, Memory và các công cụ Calendar lại với nhau.
- **Google Gemini Chat Model (`lmChatGoogleGemini`)**: Cung cấp "não bộ" cho AI Agent. Sếp cần kết nối thông tin xác thực Google Gemini API Key tại đây.
- **Simple Memory (`memoryBufferWindow`)**: Node lưu trữ ngắn hạn giúp AI nhớ được nội dung cuộc trò chuyện trước đó, hỗ trợ việc đính chính hoặc bổ sung thông tin lịch trình mượt mà hơn.
- **Google Calendar (`googleCalendarTool` - Thêm sự kiện)**: Cần kết nối tài khoản Google Calendar cá nhân hoặc doanh nghiệp thông qua OAuth2 để node này có quyền thêm sự kiện mới vào lịch.
- **Google Calendar 1 (`googleCalendarTool` - Xem sự kiện)**: Cấu hình operation là `getAll` với nhiệm vụ quét và lấy danh sách các sự kiện hiện có trong khung thời gian mà người dùng yêu cầu.

#### 3. Kích hoạt ⚡️
- Nhấn **Chat** trực tiếp trong khung test của n8n Editor để thử nghiệm các câu lệnh như: *"Tuần này tôi có lịch bận nào vào buổi sáng không?"* hoặc *"Tạo sự kiện ăn trưa với đối tác vào lúc 12h trưa thứ Sáu tuần này"*.
- Sau khi test thành công, gạt công tắc **Active** ở góc trên bên phải để bật workflow chạy chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh chat yêu thích:** Thay vì dùng chat widget mặc định, các sếp có thể thay thế node `chatTrigger` bằng **Telegram Trigger** hoặc **Slack Trigger** để quản lý lịch trình ngay trên ứng dụng chat hàng ngày.
- **Lưu log cuộc họp:** Kết hợp thêm node **Google Sheets** hoặc **Airtable** sau AI Agent để lưu lại lịch sử các cuộc họp đã được AI tạo tự động nhằm dễ dàng kiểm soát.
- **Bổ sung tính năng xóa/sửa lịch:** Mở rộng thêm các công cụ Calendar khác (như Update event, Delete event) vào AI Agent để trợ lý trở nên toàn năng hơn.

### 📌 Kết luận
Chỉ với vài phút thiết lập workflow n8n kết hợp sức mạnh của Gemini AI, các sếp đã sở hữu ngay một trợ lý ảo quản lý thời gian đắc lực, chuẩn hóa quy trình làm việc không cần viết code. Áp dụng ngay hôm nay để tối ưu hóa năng suất cá nhân và doanh nghiệp nào!