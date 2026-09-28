---
title: "🚀 Tự Động Phân Loại Tin Nhắn Intercom & Chuyển Hướng Đến ClickUp/Slack Với GPT-4o-mini"
description: "Workflow n8n sử dụng AI để phân loại tin nhắn khách hàng từ Intercom, tự động tạo task trong ClickUp cho bộ phận Support/Product hoặc thông báo Slack cho đội Sales, giúp xử lý ticket nhanh chóng và chính xác."
slug: "phan-loai-intercom-clickup-slack-gpt"
tags: [n8n, automation, no-code, intercom, clickup, slack, openai]
keywords: [n8n workflow, tự động hóa intercom, phân loại ticket, clickup automation, slack notification, ai classification]
---

# 🚀 Tự Động Phân Loại Tin Nhắn Intercom & Chuyển Hướng Đến ClickUp/Slack Với GPT-4o-mini

Trong môi trường kinh doanh hiện đại, đội ngũ hỗ trợ và bán hàng thường bị quá tải với lượng tin nhắn khổng lồ từ khách hàng qua Intercom. Việc đọc từng tin nhắn, xác định xem đó là khiếu nại kỹ thuật, yêu cầu tính năng mới hay cơ hội bán hàng, rồi sau đó chuyển tiếp thủ công sang các công cụ quản lý công việc như ClickUp hoặc Slack là một quy trình tốn kém thời gian và dễ gây sai sót.

Workflow này giải quyết triệt để vấn đề đó bằng cách sử dụng sức mạnh của **GPT-4o-mini** để tự động "đọc hiểu" nội dung hội thoại, phân loại chúng thành các nhóm (Support, Product, Sales, Other) và tự động thực hiện hành động phù hợp: tạo task chi tiết trong ClickUp hoặc gửi thông báo khẩn cấp cho đội Sales qua Slack. Tất cả diễn ra tức thì, không cần con người can thiệp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian xử lý ticket:** Loại bỏ hoàn toàn bước đọc và phân loại thủ công, giúp đội ngũ tập trung vào việc giải quyết vấn đề thay vì quản lý luồng tin nhắn.
- **Phản hồi nhanh chóng:** Tin nhắn Sales được chuyển ngay lập tức đến Slack, đảm bảo không bỏ lỡ cơ hội kinh doanh.
- **Dữ liệu chuẩn hóa:** Các task trong ClickUp được tạo với tiêu đề, mô tả, mức độ ưu tiên và tag được AI tổng hợp sẵn, giúp quản lý công việc rõ ràng hơn.
- **Chi phí thấp:** Sử dụng GPT-4o-mini (mô hình nhanh và rẻ) giúp giảm chi phí API so với các mô hình lớn hơn mà vẫn đảm bảo độ chính xác cao cho việc phân loại.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị các tài khoản và credentials sau:
1. **Tài khoản Intercom:** Đã bật tính năng Webhook cho sự kiện tin nhắn mới (New Message).
2. **Tài khoản OpenAI:** API Key để sử dụng mô hình GPT-4o-mini.
3. **Tài khoản ClickUp:** OAuth2 Credentials. Cần biết trước **List ID** hoặc **Folder ID** nơi các task sẽ được tạo.
4. **Tài khoản Slack:** API Token (Bot Token) và tên Channel (ví dụ: `#sales-alerts`) để gửi thông báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ link gốc hoặc copy toàn bộ code JSON và dán vào n8n Editor.
1. Mở n8n, tạo workflow mới.
2. Chọn **Import from URL** hoặc **Import from Clipboard**.
3. Dán link hoặc JSON code vào.
4. Workflow sẽ hiển thị 10 nodes chính: Webhook, Agent (AI), Code, 3 nodes If, 2 nodes ClickUp, và 1 node Slack.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình lại các node sau để khớp với hệ thống của mình:

*   **Node: 📨 Intercom Webhook**
    *   Vào node Webhook, thay thế `your-webhook-path-here` bằng một đường dẫn duy nhất (ví dụ: `intercom-incoming`).
    *   Đảm bảo trong phần **Credentials**, các sếp đã chọn đúng tài khoản Intercom đã được cấp quyền.
    *   *Lưu ý:* Trong Intercom, các sếp cần thêm URL webhook này vào phần **Settings > Webhooks** và chọn sự kiện `conversation.updated` hoặc `conversation.created`.

