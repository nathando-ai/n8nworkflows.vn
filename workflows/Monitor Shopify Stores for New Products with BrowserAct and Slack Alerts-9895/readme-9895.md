---
title: "🚀 Tự Động Theo Dõi Sản Phẩm Mới Trên Shopify Của Đối Thủ Bằng BrowserAct và Slack"
description: "Hướng dẫn cài đặt workflow n8n giúp tự động quét cửa hàng Shopify của đối thủ, so sánh dữ liệu và gửi cảnh báo ngay lập tức qua Slack khi có sản phẩm mới."
slug: "theo-doi-san-pham-shopify-doi-thu-browseract-slack"
tags: [n8n, automation, shopify, browseract, slack, market-research]
keywords: [n8n workflow, theo dõi shopify đối thủ, browseract n8n, cảnh báo sản phẩm mới slack, market research tự động]
---

# 🚀 Tự Động Theo Dõi Sản Phẩm Mới Trên Shopify Của Đối Thủ Bằng BrowserAct và Slack

Việc theo dõi sát sao chiến lược sản phẩm của đối thủ cạnh tranh trên nền tảng Shopify là chìa khóa vàng trong kinh doanh. Tuy nhiên, việc phải thủ công truy cập vào từng cửa hàng mỗi ngày để kiểm tra xem họ có ra mắt sản phẩm mới hay không vừa tốn thời gian, vừa dễ bỏ lỡ cơ hội. 

Workflow n8n này sẽ giải quyết triệt để vấn đề đó. Hệ thống sẽ tự động hóa 100% quy trình: quét danh sách đối thủ, thu thập dữ liệu sản phẩm mới nhất thông qua công cụ **BrowserAct**, so sánh với lịch sử dữ liệu cũ trên **Google Sheets**, và ngay lập tức bắn tin nhắn thông báo vào **Slack** nếu phát hiện sản phẩm mới ra lò. Các sếp không cần phải viết một dòng code nào cả!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Bắt nhịp thị trường nhanh chóng:** Nhận cảnh báo sản phẩm mới của đối thủ ngay trong vài phút thay vì mất hàng ngày dò tìm thủ công.
- **Tự động hóa toàn diện:** Quản lý hàng loạt đối thủ cùng lúc thông qua vòng lặp thông minh (`Loop Over Items`).
- **Lưu trữ lịch sử khoa học:** Tự động tạo và quản lý Google Sheets riêng biệt cho từng đối thủ để theo dõi biến động.
- **Cảnh báo thời gian thực:** Đội ngũ kinh doanh/R&D sẽ nhận được thông báo trực tiếp qua kênh Slack quen thuộc.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Self-hosted hoặc Cloud).
- Tài khoản và API Key của **BrowserAct** (kèm Community Node `n8n-nodes-browseract-workflows`).
- Tài khoản **Google Sheets** để quản lý danh sách đối thủ và lưu trữ dữ liệu.
- Tài khoản **Slack** để nhận thông báo thời gian thực.
- Template BrowserAct đã được tạo sẵn có tên: **“Competitors Shopify Website New Product Monitor”**.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này hoặc copy toàn bộ mã nguồn JSON, sau đó dán trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động mượt mà, các sếp cần cấu hình chính xác các thành phần sau:

- **Google Sheets Nodes (`Get row(s) in sheet`, `Create sheet`, `Store Data`, v.v.):** 
  - Kết nối tài khoản Google Sheets của các sếp.
  - Tại bảng tính chính (Master Sheet), hãy tạo một sheet mang tên `Competitor Store List` với 3 cột cơ bản: `Name`, `Link`, và `Pagination Type`.
- **BrowserAct Nodes (`Get workflow Data`, `Run a workflow`):**
  - Cấu hình API Key của BrowserAct.
  - Đảm bảo sử dụng template **“Competitors Shopify Website New Product Monitor”** trong tài khoản BrowserAct của các sếp.
- **Code Nodes (`Compare Datas`, `Parse Json`):**
  - Các node này đã được viết sẵn logic JavaScript để phân tích cấu trúc dữ liệu JSON trả về từ trình duyệt và so sánh sự chênh lệch sản phẩm cũ/mới. Các sếp không cần sửa gì thêm trừ khi muốn tùy chỉnh hiển thị.
- **Slack Node (`Send a message`):**
  - Kết nối tài khoản Slack và cập nhật chính xác **Channel ID** nơi các sếp muốn nhận thông báo sản phẩm mới.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (`Test workflow`) với một vài dòng dữ liệu mẫu để kiểm tra xem dữ liệu có đổ về Google Sheets và bắn thông báo lên Slack thành công hay không.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để hệ thống tự động chạy theo lịch của `Schedule Trigger`.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Ngoài Slack, các sếp có thể nối thêm node Telegram hoặc Email để nhận cảnh báo đa kênh.
- **Ghi log chi tiết:** Lưu lại toàn bộ lịch sử các lần quét lỗi hoặc thành công vào một bảng Google Sheet riêng để dễ dàng audit hệ thống.
- **Tích hợp AI phân tích:** Nối thêm một LLM node (như OpenAI/Claude) sau bước phát hiện sản phẩm mới để AI tự động tóm tắt đánh giá sơ bộ về sản phẩm đó của đối thủ.

### 📌 Kết luận
Workflow này là một "vũ khí bí mật" cực kỳ mạnh mẽ dành cho các nhà nghiên cứu thị trường, chủ cửa hàng Shopify và các đội ngũ Product Research. Hãy thiết lập ngay hôm nay để nắm bắt từng bước đi của đối thủ trên thị trường!