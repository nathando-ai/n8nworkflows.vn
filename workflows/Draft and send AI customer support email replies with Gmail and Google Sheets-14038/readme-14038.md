---
title: "🚀 Tự động hóa CSKH qua Email với AI, Gmail và Google Sheets (Human-in-the-loop)"
description: "Hướng dẫn cấu hình workflow n8n tự động phân tích email khách hàng, AI soạn thảo câu trả lời thông minh, kiểm duyệt qua Google Sheets trước khi gửi."
slug: "tu-dong-hoa-cham-soc-khach-hang-email-ai-gmail-google-sheets"
tags: [n8n, automation, no-code, gmail, google-sheets, openrouter, ai-chatbot]
keywords: [n8n workflow, tự động hóa email, ai customer support, gmail automation, google sheets n8n, openrouter ai]
keywords: [n8n workflow, tự động hóa, tự động hóa email, ai customer support, gmail automation, google sheets n8n, openrouter ai]
---

# 🚀 Trợ lý AI CSKH qua Email thông minh với Gmail & Google Sheets

Các sếp có đang mệt mỏi vì hàng ngày phải tốn hàng giờ đọc, phân loại và soạn email trả lời khách hàng lặp đi lặp lại không? Việc này không chỉ tốn thời gian mà đôi khi còn làm khách hàng phải chờ đợi lâu. 

Giải pháp hoàn hảo đây rồi! Workflow n8n này sẽ tự động hóa quy trình chăm sóc khách hàng qua email, sử dụng AI (qua OpenRouter) để soạn thảo câu trả lời dựa trên tài liệu doanh nghiệp, sau đó đẩy dữ liệu lên **Google Sheets** để đội ngũ của các sếp kiểm duyệt trước khi gửi. Đảm bảo vừa tận dụng sức mạnh của AI, vừa giữ được sự kiểm soát tuyệt đối của con người (**Human-in-the-loop**).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian:** Không cần gõ lại các nội dung trả lời quen thuộc, AI đã lo phần soạn thảo ban đầu.
- **Kiểm soát tuyệt đối (Human-in-the-loop):** AI chỉ soạn nháp, chỉ khi nào các sếp gõ "send" trên Google Sheets thì email mới được gửi đi.
- **Không bỏ sót email:** Tự động giám sát hộp thư Gmail mỗi phút và lọc bỏ các email rác, thông báo tự động (noreply, out-of-office).
- **Hoạt động 24/7 bền bỉ:** Chạy ngầm liên tục trên n8n, giúp doanh nghiệp phản hồi khách hàng cực kỳ chuyên nghiệp và nhanh chóng.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Self-hosted hoặc Cloud).
- **Tài khoản Gmail / Google Workspace** để nhận và gửi email.
- **Tài khoản Google Sheets** để lưu log và kiểm duyệt.
- **Tài khoản OpenRouter** (để lấy API Key sử dụng các mô hình AI mạnh mẽ như Claude, GPT, Llama...).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ n8n.io hoặc copy và paste trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các node sau để workflow chạy mượt mà:

- **Receive Customer Emails** & **Mark Email as Read** & **Send Reply to Customer** (Node `gmailTrigger` và `gmail`): Kết nối tài khoản Gmail của các sếp thông qua **Gmail OAuth2**.
- **OpenRouter Model** & **Draft AI Reply** (Node `lmChatOpenRouter` và `chainLlm`): Thêm OpenRouter API Key và cập nhật System Prompt trong node AI với thông tin, tài liệu, chính sách của công ty các sếp để AI trả lời đúng trọng tâm.
- **Filter Unwanted Emails** (Node `if`): Cập nhật điều kiện lọc để loại bỏ các email rác và đặc biệt là **loại trừ email của chính công ty các sếp** (tránh vòng lặp vô tận).
- **Log to Google Sheets** & **Get Approved Replies** & **Update Status to Replied** (Node `googleSheets`): 
  - Kết nối **Google Sheets OAuth2 API**.
  - Chuẩn bị một Google Sheet với các cột: `Message ID`, `From`, `Subject`, `Body`, `Reply`, `Send`.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** chạy thử với một email mẫu để kiểm tra xem dòng dữ liệu có đổ về Google Sheets hay không.
- Sau khi test thành công, bật công tắc **Active** góc trên cùng bên phải để workflow tự động chạy 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo Telegram/Slack:** Thêm một node Telegram hoặc Slack ngay sau khi có email mới được draft xong để bắn thông báo cho sếp vào Google Sheets kiểm duyệt ngay lập tức.
- **Mở rộng Knowledge Base:** Đối với doanh nghiệp có lượng tài liệu lớn, có thể tinh chỉnh System Prompt của AI để phân cấp các loại câu hỏi (kỹ thuật, thanh toán, bảo hành...).

### 📌 Kết luận
Workflow này là bước đệm hoàn hảo để doanh nghiệp vừa và nhỏ ứng dụng AI vào vận hành thực tế mà không cần xây dựng hệ thống phức tạp hay tốn kém. Hãy cài đặt ngay hôm nay để tối ưu hóa đội ngũ CSKH của các sếp nhé!