*   **Node: GPT model (gpt-4o-mini)**
    *   Chọn **OpenAI API** credentials đã tạo.
    *   Kiểm tra lại model đang được chọn là `gpt-4o-mini`.

*   **Node: 🧠 Classifier – AI prompt**
    *   Đây là trái tim của workflow. Các sếp có thể chỉnh sửa prompt trong node này nếu muốn thay đổi tiêu chí phân loại (ví dụ: thêm loại "Billing" hoặc thay đổi định nghĩa về "Urgency").
    *   Đảm bảo prompt yêu cầu AI trả về đúng định dạng JSON để node Code phía sau parse được.

*   **Node: 🧮 Process Classification**
    *   Node Code này xử lý output từ AI. Thông thường không cần chỉnh sửa nếu prompt không đổi. Tuy nhiên, nếu các sếp thay đổi cấu trúc JSON trả về từ AI, hãy cập nhật logic parse trong node này.

*   **Node: 🧾 Create Support Task & 🛍️ Create Product Task (ClickUp)**
    *   Chọn **ClickUp OAuth2** credentials.
    *   **Quan trọng:** Trong phần **List ID** (hoặc Folder ID), các sếp cần điền ID của danh sách công việc cụ thể trong ClickUp nơi muốn tạo task.
    *   Có thể chỉnh sửa template cho **Task Name** và **Description** để hiển thị thêm thông tin như Email khách hàng, Link hội thoại Intercom, v.v.

*   **Node: 📣 Slack – Notify Sales team**
    *   Chọn **Slack API** credentials.
    *   Trong phần **Channel**, điền tên channel (ví dụ: `#sales-team`).
    *   Chỉnh sửa nội dung tin nhắn (Message) nếu muốn thêm bớt thông tin như tên khách hàng, lý do AI phân loại là Sales, v.v.

#### 3. Kích hoạt ⚡️
1. **Test Run:** Gửi một tin nhắn mẫu từ Intercom (hoặc dùng nút "Test" trong n8n nếu có dữ liệu mock).
2. Kiểm tra xem AI có phân loại đúng không (xem output của node Code).
3. Kiểm tra xem task có được tạo trong ClickUp hoặc tin nhắn có hiện trong Slack không.
4. Nếu mọi thứ ổn, bật nút **Active** ở góc trên bên phải n8n để workflow chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm kênh Telegram:** Thay vì chỉ Slack, các sếp có thể thêm node Telegram để gửi thông báo Sales qua điện thoại, đảm bảo phản hồi tức thì.
- **Lưu log vào Google Sheets:** Thêm một node Google Sheets để ghi lại lịch sử phân loại (Thời gian, Loại, Mức độ khẩn cấp, Kết quả) để dễ dàng phân tích hiệu suất đội ngũ sau này.
- **Tùy chỉnh Prompt theo ngành:** Nếu các sếp hoạt động trong ngành y tế, tài chính hoặc giáo dục, hãy điều chỉnh prompt trong node AI để nó hiểu rõ hơn về thuật ngữ chuyên ngành và các loại yêu cầu đặc thù.
- **Gửi email xác nhận:** Thêm node Email để gửi một email tự động cho khách hàng thông báo rằng yêu cầu của họ đã được ghi nhận và đang được xử lý, tăng trải nghiệm khách hàng (CX).

### 📌 Kết luận
Việc kết hợp Intercom, AI, ClickUp và Slack trong một workflow n8n là một bước tiến lớn trong việc tối ưu hóa quy trình vận hành. Thay vì để tin nhắn nằm im trong hộp thư, các sếp sẽ có một "nhân viên ảo" làm việc 24/7, phân loại chính xác và điều phối công việc đến đúng người, đúng lúc. Hãy áp dụng ngay để giải phóng sức lao động cho đội ngũ và tập trung vào những giá trị cốt lõi của doanh nghiệp.