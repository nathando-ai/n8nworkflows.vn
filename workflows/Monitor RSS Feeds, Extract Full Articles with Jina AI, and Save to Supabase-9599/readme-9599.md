---
title: "🚀 Tự Động Theo Dõi RSS Feeds, Trích Xuất Nội Dung Đầy Đủ Bằng Jina AI & Lưu Vào Supabase"
description: "Xây dựng hệ thống tự động cào bài viết từ các trang blog/RSS feed yêu thích, trích xuất toàn bộ nội dung sạch sẽ và lưu trữ gọn gàng vào Supabase với n8n."
slug: "tu-dong-theo-doi-rss-feeds-trich-xuat-noi-dung-jina-ai-supabase"
tags: [n8n, automation, no-code, rss, jina-ai, supabase]
keywords: [n8n workflow, tự động hóa rss, trích xuất bài viết jina ai, lưu supabase n8n, automation blog tracking]
---

# 🚀 Tự Động Theo Dõi RSS Feeds, Trích Xuất Nội Dung Đầy Đủ Bằng Jina AI & Lưu Vào Supabase

Các sếp có đang tốn hàng giờ mỗi tuần để vào các trang blog yêu thích, đọc tin tức mới, copy nội dung và lưu lại thủ công không? Quá mất thời gian đúng không nào! 

Bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n cực kỳ mạnh mẽ giúp tự động hóa 100% quy trình: theo dõi danh sách RSS feed, lọc bài viết mới, tự động trích xuất toàn bộ nội dung bài viết (thay vì chỉ lấy đoạn tóm tắt ngắn ngủi từ RSS) và lưu trữ trực tiếp vào cơ sở dữ liệu Supabase mà không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hoàn toàn:** Hệ thống tự động chạy theo lịch trình (Schedule Trigger) mà không cần can thiệp thủ công.
- **Nội dung trọn vẹn:** Sử dụng Jina AI để cào trọn vẹn toàn bộ bài viết từ tiêu đề đến chân trang, vượt qua giới hạn chỉ lấy snippet của RSS feed.
- **Lọc thông minh:** Tự động loại bỏ các bài viết cũ (mặc định quá 60 ngày) để chỉ lưu trữ nội dung mới nhất.
- **Lưu trữ chuyên nghiệp:** Toàn bộ dữ liệu bài viết được gom gọn và lưu thẳng vào Supabase Database, sẵn sàng cho việc xây dựng AI Knowledge Base hoặc Social Media Automation.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **Supabase Account:** Một dự án Supabase đã tạo sẵn bảng (Table) để lưu trữ thông tin blog.
- **Jina AI:** Không cần API key phức tạp, dịch vụ trích xuất nội dung hoàn toàn miễn phí tích hợp qua HTTP Request.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy mã JSON của workflow từ nguồn cung cấp và paste trực tiếp vào màn hình làm việc của n8n Editor, hoặc import file JSON tải về từ trang chủ n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 20 nodes với logic xử lý thông minh. Các sếp hãy chú ý cấu hình kỹ các node sau:

- **Node `blogs to track` (Set):** Đây là nơi các sếp khai báo danh sách các trang blog muốn theo dõi. Mẫu có sẵn các đường dẫn RSS của n8n và Zapier. *Mẹo:* Hãy dùng Perplexity hoặc ChatGPT để tìm URL RSS chính xác nhất của trang web các sếp muốn theo dõi (tránh lỗi 403 do sai đường dẫn).
- **Node `max_content_age_days` (Set):** Mặc định cài đặt là `60` ngày. Node này quyết định chỉ lấy các bài viết được đăng trong vòng 60 ngày gần nhất. Các sếp có thể thay đổi con số này tùy theo nhu cầu.
- **Node `Extract the full blog` (HTTP Request):** Node này gọi API của Jina AI để cào toàn bộ nội dung bài viết từ URL mà không cần setup phức tạp.
- **Node `Save Blog Data to Database` (Supabase):** Các sếp cần kết nối tài khoản Supabase của mình (`supabaseApi`), chọn đúng Table và ánh xạ (map) các trường dữ liệu (Title, Content, Published Date, URL...) cho khớp với cấu trúc bảng trong database.

#### 3. Kích hoạt ⚡️
- Bấm nút **Test workflow** để chạy thử nghiệm xem dữ liệu từ RSS có được cào về, lọc và đẩy vào Supabase thành công hay không.
- Sau khi test ngon lành, hãy bật nút **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Thay đổi kho lưu trữ:** Nếu không dùng Supabase, các sếp có thể thay node Supabase bằng node **Google Sheets**, **Airtable**, hoặc node **n8n Data Table** mớingay trong n8n.
- **Tích hợp AI tóm tắt:** Nối tiếp sau bước trích xuất nội dung, các sếp có thể thêm một node LLM (OpenAI / Anthropic) để tự động tóm tắt bài viết hoặc sinh ra các bài đăng social media ngắn gọn.
- **Nhận thông báo:** Thêm node Telegram hoặc Slack ở cuối workflow để mỗi khi có bài viết mới được lưu vào database, bot sẽ bắn tin nhắn thông báo ngay lập tức cho các sếp.

### 📌 Kết luận
Workflow này là một cỗ máy tự động hóa hoàn hảo cho những ai làm Content Marketing, Research, hoặc xây dựng các hệ thống AI/RAG cá nhân. Hãy triển khai ngay để tiết kiệm hàng chục giờ làm việc thủ công mỗi tuần các sếp nhé!