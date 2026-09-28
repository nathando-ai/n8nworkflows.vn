---
title: "🚀 Tự động giám sát giá đối thủ cạnh tranh với Firecrawl, GPT-4, Google Sheets và Gmail"
description: "Hướng dẫn xây dựng hệ thống tự động cào dữ liệu giá sản phẩm từ website đối thủ, phân tích bằng AI, so sánh biến động lịch sử và gửi cảnh báo qua Gmail."
slug: "tu-dong-giam-sat-gia-doi-thu-voi-firecrawl-gpt-4-sheets-gmail"
tags: [n8n, automation, no-code, market-research, ai, firecrawl]
keywords: [n8n workflow, giám sát giá đối thủ, cào dữ liệu firecrawl, openai gpt-4, tự động hóa giá, google sheets n8n]
---

# 🚀 Tự động giám sát giá đối thủ cạnh tranh với Firecrawl, GPT-4, Google Sheets & Gmail

Các sếp làm trong ngành e-commerce hoặc phân tích thị trường chắc chắn hiểu rõ nỗi đau: Việc hàng ngày phải ngồi "soi" giá đối thủ (Nike, Adidas,...) thủ công vừa tốn thời gian, vừa dễ bỏ sót các biến động giá sốc hay tình trạng hết hàng. Chỉ cần đối thủ hạ giá 10% mà mình chậm chân một nhịp là khách bay sạch.

Giải pháp đây rồi! Workflow n8n siêu việt này sẽ thay các sếp làm tất cả: tự động cào website đối thủ, dùng AI trích xuất dữ liệu, so sánh với lịch sử giá trong Google Sheets, và bắn email cảnh báo ngay lập tức khi có biến động. Tất cả chạy tự động 100% không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 2+ giờ mỗi ngày:** Không còn phải copy-paste hay check giá thủ công từng trang web.
- **Phát hiện biến động thời gian thực:** Nhận cảnh báo qua Gmail ngay khi đối thủ thay đổi giá hoặc tình trạng kho hàng.
- **Lưu trữ dữ liệu thông minh:** Tự động ghi nhận lịch sử giá vào Google Sheets để phân tích xu hướng thị trường dài hạn.
- **Trích xuất chính xác bằng AI:** Sử dụng sức mạnh của GPT-4 để bóc tách thông tin từ các trang web phức tạp một cách chuẩn xác nhất.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Self-hosted n8n instance:** Do workflow sử dụng các node tùy chỉnh nâng cao.
- **Firecrawl Account & API Key:** Dùng cho các node `Scrape URL`.
- **OpenAI API Key:** Cho node `🤖 AI Extract Product Data using GPT-4.1-mini`.
- **Google Account:** Để kết nối Google Sheets (`📊 Read Historical Data`, `💾 Update Historical Data`, `📝 Log Alert Details`) và Gmail (`Send a message`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ đoạn JSON của workflow (hoặc tải file JSON từ nguồn gốc) và dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần cấu hình kỹ các node sau:
- **Các node Scrape URL (Nike, Adidas, Sneakerpricer):** Kết nối với `Firecrawl API` credential của các sếp và điền các URL sản phẩm cần theo dõi.
- **Node `🤖 AI Extract Product Data using GPT-4.1-mini`:** Chọn `openAiApi` credentials, sau đó tinh chỉnh prompt trong `keyParameters` để hệ thống trích xuất đúng tên sản phẩm, giá cả và tình trạng kho.
- **Các node Google Sheets (`📊 Read Historical Data`, `💾 Update Historical Data`, `📝 Log Alert Details`):** 
  - Cần tạo trước một Google Sheet với các cột bắt buộc: 
    - **Product Name** (Cột A)
    - **Current Price** (Cột B)
    - **Previous Price** (Cột C)
    - **Stock Status** (Cột D)
    - **Last Updated** (Cột E)
    - **URL** (Cột F)
    - **Change Detected** (Cột G)
  - Lấy Spreadsheet ID dán vào các node Google Sheets trong n8n.
- **Node `Send a message` (Gmail):** Kết nối `gmailOAuth2` và cấu hình email nhận cảnh báo (có thể dùng email cá nhân của các sếp hoặc đội ngũ pricing).

#### 3. Kích hoạt ⚡️
- Bấm nút **‘Execute workflow’** (`When clicking ‘Execute workflow’`) để test thử lần đầu với dữ liệu mẫu.
- Kiểm tra lại Google Sheets và hộp thư Gmail xem dữ liệu đã đổ về chuẩn chỉnh chưa.
- Sau khi test ngon nghẻ, gạt công tắc sang **Active** để workflow chạy tự động theo lịch trình!

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Slack/Telegram:** Ngoài Gmail, các sếp có thể nối thêm node Telegram Bot để nhận thông báo tức thời ngay trên điện thoại khi đang di chuyển.
- **Lên lịch chạy định kỳ (Schedule Trigger):** Thay vì dùng nút bấm thủ công, hãy gắn thêm node `Schedule Trigger` để hệ thống tự cào giá 2 lần/ngày (sáng và tối).
- **Mở rộng danh mục:** Dễ dàng nhân bản các node Firecrawl để theo dõi hàng trăm sản phẩm từ nhiều website khác nhau chỉ trong một workflow.

### 📌 Kết luận
Giám sát giá đối thủ chưa bao giờ dễ dàng và tự động đến thế. Áp dụng ngay workflow này để luôn nắm thế chủ động trong cuộc chiến giá cả thị trường e-commerce nhé các sếp!