---
title: "🚀 Tự động giám sát sức khỏe khách hàng qua cuộc họp với Fireflies, GPT-4o-mini, Google Sheets và Slack"
description: "Hướng dẫn xây dựng workflow n8n tự động phân tích cảm xúc cuộc họp hàng tuần từ Fireflies, đánh giá rủi ro rời bỏ (churn risk) bằng GPT-4o-mini, lưu log vào Google Sheets và cảnh báo khẩn cấp qua Slack."
slug: "giam-sat-suc-khoe-khach-hang-fireflies-gpt4-sheets-slack"
tags: [n8n, automation, ai-agent, openai, google-sheets, slack, fireflies]
keywords: [n8n workflow, tự động hóa chăm sóc khách hàng, phân tích cảm xúc cuộc họp, fireflies ai, gpt-4o-mini, crm automation]
---

# 🚀 Tự động giám sát sức khỏe khách hàng qua cuộc họp với Fireflies, GPT-4o-mini, Google Sheets và Slack

Các Account Manager (AM), Customer Success Team (CS) và quản lý agency thường đau đầu khi phải rà soát hàng chục, hàng trăm cuộc họp mỗi tuần để nắm bắt tâm lý khách hàng. Việc bỏ sót một tín hiệu bất mãn nhỏ có thể dẫn đến việc khách hàng rời đi (churn) trong âm thầm. 

Giải pháp thủ công vừa tốn thời gian, vừa thiếu tính hệ thống. Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n hoàn toàn tự động giúp "bắt mạch" sức khỏe khách hàng hàng tuần dựa trên nội dung hội thoại thực tế từ Fireflies AI kết hợp sức mạnh phân tích ngữ cảnh của GPT-4o-mini.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 100% hàng tuần:** Vào mỗi thứ Hai lúc 9h sáng, hệ thống tự động tổng hợp toàn bộ cuộc họp của tuần qua.
- **AI thông minh thấu hiểu khách hàng:** Không chỉ đo điểm số cảm xúc (sentiment), GPT-4o-mini còn giải thích lý do *vì sao* khách hàng vui hay buồn, đánh giá rủi ro rời bỏ và đề xuất hành động khắc phục cụ thể.
- **Lưu trữ minh bạch:** Tự động ghi nhận toàn bộ thông tin chi tiết vào Google Sheets để làm báo cáo lịch sử.
- **Cảnh báo rủi ro thời gian thực:** Lập tức bắn chuông báo động qua Slack nếu phát hiện cuộc họp có cảm xúc tiêu cực hoặc nguy cơ mất khách hàng cao (High/Critical).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn sàng (Cloud hoặc Self-hosted).
- **Fireflies.ai Account & API Key:** Để lấy dữ liệu transcript cuộc họp.
- **OpenAI Account:** Có API Key tích hợp mô hình `gpt-4o-mini`.
- **Google Sheets & Slack:** Tài khoản kết nối OAuth2 để ghi log và gửi thông báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ [n8n template gốc](https://n8n.io/workflows/15070) và import trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 16 nodes được thiết kế mạch lạc. Các sếp cần tập trung cấu hình kỹ các điểm sau:

- **Node `2. Set — Config Values`**: Điền các thông tin cấu hình cốt lõi bao gồm Fireflies API Key, Google Sheet ID, tên tab Google Sheet, tên các kênh Slack nhận tin và tên công ty của sếp.
- **Node `10. OpenAI — GPT-4o-mini Model`**: Kết nối thông tin **OpenAI Credential** chứa API Key của sếp để AI Agent có nguyên liệu phân tích.
- **Node `13. Google Sheets — Log Client Sentiment`**: Kết nối tài khoản **Google Sheets OAuth2**, chọn thao tác `Append` và trỏ đúng vào bảng tính chuẩn bị sẵn.
- **Node `15. Slack — Send Urgent Alert`**: Kết nối tài khoản **Slack OAuth2** và đảm bảo Bot đã được mời vào kênh Slack nhận cảnh báo khẩn.

> 💡 **Chuẩn bị Google Sheet:** Tạo một tab trong Google Sheet với tên `Client Sentiment Log` và các cột tiêu đề lần lượt là: `Week`, `Meeting Date`, `Meeting Title`, `Client Name`, `Duration`, `Participants`, `Sentiment Score`, `Sentiment Label`, `Positive %`, `Negative %`, `GPT Analysis`, `Churn Risk`, `Recommended Action`, `Fireflies URL`, `Logged At`.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thử với dữ liệu thực tế.
- Sau khi kiểm tra mọi thứ trơn tru, bật công tắc **Active** để hệ thống tự động chạy định kỳ mỗi thứ Hai hàng tuần.

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa quy trình chăm sóc khách hàng, các sếp có thể mở rộng thêm:
- **Tích hợp Zalo/Telegram:** Thay vì chỉ gửi Slack, có thể bổ sung node gửi tin nhắn qua Telegram Bot để các sếp nhận thông tin nhanh trên điện thoại cá nhân.
- **Tạo báo cáo tổng hợp tháng:** Dùng một workflow phụ gom dữ liệu từ Google Sheets để vẽ biểu đồ xu hướng sức khỏe khách hàng.
- **Giao việc tự động:** Kết nối thêm node tạo Task trên Trello/Asana tự động dựa trên phần `Recommended Action` mà AI đề xuất cho các cuộc họp rủi ro cao.

### 📌 Kết luận
Việc quản lý mối quan hệ khách hàng không còn dựa vào cảm tính khi đã có sự hỗ trợ của tự động hóa và AI. Hãy triển khai ngay workflow này để đội ngũ của các sếp luôn chủ động nắm bắt tâm lý khách hàng trước khi quá muộn!