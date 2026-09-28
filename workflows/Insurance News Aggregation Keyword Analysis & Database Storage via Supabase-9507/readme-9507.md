---
title: "🚀 Tự Động Tổng Hợp Tin Tức Bảo Hiểm, Phân Tích Từ Khóa & Lưu Trữ Supabase với n8n"
description: "Hướng dẫn xây dựng hệ thống tự động cào tin tức bảo hiểm từ RSS/Web, phân tích từ khóa thông minh và lưu trữ cơ sở dữ liệu Supabase bằng n8n workflow."
slug: "tu-dong-tong-hop-tin-tuc-bao-hiem-supabase-n8n"
tags: [n8n, automation, no-code, supabase, rss, web-scraping]
keywords: [n8n workflow, tổng hợp tin tức tự động, phân tích từ khóa, supabase n8n, cào dữ liệu web, insurance news automation]
---

# 🚀 Tự Động Tổng Hợp Tin Tức Bảo Hiểm, Phân Tích Từ Khóa & Lưu Trữ Supabase

Các sếp trong ngành bảo hiểm hay marketing có nhận thấy việc phải thủ công theo dõi, tổng hợp tin tức, phân tích xu hướng từ khóa từ hàng tá trang báo tốn khủng khiếp bao nhiêu thời gian không? Mỗi ngày có hàng trăm bài viết ra lò, nếu làm bằng tay thì đội ngũ của các sếp chắc chắn sẽ kiệt sức.

Đừng lo, giải pháp ở đây rồi! Workflow n8n siêu việt này sẽ thay các sếp làm từ A-Z: tự động quét tin tức, lọc nội dung quan trọng, phân tích từ khóa và đẩy thẳng vào cơ sở dữ liệu Supabase một cách mượt mà mà không cần viết một dòng code phức tạp nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Định kỳ quét tin tức mỗi 6 giờ mà không cần sự can thiệp thủ công.
- **Lọc thông minh:** Chỉ giữ lại những bài viết thực sự liên quan và hữu ích nhờ bộ lọc điều kiện (IF) và phân tích chuyên sâu.
- **Lưu trữ khoa học:** Dữ liệu sạch, bao gồm nội dung chi tiết và từ khóa, được phân loại và lưu thẳng vào Supabase (Content Library & Knowledge Base).
- **Hoạt động bền bỉ:** Tích hợp cơ chế xử lý lỗi (Error Handler) giúp hệ thống không bị "chết giữa chừng" khi gặp lỗi đường truyền hoặc nguồn tin.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống n8n (Self-hosted hoặc n8n Cloud).
- Tài khoản Supabase (đã tạo sẵn bảng/database để lưu trữ bài viết và từ khóa).
- Các nguồn cấp dữ liệu (RSS Feeds) hoặc trang web tin tức ngành bảo hiểm mục tiêu.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy mã JSON của workflow từ nguồn cung cấp, sau đó vào giao diện n8n, chọn **Add workflow** -> **Import from JSON** và dán vào là xong.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy chuẩn không cần chỉnh, các sếp nhớ cấu hình kỹ các node sau:

- **Schedule Every 6 Hours (`scheduleTrigger`):** Tần suất mặc định là 6 tiếng quét một lần. Các sếp có thể đổi lại thời gian nếu muốn quét dày hơn hoặc thưa hơn.
- **Get News Sources (`function`) & Is RSS Feed? (`if`):** Nơi định nghĩa danh sách các nguồn tin (RSS hoặc trang web). Hãy cập nhật lại danh sách link báo/RSS bảo hiểm mà các sếp muốn theo dõi.
- **Fetch RSS Feed (`rssFeedRead`) & Fetch Google News RSS (`rssFeedRead`):** Đảm bảo các node này kết nối trơn tru với các nguồn RSS đã khai báo.
- **Scrape Web Page & Fetch Full Article (`httpRequest`):** Dùng để cào toàn bộ nội dung bài viết nếu nguồn không cung cấp RSS đầy đủ. Lưu ý cấu hình User-Agent để tránh bị các trang web chặn.
- **Rate Limit Wait (`wait`):** Node cực kỳ quan trọng giúp giãn cách thời gian giữa các request, tránh việc bị bên cung cấp tin tức chặn IP vì gọi quá nhiều lần (Rate Limit).
- **Extract Content & Keywords (`code`) & Is Relevant? (`if`):** Nơi xử lý logic trích xuất nội dung chính, phân tích từ khóa và đánh giá xem bài viết có đúng chủ đề (relevant) hay không.
- **Store in Content Library & Store in Knowledge Base (`httpRequest`):** Cấu hình API endpoint, Headers và Credentials của **Supabase** để đẩy dữ liệu bài viết và kho tri thức vào đúng các bảng tương ứng.
- **Error Handler (`function`):** Node bắt lỗi tổng hợp, giúp ghi nhận lại sự cố nếu có nguồn tin nào đó bị hỏng hoặc lỗi mạng.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (**Test workflow**) một vài bản ghi đầu tiên để kiểm tra dữ liệu đẩy vào Supabase đã đúng ý chưa.
- Sau khi mọi thứ chạy mượt mà, gạt công tắc **Active** ở góc trên cùng bên phải để hệ thống tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm một node Telegram hoặc Slack vào sau node `Store in Knowledge Base` để nhận thông báo tức thì mỗi khi có bài báo hot về ngành bảo hiểm được lưu trữ.
- **Kết hợp AI:** Có thể tích hợp thêm các node OpenAI/Anthropic LLM vào giữa quy trình để tóm tắt bài viết tự động (Summary) bằng tiếng Việt trước khi lưu vào Supabase.
- **Lưu log định kỳ:** Thiết lập gửi báo cáo tổng kết số lượng bài viết đã cào được qua Email vào cuối tuần.

### 📌 Kết luận
Với workflow n8n này, việc nghiên cứu thị trường, tổng hợp tin tức bảo hiểm và xây dựng kho tri thức (Knowledge Base) chưa bao giờ dễ dàng đến thế. Hãy "lên đồ" ngay hôm nay để tối ưu hóa năng suất cho đội ngũ của các sếp!