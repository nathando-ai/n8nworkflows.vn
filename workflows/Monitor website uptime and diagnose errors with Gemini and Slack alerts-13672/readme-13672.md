---
title: "🚀 Tự động giám sát Uptime website và chẩn đoán lỗi bằng AI Gemini kết hợp Slack"
description: "Giải pháp tự động kiểm tra trạng thái website 24/7, tự động phân tích nguyên nhân lỗi bằng Google Gemini AI và gửi cảnh báo thông minh ngay lập tức qua Slack."
slug: "giam-sat-website-uptime-chan-doan-loi-gemini-slack"
tags: [n8n, automation, devops, ai, google-gemini, slack, monitoring]
keywords: [n8n workflow, giám sát uptime website, check lỗi website tự động, google gemini ai, slack alerts, devops automation]
keywords: [n8n workflow, giám sát uptime website, check lỗi website tự động, google gemini ai, slack alerts, devops automation]
---

# 🚀 Tự động giám sát Uptime website và chẩn đoán lỗi bằng AI Gemini kết hợp Slack

Các sếp có bao giờ đau đầu khi website công ty "sập" giữa đêm, khách hàng không truy cập được mà đội ngũ kỹ thuật chỉ phát hiện ra sau khi bị khách phàn nàn? Việc check thủ công hoặc dùng các dịch vụ ping đơn thuần đôi khi chỉ báo lỗi chung chung (như `500 Internal Server Error` hay `Timeout`), khiến anh em lập trình mất nhiều thời gian mò mẫm tìm nguyên nhân.

Đừng lo, workflow n8n cực đỉnh này do **Oka Hironobu** thiết kế sẽ thay bạn làm tất cả: tự động kiểm tra uptime định kỳ, khi website "ngỏm", hệ thống sẽ nhờ **Google Gemini AI** phân tích sâu mã lỗi/phản hồi, sau đó bắn báo cáo chi tiết kèm hướng giải quyết thẳng vào **Slack** và **Gmail** của team DevOps. Tất cả hoàn toàn tự động 100% không tốn một giọt mồ hôi!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phát hiện sự cố tức thì:** Lịch trình tự động chạy liên tục, không bỏ sót bất kỳ phút "chết" nào của website.
- **Chẩn đoán thông minh bằng AI:** Google Gemini phân tích nội dung phản hồi lỗi, đưa ra nguyên nhân gốc rễ (root cause) và gợi ý cách fix thay vì chỉ báo lỗi "trơ trẽn".
- **Cảnh báo đa kênh:** Đẩy thông báo khẩn cấp qua Slack để team DevOps xử lý ngay lập tức, đồng thời lưu trữ log vào Google Sheets hoặc gửi email báo cáo.
- **Tiết kiệm nguồn lực:** Không cần tốn tiền mua các tool giám sát đắt đỏ, tự chủ hoàn toàn hệ thống cảnh báo riêng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow này "mượt mà" khi lên sóng, các sếp cần chuẩn bị trước:
- **n8n Instance** (Self-hosted hoặc Cloud).
- **Google Gemini API Key** (để AI phân tích lỗi).
- **Slack Workspace & Bot Token** (để bắn tin nhắn cảnh báo).
- **Google Sheets** (tùy chọn: để ghi log lịch sử uptime).
- **Tài khoản Gmail** (tùy chọn: gửi email thông báo dự phòng).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này từ kho lưu trữ n8n, sau đó tại giao diện n8n Editor, các sếp chọn **Add workflow** -> **Import from File** và chọn file JSON vừa tải.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Khi import xong, các sếp nhớ cấu hình lại các node cốt lõi sau để hệ thống chạy chuẩn chỉnh:
- **Schedule Trigger:** Cài đặt tần suất kiểm tra website (ví dụ: cứ mỗi 5 phút hoặc 15 phút chạy 1 lần).
- **HTTP Request (Kiểm tra Website):** Điền URL website của các sếp vào đây. Cài đặt phương thức GET và thiết lập bắt lỗi (ignore HTTP errors) để workflow không bị dừng khi website trả về mã lỗi 4xx/5xx.
- **If Node (Kiểm tra trạng thái):** Đặt điều kiện kiểm tra mã status code (ví dụ: nếu status khác 200 hoặc request thất bại -> chuyển sang nhánh báo lỗi).
- **Google Gemini (LM Chat / Chain LLM):** Kết nối credentials Gemini API. Viết một đoạn Prompt định hướng rõ ràng cho AI (ví dụ: *"Bạn là một DevOps Expert. Hãy phân tích đoạn mã lỗi sau từ website và đưa ra nguyên nhân có thể xảy ra cùng hướng khắc phục ngắn gọn"*).
- **Slack Node:** Chọn kênh (Channel) trên Slack mà các sếp muốn bot bắn tin nhắn cảnh báo khi website gặp sự cố.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thử luồng chạy thủ công (kiểm tra xem bot có bắn tin nhắn qua Slack thành công không).
- Nếu mọi thứ xanh mượt, gạt công tắc sang **Active** để n8n tự động túc trực 24/7 cho các sếp.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Telegram:** Ngoài Slack, các sếp có thể add thêm node Telegram để bắn tin thẳng vào group chat cá nhân hoặc group Telegram của công ty cho tiện check trên điện thoại.
- **Lưu log Google Sheets:** Thêm một node Google Sheets để ghi lại lịch sử mỗi lần check (Thời gian, Trạng thái, HTTP Status, Phản hồi của AI) phục vụ việc thống kê độ ổn định (Uptime SLA) cuối tháng.
- **Cơ chế hồi phục (Recovery Alert):** Tạo thêm nhánh khi website hoạt động bình thường trở lại sau sự cố, gửi một tin nhắn "Website đã hoạt động bình thường 🎉" để team thở phào nhẹ nhõm.

### 📌 Kết luận
Việc giám sát uptime kết hợp AI chẩn đoán lỗi là bước tiến lớn giúp tối ưu hóa vận hành hệ thống, giảm thiểu tối đa thời gian downtime ảnh hưởng đến doanh thu. Hãy import ngay workflow này lên n8n của các sếp và tận hưởng sức mạnh của automation ngay hôm nay!