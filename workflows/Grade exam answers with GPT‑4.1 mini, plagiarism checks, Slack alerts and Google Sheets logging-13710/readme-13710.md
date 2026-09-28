---
title: "🚀 Tự động chấm bài thi bằng GPT-4o mini, kiểm đạo văn, gửi cảnh báo Slack và lưu Google Sheets"
description: "Hướng dẫn xây dựng hệ thống đa tác nhân (Multi-Agent) trên n8n để tự động chấm điểm bài thi, kiểm tra đạo văn, đánh giá chất lượng và gửi báo cáo với GPT-4.1 mini."
slug: "tu-dong-cham-bai-thi-ai-n8n-gpt-slack-google-sheets"
tags: [n8n, automation, ai-agents, openai, google-sheets, slack, education]
keywords: [n8n workflow, tự động hóa chấm bài, AI grading agent, kiểm tra đạo văn n8n, GPT-4o mini n8n, google sheets integration]
keywords: [n8n workflow, tự động hóa chấm bài, AI grading agent, kiểm tra đạo văn n8n, GPT-4o mini n8n, google sheets integration]
---

# 🚀 Tự động chấm bài thi thông minh bằng Multi-Agent AI, GPT-4.1 mini, kiểm tra đạo văn và đồng bộ Google Sheets

Việc chấm hàng trăm bài thi tự luận hoặc câu hỏi ngắn thủ công là một "nỗi đau" lớn đối với các thầy cô giáo và nhà quản lý giáo dục: tốn thời gian, dễ xảy ra sai sót, thiên vị chủ quan và khó kiểm soát nạn đạo văn. 

Workflow n8n tuyệt vời này từ chuyên gia **Cheng Siong Chin** sẽ giải quyết triệt để vấn đề trên. Hệ thống sử dụng kiến trúc **Multi-Agent (Đa tác nhân AI)** kết hợp **GPT-4.1 mini** để tự động hóa toàn bộ quy trình: từ việc giải mã đáp án (rubric), chấm điểm khách quan, phân tích đạo văn, kiểm định chất lượng, tạo phản hồi cho học sinh, đến việc gửi cảnh báo qua Slack và lưu trữ lịch sử chi tiết vào Google Sheets.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Giảm tải 90% thời gian chấm bài thủ công cho giảng viên và trường học.
- **Khách quan & Minh bạch:** Điểm số được căn cứ chuẩn xác theo tiêu chí (Rubric) đã thiết lập bằng AI agents.
- **Tích hợp kiểm tra đạo văn:** Tự động phát hiện các dấu hiệu gian lận, sao chép bài làm song song với quá trình chấm điểm.
- **Đồng bộ liền mạch:** Tự động ghi log kết quả vào Google Sheets và bắn thông báo cảnh báo/kết quả khẩn cấp qua Slack.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **OpenAI API Key:** Cần cấp quyền truy cập mô hình GPT-4.1 mini cho các AI Agent nodes.
- **Google Sheets:** Tài khoản Google có quyền truy cập bảng tính lưu kết quả chấm thi.
- **Slack Workspace:** Cấu hình Webhook hoặc OAuth2 để nhận tin nhắn cảnh báo escalation.
- **Nguồn dữ liệu:** API hoặc Google Sheets chứa danh sách câu trả lời của học sinh và bảng tiêu chí chấm điểm (Rubric).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ n8n.io hoặc copy toàn bộ JSON.
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File / Paste JSON** để đưa toàn bộ 31 nodes lên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần cấu hình kỹ các điểm sau:
- **OpenAI Chat Model nodes** (`OpenAI Chat Model - Rubric`, `Marker`, `Moderator`, `Feedback`, `Secondary`, `Plagiarism`): Kết nối với credentials OpenAI của sếp và đảm bảo chọn đúng model `gpt-4.1-mini`.
- **Retrieve Student Answer and Rubric**: Trỏ nguồn dữ liệu đầu vào tới Google Sheets hoặc API chứa bài làm của học sinh.
- **Route by Moderation Decision** (`switch`) & **Check Integrity Flags** (`if`): Thiết lập ngưỡng điểm hoặc cờ cảnh báo để hệ thống tự động lọc các bài thi cần chấm lại (Secondary Marker) hoặc bài có dấu hiệu đạo văn.
- **Log to Google Sheets**: Chọn đúng File ID, Sheet Name và map các cột dữ liệu đầu ra (Tên học sinh, Điểm số, Nhận xét, Cờ đạo văn...).
- **Send Escalation Alert** (`slack`): Kết nối Slack credentials và chọn channel nhận thông báo khi có bài thi gặp vấn đề cần can thiệp thủ công.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** với nút **Manual Trigger** để test thử với 1-2 bài thi mẫu.
- Kiểm tra kết quả trên Google Sheets và kênh Slack xem thông tin đã đổ về chuẩn xác chưa.
- Bật công tắc **Active** ở góc trên bên phải để hệ thống sẵn sàng hoạt động tự động.

### ✍️ Gợi ý nâng cao & Mở rộng
- **Mở rộng nguồn dữ liệu:** Thay vì Manual Trigger, có thể đổi thành Webhook nhận bài làm trực tiếp từ Google Forms hoặc hệ thống LMS (Moodle, Canvas).
- **Đa dạng hóa AI Model:** Ngoài OpenAI, các sếp có thể thay thế bằng node Anthropic Claude cho các agent chấm điểm chuyên sâu.
- **Báo cáo định kỳ:** Thêm một node Cron (Schedule Trigger) chạy cuối tuần để tổng hợp điểm số và gửi email báo cáo tổng quan cho ban giám hiệu.

### 📌 Kết luận
Workflow tích hợp Multi-Agent AI này là một vũ khí cực kỳ mạnh mẽ giúp các tổ chức giáo dục, trung tâm đào tạo tối ưu hóa quy trình đánh giá năng lực học viên. Hãy triển khai ngay hôm nay để tiết kiệm hàng tá thời gian và nâng cao chất lượng phản hồi cho học sinh!