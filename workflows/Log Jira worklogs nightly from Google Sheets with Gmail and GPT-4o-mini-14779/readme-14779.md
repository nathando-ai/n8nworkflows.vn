---
title: "🚀 Tự động hóa log Jira worklog hàng đêm từ Google Sheets với GPT-4o-mini & Gmail"
description: "Hướng dẫn cài đặt workflow n8n tự động đọc Google Sheets, log thời gian vào Jira mỗi tối lúc 10h, tóm tắt bằng AI GPT-4o-mini và gửi báo cáo qua Gmail."
slug: "tu-dong-hoa-log-jira-worklog-hang-dem-google-sheets-gpt-4o-mini"
tags: [n8n, automation, jira, google-sheets, openai, gmail, productivity]
keywords: [n8n workflow, tự động hóa jira, log worklog tự động, google sheets jira n8n, gpt-4o-mini tóm tắt công việc]
---

# 🚀 Tự động hóa log Jira worklog hàng đêm từ Google Sheets với GPT-4o-mini & Gmail

Các sếp có đang mệt mỏi vì cuối tuần hay cuối ngày lại phải ngồi lục lại trí nhớ để log thời gian (worklog) lên Jira cho từng task? Việc quên log thời gian không chỉ làm sai lệch báo cáo tiến độ dự án mà còn cực kỳ mất thời gian.

Giải pháp đây rồi! Workflow n8n này sẽ tự động hóa 100% quy trình: Đọc dữ liệu từ Google Sheets, đẩy worklog lên Jira mỗi 10 giờ đêm, xử lý thông minh các bản ghi lỗi/chưa làm, nhờ AI GPT-4o-mini viết bản tóm tắt ngắn gọn và gửi báo cáo tổng kết qua Gmail. Các sếp không cần phải động tay vào một bước thủ công nào nữa!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Chạy đều đặn mỗi 10 giờ đêm, không lo bỏ sót thời gian làm việc.
- **Xử lý thông minh & an toàn**: Tự động lọc các task chưa log (`pending`), bao gồm cả các task bị lỡ từ những ngày trước.
- **AI Tóm tắt tinh tế**: Sử dụng GPT-4o-mini để tổng hợp báo cáo tiến độ 2-3 câu gửi qua email vô cùng chuyên nghiệp.
- **Kiểm soát lỗi chặt chẽ**: Nếu lỗi Jira xảy ra, hệ thống tự động tăng `retry_count` và giữ trạng thái `Pending` để xử lý lần sau mà không làm sập toàn bộ chuỗi loop.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance** (Cloud hoặc Self-hosted).
- **Google Sheets**: Tài khoản kết nối OAuth2 và file Google Sheet mẫu chứa các cột worklog.
- **Jira Account**: Tài khoản Jira Cloud kèm **HTTP Basic Auth** (Email đăng nhập + Jira API Token).
- **OpenAI API Key**: Để sử dụng mô hình GPT-4o-mini viết báo cáo tóm tắt.
- **Gmail Account**: Tài khoản Gmail kết nối OAuth2 để gửi email thông báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow, mở n8n Editor, tạo một workflow mới và chọn **Paste from Clipboard** (hoặc import trực tiếp file JSON).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 15 nodes được thiết kế chặt chẽ. Các sếp cần chú ý cấu hình kỹ các điểm sau:

- **Read Log Sheet & Update Sheet** (Node loại `googleSheets`): 
  - Chọn Credentials Google Sheets OAuth2.
  - Điền chính xác **Google Sheet ID** và tên Sheet (Tab Name) chứa dữ liệu công việc.
- **Jira: Add Worklog** (Node loại `httpRequest`):
  - Chọn Credentials **HTTP Basic Auth** (Điền Email tài khoản Jira và Jira API Token).
  - Thay đổi domain Jira của các sếp vào URL: `https://your-domain.atlassian.net/rest/api/3/issue/{ticket_id}/worklog`.
- **AI Summary** (Node loại `openAi`):
  - Chọn Credentials OpenAI API.
  - Đảm bảo model được cấu hình là `gpt-4o-mini` để tối ưu chi phí và tốc độ.
- **Email: Nothing To Do & Email: Final Report** (Node loại `gmail`):
  - Chọn Credentials Gmail OAuth2.
  - Điền địa chỉ email nhận báo cáo (`sendTo`) trong cả hai node Gmail.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử nghiệm (Test Run) với dữ liệu mẫu trong Google Sheets.
- Kiểm tra kết quả trả về ở Jira và Gmail.
- Nếu mọi thứ mượt mà, gạt công tắc sang **Active** để hệ thống tự động chạy vào 10 giờ đêm hàng ngày.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm kênh chat**: Ngoài Gmail, các sếp có thể nối thêm node Telegram hoặc Slack vào cuối chuỗi để bắn thông báo báo cáo nhanh lên nhóm chat team.
- **Lưu lịch sử chạy (Log)**: Tạo thêm một Google Sheet riêng chuyên lưu trữ log lịch sử thành công/thất bại của từng đêm để tiện audit.
- **Tùy chỉnh giờ chạy**: Sửa cron expression trong node `Every Night 10 PM` (`0 0 22 * * *`) thành khung giờ khác nếu muốn (ví dụ 6 giờ chiều hoặc sáng sớm).

### 📌 Kết luận
Workflow này là một "vũ khí" tối ưu hóa thời gian cực kỳ mạnh mẽ cho các lập trình viên, agency hoặc quản lý dự án sử dụng Jira. Hãy cài đặt ngay hôm nay để giải phóng bản thân khỏi những tác vụ ghi chép thủ công nhàm chán!