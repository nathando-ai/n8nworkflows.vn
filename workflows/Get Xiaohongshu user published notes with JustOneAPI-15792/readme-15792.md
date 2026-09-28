---
title: "🚀 Tự động lấy danh sách bài viết từ Xiaohongshu bằng n8n và JustOneAPI"
description: "Hướng dẫn chi tiết cách tự động thu thập và xử lý danh sách bài viết đã xuất bản của người dùng trên nền tảng Xiaohongshu (RED) thông qua JustOneAPI và n8n."
slug: "lay-bai-viet-xiaohongshu-n8n-justoneapi"
tags: [n8n, automation, no-code, xiaohongshu, market-research, api]
keywords: [n8n workflow, xiaohongshu automation, justoneapi, nghiên cứu thị trường, cào dữ liệu xiaohongshu]
---

# 🚀 Tự động lấy danh sách bài viết từ Xiaohongshu với n8n và JustOneAPI

Các sếp làm marketing, nghiên cứu thị trường hay xây dựng nội dung chắc hẳn đã biết Xiaohongshu (RED - Tiểu Hồng Thư) là một mỏ vàng ý tưởng. Tuy nhiên, việc phải thủ công tìm kiếm, sao chép từng bài viết của một tài khoản mục tiêu cực kỳ tốn thời gian và công sức. 

Đừng lo, bài viết này sẽ hướng dẫn các sếp cách thiết lập một workflow n8n tự động hóa 100% việc gọi API qua **JustOneAPI** để thu thập toàn bộ bài viết đã xuất bản của bất kỳ người dùng Xiaohongshu nào một cách nhanh chóng, sạch sẽ và chuẩn cấu trúc.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Thay vì copy/paste thủ công từng bài viết, hệ thống tự động hóa hoàn toàn.
- **Dữ liệu có cấu trúc:** Chuyển đổi dữ liệu JSON thô từ API thành danh sách bài viết sạch sẽ, dễ dàng xuất ra Google Sheets hoặc Notion.
- **Nghiên cứu đối thủ dễ dàng:** Dễ dàng phân tích nội dung, xu hướng bài viết của các KOL/KOC hàng đầu trên Xiaohongshu.
- **Linh hoạt mở rộng:** Dễ dàng kết nối tiếp với các công cụ lưu trữ hoặc AI để phân tích sentiment bài viết.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt sẵn sàng (Cloud hoặc Self-hosted).
- **JustOneAPI Account:** Tài khoản và API Key để truy cập dịch vụ bóc tách dữ liệu Xiaohongshu.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ kho lưu trữ n8n (Link gốc: [Get Xiaohongshu user published notes with JustOneAPI](https://n8n.io/workflows/15792)) hoặc copy đoạn JSON và paste trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 6 nodes chính, các sếp cần chú ý cấu hình kỹ các node sau:

- **Start Workflow (`manualTrigger`):** Node kích hoạt thủ công. Các sếp có thể thay đổi thành *Schedule Trigger* hoặc *Webhook* nếu muốn tự động hóa theo lịch trình.
- **Set API Request Parameters (`set`):** Node thiết lập các tham số đầu vào. Các sếp cần cấu hình đúng các thông số yêu cầu của JustOneAPI (ví dụ: `user_id` của tài khoản Xiaohongshu cần lấy bài viết).
- **Fetch User Notes from JustOneAPI (`httpRequest`):** Node thực hiện gọi HTTP Request đến API. Các sếp cần:
  - Điền đúng Endpoint URL của JustOneAPI.
  - Thêm thông tin xác thực (API Key/Headers) vào phần Authentication của node này.
- **Store Raw API Response Data (`set`):** Lưu lại phản hồi thô (Raw Data) trả về từ API để tiện cho việc kiểm tra, debug.
- **Process Notes into Structured List (`code`):** Node sử dụng mã JavaScript để lọc và định dạng lại dữ liệu thô thành một danh sách bài viết gọn gàng, đúng cấu trúc mong muốn.
- **Store Final Processed Notes (`set`):** Node xuất ra danh sách bài viết cuối cùng đã được xử lý sạch sẽ.

#### 3. Kích hoạt ⚡️
- Nhấn **Test step** hoặc **Execute Workflow** để chạy thử với một `user_id` mẫu và kiểm tra kết quả trả về ở node cuối cùng.
- Sau khi kiểm tra dữ liệu đã chuẩn chỉnh, gạt công tắc sang **Active** để chính thức đưa workflow vào vận hành.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu vào Google Sheets / Airtable:** Thay vì chỉ dừng ở node kết quả, các sếp hãy nối thêm node *Google Sheets* hoặc *Airtable* để tự động lưu danh sách bài viết vào bảng tính.
- **Tích hợp Telegram/Slack:** Gửi thông báo về Telegram cá nhân mỗi khi quét xong danh sách bài viết của một tài khoản mới.
- **Kết hợp AI (OpenAI/Anthropic):** Đưa nội dung các bài viết vừa lấy được vào LLM để tóm tắt xu hướng nội dung mà đối thủ đang theo đuổi.

### 📌 Kết luận
Workflow này là một "vũ khí" cực kỳ lợi hại cho anh em làm nghiên cứu thị trường và sáng tạo nội dung trên Xiaohongshu. Hãy áp dụng ngay vào hệ thống n8n của các sếp để tối ưu hóa công việc ngay hôm nay!