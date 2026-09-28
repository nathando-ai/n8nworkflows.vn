---
title: "🚀 Tự động hóa nhắc nhở công việc hằng ngày từ Airtable lên Slack với n8n"
description: "Xây dựng hệ thống tự động quét task đang thực hiện trong Airtable và gửi tin nhắn nhắc nhở trực tiếp lên Slack vào 9h sáng mỗi ngày, giúp đội ngũ không bỏ lỡDEADLINE."
slug: "tu-dong-hoa-nhac-nho-cong-viec-airtable-slack-n8n"
tags: [n8n, automation, airtable, slack, project-management, productivity]
keywords: [n8n workflow, Airtable to Slack, tự động nhắc nhở công việc, bot slack airtable, quan ly du an no-code]
---

# 🚀 Tự động hóa nhắc nhở công việc hằng ngày từ Airtable lên Slack với n8n

Các sếp có còn đang tốn thời gian mỗi sáng để đi "réo gọi" từng thành viên trong team xem hôm nay họ phải làm gì không? Thật tẻ nhạt và mất thời gian phải không nào!

Điều gì sẽ xảy ra nếu Slack có thể tự làm việc đó thay các sếp — tự động hoàn toàn vào đúng 9 giờ sáng mỗi ngày, không sót một task nào mà các sếp không cần phải nhấc một ngón tay? 

Trong bài hướng dẫn này, chúng ta sẽ cùng thiết lập một workflow n8n cực kỳ tinh gọn do tác giả **Baptiste Fort** xây dựng, giúp tự động quét các task đang chạy trong Airtable và gửi thông báo trực tiếp vào kênh Slack.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian:** Loại bỏ hoàn toàn việc nhắc việc thủ công mỗi buổi sáng.
- **Tăng tính kỷ luật:** Thành viên nhận thông báo trực diện trên Slack kèm theo tiêu đề task và deadline rõ ràng.
- **Không bỏ lỡ tiến độ:** Tự động lọc chính xác các task đang ở trạng thái "In Progress" (Đang thực hiện).
- **Hoạt động tự động 24/7:** Chạy ngầm ổn định trên n8n mà không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản **n8n** (Cloud hoặc Self-hosted).
- Tài khoản **Airtable** đã tạo sẵn Base quản lý công việc.
- Tài khoản **Slack** và quyền cấu hình Bot/App để gửi tin nhắn vào kênh.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng file JSON workflow hoặc tạo mới trực tiếp trên n8n Editor với 3 nodes cơ bản sau:
**Schedule Trigger → Search records (Airtable) → Send a message (Slack)**

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

##### ⚙️ Bước 1: Chuẩn bị Base trên Airtable
Tạo một bảng quản lý công việc với các trường dữ liệu (fields) mẫu:
* **Title** (Text): Tiêu đề công việc (Ví dụ: *Finalize quote for Client A*)
* **Assignee** (Text): Người thực hiện
* **Email** (Email): Email người thực hiện
* **Status** (Single select): Trạng thái (*In Progress* / *Done*)
* **Due Date** (Date): Ngày hết hạn

##### ⏰ Bước 2: Cấu hình node `Schedule Trigger`
* Đặt lịch chạy tự động mỗi ngày vào lúc 9:00 sáng.
* **Trigger interval:** Days (Hằng ngày).
* **Trigger at hour:** 9 | **Trigger at minute:** 0.

##### 🗄️ Bước 3: Cấu hình node `Search records` (Airtable)
* **Credentials:** Tạo Airtable Personal Access Token tại [airtable.com/create/tokens](https://airtable.com/create/tokens) với quyền `data.records:read`.
* **Base & Table:** Chọn đúng tên Base và Table quản lý task của các sếp.
* **Filter By Formula:** Nhập công thức lọc task đang làm, ví dụ: `{Statut} = "En cours"` hoặc `{Status} = "In Progress"`.
* **Return All:** Bật `✅ Yes`.

##### 💬 Bước 4: Cấu hình node `Send a message` (Slack)
* **Credentials:** Kết nối tài khoản Slack thông qua Slack API / OAuth2 Token.
* **Send Message To:** Channel.
* **Channel:** Chọn kênh Slack nhận thông báo (Ví dụ: `#tous-n8n` hoặc `#general`).
* **Message Template:** Dán cú pháp nội dung tin nhắn để cá nhân hóa từng task:
  ```text
  New task for {{ $json.name }}: *{{ $json["Titre"] }}* 👉 Deadline: {{ $json["Date limite"] }}
  ```

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Node** ở từng bước để kiểm tra dữ liệu trả về từ Airtable và test gửi tin nhắn lên Slack.
- Nếu mọi thứ hoạt động trơn tru, hãy bật công tắc **Active** góc trên bên phải để workflow chính thức tự động vận hành.

### ✍️ Mẹo & gợi ý nâng cao
- **Gửi tin nhắn riêng (Direct Message):** Thay vì gửi vào chung một kênh channel, các sếp có thể cấu hình Slack gửi tin nhắn trực tiếp (DM) cho từng Assignee dựa vào địa chỉ Email của họ.
- **Tích hợp thêm Google Calendar/Notion:** Ngoài Airtable, có thể mở rộng nguồn dữ liệu lấy task từ Notion Database hoặc Google Sheets.
- **Lưu log báo cáo:** Thêm một node Google Sheets ở cuối luồng để ghi lại lịch sử những task nào đã được gửi thông báo thành công mỗi ngày.

### 📌 Kết luận
Hệ thống tự động nhắc việc từ Airtable lên Slack là một "vũ khí" nhỏ nhưng có võ giúp tối ưu hóa hiệu suất làm việc nhóm mà không tốn một xu chi phí phần mềm quản lý phức tạp nào. Hãy thiết lập ngay hôm nay để giải phóng thời gian cho bản thân các sếp nhé!