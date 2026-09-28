---
title: "🚀 Tìm kiếm khoảng trống nội dung website đối thủ với InfraNodus GraphRAG và n8n"
description: "Tự động hóa quy trình phân tích SEO đối thủ cạnh tranh bằng InfraNodus GraphRAG, OpenAI và Google Sheets. Khám phá khoảng trống nội dung để thống trị từ khóa."
slug: "tim-kiem-khoang-trong-noi-dung-website-doi-thu-voi-infranodus-graphrag"
tags: [n8n, automation, seo, graphrag, infranodus, ai, marketing]
keywords: [n8n workflow, infranodus, graphrag seo, content gap analysis, tự động hóa seo, phân tích đối thủ cạnh tranh]
---

# 🚀 Tìm kiếm khoảng trống nội dung website đối thủ với InfraNodus GraphRAG và n8n

Các sếp làm SEO chắc chắn đều hiểu cảm giác đau đầu khi phải thủ công lướt qua hàng loạt website đối thủ, đọc từng bài viết để mò mẫm xem họ đang thiếu sót những chủ đề gì, từ đó lên kế hoạch viết bài vượt mặt họ. Việc này vừa tốn hàng tá thời gian, vừa dễ bỏ sót các ngóc ngách từ khóa tiềm năng.

Đừng lo nữa các sếp! Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ mạnh mẽ, kết hợp giữa **InfraNodus GraphRAG**, **OpenAI**, và **Google Sheets**. Workflow này sẽ tự động crawl dữ liệu website đối thủ, phân tích mạng lưới từ khóa, tìm ra "content gap" (khoảng trống nội dung) và tổng hợp thành báo cáo chi tiết gửi thẳng vào Google Docs cho các sếp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100% quy trình nghiên cứu đối thủ:** Từ việc crawl nội dung website đến phân tích chiều sâu.
- **Phát hiện khoảng trống nội dung (Content Gaps):** Nhờ sức mạnh của đồ thị tri thức InfraNodus GraphRAG, tìm ra những chủ đề mà đối thủ chưa khai thác.
- **Tiết kiệm 90% thời gian:** Thay vì mất vài ngày soi đối thủ, hệ thống xử lý hàng loạt theo batch và trả về báo cáo gọn gàng.
- **Đồng bộ hóa dữ liệu thông minh:** Tự động cập nhật kết quả vào Google Sheets để tái sử dụng và lưu trữ báo cáo chiến lược vào Google Docs.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động mượt mà, các sếp cần chuẩn bị sẵn:
- **Tài khoản n8n** (Self-hosted hoặc Cloud).
- **Tài khoản InfraNodus** kèm API Key (để sử dụng các node InfraNodus GraphRAG, AI Advice, Question Generator).
- **OpenAI API Key** (cho node OpenAI).
- **Google Account** (để cấu hình Google Sheets template và Google Docs lưu báo cáo).
- **Perplexity API / HTTP Bearer Auth** (nếu dùng tính năng Perplexity Research).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này từ n8n template (hoặc file JSON được cung cấp), sau đó dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 23 nodes được chia thành các giai đoạn Data Enrichment và Insight Generation. Các sếp lưu ý cấu hình kỹ các node sau:

- **Read a Google Sheets File / Get the content from Google Sheets / Update Google Sheets with Content Insights / Google Sheets:** 
  - Sử dụng template mẫu tại [Google Sheets Template](https://docs.google.com/spreadsheets/d/14qR7Gi8SRCd3eM6_V3ftRcDODkEFAILEqogjUvk7hKs/edit?usp=sharing).
  - Kết nối tài khoản Google Sheets OAuth2 và trỏ chính xác đến file Google Sheets của các sếp (chứa danh sách tên công ty và URL cần phân tích).
- **HTTP Request / InfraNodus GraphRAG Content Enhancer / InfraNodus AI Advice / InfraNodus Question Generator:**
  - Nhập thông tin xác thực `httpBearerAuth` với API key lấy từ tài khoản InfraNodus của các sếp.
- **OpenAI:**
  - Cấu hình thông tin xác thực `openAiApi` để các node AI hoạt động ổn định.
- **Google Docs:**
  - Trỏ đến file Google Docs đích để lưu trữ toàn bộ báo cáo tổng hợp (Insight Report) được tạo ra từ workflow.
- **Split In Batches / Wait to avoid API overload:**
  - Giữ nguyên cấu hình chia batch (mỗi lần 10 URLs) và thời gian chờ (Wait) để tránh tình trạng quá tải API (Rate Limit) từ phía đối tác.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (`Test Workflow` hoặc dùng `On form submission` / `When clicking "Execute Workflow"`) với một vài URL mẫu để kiểm tra dữ liệu trả về.
- Sau khi kiểm tra mọi thứ trơn tru, hãy bật công tắc **Active** để workflow sẵn sàng hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh thông báo:** Nối thêm node Telegram hoặc Slack ở cuối workflow để nhận ngay thông báo khi báo cáo phân tích đối thủ đã được lưu thành công vào Google Docs.
- **Tự động viết bài:** Lấy kết quả "Content Gaps" từ Google Sheets truyền tiếp vào một AI Agent workflow khác để tự động sinh ra dàn ý (outline) hoặc bài viết chuẩn SEO.
- **Lên lịch chạy định kỳ (Cron):** Thay vì kích hoạt bằng tay hay form, các sếp có thể đổi trigger thành `Schedule Trigger` để hệ thống tự quét đối thủ mỗi tuần/mỗi tháng một lần.

### 📌 Kết luận
Việc phân tích đối thủ cạnh tranh chưa bao giờ dễ dàng và khoa học đến thế khi kết hợp sức mạnh của n8n và InfraNodus GraphRAG. Hãy "lên đồ" ngay hôm nay để tối ưu hóa chiến lược SEO và chiếm lĩnh mọi thứ hạng từ khóa các sếp nhé!