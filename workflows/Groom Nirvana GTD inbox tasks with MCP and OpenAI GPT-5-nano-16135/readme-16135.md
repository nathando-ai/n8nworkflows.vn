---
title: "🚀 Tự động hóa dọn dẹp hòm thư GTD Nirvana với AI và MCP"
description: "Hướng dẫn sử dụng n8n workflow tích hợp AI Agent và Model Context Protocol (MCP) để tự động hóa quy trình phân loại, tối ưu hóa task trong hòm thư Nirvana GTD."
slug: "tu-dong-hoa-nirvana-gtd-inbox-voi-mcp-va-openai"
tags: [n8n, automation, ai-agent, mcp, productivity, openai]
keywords: [n8n workflow, nirvana gtd, mcp client, openai gpt, tu dong hoa task, quan ly cong viec]
---

# 🚀 Tự động hóa dọn dẹp hòm thư GTD Nirvana với AI và MCP

Các sếp có bao giờ cảm thấy ngợp trước danh sách hòm thư (Inbox) lộn xộn trong phương pháp quản lý công việc GTD (Getting Things Done) với Nirvana chưa? Việc ngồi đọc lại từng task, viết lại tiêu đề cho rõ nghĩa, thêm ghi chú chi tiết thủ công thực sự tốn rất nhiều thời gian và năng lượng "não bộ".

Workflow n8n này sinh ra để giải quyết triệt để vấn đề đó! Bằng cách kết hợp **Model Context Protocol (MCP)** và sức mạnh của **OpenAI (GPT-5-nano)** thông qua **AI Agent**, workflow sẽ tự động hóa 100% quá trình "làm sạch" và chuẩn hóa hòm thư Nirvana của các sếp một cách mượt mà và thông minh.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Gom task từ Nirvana Inbox, xử lý qua AI và cập nhật lại kết quả mà không cần thao tác tay.
- **Tối ưu hóa nội dung:** AI tự động viết lại tên task ngắn gọn, rõ ràng và bổ sung ghi chú (notes) mạch lạc, dễ hiểu.
- **Chuẩn hóa cấu trúc:** Đảm bảo dữ liệu trả về khớp hoàn hảo với định dạng yêu cầu của Nirvana GTD thông qua Structured Output Parser.
- **Tiết kiệm thời gian:** Giải phóng hàng giờ đồng hồ dọn dẹp hòm thư mỗi tuần để tập trung vào việc thực thi công việc thực tế.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (phiên bản hỗ trợ Langchain và MCP nodes).
- **OpenAI API Key:** Tài khoản OpenAI có quyền truy cập mô hình mong muốn (workflow mẫu sử dụng `gpt-5-nano`).
- **Nirvana MCP Server:** Đã thiết lập kết nối MCP (Model Context Protocol) với Nirvana GTD và Token xác thực (Bearer Token lấy từ [Nirvana Dashboard](https://mcp.nirvanahq.com/tokens)).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể copy mã JSON của workflow từ [Nirvana GTD Workflow trên n8n.io](https://n8n.io/workflows/16135) và dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru, các sếp cần cấu hình chính xác các node sau:

- **OpenAI Chat Model:** 
  - Chọn Credentials OpenAI của các sếp.
  - Đảm bảo tham số model được cấu hình đúng (Mặc định trong workflow là `gpt-5-nano` hoặc có thể thay thế bằng các model phù hợp khác).
- **Nirvana MCP Get & Nirvana MCP Update:**
  - Cấu hình phương thức xác thực **Bearer Auth**.
  - Nhập Token được tạo từ bảng điều khiển Nirvana tại: `https://mcp.nirvanahq.com/tokens`. Token này dùng chung cho cả 2 node Get và Update.
- **Structured Output Parser to Match Nirvana Reqs:**
  - Kiểm tra và tùy chỉnh schema đầu ra nếu các sếp muốn AI định dạng tiêu đề và ghi chú task theo ý muốn riêng.
- **Edit Fields To Match Nirvana Reqs:**
  - Node này thực hiện map lại dữ liệu phản hồi từ AI Agent sang đúng cấu trúc payload mà Nirvana yêu cầu trước khi tiến hành cập nhật.

#### 3. Kích hoạt ⚡️
- Bấm nút **When clicking ‘Execute workflow’** để chạy thử nghiệm (Manual Trigger) với dữ liệu mẫu trong hòm thư Nirvana.
- Kiểm tra kết quả trên Nirvana xem các task đã được tối ưu hóa thành công chưa.
- Sau khi test ngon lành, hãy gạt công tắc **Active** để sẵn sàng sử dụng bất cứ lúc nào.

### ✍️ Mẹo & gợi ý nâng cao
- **Tự động hóa theo lịch:** Thay thế node `When clicking ‘Execute workflow’` bằng node `Schedule Trigger` để n8n tự động dọn dẹp hòm thư Nirvana vào mỗi buổi sáng hoặc cuối ngày.
- **Gửi thông báo:** Thêm node Telegram hoặc Slack ở cuối workflow để nhận báo cáo số lượng task đã được AI dọn dẹp thành công.
- **Lưu lịch sử:** Kết nối thêm Google Sheets để lưu trữ log các task trước và sau khi được AI tối ưu hóa nhằm dễ dàng tra cứu lại khi cần.

### 📌 Kết luận
Việc quản lý hòm thư GTD chưa bao giờ nhàn hạ đến thế khi có sự trợ giúp của AI và kiến trúc MCP hiện đại trong n8n. Hãy áp dụng ngay workflow này để tối ưu hóa năng suất cá nhân của các sếp ngay hôm nay!