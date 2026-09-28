---
title: "🚀 Tự động trích xuất Email Creator YouTube với Apify Scraper và GPT-4o Mini trên n8n"
description: "Hướng dẫn chi tiết xây dựng workflow n8n tự động tìm kiếm kênh YouTube, cào dữ liệu mô tả và dùng AI GPT-4o Mini để trích xuất email liên hệ phục vụ outreach."
slug: "tu-dong-trich-xuat-email-youtube-apify-gpt4o-mini"
tags: [n8n, automation, apify, openai, youtube, email-finder]
keywords: [n8n workflow, trích xuất email youtube, apify scraper, gpt-4o mini, tự động hóa marketing, outreach]
---

# 🚀 Tự động trích xuất Email Creator YouTube với Apify Scraper và GPT-4o Mini

Các sếp làm Influencer Marketing hay Partnership chắc chắn đã quá ngán ngẩm cảnh phải lướt từng kênh YouTube, bấm vào tab "Giới thiệu" (About), giải Captcha để xem địa chỉ email của các Creator. Việc làm thủ công này vừa tốn thời gian, dễ bỏ sót lại cực kỳ nhàm chán.

Đừng lo, workflow n8n được thiết kế bởi chuyên gia Robert Breen này sẽ giúp các sếp tự động hóa 100% quy trình trên: từ tìm kiếm từ khóa, cào dữ liệu kênh YouTube thông qua **Apify**, cho đến sử dụng sức mạnh AI của **GPT-4o Mini** để lọc và trả về danh sách email sạch sẽ, chuẩn xác.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần thủ công tìm kiếm và copy/paste email từ hàng trăm kênh YouTube.
- **Trích xuất thông minh bằng AI:** GPT-4o Mini phân tích đoạn mô tả kênh phức tạp để bóc tách chính xác địa chỉ email liên hệ hợp lệ.
- **Tự động hóa theo lô (Batch Processing):** Xử lý mượt mà danh sách dài các kênh thông qua vòng lặp thông minh.
- **Sẵn sàng cho chiến dịch Outreach:** Dữ liệu đầu ra sạch sẽ, sẵn sàng tích hợp vào CRM hoặc các công cụ gửi email tự động.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản OpenAI:** Có API Key và đã nạp tiền (Billing) để sử dụng mô hình `gpt-4o-mini`.
- **Tài khoản Apify:** Đã đăng ký và lấy API Token để sử dụng các dịch vụ YouTube Scraper.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ thư viện n8n (Link gốc: [n8n.io/workflows/7597](https://n8n.io/workflows/7597)), sau đó copy toàn bộ nội dung JSON và dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 8 nodes chính. Các sếp cần tập trung cấu hình kỹ các phần sau để hệ thống chạy trơn tru:

- **Node `Set Search Term and # of searches`:** Thiết lập từ khóa tìm kiếm kênh YouTube mục tiêu và số lượng kết quả muốn cào.
- **Node `Search YouTube` & `Scrape Channels` (HTTP Request):** 
  - Cần tạo **HTTP Query Auth** credential trong n8n.
  - Query Key điền: `token`
  - Value điền: `YOUR_APIFY_API_KEY` (Lấy từ Apify Console -> Integrations).
  - Đảm bảo các sếp đã chuẩn bị sẵn 2 Scraper trong tài khoản Apify: *YouTube Scraper by streamers* và *YouTube Scraper by apidojo*.
- **Node `OpenAI Chat Model3`:**
  - Chọn credentials OpenAI API.
  - Đảm bảo model được cấu hình là `gpt-4o-mini` để tối ưu chi phí và tốc độ.
- **Node `Structured Output Parser4` & `Extract Email Address` (Agent):** AI sẽ dựa vào cấu trúc được định nghĩa sẵn để bóc tách email từ phần mô tả kênh một cách chính xác nhất.

#### 3. Kích hoạt ⚡️
- Bấm nút **‘Execute workflow’** (thông qua node `When clicking ‘Execute workflow’`) để chạy thử nghiệm với một từ khóa mẫu.
- Kiểm tra kết quả đầu ra ở các node AI Agent.
- Nếu mọi thứ hoạt động mượt mà, hãy bật nút **Active** để đưa workflow vào trạng thái tự động hoạt động.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu trữ tự động:** Kết nối thêm node **Google Sheets** hoặc **Airtable** ở cuối workflow để tự động lưu danh sách email thu thập được vào bảng tính.
- **Thông báo qua Telegram/Slack:** Thêm node gửi tin nhắn thông báo mỗi khi workflow quét xong một danh sách kênh mới.
- **Lọc trùng lặp:** Thêm một bước kiểm tra database hiện có trước khi cào để tránh quét lại các kênh đã lưu trữ email trước đó.

### 📌 Kết luận
Việc tìm kiếm khách hàng tiềm năng trên YouTube chưa bao giờ dễ dàng đến thế khi kết hợp sức mạnh của cào dữ liệu Apify và AI thông minh từ OpenAI trên nền tảng n8n. Hãy áp dụng ngay vào quy trình của các sếp để tối ưu hóa hiệu suất làm việc ngay hôm nay!