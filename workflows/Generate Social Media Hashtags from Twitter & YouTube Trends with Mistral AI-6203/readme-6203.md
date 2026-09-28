---
title: "🚀 Tự Động Tạo Hashtag Xu Hướng Mạng Xã Hội Từ Twitter & YouTube Với Mistral AI"
description: "Hướng dẫn xây dựng workflow n8n tự động cào xu hướng từ Twitter, YouTube kết hợp Mistral AI để sinh hashtag triệu view và lưu tự động vào Google Sheets."
slug: "tu-dong-tao-hashtag-tu-twitter-youtube-mistral-ai"
tags: [n8n, automation, mistral-ai, content-creation, google-sheets, social-media]
keywords: [n8n workflow, tạo hashtag tự động, xu hướng twitter youtube, mistral ai, cào dữ liệu xu hướng, automation content]
---

# 🚀 Tự Động Tạo Hashtag Xu Hướng Mạng Xã Hội Từ Twitter & YouTube Với Mistral AI

Việc bắt trend thủ công hàng ngày để tìm ra các hashtag triệu view cho nội dung TikTok, Facebook hay Instagram cực kỳ tốn thời gian. Các sếp có đang chật vật lướt hàng giờ trên mạng xã hội chỉ để tìm xem hôm nay chủ đề nào đang hot?

Giải pháp ở đây là để **n8n** tự động hóa toàn bộ quy trình: Tự động cào dữ liệu xu hướng mới nhất từ Twitter và YouTube, phân tích bằng trí tuệ nhân tạo **Mistral AI**, và xuất ra danh sách hashtag chuẩn SEO được lưu thẳng vào **Google Sheets**. Không cần viết code, chạy tự động 100%!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian:** Không còn phải thủ công tổng hợp trend từ nhiều nền tảng.
- **Bắt trend thần tốc:** Tự động hóa lịch trình hàng ngày (`daily trigger`), giúp nội dung luôn đón đầu xu hướng.
- **Cá nhân hóa bằng AI:** Sử dụng mô hình `Mistral Cloud Chat Model1` thông minh để lọc và đề xuất hashtag chính xác nhất theo chủ đề định sẵn.
- **Lưu trữ khoa học:** Mọi dữ liệu trả về đều được tự động đồng bộ gọn gàng vào `Google Sheets2`.
:::

### 🔍 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Mistral AI API Key** để kết nối với `Mistral Cloud Chat Model1`.
- **Tài khoản Google** để cấu hình `Google Sheets2`.
- **Crawlee Node** (Cộng đồng) hỗ trợ cào dữ liệu web.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này từ n8n.io (hoặc copy nội dung JSON), sau đó dán trực tiếp vào n8n Editor của các sếp qua tính năng **Import from JSON**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống mượt mà vận hành, các sếp cần cấu hình chính xác các node trọng điểm sau:

- **`daily trigger`**: Node kích hoạt lịch chạy tự động theo ngày/giờ mong muốn. Các sếp có thể đổi tần suất nếu muốn quét trend thường xuyên hơn (ví dụ: vài tiếng/lần).
- **`extract twitter trends`** & **`extract YouTube trends`**: Sử dụng `crawleeNode` để cào dữ liệu từ trang tổng hợp xu hướng `https://trends24.in/`. Đảm bảo kết nối mạng của VPS ổn định để node này thực hiện việc cào mượt mà.
- **`filter twitter trends`** & **`filter YouTube trends`**: Các node `html` giúp bóc tách và lọc lấy nội dung thô chứa hashtag/chủ đề từ kết quả cào về.
- **`get only top 100 trends`**: Node `code` JavaScript tinh chỉnh dữ liệu, giới hạn danh sách gọn gàng ở top 100 xu hướng nổi bật nhất.
- **`Merge`**: Gom nhóm dữ liệu xu hướng từ cả hai nền tảng Twitter và YouTube lại với nhau trước khi đẩy vào AI.
- **`Loop Over Items2`** (`splitInBatches`): Xử lý dữ liệu tuần tự từng đợt tránh bị quá tải request.
- **`Mistral Cloud Chat Model1`** & **`hashtag generator`** (`agent`): Cấu hình Credentials của Mistral AI, lựa chọn model `mistral-small-latest` để AI tiến hành phân tích xu hướng và sinh hashtag.
- **`Structured Output Parser1`**: Đảm bảo AI trả về kết quả chuẩn định dạng JSON, giúp các bước tiếp theo dễ dàng đọc hiểu.
- **`Google Sheets2`**: Kết nối tài khoản Google Sheets của các sếp, chọn đúng file Sheet và bảng tính (Sheet Name) để lưu lại danh sách hashtag tự động sinh ra.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** chạy thử thủ công để kiểm tra dữ liệu trả về ở từng node.
- Khi mọi thứ xanh mướt (success), các sếp bật nút **Active** góc trên cùng bên phải để workflow tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node Telegram hoặc Slack ngay sau `Google Sheets2` để mỗi khi AI tạo xong bộ hashtag, hệ thống sẽ bắn tin nhắn trực tiếp về máy cho các sếp duyệt ngay.
- **Mở rộng nguồn trend:** Thêm các nguồn cào dữ liệu khác như TikTok Trending hoặc Google Trends để bộ hashtag đa chiều và phong phú hơn.
- **Lưu log lỗi:** Thiết lập Error Trigger để nhận cảnh báo qua email nếu quá trình cào dữ liệu web gặp sự cố (ví dụ trang web thay đổi cấu trúc HTML).

### 📌 Kết luận
Việc bắt trend chưa bao giờ dễ dàng đến thế khi có sự trợ giúp của tự động hóa n8n và AI. Hãy cài đặt ngay workflow này để tối ưu hóa hiệu suất sáng tạo nội dung của các sếp ngay hôm nay!