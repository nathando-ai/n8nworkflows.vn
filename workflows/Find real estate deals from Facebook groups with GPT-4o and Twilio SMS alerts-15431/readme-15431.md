---
title: "🚀 Tự động săn bất động sản từ Facebook Groups bằng AI GPT-4o và Twilio SMS"
description: "Hướng dẫn xây dựng workflow n8n tự động quét bài đăng từ các nhóm Facebook BĐS, dùng GPT-4o phân tích tiêu chí đầu tư (buy box) và gửi tin nhắn SMS cảnh báo qua Twilio."
slug: "san-bat-dong-san-facebook-groups-gpt4o-twilio"
tags: [n8n, automation, ai, openai, twilio, facebook-scraper, real-estate]
keywords: [n8n workflow, săn bất động sản tự động, facebook scraper, gpt-4o ai agent, twilio sms alert]
---

# 🚀 Tự động săn bất động sản từ Facebook Groups bằng AI GPT-4o và Twilio SMS

Các nhà đầu tư bất động sản hay nhà môi giới chắc chắn hiểu cảm giác "bội thực" thông tin khi phải hàng ngày lướt qua hàng chục hội nhóm Facebook (Groups) để tìm kiếm các deal hời (off-market, wholesale). Việc làm thủ công này cực kỳ tốn thời gian, dễ bỏ sót những cơ hội tốt vì tin trôi nhanh.

Giải pháp ở đây là gì? Workflow n8n tự động hóa 100% này sẽ thay các sếp cào dữ liệu từ các nhóm Facebook, giao cho **AI (GPT-4o)** đọc hiểu, chấm điểm theo tiêu chí đầu tư ("buy box") riêng của các sếp, sau đó bắn tin nhắn **SMS (Twilio)** thẳng về điện thoại ngay khi có deal ngon!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần ngồi lướt Facebook hàng giờ để lọc tin rác.
- **Không bỏ lỡ cơ hội:** AI quét liên tục theo lịch trình cài sẵn (mấy tiếng/lần), phát hiện deal hời nhanh hơn đối thủ.
- **Cá nhân hóa tuyệt đối:** AI tự động so sánh bài đăng với bộ tiêu chí "buy box" riêng của từng nhà đầu tư (số phòng ngủ, diện tích, giá, khu vực...).
- **Cảnh báo tức thì:** Nhận tin nhắn SMS qua Twilio ngay khi tìm thấy "Preferred Deal".
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **RapidAPI Key**: Cần đăng ký gói Facebook Scraper3 API trên RapidAPI.
- **OpenAI API Key**: Sử dụng mô hình GPT-4o hoặc GPT-4o-mini.
- **Twilio Account**: Cần có Account SID, Auth Token và một số điện thoại Twilio để gửi SMS.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ n8n template (ID: 15431) và import trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các node sau để hệ thống vận hành trơn tru:

- **Schedule Trigger**: Mặc định chạy mỗi 4 tiếng từ 9h sáng đến 9h tối (`0 9-21/4 * * *`). Có thể chỉnh lại tần suất tùy ý (nhưng lưu ý giới hạn request của gói RapidAPI).
- **Các node HTTP Request (Group 1 đến Group 6)**: 
  - Thêm header `x-rapidapi-key` (hoặc tạo Header Auth credential).
  - Thay thế `group_id` bằng ID các nhóm Facebook các sếp muốn quét (Lấy ID bằng cách nhìn dãy số trên URL của nhóm Facebook, ví dụ: `facebook.com/groups/331454348246054`).
- **AI Agent & OpenAI Chat Model**: 
  - Chọn credential OpenAI.
  - Cấu hình lại phần **System Message** trong AI Agent để khớp với tiêu chí "buy box" của các sếp (ví dụ: số phòng ngủ/phòng tắm tối thiểu, diện tích, khu vực, từ khóa như FSBO, giá trần...).
- **Edit Fields & Twilio**:
  - Nhập Twilio Credentials (Account SID + Auth Token).
  - Cấu hình số nhận tin (`to`) và số gửi (`from`).
  - Kiểm tra lại định dạng tin nhắn SMS trong node **Edit Fields** để hiển thị gọn gàng, dễ đọc trên màn hình điện thoại.

#### 3. Kích hoạt ⚡️
- Chạy thử (Test step/Test execution) để kiểm tra luồng dữ liệu từ việc cào bài đăng, qua AI phân tích cho đến lúc định dạng tin nhắn.
- Bật công tắc **Active** để workflow tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Lọc thông minh hơn**: Thêm một node **IF** ngay trước node Twilio để lọc chỉ gửi SMS khi `status === "Preferred Deal"`, tránh bị làm phiền bởi các tin không đạt yêu cầu.
- **Lưu trữ dữ liệu**: Kết nối thêm node **Google Sheets** hoặc **Airtable** sau bước AI Agent để lưu toàn bộ lịch sử các bài đăng vào database phục vụ phân tích thị trường sau này.
- **Đa kênh thông báo**: Ngoài SMS Twilio, các sếp có thể kết hợp thêm node **Telegram** hoặc **Slack** để bắn thông báo kèm link trực tiếp bài đăng vào group chat nội bộ team.

### 📌 Kết luận
Việc tự động hóa quy trình tìm kiếm bất động sản từ mạng xã hội chưa bao giờ dễ dàng đến thế với sức mạnh kết hợp giữa n8n và AI Agent. Hãy áp dụng ngay workflow này để trở thành người đầu tiên tiếp cận các deal hời trên thị trường!