---
title: "🚀 Tự động hóa sáng tạo nội dung Blog toàn diện với Gemini AI, Supabase và Nano-Banana trong n8n"
description: "Xây dựng hệ thống tự động hóa viết blog từ A-Z sử dụng AI đa phương thức (Gemini, Groq, Perplexity), lưu trữ Supabase và thiết kế hình ảnh tự động. Tiết kiệm 100% thời gian."
slug: "tu-dong-hoa-viet-blog-gemini-supabase-n8n"
tags: [n8n, automation, gemini-ai, supabase, content-creation, ai-agent]
keywords: [n8n workflow, viết blog tự động, gemini ai n8n, supabase automation, ai content creator]
---

# 🚀 Tự động hóa sáng tạo nội dung Blog toàn diện với Gemini AI, Supabase và Nano-Banana

Viết blog chất lượng cao đòi hỏi rất nhiều công sức: từ việc nghiên cứu chủ đề, tổng hợp thông tin từ RSS feeds, viết bài chuẩn SEO, tìm kiếm hoặc tạo hình ảnh minh họa cho đến khâu lưu trữ và xuất bản. Việc làm thủ công này ngốn rất nhiều thời gian của các content creator và doanh nghiệp.

Được thiết kế bởi chuyên gia dữ liệu và AI **Muhammad Asadullah**, workflow n8n đỉnh cao này sẽ giúp các sếp tự động hóa **100% quy trình sản xuất bài viết blog** bằng sức mạnh của các mô hình AI tiên tiến (Gemini, Groq, Perplexity), kết hợp cùng cơ sở dữ liệu Supabase và công cụ tạo ảnh chuyên nghiệp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Từ khâu lấy ý tưởng qua RSS/Google Search, viết nội dung đến tạo ảnh minh họa mà không cần can thiệp thủ công.
- **Nội dung đa nguồn thông minh:** Tích hợp AI Agent, Perplexity, và Google Search Tool để tổng hợp thông tin sâu sắc, chính xác.
- **Hình ảnh độc quyền:** Tự động tạo ảnh minh họa chất lượng cao thông qua Gemini/Nano-Banana, xử lý định dạng và lưu trữ an toàn.
- **Lưu trữ khoa học:** Tự động lưu toàn bộ bài viết, metadata và hình ảnh vào cơ sở dữ liệu Supabase một cách có hệ thống.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API Keys sau:
- **n8n Instance** (phiên bản Cloud hoặc Self-hosted phiên bản mới hỗ trợ LangChain/AI nodes).
- **Google Gemini API Key** (cho các node Gemini Chat Model & Image Generation).
- **Groq API Key** (cho Groq Chat Model tốc độ cao).
- **Perplexity API Key** (cho công cụ tìm kiếm và nghiên cứu thông tin).
- **Supabase Account & Database** (để lưu trữ dữ liệu blog và hình ảnh).
- Các API/Credential liên quan đến dịch vụ lưu trữ ảnh hoặc HTTP Request (Nano-banana, v.v.).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này hoặc copy toàn bộ mã JSON từ [n8n Template #9079](https://n8n.io/workflows/9079).
- Trong giao diện n8n Editor, chọn **Add workflow** -> Nhấn tổ hợp `Ctrl + V` (hoặc `Cmd + V`) để dán toàn bộ workflow vào màn hình làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Vì workflow này có quy mô lớn (42 nodes) kết hợp giữa AI Agents và Database, các sếp cần chú ý cấu hình kỹ các phần sau:
- **Schedule Trigger:** Cài đặt lịch chạy tự động (ví dụ: chạy mỗi ngày 1 bài hoặc hàng tuần tùy ý).
- **Credentials cho LLM (Groq Chat Model, Google Gemini Chat Model):** Kết nối đúng tài khoản API của Groq và Google Gemini cho các AI Agent.
- **Supabase Nodes (`Create a row`, `Get many rows`):** Kết nối tài khoản Supabase của các sếp, trỏ tới đúng bảng (Table) đã chuẩn bị sẵn các trường (columns) nhận dữ liệu tiêu đề, nội dung HTML, và URL hình ảnh.
- **Tools Nodes (`Google search`, `URL Scraper`, `Message a model in Perplexity`):** Đảm bảo các API Key tìm kiếm và trích xuất dữ liệu đã được cấu hình chính xác để AI Agent có nguyên liệu viết bài.
- **Image & Storage Nodes (`Generate an image`, `Upload object`, `Generate presigned URL`, `nano banana`):** Kiểm tra lại các endpoint HTTP Request và biến môi trường để quá trình tạo ảnh, đổi định dạng (Edit Image), upload và lấy link hiển thị diễn ra mượt mà.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** chạy thử thủ công (Test run) với một vài từ khóa mẫu hoặc nguồn RSS đầu vào để kiểm tra log hoạt động của các AI Agent và Supabase.
- Nếu dữ liệu đổ về Supabase thành công và bài viết kèm hình ảnh hoàn thiện, hãy chuyển công tắc sang **Active** để hệ thống tự động vận hành 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo qua Telegram/Slack:** Thêm một node Telegram hoặc Slack vào cuối chuỗi để nhận thông báo ngay khi hệ thống tạo xong một bài blog mới.
- **Tự động đăng lên WordPress/Webflow:** Mở rộng workflow bằng cách kết nối thêm API của WordPress hoặc Webflow để tự động publish bài viết lên website công ty.
- **Kiểm duyệt con người (Human-in-the-loop):** Thêm node `Wait` và gửi email/tin nhắn kèm bản nháp cho biên tập viên duyệt trước khi lưu chính thức vào Supabase.

### 📌 Kết luận
Workflow End-to-End Blog Creation Automation này là một "vũ khí tối thượng" giúp tối ưu hóa đội ngũ Content Marketing, biến việc sản xuất nội dung quy mô lớn trở nên dễ dàng và chuyên nghiệp hơn bao giờ hết. Hãy cài đặt ngay hôm nay để giải phóng sức lao động và bứt phá lượng traffic cho website của các sếp!