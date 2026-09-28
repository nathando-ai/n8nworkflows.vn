---
title: "🚀 Tự động tạo bài viết Cơ sở Tri thức với GPT & Perplexity AI cho Contentful CMS"
description: "Hướng dẫn xây dựng hệ thống tự động hóa sử dụng n8n, OpenAI GPT và Perplexity AI để nghiên cứu, tổng hợp và xuất bản bài viết Knowledge Base trực tiếp lên Contentful CMS."
slug: "tao-bai-viet-knowledge-base-gpt-perplexity-contentful"
tags: [n8n, automation, no-code, openai, perplexity, contentful, ai-content]
keywords: [n8n workflow, tạo bài viết tự động, perplexity ai, gpt chat, contentful cms, knowledge base automation]
---

# 🚀 Tự động tạo bài viết Cơ sở Tri thức với GPT & Perplexity AI cho Contentful CMS

Việc xây dựng một hệ thống Cơ sở Tri thức (Knowledge Base) chất lượng cao đòi hỏi quá trình nghiên cứu sâu rộng, tổng hợp thông tin chính xác từ internet và biên tập thành bài viết mạch lạc. Nếu làm thủ công, các sếp sẽ mất hàng giờ cho mỗi bài viết. 

Giải pháp? Workflow n8n này sẽ tự động hóa 100% quy trình từ khâu nghiên cứu thông tin thời gian thực bằng **Perplexity AI**, viết nội dung chuyên sâu bằng **OpenAI GPT**, cho đến việc đẩy bài viết hoàn thiện lên **Contentful CMS** mà không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và xử lý các tác vụ AI nặng mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Giảm thời gian nghiên cứu và viết bài từ vài tiếng xuống chỉ còn vài phút.
- **Nội dung luôn cập nhật:** Tận dụng khả năng tìm kiếm web thời gian thực của Perplexity AI để cung cấp thông tin chính xác, mới nhất.
- **Tự động hóa xuất bản:** Bài viết sau khi tạo sẽ tự động được định dạng và đẩy thẳng lên Contentful CMS, sẵn sàng để xuất bản.
- **Hoạt động không nghỉ:** Xử lý hàng loạt chủ đề hoặc tự động hóa theo lịch trình, giúp scale hệ thống content cực nhanh.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **n8n Instance** (Cloud hoặc Self-hosted phiên bản mới hỗ trợ Langchain).
- **OpenAI API Key** (Dùng cho GPT models tạo nội dung).
- **Perplexity AI API Key** (Dùng để nghiên cứu và tổng hợp thông tin web).
- **Contentful CMS Account** (Space ID và Content Management API Access Token).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ nguồn cung cấp.
- Trong giao diện n8n, chọn **Workflows** -> **Add workflow** -> **Import from File** (hoặc copy toàn bộ mã JSON và dán trực tiếp vào n8n Editor).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Khi import xong, các sếp cần cấu hình lại các kết nối cốt lõi sau để workflow nhận diện đúng tài khoản của doanh nghiệp:
- **AI Agent & Langchain Nodes (`@n8n/n8n-nodes-langchain.agent`, `lmChatOpenAi`):** Cần thiết lập credential của OpenAI và cấu hình System Prompt để định hình phong cách viết bài Knowledge Base chuẩn SEO và thân thiện với người đọc.
- **HTTP Request / Tool Nodes (Perplexity AI):** Điền API Key của Perplexity để các node thực hiện truy vấn tìm kiếm dữ liệu đầu vào.
- **Contentful Nodes / HTTP Request (Contentful CMS):** Cấu hình Space ID, Environment và Contentful Management Token để n8n có thể tạo Draft hoặc Publish bài viết mới trực tiếp vào kho lưu trữ của Contentful.
- **Các node phụ trợ (`Code`, `Set`, `If`, `Merge`):** Kiểm tra lại các biến đầu ra (JSON payload) để đảm bảo dữ liệu từ AI được bóc tách và map chính xác vào các trường tiêu đề (`title`), nội dung (`body`), và thẻ tag (`tags`) trên Contentful.

#### 3. Kích hoạt ⚡️
- Nhấp vào nút **Execute Workflow** để chạy thử với một chủ đề (topic) mẫu.
- Kiểm tra kết quả trả về trên Contentful CMS xem bài viết đã hiển thị đúng định dạng chưa.
- Sau khi test thành công, gạt công tắc sang chế độ **Active** để hệ thống tự động vận hành.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack/Telegram:** Thêm node thông báo về kênh chat nội bộ mỗi khi workflow tạo thành công một bài viết mới trên Contentful.
- **Mở rộng nguồn từ Google Sheets:** Thay vì nhập thủ công từng chủ đề, hãy cấu hình n8n đọc danh sách từ một file Google Sheets chứa danh sách các từ khóa/chủ đề cần viết.
- **Quy trình duyệt bài (Human-in-the-loop):** Thay vì publish trực tiếp, hãy cấu hình workflow lưu bài viết ở trạng thái *Draft* trên Contentful và gửi link bản nháp kèm nút duyệt qua Telegram cho quản lý.

### 📌 Kết luận
Việc tự động hóa quy trình sản xuất nội dung Knowledge Base với sự kết hợp giữa GPT và Perplexity AI không chỉ giúp tiết kiệm nguồn lực mà còn nâng tầm chất lượng tài liệu hỗ trợ khách hàng. Hãy áp dụng ngay vào hệ thống của các sếp để tối ưu hóa vận hành ngay hôm nay!