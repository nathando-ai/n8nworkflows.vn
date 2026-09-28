---
title: "🚀 Tự động đồng bộ Highlight từ Glasp sang Notion, Slack hoặc Google Sheets với n8n"
description: "Hướng dẫn thiết lập workflow n8n tự động trích xuất các đoạn highlight và ghi chú từ Glasp, đồng bộ liền mạch về Notion, Google Sheets, Slack hoặc Webhook mỗi 6 giờ."
slug: "tu-dong-dong-bo-highlight-tu-glasp-sang-notion-slack-google-sheets"
tags: [n8n, automation, no-code, glasp, notion, productivity]
keywords: [n8n workflow, tự động hóa glasp, đồng bộ highlight glasp notion, trích xuất ghi chú glasp, n8n http request]
---

# 🚀 Tự động đồng bộ Highlight từ Glasp sang Notion, Slack hoặc Google Sheets

Các sếp có hay đọc sách, đọc báo qua extension Glasp và highlight lại những câu nói hay, kiến thức đắt giá không? Nhưng ngặt một nỗi là các highlight đó cứ nằm ì trên Glasp, mỗi lần cần tra cứu lại phải mò mẫm thủ công rất mất thời gian. 

Workflow n8n này sinh ra để giải quyết triệt để vấn đề đó! Nó sẽ tự động "hút" toàn bộ dữ liệu highlight mới nhất của các sếp từ Glasp và chuyển thẳng đến bất cứ nơi nào các sếp muốn (Notion, Google Sheets, Slack, Webhook...) hoàn toàn tự động 100% không cần đụng tay.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hoàn toàn:** Không cần copy-paste thủ công, dữ liệu highlight tự động đồng bộ theo lịch trình (mặc định 6 tiếng/lần).
- **Lưu trữ tập trung:** Gom toàn bộ tri thức đọc được vào kho lưu trữ cá nhân như Notion hoặc Google Sheets để dễ dàng search và tổng hợp.
- **Cá nhân hóa linh hoạt:** Dễ dàng "cắm" thêm các node đích (Destination) như gửi thông báo về Slack, gửi Email hoặc bắn Webhook sang hệ thống khác.
- **Bảo mật tuyệt đối:** Token xác thực được lưu trữ mã hóa trong n8n Credentials, không lộ trong code hay file JSON.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động.
- Tài khoản Glasp và **Glasp Access Token** (lấy tại: [glasp.co/settings/access_token](https://glasp.co/settings/access_token)).
- Ứng dụng đích mà các sếp muốn đồng bộ tới (Notion Database, Google Sheets, kênh Slack, v.v.).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này hoặc copy đoạn code JSON từ n8n.io, sau đó vào giao diện n8n Editor chọn **Import from JSON** để dán vào. Workflow gồm 4 nodes chính:
- **Schedule Trigger**: Lên lịch chạy định kỳ.
- **Prepare Parameters**: Chuẩn bị các tham số gọi API.
- **Glasp API**: Kết nối lấy dữ liệu highlight từ Glasp.
- **Filter & Format**: Lọc và định dạng lại dữ liệu đầu ra cho sạch sẽ.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node `Glasp API` (HTTP Request)**: 
  - Các sếp cần tạo một **Header Auth** credential mới:
    - **Name**: `Authorization`
    - **Value**: `Bearer YOUR_TOKEN` (Thay `YOUR_TOKEN` bằng Access Token lấy từ trang cài đặt của Glasp).
  - Gán credential này vào node `Glasp API`.
- **Node `Schedule Trigger`**: 
  - Mặc định workflow chạy mỗi 6 giờ. Các sếp có thể bấm vào node này để chỉnh lại tần suất chạy (chạy hàng ngày, hàng tuần tùy nhu cầu).
- **Kết nối đích (Destination)**:
  - Hãy thêm node đích của các sếp ngay sau node **Filter & Format**.
  - Các trường dữ liệu (fields) sẵn sàng để map sang node đích bao gồm:
    - `title`: Tiêu đề bài viết/trang sách
    - `url`: Link gốc của bài viết
    - `glasp_url`: Link trang highlight trên Glasp
    - `domain`, `category`, `tags`: Phân loại và thẻ
    - `highlightCount`: Tổng số câu highlight
    - `highlightsText`: Dạng văn bản thuần (Plain text)
    - `highlightsMarkdown`: Dạng Markdown
    - `createdAt`, `updatedAt`: Thời gian tạo và cập nhật

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** chạy thử lần đầu để kiểm tra xem dữ liệu từ Glasp có kéo về mượt mà không.
- Nếu mọi thứ xanh mướt, gạt công tắc **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp AI Summarization**: Nối thêm node AI (OpenAI/Anthropic) sau node `Filter & Format` để tóm tắt lại các đoạn highlight dài trước khi lưu vào Notion.
- **Bắn thông báo Teamwork**: Kết nối thêm node Slack để mỗi khi sếp đọc được bài hay và highlight, tự động bắn một tin nhắn vào kênh chung cho cả team cùng đọc.
- **Lưu lịch sử Tracking**: Workflow có cơ chế tự động làm sạch dữ liệu đã tracking sau 30 ngày để tránh phình to bộ nhớ.

### 📌 Kết luận
Việc gom nhặt kiến thức chưa bao giờ dễ dàng đến thế khi đã có trợ lý n8n và Glasp lo. Hãy cài đặt ngay workflow này để xây dựng "second brain" (bộ não thứ hai) cực kỳ xịn sò cho riêng mình các sếp nhé!