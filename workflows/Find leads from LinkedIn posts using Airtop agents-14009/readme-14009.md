---
title: "🚀 Tự động tìm kiếm Leads chất lượng từ bài viết LinkedIn với Airtop Agents"
description: "Hướng dẫn tích hợp Airtop Agent vào n8n để tự động biến các tương tác, bình luận trên bài viết LinkedIn thành danh sách khách hàng tiềm năng cực kỳ nhanh chóng."
slug: "tim-kiem-leads-tu-linkedin-bang-airtop-agents"
tags: [n8n, automation, no-code, lead-generation, linkedin, airtop, ai-agent]
keywords: [n8n workflow, tự động hóa linkedin, tìm kiếm leads, airtop agent, linkedin lead generation, trích xuất dữ liệu linkedin]
---

# 🚀 Tự động tìm kiếm Leads chất lượng từ bài viết LinkedIn với Airtop Agents

Các sếp có bao giờ cảm thấy mệt mỏi khi phải thủ công lọc từng bình luận (comment), tương tác trên các bài đăng LinkedIn hot để tìm kiếm khách hàng tiềm năng (leads)? Công việc này không chỉ tốn hàng giờ đồng hồ mỗi ngày mà còn rất dễ bỏ sót những cơ hội kinh doanh giá trị.

Giải pháp là đây! Workflow n8n kết hợp với **Airtop AI Agent** sẽ giúp các sếp tự động hóa 100% quy trình này bằng ngôn ngữ tự nhiên, biến mọi tương tác trên LinkedIn thành một phễu khách hàng tiềm năng tự động chạy ngầm.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không còn phải copy-paste profile hay thủ công check từng người tương tác bài viết.
- **Tự động hóa thông minh:** Tận dụng công nghệ AI Browser Automation của Airtop để trích xuất dữ liệu chính xác từ LinkedIn mà không sợ bị chặn.
- **Mở rộng phễu bán hàng liên tục:** Dễ dàng kết nối danh sách leads mới tìm được vào CRM, Google Sheets hoặc gửi thông báo về Telegram/Slack ngay lập tức.
- **Hoạt động linh hoạt:** Có thể kích hoạt thủ công, theo lịch trình hoặc gọi từ một workflow tổng khác (`Execute Workflow Trigger`).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một tài khoản **n8n** (Cloud hoặc Self-hosted).
- Tài khoản **Airtop** và đã tạo/cài đặt template **"Turn LinkedIn Engagements to Pipeline"** trên nền tảng Airtop.
- **Airtop API Key** để kết nối n8n với Airtop Agent.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một Sub-workflow mới trong n8n, sau đó thêm các node tương ứng hoặc copy/paste đoạn JSON workflow vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 2 nodes chính, các sếp cần chú ý cấu hình kỹ lưỡng:

- **Node: When Executed by Another Workflow (`executeWorkflowTrigger`)**
  - Node này đóng vai trò nhận dữ liệu đầu vào (thường là link bài viết LinkedIn hoặc Profile) từ một workflow mẹ khác. Các sếp có thể cấu hình thêm các tham số đầu vào (như `postUrl`) để truyền vào Agent.

- **Node: Run "Turn LinkedIn Engagements to Pipeline" (`airtop`)**
  - **Credentials:** Cần tạo kết nối `airtopApi` bằng cách nhập API Key lấy từ tài khoản Airtop của các sếp.
  - **Resource:** Chọn `agent`.
  - **Template Setup (CỰC KỲ QUAN TRỌNG):** Trước khi chạy n8n, các sếp bắt buộc phải cài đặt template [*Turn LinkedIn Engagements to Pipeline*](https://www.airtop.ai/templates/linkedin-lead-generation-from-post-commenters-old-3) trực tiếp trong tài khoản Airtop của mình. Airtop Agent sẽ sử dụng template này để thực thi kịch bản duyệt web và trích xuất dữ liệu trên LinkedIn.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (Test run) với một link bài viết LinkedIn cụ thể để kiểm tra xem Airtop Agent đã trích xuất dữ liệu trả về n8n thành công chưa.
- Sau khi test ngon lành, các sếp có thể kết nối workflow này vào hệ thống tự động hóa tổng thể của mình.

### ✍️ Mẹo & gợi ý nâng cao
- **Đẩy dữ liệu vào Google Sheets / Airtable:** Sau node Airtop, các sếp có thể gắn thêm node Google Sheets để lưu trữ danh sách Leads vừa tìm được.
- **Bắn thông báo về Telegram/Slack:** Thêm node Telegram để nhận tin nhắn báo cáo mỗi khi có một lead chất lượng mới được quét từ bài viết LinkedIn.
- **Tự động gửi kết bạn/nhắn tin:** Mở rộng workflow bằng cách kết hợp thêm các bước xử lý nội dung AI (OpenAI/Anthropic) để soạn tin nhắn cá nhân hóa gửi cho leads.

### 📌 Kết luận
Việc khai thác khách hàng tiềm năng từ các bài viết LinkedIn giờ đây đã trở nên đơn giản hơn bao giờ hết nhờ sự kết hợp giữa n8n và Airtop AI Agents. Hãy cài đặt ngay hôm nay để tối ưu hóa quy trình Sales và Marketing cho doanh nghiệp của các sếp nhé!