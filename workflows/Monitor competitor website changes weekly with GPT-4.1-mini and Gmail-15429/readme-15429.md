---
title: "🚀 Tự động theo dõi thay đổi website đối thủ hàng tuần với OpenAI và Gmail"
description: "Hướng dẫn cài đặt workflow n8n tự động quét website đối thủ, phát hiện thay đổi, tóm tắt bằng OpenAI GPT và tạo bản thảo Gmail hàng tuần."
slug: "tu-dong-theo-doi-thay-doi-website-doi-thuu-n8n"
tags: [n8n, automation, market-research, ai-summarization, openai, gmail]
keywords: [n8n workflow, theo dõi đối thủ cạnh tranh, competitor monitoring, openai gpt n8n, tự động hóa gmail]
---

# 🚀 Tự động theo dõi thay đổi website đối thủ hàng tuần với OpenAI và Gmail

Việc thủ công truy cập vào website của các đối thủ cạnh tranh mỗi tuần để xem họ có thay đổi giá cả, tính năng hay ra mắt sản phẩm mới không thực sự tốn rất nhiều thời gian và dễ bỏ sót. Các sếp có đang gặp tình trạng này không? 

Hãy để workflow n8n này làm thay các sếp! Hệ thống sẽ tự động quét website đối thủ theo lịch trình, lọc nội dung, sử dụng AI (OpenAI GPT) để phân tích sự thay đổi và tự động tạo một bản thảo (Draft) trên Gmail với báo cáo cực kỳ chi tiết, sẵn sàng để gửi cho đội ngũ của bạn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian thủ công**: Không cần phải "soi" từng trang web của đối thủ hàng tuần nữa.
- **Phát hiện thay đổi chính xác**: Hệ thống tự động so sánh mã nguồn/nội dung trang web với bản lưu gần nhất (Snapshot) để tìm điểm khác biệt.
- **Báo cáo thông minh bằng AI**: Sử dụng OpenAI GPT để cô đọng thông tin thành báo cáo chiến lược rõ ràng (Executive summary, thay đổi cốt lõi, hành động đề xuất).
- **An toàn tuyệt đối**: Workflow chỉ dừng lại ở việc **tạo bản thảo Gmail (Draft)**, giúp các sếp kiểm tra lại thông tin trước khi chính thức bấm gửi.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động.
- Tài khoản **OpenAI API Key** (kèm theo kết nối OpenAi credential trong n8n).
- Tài khoản **Gmail** để cấu hình phân quyền OAuth2 gửi bản thảo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow này từ n8n.io (ID: 15429) và Import trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình chính xác các node sau:
- **Define Competitors (Code Node)**: Mở node này và điền danh sách các đối thủ cần theo dõi bao gồm: `name` (tên đối thủ), `url` (đường dẫn trang web), và `watch_for` (nội dung cần tập trung theo dõi như "thay đổi giá", "tính năng mới").
- **Build Digest Prompt (Code Node)**: Tìm và thay thế địa chỉ `replace-me@example.com` bằng email nhận báo cáo thực tế của các sếp.
- **OpenAI - Summarize Competitor Changes**: Chọn/kết nối credential **OpenAI API** của các sếp.
- **Gmail - Draft Digest**: Kết nối tài khoản **Gmail OAuth2** của các sếp và đảm bảo resource được chọn là `draft`.

#### 3. Kích hoạt ⚡️
- **Chạy thử lần đầu (Test run)**: Chạy workflow thủ công một lần đầu tiên để hệ thống lưu lại các bản Snapshot cơ sở (Baseline). Lưu ý: Lần chạy đầu tiên sẽ không tạo email vì chưa có dữ liệu để so sánh.
- **Bật Active workflow**: Sau khi test thành công, bật công tắc **Active** để lịch trình hàng tuần tự động hóa mọi thứ.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm kênh chat**: Thay vì chỉ nhận Gmail, các sếp có thể nối thêm node **Slack** hoặc **Telegram** để bắn thông báo ngay khi có bản tóm tắt chiến lược được tạo.
- **Lưu lịch sử vào Google Sheets**: Thêm node Google Sheets để lưu lại lịch sử biến động của đối thủ theo từng tuần nhằm phục vụ việc phân tích xu hướng dài hạn.
- **Tùy chỉnh lịch chạy**: Mở node **Weekly Schedule** để đổi lịch quét từ hàng tuần sang hàng ngày hoặc 2 tuần/lần tùy thuộc vào độ nhanh nhạy của thị trường ngách các sếp đang làm.

### 📌 Kết luận
Với workflow n8n này, việc theo dõi đối thủ cạnh tranh đã trở thành một quy trình tự động hóa hoàn toàn chuyên nghiệp. Hãy triển khai ngay hôm nay để luôn đi trước đối thủ một bước!