---
title: "🧠 AI Blog Post Journalist (Perplexity + Claude) – Tự động tạo bài blog SEO"
description: "Workflow tự động nghiên cứu chủ đề AI qua Perplexity, viết bài blog bằng Claude và lưu kết quả vào Google Docs – giúp bạn có nội dung mới mỗi ngày mà không cần viết tay."
slug: "ai-blog-post-journalist-perplexity-claude"
tags: [n8n, automation, no-code, AI, Perplexity, Anthropic Claude, Google Docs]
keywords: [n8n workflow, tự động hóa, AI blog writer, Perplexity, Claude, Google Docs]
---

# 🚀 AI Blog Post Journalist – Tự động nghiên cứu & viết bài blog bằng AI

Các sếp làm content đều biết cảm giác “hết ý tưởng” khi phải liên tục tìm xu hướng AI mới, nghiên cứu và viết bài dài. Quá trình này tốn thời gian, dễ bị lỗi thô và khó duy trì tần suất đăng bài ổn định. Workflow **AI Blog Post Journalist** giải quyết triệt để vấn đề đó bằng cách kết hợp sức mạnh của **Perplexity** (nghiên cứu thực시간) và **Claude 4 Sonnet** (viết bài sáng tạo) – toàn bộ tự động, không cần viết một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm hàng giờ mỗi tuần**: Không cần manually search, outline và viết tay.
- **Nội dung luôn mới mẻ & SEO‑friendly**: Perplexity lấy tin tức mới nhất, Claude viết theo cấu trúc tiêu đề, mô tả meta, 3+ phần.
- **Lưu trữ tự động**: Bài viết cuối cùng được ghi trực tiếp vào Google Docs, sẵn sàng để duyệt, lên lịch hoặc xuất ra các nền tảng khác.
- **Tùy biến cao**: Dễ dàng thay đổi tần suất, prompt, hoặc thêm công cụ (Slack, Telegram…) mà không làm thay đổi luồng chính.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Perplexity API Key** – để tạo credential `perplexityApi` (dùng cho cả hai node Perplexity).
- **Anthropic API Key** – để tạo credential `anthropicApi` (dùng cho node `Anthropic Chat Model`).
- **Google Docs (OAuth2)** – để tạo credential `googleDocsOAuth2Api` và có quyền chỉnh sửa tài liệu đích.
- **ID của Google Docs** mà bạn muốn lưu bài viết (sẽ được nhập ở node Google Docs).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Sao chép toàn bộ JSON workflow từ trang n8n.io (link gốc) hoặc tải file JSON về.
2. Trong n8n Editor → nhấn **Import** → chọn **Upload file** hoặc dán JSON vào ô **Paste**.
3. Nhấn **Import** để workflow xuất hiện trong danh sách.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình cụ thể cho từng node sau:

