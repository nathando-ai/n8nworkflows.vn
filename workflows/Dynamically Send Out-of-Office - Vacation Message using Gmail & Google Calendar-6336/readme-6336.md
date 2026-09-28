---
title: "🚀 Tự động gửi tin nhắn vắng mặt (Out-of-Office) thông minh dựa trên lịch Google Calendar và Gmail"
description: "Hướng dẫn xây dựng workflow n8n tự động kiểm tra lịch làm việc trên Google Calendar và gửi email phản hồi vắng mặt (OOO) cá nhân hóa qua Gmail một cách thông minh."
slug: "tu-dong-gui-tin-nhan-vang-mat-google-calendar-gmail"
tags: [n8n, automation, gmail, google-calendar, productivity, no-code]
keywords: [n8n workflow, out of office automation, tu dong gui email vang mặt, tich hop gmail google calendar]
---

# 🚀 Tự động gửi tin nhắn vắng mặt (Out-of-Office) thông minh dựa trên lịch Google Calendar và Gmail

Các sếp có hay gặp tình trạng nghỉ phép đột xuất hoặc làm việc tự do (freelance) nhưng quên cài đặt chế độ vắng mặt (Out-of-Office - OOO) tĩnh trên email? Hoặc cài chế độ OOO cố định nhưng lại không biết chính xác khi nào mình sẽ quay lại làm việc để báo cho khách hàng? 

Việc cấu hình thủ công mỗi lần nghỉ ngơi vừa phiền phức, vừa dễ quên. Chưa kể, các thiết lập OOO truyền thống thường rất cứng nhắc và không linh hoạt theo lịch trình thực tế.

Giải pháp đây rồi! Workflow n8n này sẽ tự động hóa 100 quy trình: lắng nghe email đến, kiểm tra lịch trên Google Calendar xem các sếp có đang bận hoặc đã hết việc trong ngày chưa, tìm kiếm ngày đi làm lại tiếp theo, và tự động gửi email phản hồi vắng mặt kèm thời gian cụ thể các sếp tái xuất. Không cần code, hoạt động mượt mà 24/7!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Phản hồi email khách hàng/đối tác ngay cả khi các sếp đang nghỉ ngơi, đi du lịch.
- **Cá nhân hóa thông minh**: Email trả lời tự động đính kèm chính xác ngày các sếp sẽ quay lại làm việc (được quét trực tiếp từ Google Calendar trong 14 ngày tới).
- **Linh hoạt theo thời gian thực**: Không cần bật/tắt thủ công; hệ thống dựa vào lịch trình thực tế để quyết định có gửi OOO hay không.
- **Dành riêng cho người bận rộn**: Cực kỳ phù hợp cho freelancer, chuyên gia tư vấn hoặc nhân sự làm việc từ xa (remote worker) không theo giờ hành chính cố định 9-5.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Gmail** (Kết nối qua OAuth2) để nhận email kích hoạt và gửi email phản hồi.
- **Tài khoản Google Calendar** (Kết nối qua OAuth2) để kiểm tra sự kiện và lịch làm việc.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể copy mã JSON của workflow từ trang chủ n8n (Link gốc: [n8n.io/workflows/6336](https://n8n.io/workflows/6336)) hoặc tải file JSON, sau đó paste trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 6 nodes chính, các sếp cần cấu hình các điểm sau để nó chạy trơn tru:

- **Receive an Email in Gmail (`gmailTrigger`)**: 
  - Kết nối tài khoản Gmail của các sếp.
  - Thiết lập bộ lọc (nếu muốn) như chỉ kích hoạt với các nhãn (labels) cụ thể hoặc người gửi quan trọng để tránh gửi OOO cho thư rác/newsletter.
- **Check Calendar for Upcoming Work Events (`googleCalendar`)**: 
  - Kết nối tài khoản Google Calendar.
  - Chọn đúng lịch làm việc (Work Calendar) của các sếp để kiểm tra xem hôm nay còn sự kiện nào diễn ra hay không.
- **Any Upcoming Events Today? (`if`)**: 
  - Node điều kiện kiểm tra kết quả từ bước trước. Nếu không còn sự kiện nào trong ngày, hệ thống sẽ chuyển sang bước tìm ngày quay lại làm việc.
- **Find Return-to-Office Date (`googleCalendar`)**: 
  - Quét các sự kiện trong 14 ngày tiếp theo trên lịch để xác định chính xác sự kiện tiếp theo (ngày các sếp quay lại làm việc).
- **Nicely Format Return Date (`code`)**: 
  - Chạy đoạn mã JavaScript có sẵn để định dạng ngày trả về theo chuẩn thân thiện (Ví dụ: *"Thursday, July 24, 2025"*). Không cần thay đổi gì trừ khi muốn đổi định dạng ngày tháng.
- **Send Out of Office Message (`gmail`)**: 
  - Soạn nội dung template email phản hồi vắng mặt theo phong cách cá nhân của các sếp. 
  - Đảm bảo chèn biến ngày tháng đã được format từ node Code vào nội dung email.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và gửi một email test đến tài khoản của các sếp để kiểm tra xem hệ thống phản hồi có chính xác không.
- Sau khi test ngon lành, gạt công tắc sang **Active** để workflow chính thức trực chiến 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh thông báo phụ**: Kết nối thêm node Slack hoặc Telegram để nhận thông báo mỗi khi có email tự động gửi tin nhắn OOO đi, giúp các sếp nắm được ai đang liên hệ trong lúc nghỉ ngơi.
- **Lưu log vào Google Sheets**: Thêm một node Google Sheets để ghi lại danh sách những ai đã nhận được email OOO, tiện cho việc theo dõi sau khi kỳ nghỉ kết thúc.
- **Bộ lọc thông minh**: Tận dụng tính năng lọc trong Gmail Trigger để chỉ tự động trả lời cho danh bạ hoặc các email có chứa từ khóa công việc quan trọng.

### 📌 Kết luận
Với workflow n8n này, việc quản lý thời gian nghỉ ngơi và chăm sóc khách hàng tự động chưa bao giờ dễ dàng đến thế. Hãy "lên đồ" ngay hôm nay để tận hưởng kỳ nghỉ trọn vẹn mà không sợ bỏ lỡ thông tin quan trọng từ đối tác!