---
title: "🚀 Tự động tìm kiếm và lọc danh sách khách hàng tiềm năng gọi vốn với BrowserAct & Gemini"
description: "Hướng dẫn xây dựng workflow n8n tự động cào dữ liệu bài viết gọi vốn, sử dụng AI Gemini phân tích và lưu trữ lead chất lượng cao vào Google Sheets."
slug: "tim-kiem-khach-hang-tiem-nang-browseract-gemini-n8n"
tags: [n8n, automation, lead-generation, browseract, google-gemini, google-sheets]
keywords: [n8n workflow, tìm kiếm khách hàng tiềm năng, lead generation, browseract, google gemini ai, tự động hóa n8n]
---

# 🚀 Tự động tìm kiếm và lọc danh sách khách hàng tiềm năng gọi vốn với BrowserAct & Gemini

Việc thủ công lướt các trang tin tức công nghệ (như TechCrunch) để tìm kiếm các công ty vừa gọi vốn thành công nhằm tiếp cận bán hàng cực kỳ tốn thời gian và dễ bỏ lỡ cơ hội. Nỗi đau này sẽ được giải quyết triệt để với workflow n8n tự động hóa 100% không cần code dưới đây, giúp các sếp gom lead "nóng hổi" mỗi ngày mà không tốn một giọt mồ hôi.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện**: Cào dữ liệu bài viết, phân tích thông tin công ty gọi vốn mà không cần can thiệp thủ công.
- **Dữ liệu chuẩn xác nhờ AI**: Ứng dụng Google Gemini kết hợp Structured Output để trích xuất thông tin công ty, số vốn, lĩnh vực cực kỳ chuẩn xác.
- **Chống trùng lặp thông minh**: Tự động cập nhật hoặc thêm mới dữ liệu vào Google Sheets dựa trên tên công ty.
- **Cảnh báo tức thì**: Gửi thông báo trực tiếp về kênh Slack ngay khi có lead chất lượng mới.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Đã cài đặt sẵn sàng.
- **BrowserAct Account**: Tài khoản và API Key để thực hiện tác vụ web scraping (kèm template *Funding Announcement to Lead List*).
- **Google Gemini (Google Palm API)**: Credentials để AI Agent xử lý văn bản.
- **Google Sheets**: Tài liệu lưu trữ danh sách lead.
- **Slack Account**: Cấu hình OAuth2 để nhận tin nhắn cảnh báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này và import trực tiếp vào n8n Editor của các sếp, hoặc tạo mới một workflow và copy/paste cấu trúc JSON tương ứng.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Get row(s) in sheet & Append or update row in sheet**: Chọn đúng Credentials tài khoản Google Sheets của các sếp, trỏ tới đúng File Google Sheet chứa danh sách từ khóa và bảng lưu trữ lead.
- **BrowserAct Nodes (`Run a workflow Series 1/2`, `Get workflow Series 1/2`)**: Cấu hình BrowserAct API credentials, kiểm tra và điền chính xác `workflow_Name` tương ứng với template scraping trong tài khoản BrowserAct của các sếp.
- **AI Agent & Gemini l**: Cấu hình API Key cho Google Gemini. Tinh chỉnh prompt trong AI Agent nếu muốn trích xuất thêm các trường thông tin cụ thể khác.
- **Send a message (Slack)**: Kết nối tài khoản Slack và chọn kênh nhận thông báo lead mới.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** (hoặc dùng node Trigger thủ công) để chạy thử nghiệm với dữ liệu mẫu từ Google Sheets.
- Kiểm tra kết quả trên Google Sheets và Slack. Sau khi mọi thứ chạy mượt mà, hãy gạt công tắc sang **Active** để workflow hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm Cron Node**: Thay thế `manualTrigger` bằng node Cron để chạy định kỳ (ví dụ: tự động cào tin tức mỗi sáng lúc 8:00 AM).
- **Mở rộng kênh thông báo**: Kết hợp thêm node Telegram hoặc Email bên cạnh Slack để không bỏ lỡ bất kỳ lead tiềm năng nào.
- **Ghi Log lỗi**: Thêm node bắt lỗi (Error Trigger) để tự động gửi thông báo về Slack nếu quá trình scraping hoặc AI gặp sự cố.

### 📌 Kết luận
Workflow này là một "vũ khí" hạng nặng cho các đội ngũ Sales và Growth muốn tiếp cận sớm với các công ty có nguồn tiền đầu tư. Hãy thiết lập ngay hôm nay để tự động hóa phễu tìm kiếm khách hàng tiềm năng của các sếp!