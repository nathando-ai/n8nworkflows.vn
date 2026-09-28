---
title: "🚀 Tự động tạo video AI siêu đỉnh bằng Havis AI Grok Imagine và n8n"
description: "Hướng dẫn cấu hình và sử dụng workflow n8n để tự động hóa quy trình tạo video AI thông qua Havis AI Grok Imagine API với cơ chế Polling thông minh."
slug: "tao-video-ai-tu-dong-havis-ai-grok-imagine-n8n"
tags: [n8n, automation, ai-video, havis-ai, grok-imagine, no-code, content-creation]
keywords: [n8n workflow, tạo video ai tự động, havis ai grok imagine, n8n http request polling, no-code automation]
---

# 🚀 Tự động tạo video AI siêu đỉnh bằng Havis AI Grok Imagine và n8n

Việc tạo video bằng trí tuệ nhân tạo (AI) ngày càng trở nên phổ biến, nhưng quá trình nhập liệu, gửi yêu cầu và chờ đợi kết quả thủ công thường tốn rất nhiều thời gian. Các sếp có bao giờ cảm thấy bất tiện khi phải liên tục F5 trình duyệt để kiểm tra xem video đã render xong chưa không?

Giải pháp ở đây chính là workflow n8n tích hợp **Havis AI Grok Imagine**. Workflow này sẽ tự động hóa toàn bộ quy trình: từ việc nhận yêu cầu qua Form, gửi lệnh tạo video, tự động kiểm tra trạng thái (Polling) cho đến khi video hoàn thành và trả kết quả về cho các sếp mà không cần một dòng code thủ công nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Gửi yêu cầu qua Form công khai và nhận lại kết quả dạng link video hoàn chỉnh.
- **Cơ chế Polling thông minh:** Tự động chờ và kiểm tra trạng thái task (Wait & Check Task Status) liên tục cho đến khi render xong hoặc thất bại.
- **Tối ưu thời gian:** Giải phóng hoàn toàn thời gian chờ đợi render thủ công trước màn hình.
- **Quản lý linh hoạt:** Theo dõi được cả lượng credit tiêu thụ và metadata của task ngay trong kết quả trả về.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống n8n đã được cài đặt (Self-hosted hoặc Cloud).
- Tài khoản và **Havis API key** (Lấy tại [Havis AI Profile Manager](https://havis.ai/manager/profile)).
- Tài khoản Havis AI phải còn đủ credit để tạo video.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy trực tiếp đoạn JSON.
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File / Paste JSON** để đưa các node lên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Hệ thống workflow bao gồm 10 nodes phối hợp nhịp nhàng. Các sếp cần chú ý các điểm sau:

- **Form - Grok Imagine (`formTrigger`):** Node này tạo một giao diện Web Form công khai. Sau khi active workflow, các sếp có thể mở URL của Form để điền các thông số như: `prompt`, `model`, `duration`, `image_url_1`, v.v. Cần đảm bảo nhập chính xác Havis API key tại đây.
- **Build Payload (`code`):** Node Javascript này có nhiệm vụ làm sạch dữ liệu, loại bỏ các giá trị trống, áp dụng các tùy chọn mặc định và đóng gói thành JSON body chuẩn xác gửi đi.
- **Submit - Havis API (`httpRequest`):** Node gửi request POST đến `https://havis.ai/api/grok-imagine` kèm theo Bearer Token là Havis API key. Node này sẽ trả về `task_id`.
- **Wait 8s & Wait 8s (loop) (`wait`):** Các node tạm dừng thời gian (mặc định 8 giây) để tránh việc gửi quá nhiều request liên tục (Rate Limit) trong lúc đợi AI render video. Các sếp có thể điều chỉnh thời gian này nếu cần.
- **Check Task Status (`httpRequest`):** Node kiểm tra trạng thái task định kỳ tại `https://havis.ai/api/task/{task_id}`.
- **Is Completed? / Is Failed? (`if`):** Các node rẽ nhánh kiểm tra xem tác vụ đã hoàn thành công hay gặp lỗi.
- **Return Result / Return Error (`set`):** Trả về kết quả cuối cùng gồm link video, metadata, thông tin credit đã dùng hoặc thông báo lỗi chi tiết nếu có.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng cách điền form mẫu.
- Kiểm tra kết quả trả về ở node `Return Result`.
- Sau khi test ngon lành, hãy gạt công tắc **Active** góc trên bên phải để bật workflow chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa quy trình sáng tạo nội dung của doanh nghiệp, các sếp có thể mở rộng workflow này:
- **Tích hợp Telegram/Slack:** Thay vì trả kết quả về form, hãy cấu hình gửi trực tiếp link video hoàn thành vào nhóm chat Telegram hoặc Slack của team media.
- **Lưu trữ tự động:** Kết nối thêm node Google Sheets hoặc Airtable để lưu lại lịch sử các câu lệnh (prompt), thời gian chạy và link video phục vụ việc tra cứu sau này.
- **Xử lý hàng loạt (Batch Processing):** Kết hợp đọc danh sách prompt từ file CSV hoặc Google Sheets để tự động tạo hàng loạt video xuyên đêm.

### 📌 Kết luận
Workflow tích hợp Havis AI Grok Imagine và n8n là một "vũ khí" cực kỳ lợi hại cho các nhà sáng tạo nội dung và doanh nghiệp muốn ứng dụng AI vào sản xuất video tự động. Hãy cài đặt ngay lên hệ thống n8n của các sếp để tối ưu hóa hiệu suất công việc ngay hôm nay!