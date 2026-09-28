---
title: "🚀 Tự động trích xuất và giải mã Google News RSS thành link gốc chuẩn xác bằng n8n"
description: "Hướng dẫn xây dựng workflow n8n giúp đọc RSS Google News, bóc tách và giải mã các URL được mã hóa thành các link bài báo sạch, sẵn sàng sử dụng cho các ứng dụng AI và Content."
slug: "giai-ma-google-news-rss-url-clean-n8n"
tags: [n8n, automation, no-code, rss, google-news, web-scraping]
keywords: [n8n workflow, giải mã google news url, rss feed n8n, tự động hóa google news, trích xuất link bài báo]
---

# 🚀 Tự động trích xuất và giải mã Google News RSS thành link gốc chuẩn xác

Các sếp đang làm về mảng nội dung, nghiên cứu thị trường hoặc xây dựng hệ thống AI cập nhật tin tức chắc chắn đã từng "đau đầu" với Google News. Khi lấy link từ RSS Feed của Google News, các URL trả về đều bị mã hóa phức tạp (định dạng `https://news.google.com/rss/articles/...`) chứ không phải là link gốc của trang báo. Việc click thủ công hoặc viết code xử lý từng link cực kỳ mất thời gian và dễ lỗi.

Giải pháp ở đây là gì? Workflow n8n tự động hóa 100% giúp các sếp đọc RSS, trích xuất các khóa bảo mật, gọi API giải mã ngầm để thu về **link bài báo gốc (Clean Article Links)** một cách mượt mà và không cần một dòng code phức tạp nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Biến các URL Google News bị mã hóa thành link bài báo gốc chỉ trong vài giây.
- **Tiết kiệm thời gian:** Không còn phải copy/paste hay giải mã thủ công từng URL tin tức.
- **Dữ liệu sạch sẵn sàng sử dụng:** Dễ dàng tích hợp tiếp vào các hệ thống AI (như OpenAI, Claude để tóm tắt tin tức) hoặc lưu vào Google Sheets/Database.
- **Hoạt động linh hoạt:** Tùy chỉnh ngôn ngữ, khu vực và số lượng bản tin theo nhu cầu chiến dịch.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống **n8n** đang hoạt động (Cloud hoặc Self-hosted).
- Không cần tài khoản API trả phí nào vì workflow sử dụng trực tiếp các kỹ thuật reverse-engineering HTTP request thông minh.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tạo một workflow mới trong n8n Editor của các sếp, sau đó copy toàn bộ mã JSON của workflow này và paste trực tiếp vào giao diện (n8n sẽ tự động tạo toàn bộ 10 nodes cho các sếp).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này sử dụng kỹ thuật reverse-engineering để giải mã URL từ Google News, do đó các sếp cần lưu ý các điểm mấu chốt sau:
- **Node `Reading Google News RSS` (rssFeedRead):** 
  - Cấu hình nguồn RSS của Google News. 
  - *Lưu ý về ngôn ngữ/Khu vực:* Các sếp có thể thay đổi tham số chuẩn ISO639-1 (ví dụ: `hl=it`, `gl=IT`, `ceid=IT:it` cho tiếng Ý, hoặc đổi thành `hl=vi`, `gl=VN`, `ceid=VN:vi` cho thị trường Việt Nam).
- **Node `Limit` (limit):**
  - **CỰC KỲ QUAN TRỌNG:** Tác giả khuyến nghị nên giới hạn số lượng kết quả (ví dụ tối đa 3 bài viết mỗi lần chạy) vì mỗi bài viết đòi hỏi nhiều HTTP request ngầm để bóc tách khóa và giải mã. Đặt số lượng quá lớn trong một lần chạy có thể khiến IP của các sếp bị Google tạm khóa (rate limit).
- **Node `Get encoded news URL` & `Call decoding URL` (httpRequest):**
  - Các node này thực hiện việc tải nội dung HTML, trích xuất các biến giải mã (`signature`, `timestamp`, `base64string`) thông qua node `Extract decoding keys` (html) và gửi request đến endpoint giải mã của Google. Các sếp giữ nguyên cấu hình mặc định vì đã được tác giả tối ưu sẵn.
- **Node `Clean output` (set):**
  - Dùng để làm sạch kết quả cuối cùng, loại bỏ các ký tự rác do Google chèn thêm vào đầu URL, trả về link bài báo chuẩn xác 100%.

#### 3. Kích hoạt ⚡️
- Nhấn **‘Test workflow’** bằng node `When clicking ‘Test workflow’` để kiểm tra kết quả đầu ra ở node `Aggregate results in a single object`.
- Sau khi kiểm tra thấy các link bài báo trả về đã sạch đẹp, hãy bật nút **Active** để workflow sẵn sàng hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp AI tóm tắt tin tức:** Nối tiếp node cuối cùng vào node OpenAI hoặc Claude để tự động tóm tắt nội dung các bài báo vừa giải mã.
- **Lưu trữ tự động:** Đẩy các clean URL này vào Google Sheets hoặc Notion để tạo một kho lưu trữ thông tin/nghiên cứu đối thủ.
- **Gửi thông báo:** Tích hợp thêm node Telegram hoặc Slack để bắn tin tức nóng hổi về máy cá nhân ngay khi có bài viết mới.
- **Lưu ý vận hành:** Không nên đặt lịch chạy (Cron trigger) quá dày đặc (ví dụ: chỉ nên chạy 2-4 tiếng/lần) để tránh việc Google phát hiện và chặn IP.

### 📌 Kết luận
Workflow "Extract And Decode Google News RSS URLs" là một cỗ máy nhỏ gọn nhưng cực kỳ mạnh mẽ giúp các sếp giải quyết triệt để bài toán "link rác" từ Google News. Hãy áp dụng ngay vào hệ thống n8n của các sếp để tối ưu hóa quy trình thu thập dữ liệu tin tức mỗi ngày!