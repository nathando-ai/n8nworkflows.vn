---
title: "🚀 Xây dựng hệ thống Intelligent Web Query và Semantic Re-Ranking với Brave Search và Google Gemini trên n8n"
description: "Tự động hóa quy trình tìm kiếm web thông minh kết hợp AI Semantic Re-Ranking sử dụng Brave API, Google Gemini, OpenAI và Anthropic để phân tích dữ liệu chuyên sâu."
slug: "intelligent-web-query-semantic-reranking-n8n"
tags: [n8n, automation, ai, google-gemini, brave-search, semantic-search]
keywords: [n8n workflow, intelligent web query, semantic re-ranking, brave search api, google gemini n8n, ai automation]
keywords: [n8n workflow, tự động hóa, tìm kiếm web thông minh, phân tích dữ liệu ai, brave api]
---

# 🚀 Tự động hóa Tìm kiếm Web thông minh & Sắp xếp lại ngữ nghĩa (Semantic Re-Ranking) với n8n

Các sếp có bao giờ cảm thấy mệt mỏi khi phải thực hiện các truy vấn tìm kiếm thủ công trên web, sau đó lọc hàng chục kết quả rác để tìm ra thông tin thực sự hữu ích cho báo cáo thị trường hay nghiên cứu sản phẩm? Việc tổng hợp dữ liệu rời rạc vừa tốn thời gian, vừa dễ bỏ sót các insights quan trọng.

Được thiết kế bởi **Mind-Front** (dự án tiên phong cung cấp báo cáo thị trường dựa trên dữ liệu), workflow này là một giải pháp tự động hóa 100% không cần code (No-Code). Hệ thống kết hợp sức mạnh của **Brave Web Search API** và các mô hình AI hàng đầu như **Google Gemini, OpenAI GPT, và Anthropic Claude** để tự động tạo truy vấn thông minh, truy vấn dữ liệu web và thực hiện chấm điểm, sắp xếp lại kết quả (Semantic Re-Ranking) dựa trên ngữ nghĩa.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Nhận câu hỏi nghiên cứu qua Webhook, tự sinh query, search web và trả về kết quả đã được tinh chỉnh qua API.
- **Độ chính xác cao nhờ AI Re-Ranking:** Sử dụng LLM để phân tích và sắp xếp lại các kết quả tìm kiếm, loại bỏ thông tin nhiễu, chỉ giữ lại tài liệu có giá trị ngữ nghĩa cao nhất.
- **Linh hoạt đa mô hình (Multi-LLM):** Tích hợp sẵn Google Gemini, OpenAI và Anthropic Claude, cho phép các sếp tùy chỉnh model phù hợp với nhu cầu và chi phí.
- **Hoạt động 24/7:** Biểu mẫu tự động hóa chạy ngầm, sẵn sàng tích hợp vào bất kỳ hệ thống CRM, Chatbot hoặc công cụ nội bộ nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
1. **n8n Instance:** Đã cài đặt n8n (phiên bản Cloud hoặc Self-hosted).
2. **Brave Search API Key:** Tài khoản miễn phí từ Brave Search API.
3. **AI Model API Keys:** Ít nhất một trong các API Keys sau:
   - Google Gemini API Key (`googlePalmApi`)
   - OpenAI API Key (`openAiApi`)
   - Anthropic API Key (`anthropicApi`)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ n8n template hoặc copy toàn bộ JSON.
- Mở n8n Editor, chọn **Add workflow** -> **Import from File** hoặc dán trực tiếp vào màn hình làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 16 nodes kết hợp chặt chẽ với nhau. Các sếp cần chú ý cấu hình kỹ các điểm sau:

- **Node "Query" (HTTP Request):** 
  - Lấy API Key từ [api.search.brave.com](https://api.search.brave.com) (đăng ký gói Free).
  - Vào node **Query**, tìm mục header `X-Subscription-Token` và thay thế giá trị mẫu bằng **Brave API Key** của các sếp.
- **Các Node AI Model (`Agent Model`, `Parser Model`, `OpenAI Chat Model`, `Anthropic Chat Model`):**
  - Kết nối các credentials tương ứng cho Google Gemini, OpenAI hoặc Anthropic. 
  - Workflow được tối ưu sẵn cho Google Gemini (`Parser Model`, `Agent Model`), OpenAI GPT-4o và Anthropic Claude (`claude-3-5-haiku-20241022`).
- **Node "Webhook" & "Webhook Call":**
  - Chuyển đổi URL từ chế độ **Test URL** sang **Production URL** khi đưa vào vận hành thực tế.
  - Sử dụng node **Webhook Call** bên trong hệ thống gọi để truyền tham số `"Research Question"` vào workflow này.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (Test workflow) bằng một câu hỏi mẫu qua Webhook để kiểm tra luồng dữ liệu trả về từ Semantic Re-Ranker.
- Bật công tắc **Active** để đưa workflow vào trạng thái chạy tự động 24/7.

### ✍️ Gợi ý nâng cao & Mở rộng
- **Tích hợp Slack / Telegram:** Thêm node gửi thông báo tự động về kênh chat nhóm ngay khi kết quả nghiên cứu hoàn tất.
- **Lưu trữ vào Google Sheets / Airtable:** Thêm node database để lưu lại lịch sử các câu hỏi nghiên cứu và kết quả tổng hợp phục vụ việc audit sau này.
- **Xây dựng Agent Chatbot:** Kết nối Webhook này với một trợ lý ảo trên Telegram hoặc Web UI để tạo ra công cụ nghiên cứu thị trường tự động cho riêng doanh nghiệp.

### 📌 Kết luận
Với sự kết hợp giữa Brave Search tốc độ cao và khả năng xử lý ngữ nghĩa đỉnh cao của Google Gemini/OpenAI, workflow này sẽ là trợ thủ đắc lực giúp tiết kiệm hàng tá giờ làm việc thủ công mỗi tuần. Hãy import và cấu hình ngay hôm nay để tối ưu hóa quy trình nghiên cứu của các sếp!