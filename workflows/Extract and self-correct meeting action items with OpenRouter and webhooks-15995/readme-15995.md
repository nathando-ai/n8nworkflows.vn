---
title: "🚀 Tự động trích xuất và tự sửa lỗi Action Items cuộc họp thông AI Agent với n8n và OpenRouter"
description: "Hướng dẫn xây dựng hệ thống AI tự động phân tích biên bản cuộc họp, trích xuất action items chuẩn JSON, tự động sửa lỗi và duy trì ngữ cảnh với OpenRouter."
slug: "tu-dong-trich-xuat-action-items-cuoc-hop-voi-openrouter-n8n"
tags: [n8n, automation, ai-agent, openrouter, webhook, productivity]
keywords: [n8n workflow, tự động hóa cuộc họp, AI extraction agent, openrouter n8n, self-correcting agent, action items]
useCases: [Tự động hóa doanh nghiệp, Quản lý dự án, AI Workflow]
---

# 🚀 Tự động trích xuất và tự sửa lỗi Action Items cuộc họp thông AI Agent với n8n và OpenRouter

Các sếp có bao giờ cảm thấy mệt mỏi sau mỗi cuộc họp dài? Nào là đống ghi chú lộn xộn (meeting notes), nào là ngồi lọc xem ai làm gì, hạn chót khi nào, mức độ ưu tiên ra sao? Việc làm thủ công này vừa tốn thời gian, dễ sót việc lại cực kỳ chán ngắt.

Đừng lo, workflow n8n cực đỉnh này sẽ giúp các sếp giải quyết triệt để vấn đề trên! Sử dụng sức mạnh của **AI Agent kết hợp OpenRouter**, hệ thống sẽ tự động đọc biên bản cuộc họp, trích xuất danh sách công việc (`action items`) dưới dạng cấu trúc JSON nghiêm ngặt, tự động kiểm tra, **tự sửa lỗi (self-correct)** nếu kết quả chưa đạt chuẩn, và ghi nhớ ngữ cảnh qua từng phiên làm việc nhờ bộ nhớ thông minh. Tự động hóa 100%, không cần viết code phức tạp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Biến đống ghi chú thô sơ thành danh sách công việc chuẩn xác trong vài giây.
- **Cơ chế tự sửa lỗi thông minh (Self-Correcting)**: Nếu AI xuất dữ liệu sai định dạng hoặc thiếu trường, hệ thống sẽ tự động phản hồi lại lỗi cho AI để nó tự sửa cho đến khi đạt yêu cầu hoặc chạm ngưỡng tối đa.
- **Duy trì ngữ cảnh (Memory)**: Nhờ có *Window Buffer Memory*, ID công việc và văn phong được giữ nhất quán qua nhiều lần chạy trong cùng một phiên (`sessionId`).
- **Tích hợp linh hoạt**: Dễ dàng nhận request qua Webhook từ bất kỳ hệ thống nào (CRM, Notion, Slack, v.v.).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n**: Đã cài đặt phiên bản mới nhất hỗ trợ Langchain nodes (Agent, Memory, LLM).
- **Tài khoản OpenRouter**: Cần có API Key để kết nối với các mô hình ngôn ngữ lớn mạnh mẽ (như Claude 3.5 Sonnet, GPT-4o, v.v.).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần tải file JSON của workflow này từ n8n.io (Link: `https://n8n.io/workflows/15995`), sau đó vào giao diện n8n, chọn **Import from File** hoặc copy/paste trực tiếp đoạn JSON vào n8n Editor là xong.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 10 nodes phối hợp nhịp nhàng. Các sếp cần chú ý cấu hình các điểm sau:
- **Webhook - Meeting Notes**: Node nhận dữ liệu đầu vào qua phương thức `POST` với đường dẫn `self-correcting-agent`. Các sếp hãy lấy URL test/production để gửi request với các tham số: `meetingNotes`, `sessionId`, và `maxAttempts`.
- **OpenRouter Chat Model**: Node kết nối với OpenRouter. Các sếp bắt buộc phải tạo và gắn **OpenRouter Credentials** (API Key) vào đây để AI có thể hoạt động.
- **Extraction Agent & Window Buffer Memory**: Bộ đôi AI Agent và bộ nhớ đệm giúp phân tích dữ liệu và giữ ngữ cảnh theo `sessionId`. Đảm bảo các sếp cấu hình prompt cho Agent hướng dẫn nó trả về đúng cấu trúc JSON yêu cầu (id, title, assignee, deadline, priority, context).
- **Parse + Validate**: Node code kiểm tra tính hợp lệ của dữ liệu đầu ra từ AI (định dạng deadline, các trường bắt buộc, enum độ ưu tiên...).
- **Validated or Max Attempts? (IF Node)**: Quyết định xem dữ liệu đã chuẩn chưa hoặc đã đạt số lần thử tối đa (`maxAttempts`) chưa để kết thúc hoặc chuyển sang bước xử lý tiếp theo.

#### 3. Kích hoạt ⚡️
- Gửi một POST request mẫu qua Postman, cURL hoặc n8n Test Webhook với nội dung meeting notes của sếp.
- Kiểm tra kết quả trả về từ node **Respond to Client**.
- Nếu mọi thứ chạy mượt mà, hãy gạt công tắc sang **Active** để đưa vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Tùy biến quy tắc kiểm duyệt**: Sửa đổi logic trong node *Parse + Validate* nếu doanh nghiệp có các tiêu chuẩn khắt khe hơn (ví dụ: bắt buộc deadline không được để trống hoặc dạng "TBD").
- **Mở rộng bộ nhớ**: Thay thế *Window Buffer Memory* bằng cơ chế lưu trữ cơ sở dữ liệu (Database-backed memory) nếu cần lưu lịch sử dài hạn cho các phiên họp định kỳ.
- **Kết hợp thông báo**: Thêm node Slack hoặc Telegram sau node *Respond to Client* để bắn thông báo danh sách action items trực tiếp vào group chat của team ngay sau khi cuộc họp kết thúc.

### 📌 Kết luận
Workflow trích xuất và tự sửa lỗi Action Items cuộc họp với OpenRouter là một "vũ khí" lợi hại giúp tự động hóa khâu quản lý công việc sau họp, tiết kiệm hàng giờ đồng hồ mỗi tuần cho đội ngũ. Hãy áp dụng ngay vào hệ thống của các sếp để tối ưu hóa hiệu suất làm việc!