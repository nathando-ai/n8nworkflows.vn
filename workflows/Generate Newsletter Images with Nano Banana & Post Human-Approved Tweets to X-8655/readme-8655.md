---
title: "🚀 Tự động tạo ảnh Newsletter với Nano Banana và Kiểm duyệt Tweet qua Telegram trước khi đăng lên X"
description: "Hướng dẫn xây dựng hệ thống tự động hóa n8n: AI viết tweet và tạo ảnh từ Google Sheets, gửi duyệt qua Telegram, sau đó tự động đăng lên X (Twitter)."
slug: "tu-dong-tao-anh-newsletter-va-dang-tweet-qua-telegram-n8n"
tags: [n8n, automation, ai-agent, twitter, telegram, google-sheets, openAI]
keywords: [n8n workflow, tu dong hoa twitter, ai tao anh, telegram approval, google sheets automation]
---

# 🚀 Tự động tạo ảnh Newsletter với Nano Banana và Kiểm duyệt Tweet qua Telegram trước khi đăng lên X

Việc duy trì sự hiện diện thường xuyên trên mạng xã hội X (Twitter) bằng nội dung chất lượng kết hợp hình ảnh bắt mắt đòi hỏi rất nhiều thời gian thủ công. Các sếp thường phải mất hàng giờ để lên ý tưởng, viết bài, thiết kế ảnh, và đặc biệt là lo sợ việc AI đăng những nội dung chưa chuẩn xác. 

Workflow n8n này chính là giải pháp tự động hóa 100% không cần code giúp giải quyết triệt để nỗi đau đó. Hệ thống sẽ tự động lấy dữ liệu từ Google Sheets, sử dụng AI (OpenAI) để viết nội dung Tweet và tạo prompt vẽ ảnh, kết hợp dịch vụ **Nano Banana** để tạo ảnh minh họa, sau đó gửi qua **Telegram** để các sếp kiểm duyệt trước khi chính thức "lên sóng" trên X!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Kiểm soát tuyệt đối nội dung:** Mọi bài viết và hình ảnh AI tạo ra đều phải thông qua "cửa ải" duyệt trên Telegram trước khi xuất bản.
- **Tiết kiệm 90% thời gian:** Tự động hóa hoàn toàn quy trình từ ý tưởng (Google Sheets), sinh nội dung (OpenAI), tạo hình ảnh (Nano Banana) đến đăng bài (X).
- **Cá nhân hóa và chuyên nghiệp:** Hình ảnh newsletter độc quyền được tạo tự động cho từng chủ đề bài viết.
- **Vận hành không gián đoạn:** Hoạt động tự động kích hoạt ngay khi có dòng dữ liệu mới được thêm vào Google Sheets.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị sẵn các tài khoản và API Keys sau:
- **n8n Instance** (Self-hosted hoặc Cloud).
- **Google Sheets account** (chứa file quản lý nội dung/newsletter).
- **OpenAI API Key** (cho các AI Agent viết tweet và tạo prompt).
- **Nano Banana API** (hoặc dịch vụ tạo ảnh tương ứng được cấu hình trong `Image Gen`).
- **Telegram Bot Token & Chat ID** (để nhận thông báo và gửi phản hồi duyệt bài).
- **X (Twitter) Developer Account** (để lấy API Credentials đăng bài tự động).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn JSON của workflow (hoặc tải file từ nguồn gốc) và dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình chính xác các node quan trọng sau đây:
- **Google Sheets Trigger**: Kết nối tài khoản Google, chọn đúng Spreadsheet và Sheet chứa dữ liệu bài viết đầu vào.
- **Tweet Generator & Prompt Generator (Agent)**: Chọn `OpenAI Chat Model` và `OpenAI Chat Model1` tương ứng, đảm bảo OpenAI Credentials đã được thêm và có hạn mức (quota) hoạt động.
- **Image Gen (Nano Banana)** (`httpRequest`): Cấu hình Endpoint API và API Key của Nano Banana để hệ thống gửi yêu cầu tạo ảnh dựa trên prompt do AI sinh ra.
- **Send Tweet text for approval & Send Tweet image for approval** (`telegram`): Điền thông tin Bot Token và Chat ID của sếp để nhận tin nhắn duyệt bài kèm hình ảnh.
- **Approved** (`if`): Kiểm tra logic phản hồi từ Telegram (nút bấm "Approve" hoặc "Reject").
- **Create Tweet** (`twitter`): Kết nối tài khoản X (Twitter) cá nhân hoặc doanh nghiệp để tiến hành đăng bài khi có lệnh duyệt.
- Các node **Google Sheets** còn lại (`Add Image URL`, `Tweet not approved`, `Tweet posted`): Cấu hình để cập nhật trạng thái bài viết (Đã duyệt, Đã đăng, Hay Từ chối) ngược lại vào Google Sheets nhằm quản lý lịch sử.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (**Test Workflow**) với một dòng dữ liệu mẫu trên Google Sheets để kiểm tra luồng tin nhắn qua Telegram.
- Sau khi mọi thứ chạy mượt mà, hãy gạt công tắc sang chế độ **Active** để hệ thống tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Thay vì chỉ dùng Telegram, các sếp có thể tích hợp thêm Slack hoặc Discord để team cùng tham gia kiểm duyệt nội dung.
- **Lưu trữ ảnh tự động:** Kết hợp thêm node Google Drive hoặc AWS S3 để lưu lại các bức ảnh do Nano Banana tạo ra trước khi đưa lên X.
- **Báo cáo định kỳ:** Thêm một nhánh thống kê số lượng Tweet đã đăng thành công gửi về Telegram vào cuối tuần để nắm tình hình hoạt động.

### 📌 Kết luận
Workflow "Generate Newsletter Images with Nano Banana & Post Human-Approved Tweets to X" là một cỗ máy tự động hóa hoàn hảo giúp kết hợp sức mạnh của Generative AI với sự kiểm soát của con người. Hãy thiết lập ngay hôm nay để tối ưu hóa kênh truyền thông mạng xã hội của doanh nghiệp các sếp nhé!