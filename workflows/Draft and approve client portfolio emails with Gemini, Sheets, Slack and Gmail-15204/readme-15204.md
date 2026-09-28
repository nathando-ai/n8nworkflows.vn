---
title: "🚀 Tự động soạn thảo và phê duyệt email danh mục đầu tư khách hàng với Gemini, Google Sheets, Slack và Gmail"
description: "Xây dựng hệ thống quản lý tài sản thông minh kết hợp AI Agent của Gemini, Google Sheets, Slack và Gmail để tự động hóa quy trình duyệt và gửi email báo cáo danh mục đầu tư."
slug: "tu-dong-soan-thao-phe-duyet-email-danh-muc-dau-tu-gemini-slack-gmail"
tags: [n8n, automation, no-code, ai-agent, google-sheets, slack, gmail, gemini]
keywords: [n8n workflow, tự động hóa email, google sheets trigger, slack approval, gemini ai, quản lý tài sản]
info:
  title: "Gợi ý hạ tầng cho n8n"
  content: |
    Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
    👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
    👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
---

# 🚀 Tự động soạn thảo và phê duyệt email danh mục đầu tư khách hàng với Gemini, Google Sheets, Slack và Gmail

Các chuyên viên tư vấn tài chính hoặc đội ngũ quản lý tài sản thường tốn rất nhiều thời gian để cập nhật danh mục đầu tư, phân tích dữ liệu giao dịch, soạn thảo email cá nhân hóa cho từng khách hàng và chờ cấp trên hoặc chính họ phê duyệt trước khi gửi. Việc làm thủ công này không chỉ chậm trễ mà còn dễ xảy ra sai sót.

Workflow này sinh ra để giải quyết triệt để vấn đề đó! Nó kết hợp sức mạnh của **AI Agent (Gemini)**, **Google Sheets**, **Slack (Human-in-the-loop)** và **Gmail** để tự động hóa 100% quy trình: phát hiện thay đổi danh mục -> AI viết email -> Gửi Slack xin duyệt -> Tự động gửi khách hàng hoặc lưu vết khi bị từ chối.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian:** AI tự động soạn thảo email giải thích biến động danh mục dựa trên dữ liệu giao dịch thực tế.
- **Kiểm soát tuyệt đối (Human-in-the-loop):** Email không bao giờ được gửi đi nếu chưa có sự phê duyệt của chuyên viên qua Slack.
- **Đồng bộ dữ liệu thời gian thực:** Google Sheets tự động cập nhật trạng thái "Completed" hoặc "Needs Review" sau mỗi bước xử lý.
- **Chuyên nghiệp và cá nhân hóa:** Khách hàng nhận được email giải thích chi tiết, chuẩn xác, đúng hồ sơ rủi ro.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow chạy mượt mà, các sếp cần chuẩn bị sẵn các tài khoản và credentials sau:
- **Google Sheets:** Tài khoản Google để kết nối `Trigger: Portfolio Updated`, `Sheet: Mark as Completed`, và `Sheet: Mark 'Needs Review'`.
- **Google Gemini API (Google Palm API):** API Key để kết nối với node `LLM: Gemini`.
- **Slack Workspace:** Bot Token hoặc OAuth để kết nối với các node `Slack: Request Advisor Approval` và `Slack: Draft Rejected Alert`.
- **Gmail Account:** Tài khoản Google OAuth2 để cấu hình node `Gmail: Send to Client`.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow từ nguồn cung cấp, sau đó paste trực tiếp vào n8n Editor thông qua tính năng Import từ clipboard.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình lại các node cốt lõi sau:
- **Trigger: Portfolio Updated (`googleSheetsTrigger`):** Chọn đúng file Google Sheets và Sheet chứa dữ liệu danh mục đầu tư đang ở trạng thái "Pending".
- **AI: Draft Client Email (`agent`) & LLM: Gemini (`lmChatGoogleGemini`):** Nhập thông tin xác thực Google Gemini API (`googlePalmApi`). Tinh chỉnh Prompt trong Agent nếu muốn thay đổi phong cách văn bản email gửi khách hàng.
- **Slack: Request Advisor Approval (`slack`):** Kết nối tài khoản Slack và chọn đúng Channel ID nhận thông báo phê duyệt. Cấu hình các nút bấm tương tác (Approve/Reject).
- **Gmail: Send to Client (`gmail`):** Chọn credentials Gmail OAuth2 để hệ thống có quyền gửi email thay cho sếp.
- **Sheet: Mark as Completed & Sheet: Mark 'Needs Review' (`googleSheets`):** Cấu hình lại Document ID và Sheet Name để ghi log trạng thái chính xác vào file quản lý.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) với một dòng dữ liệu mẫu trên Google Sheets để kiểm tra toàn bộ luồng từ AI viết mail đến Slack thông báo.
- Sau khi test thành công, bấm nút **Active** để bật workflow chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm thông báo Telegram:** Thay thế hoặc bổ sung thông báo Slack bằng Telegram Bot để chuyên viên duyệt nhanh qua điện thoại di động.
- **Lưu lịch sử vào Database:** Lưu toàn bộ nội dung email đã gửi và phản hồi của khách hàng vào PostgreSQL hoặc Airtable để làm báo cáo thống kê định kỳ.
- **Đa dạng hóa AI:** Dễ dàng chuyển đổi linh hoạt từ Gemini sang OpenAI GPT-4 bằng cách thay thế node LLM tương ứng trong n8n.

### 📌 Kết luận
Workflow này là một minh chứng tuyệt vời cho việc ứng dụng AI và tự động hóa No-Code vào lĩnh vực tài chính - ngân hàng. Hãy "lên đồ" ngay hôm nay để tối ưu hóa quy trình chăm sóc khách hàng và nâng tầm chuyên nghiệp cho doanh nghiệp của các sếp!