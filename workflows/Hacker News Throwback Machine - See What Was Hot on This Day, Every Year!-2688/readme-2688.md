---
title: "🚀 Hacker News Throwback Machine - Nhìn lại quá khứ công nghệ mỗi ngày"
description: "Khám phá những tin tức công nghệ hot nhất trên Hacker News vào đúng ngày này trong quá khứ qua từng năm, được tổng hợp và phân tích tự động bằng AI và gửi thẳng về Telegram."
slug: "hacker-news-throwback-machine-n8n-workflow"
tags: [n8n, automation, no-code, ai, telegram, hacker-news, gemini]
keywords: [n8n workflow, hacker news throwback, tự động hóa telegram, google gemini ai, scraper tin tức công nghệ]
---

# 🚀 Hacker News Throwback Machine - Nhìn lại quá khứ công nghệ mỗi ngày

Bạn có bao giờ tò mò muốn biết 5 năm, 10 năm trước, cộng đồng công nghệ thế giới đang bàn tán xôn xao về chủ đề gì trên Hacker News vào đúng ngày hôm nay không? Việc phải thủ công lội ngược dòng thời gian qua các trang lưu trữ như Wayback Machine để tìm kiếm từng năm thực sự rất mất thời gian và nhàm chán. 

Đừng lo, workflow **Hacker News Throwback Machine** do tác giả *ibrhdotme* xây dựng sẽ giải quyết triệt để vấn đề này. Hệ thống sẽ tự động truy vấn dữ liệu lịch sử của Hacker News qua các năm, dùng sức mạnh của AI (Google Gemini) để phân tích, tổng hợp và bắn bản tin hoài niệm này thẳng về Telegram của các sếp mỗi ngày! Hoàn toàn tự động 100% không cần tốn một giọt mồ hôi.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Du hành thời gian tự động:** Nhận bản tin tổng hợp các bài viết "hot hit" nhất của Hacker News vào cùng một ngày trong quá khứ (ví dụ: ngày 15/05 của các năm 2020, 2019, 2018...).
- **Phân tích thông minh bằng AI:** Sử dụng Google Gemini để tóm tắt các xu hướng công nghệ nổi bật thay vì chỉ liệt kê khô khan các đường link.
- **Cập nhật liền mạch qua Telegram:** Nhận thông tin trực tiếp trên điện thoại cá nhân hoặc nhóm chat Telegram vào khung giờ cố định mỗi ngày.
- **Tiết kiệm thời gian:** Thay vì mất hàng giờ lục lọi internet, mọi thứ đã có n8n lo trọn gói.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các nguyên liệu sau:
- **n8n Instance:** Đã cài đặt sẵn sàng (Self-hosted hoặc Cloud).
- **Google Gemini API Key:** Dùng cho node **Google Gemini Chat Model** để xử lý và phân tích nội dung.
- **Telegram Bot Token & Chat ID:** Tạo qua `@BotFather` để bot có quyền gửi tin nhắn về tài khoản hoặc group Telegram của các sếp.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow (hoặc tải file JSON từ nguồn gốc) và dán trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 13 nodes hoạt động nhịp nhàng từ việc tính toán ngày tháng, cào dữ liệu đến xử lý AI. Các sếp cần chú ý cấu hình các điểm sau:

- **Schedule Trigger:** Cấu hình lịch chạy định kỳ (ví dụ: chạy vào 8 giờ sáng mỗi ngày) để bot gửi bản tin khởi đầu ngày mới.
- **CreateYearsList & CleanUpYearList (Nodes Code & Set):** Xử lý logic để tự động sinh ra danh sách các năm cần "quay ngược thời gian" (ví dụ từ năm hiện tại lùi về trước 5-10 năm).
- **GetFrontPage (Node HTTP Request):** Gọi đến các dịch vụ lưu trữ trang chủ Hacker News theo ngày/tháng/năm tương ứng.
- **ExtractDetails (Node HTML):** Trích xuất tiêu đề và đường dẫn bài viết từ mã HTML trả về.
- **Google Gemini Chat Model & Basic LLM Chain:** 
  - Chọn credentials `googlePalmApi` đã kết nối với tài khoản Google AI Studio của các sếp.
  - Tinh chỉnh Prompt trong chuỗi LLM nếu muốn AI dịch sang tiếng Việt hoặc thay đổi phong cách viết bản tin (hóm hỉnh, trang trọng, v.v.).
- **Telegram (Node Telegram):** 
  - Chọn credentials `telegramApi` với Bot Token của các sếp.
  - Điền chính xác `Chat ID` nơi nhận tin nhắn (có thể là ID cá nhân hoặc group chat).

#### 3. Kích hoạt ⚡️
- Nhấn nút **Test Workflow** để chạy thử xem dữ liệu từ code sinh ra, gọi API và gửi về Telegram có mượt mà không.
- Nếu mọi thứ hiển thị ngon lành trên Telegram, các sếp bật công tắc **Active** ở góc trên bên phải để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng lưu trữ:** Thay vì chỉ gửi Telegram, các sếp có thể nối thêm node **Google Sheets** hoặc **Notion** để lưu lại toàn bộ các bài viết hoài niệm này thành một cơ sở dữ liệu tri thức cá nhân.
- **Đa kênh thông báo:** Kết hợp thêm node **Slack** hoặc **Discord** để gửi bản tin vào kênh chat chung của team kỹ thuật, tạo chủ đề trò chuyện thú vị mỗi giờ giải lao.
- **Tùy biến khoảng thời gian:** Chỉnh sửa lại logic trong code node để chỉ quét các năm có dấu mốc đặc biệt (ví dụ: cách đây tròn 10 năm).

### 📌 Kết luận
Hacker News Throwback Machine là một workflow cực kỳ thú vị, vừa giúp các sếp giải trí, vừa cập nhật được lịch sử tiến hóa của công nghệ thế giới qua góc nhìn AI. Hãy import ngay vào n8n và trải nghiệm cảm giác du hành thời gian ngay hôm nay thôi nào các sếp!