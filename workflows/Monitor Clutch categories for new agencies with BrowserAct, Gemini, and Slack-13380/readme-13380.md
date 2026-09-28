---
title: "🚀 Tự động quét và tìm kiếm Agency mới trên Clutch.co với BrowserAct, Gemini & Slack"
description: "Hướng dẫn xây dựng hệ thống tự động theo dõi danh mục B2B trên Clutch, phát hiện agency mới gia nhập thị trường bằng AI và gửi cảnh báo tức thì qua Slack."
slug: "tu-dong-quet-agency-moi-tren-clutch-browseract-gemini-slack"
tags: [n8n, automation, lead-generation, ai-summarization, browseract, slack]
keywords: [n8n workflow, tu dong hoa lead generation, scrape clutch, browseract n8n, ai agent n8n]
---

# 🚀 Tự động quét và tìm kiếm Agency mới trên Clutch.co với BrowserAct, Gemini & Slack

Các sếp làm trong lĩnh vực Agency, B2B Sales hay Marketing chắc hẳn đều hiểu việc tìm kiếm các đối thủ mới nổi hoặc các agency vừa gia nhập thị trường trên Clutch.co tốn nhiều thời gian thế nào. Việc ngồi thủ công click từng trang, copy thông tin vào Excel mỗi tuần không chỉ nhàm chán mà còn dễ bỏ lỡ cơ hội tiếp cận khách hàng/đối tác tiềm năng sớm.

Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n tự động hóa 100% giúp quét danh mục Clutch, làm sạch dữ liệu bằng AI, so sánh với cơ sở dữ liệu cũ và bắn thông báo "nóng" về Slack ngay khi có agency mới xuất hiện!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hoàn toàn (Set & Forget):** Lịch trình hàng tuần (Weekly Trigger) tự động chạy quét dữ liệu mà không cần can thiệp thủ công.
- **Phát hiện lead "nóng" chớp nhoáng:** Hệ thống AI (Gemini/OpenRouter) tự động so sánh dữ liệu cũ và mới để lọc ra chính xác các agency vừa xuất hiện.
- **Cảnh báo tức thì:** Đội ngũ Sales/Marketing nhận ngay thông tin chi tiết về agency mới qua kênh Slack.
- **Quản trị dữ liệu thông minh:** Tự động đồng bộ và cập nhật danh sách vào Google Sheets một cách ngăn nắp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Self-hosted hoặc Cloud).
- **BrowserAct API & Template:** Cần tài khoản BrowserAct và kích hoạt template "The New Entrant Asset Finder".
- **OpenRouter API Key:** Để sử dụng các mô hình AI mạnh mẽ (như Google Gemini 2.5 Pro qua OpenRouter).
- **Google Sheets:** Chuẩn bị sẵn một file Google Sheets gồm các sheet phục vụ cho Database và dữ liệu trích xuất (Extraction).
- **Slack Workspace:** Kênh Slack để nhận cảnh báo (Hot Alert).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow từ nguồn gốc hoặc tải file về, sau đó chọn **Import from File** hoặc dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node trọng điểm sau:
- **Clutch Category Link (`set`):** Điền đường dẫn danh mục Clutch.co mà các sếp muốn theo dõi (ví dụ: `https://clutch.co/developers`).
- **Scrape page funding data (`n8n-nodes-browseract.browserAct`):** Kết nối tài khoản BrowserAct, chọn đúng template "The New Entrant Asset Finder" và điền API Key tương ứng.
- **OpenRouter Chat Model & OpenRouter Chat Model1 (`lmChatOpenRouter`):** Thêm OpenRouter API Key. Tại node số 1, hãy đảm bảo chọn model `google/gemini-2.5-pro` để AI xử lý làm sạch và so sánh dữ liệu chuẩn xác nhất.
- **Các node Google Sheets (`Clear Database`, `Upsert new records`, `Get old extraction data`, v.v.):** Kết nối với tài khoản Google Sheets thông qua OAuth2, sau đó trỏ đến file Google Sheet và tên Sheet (Tab) tương ứng mà các sếp đã chuẩn bị sẵn cho Database và Second Extraction.
- **Notify team (`slack`):** Cấu hình kết nối Slack và chọn kênh (Channel) mà bot sẽ gửi tin nhắn cảnh báo khi phát hiện agency mới.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** chạy thử lần đầu với dữ liệu thủ công để kiểm tra các bước Scrape, AI parsing và Google Sheets.
- Nếu mọi thứ xanh mướt (success), các sếp bật công tắc **Active** ở góc trên bên phải để hệ thống tự động chạy theo lịch hẹn hàng tuần.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa kênh thông báo:** Ngoài Slack, các sếp có thể nối thêm node Telegram hoặc Email để gửi báo cáo tóm tắt cho sếp lớn hoặc đội ngũ quản lý.
- **Lưu log chi tiết:** Thêm các bước ghi log lịch sử quét vào một sheet riêng để dễ dàng theo dõi biến động thị trường theo quý/năm.
- **Tích hợp CRM:** Nối tiếp bước phát hiện lead mới bằng việc tự động đẩy thông tin agency đó vào các CRM như HubSpot, Notion hoặc Pipedrive để đội sales tiến hành outreach ngay lập tức.

### 📌 Kết luận
Workflow này là một "vũ khí bí mật" giúp các sếp chiếm lĩnh thị trường B2B bằng cách nắm bắt danh sách các đối thủ/agency mới xuất hiện trước cả đối thủ cạnh tranh. Hãy áp dụng ngay vào hệ thống n8n của các sếp để tối ưu hóa quy trình Lead Generation từ hôm nay!