| Node | Cấu hình bắt buộc |
|------|-------------------|
| **Schedule Trigger** | Chọn tần suất chạy (ví dụ: mỗi ngày 08:00, hoặc mỗi 12 giờ). Đảm bảo múi giờ đúng với vùng bạn làm việc. |
| **Perplexity - Blog Topic Research Node** | - Credential: chọn `perplexityApi` (đã tạo từ API Key).<br>- Model: `sonar-pro` (đã được preselect).<br>- Prompt (nếu muốn tùy chỉnh): ví dụ “Give me the top 5 AI news items from the last 24 hours suitable for a non‑technical audience”. |
| **Anthropic Chat Model** | - Credential: chọn `anthropicApi`.<br>- Model: `claude-sonnet-4-20250514` (label “Claude 4 Sonnet”).<br>- Temperature: để mặc định 0.7 hoặc điều chỉnh để控制 sáng tạo. |
| **AI Agent** | - **Tools**: thêm `Perplexity Search Tool` (node dưới) để agent có thể truy xuất thêm thông tin khi cần.<br>- **Memory**: kết nối với `Simple Memory` (node `memoryBufferWindow`) để agent ghi nhớ ngữ cảnh trong quá trình chạy.<br>- **System Prompt** (Prompt): dán vào trường “Instructions” của agent, ví dụ:<br>```\nBạn là một nhà báo AI chuyên viết blog cho người đọc không chuyên.\nNhiệm vụ: dựa trên chủ đề được cung cấp từ Perplexity, viết một bài blog đầy đủ bao gồm:\n1. Tiêu đề hấp dẫn (SEO‑friendly).\n2. Giới thiệu ngắn gọn (hook).\n3. 3+ phần chính, mỗi phần có tiêu đề rõ ràng.\n4. Phần “Key Takeaway” tóm tắt điểm mấu chốt.\n5. Meta description (≤160 ký tự) cho SEO.\nNgôn ngữ: tiếng Việt, tự nhiên, dễ hiểu.\n``` |
| **Simple Memory** | - Window Size: số lượng tin nhắn muốn giữ (ví dụ: 5). Để agent có thể tham khảo lại các bước ricerca trước đó. |
| **Perplexity Search Tool** | - Credential: chọn `perplexityApi`.<br>- Model: `sonar-pro`.<br>- Đây là công cụ mà AI Agent sẽ gọi khi cần tra cứu thêm thông tin trong quá trình viết. |
| **Google Docs** | - Credential: chọn `googleDocsOAuth2Api`.<br>- Operation: `Update` (đã preselect).<br>- Document ID: dán ID của file Google Docs bạn muốn ghi (có thể lấy từ URL: `https://docs.google.com/document/d/<ID>/edit`).<br>- Trong trường “Content”, map output từ node **AI Agent** (thường là `{{ $json["response"] }}` hoặc `{{ $aiAgent.output }}` tùy thuộc phiên bản n8n).<br>- Tùy chọn: bật “Append” nếu muốn nối nội dung vào cuối tài liệu thay vì ghi đè. |

#### 3. Kích hoạt ⚡️
- Nhấn **Workflow → Execute Workflow** để test run với dữ liệu mẫu (Perplexity sẽ trả về tin tức thực).
- Kiểm tra output ở mỗi node, đặc biệt là nội dung cuối cùng ở node **Google Docs** để đảm bảo định dạng đúng.
- Nếu tudo ổn, chuyển sang toggle **Active** ở góc trên bên phải để workflow chạy tự động theo lịch đã đặt.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo tự động**: Thêm node **Slack** hoặc **Telegram** sau Google Docs để gửi link bài viết mới tới kênh team mỗi khi workflow hoàn thành.
- **Lưu log**: Ghi lại mỗi lần chạy vào Google Sheets (node **Google Sheets**) để theo dõi chủ đề, thời gian và độ dài bài viết.
- **Đa dạng nội dung**: Sau khi có bài trong Google Docs, dùng node **HTTP Request** để đăng bài trực tiếp lên WordPress, Medium hoặc Ghost qua API.
- **Tối ưu prompt**: Thử nghiệm với các biến số như `tone` (professional, friendly) hoặc `audience` (beginner, decision‑maker) trong System Prompt của Agent để tạo ra nhiều phiên bản bài viết khác nhau cho các kênh khác nhau.
- **Batch processing**: Thay đổi Schedule Trigger thành **Cron** chạy mỗi 6 giờ và thêm một node **Set** để tạo danh sách chủ đề từ một file CSV, cho phép tạo nhiều bài trong một lần chạy.

### 📌 Kết luận
Workflow **AI Blog Post Journalist** mang lại giải pháp hoàn toàn tự động để nghiên cứu, viết và lưu trữ bài blog AI mà không cần viết code. Với sự kết hợp của Perplexity (nghiên cứu thực시간) và Claude 4 Sonnet (viết bài sáng tạo), các sếp có thể duy trì luồng nội dung ổn định, tiết kiệm thời gian và vẫn đảm bảo chất lượng SEO. Hãy import ngay, cấu hình credentials và để n8n làm việc thay bạn – thời gian của bạn sẽ dành cho chiến lược và sự sáng tạo, chứ không phải cho việc tìm kiếm và gõ phím tay. 🚀