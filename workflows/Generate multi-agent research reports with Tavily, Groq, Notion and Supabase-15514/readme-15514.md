---
title: "🚀 Tự động hóa tạo báo cáo nghiên cứu chuyên sâu đa tác nhân với Tavily, Groq, Notion và Supabase trên n8n"
description: "Xây dựng hệ thống AI Research Agent tự động tìm kiếm web, phân tích đa chiều bằng LLM, xuất báo cáo chuyên nghiệp lên Notion và lưu trữ vector trên Supabase."
slug: "tao-bao-cao-nghien-cuu-da-tac-nhan-ai-n8n"
tags: [n8n, automation, ai-agents, notion, supabase, groq, tavily]
keywords: [n8n workflow, ai research agent, tavily search, groq llama 3, notion automation, supabase vector store]
keywords: [n8n workflow, tự động hóa, ai agent, nghiên cứu thị trường, notion, supabase]
---

# 🚀 Tự động hóa tạo báo cáo nghiên cứu chuyên sâu đa tác nhân với Tavily, Groq, Notion và Supabase

Các sếp có bao giờ mất hàng giờ, thậm chí hàng ngày chỉ để tổng hợp thông tin, đọc hàng chục bài viết, sau đó tự tay viết các báo cáo nghiên cứu thị trường hay chiến lược? Công việc thủ công này cực kỳ ngốn thời gian và dễ bỏ sót các xu hướng quan trọng.

Giải pháp đây rồi! Workflow n8n này sẽ giúp các sếp vận hành một **Hệ thống Nghiên cứu Tự động hóa Đa tác nhân (Multi-Agent Research Pipeline)** hoàn chỉnh. Hệ thống sẽ tự động quét web song song, sử dụng các AI Agent chuyên biệt để tóm tắt, phân tích chiều sâu, tổng hợp thành báo cáo hoàn chỉnh, lưu trực tiếp vào Notion và đưa vào Vector Database trên Supabase để tra cứu ngữ nghĩa sau này. Tất cả chỉ trong vòng vài phút và hoàn toàn tự động!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Biến quy trình nghiên cứu thủ công thành một cú click chuột.
- **Phân tích đa chiều:** Kết hợp sức mạnh của nhiều mô hình AI (Groq Llama 3.3, OpenRouter GPT) thực hiện tóm tắt sự kiện, phân tích rủi ro và dự phóng xu hướng.
- **Lưu trữ thông minh:** Tự động đồng bộ báo cáo định dạng chuẩn vào Notion workspace và đánh chỉ mục vector vào Supabase phục vụ cho các hệ thống RAG (Retrieval-Augmented Generation) sau này.
- **Hoạt động linh hoạt:** Dễ dàng thay đổi chủ đề nghiên cứu, độ sâu và phạm vi tìm kiếm theo nhu cầu thực tế của doanh nghiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow chạy mượt mà, các sếp cần chuẩn bị sẵn các tài khoản và API Keys sau:
- **Tavily API:** Dùng cho các node Web Search truy vấn dữ liệu web nâng cao.
- **Groq API:** Cung cấp mô hình Llama 3.3 70B cho Sub-Agent tóm tắt và Synthesis Agent tổng hợp.
- **OpenRouter API:** Cung cấp mô hình AI cho Analyst Sub-Agent phân tích chuyên sâu.
- **OpenAI API Key:** Dùng để tạo embeddings cho Supabase Vector Store.
- **Notion Account & Database:** Kết nối qua OAuth2 để lưu trữ báo cáo tự động.
- **Supabase Project:** Đã tạo sẵn bảng `documents` có hỗ trợ cột vector để lưu trữ tri thức.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ nguồn cung cấp.
- Mở n8n Editor, chọn **Workflows** -> **Import from File** (hoặc copy toàn bộ JSON và paste trực tiếp vào không gian làm việc của n8n).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các thông số và credentials sau trước khi kích hoạt:
- **Web Search Query, Web Search Query 4, Web Search Query 5 (HTTP Request Nodes):** Thay thế khóa API Tavily mẫu bằng API Key riêng của sếp (đăng ký tại tavily.com).
- **Summarizer LLM1 & Groq Chat Model:** Chọn credentials `groqApi` và kiểm tra model `llama-3.3-70b-versatile`.
- **OpenAi Analyst LLM1:** Chọn credentials `openRouterApi` và chọn model phù hợp (ví dụ `openai/gpt-oss-20b` hoặc model tương đương).
- **Save Report to Notion1:** Kết nối tài khoản Notion qua OAuth2, cung cấp đúng `databaseId` nơi lưu báo cáo.
- **Supabase Vector Store1 & Embeddings OpenAI1:** Điền thông tin kết nối Supabase, cấu hình OpenAI API Key để sinh vector embeddings chính xác.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** tại node `Start Research` để chạy thử nghiệm với chủ đề mặc định.
- Kiểm tra kết quả trả về ở Notion và Supabase.
- Nếu mọi thứ hoạt động trơn tru, hãy bật **Active** để đưa workflow vào trạng thái tự động sẵn sàng phục vụ.

---

### Quy trình hoạt động chi tiết của hệ thống

1. **Khởi tạo & Lên kế hoạch (Trigger & Topic Setup):**
   Node `Start Research` kích hoạt quy trình. `Set Research Topic1` thiết lập chủ đề nghiên cứu (ví dụ: xu hướng AI Automation) và tạo Session ID độc lập. Node `Code in JavaScript` (`Parse Orchestrator Tasks1`) chia nhỏ chủ đề thành 3 câu lệnh tìm kiếm Tavily riêng biệt kèm theo prompt nhiệm vụ cho các tác nhân phía sau.

2. **Nghiên cứu Web Song Song (Parallel Web Research):**
   Các node `Web Search Query`, `Web Search Query 4`, `Web Search Query 5` thực hiện truy vấn đồng thời qua API Tavily. Sau đó, node `Merge Search Results1` và `Aggregate Research Context1` gom nhóm, khử trùng lặp và tạo thành một khối ngữ cảnh nghiên cứu duy nhất (tối đa 12 nguồn).

3. **Phân tích Đa Tác Nhân (Multi-Agent AI Analysis):**
   Khối ngữ cảnh được đưa vào 2 luồng AI chạy song song:
   - **Summarizer Sub-Agent1** (Groq Llama 3.3 70B): Trích xuất sự kiện, số liệu thống kê chính xác.
   - **Analyst Sub-Agent1** (OpenRouter GPT-OSS 20B): Đánh giá xu hướng, rủi ro và đưa ra dự phóng 12 tháng.
   Cuối cùng, `Synthesis Agent1` (Groq Llama 3.3 70B) tiếp nhận kết quả từ cả hai tác nhân để viết nên báo cáo điều hành (Executive Report) hoàn chỉnh bằng định dạng Markdown.

4. **Xuất bản & Lưu trữ Vector (Output & Vector Storage):**
   Báo cáo hoàn thiện được định dạng lại, cắt nhỏ thành các đoạn dưới 1.900 ký tự bằng đoạn mã JavaScript để phù hợp với giới hạn của Notion, sau đó lưu tự động vào database Notion thông qua node `Save Report To Notion1`. Song song đó, toàn bộ báo cáo được đưa vào `Supabase Vector Store1` để tạo Embeddings, phục vụ cho việc tìm kiếm ngữ nghĩa thông minh trong tương lai.

---

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh thông báo:** Nối thêm một node Telegram hoặc Slack ở cuối workflow để gửi thông báo trực tiếp kèm link báo cáo Notion đến team ngay khi nghiên cứu hoàn tất.
- **Tự động hóa theo lịch:** Thay thế node `manualTrigger` bằng `Schedule Trigger` để hệ thống tự động quét và báo cáo thị trường định kỳ mỗi tuần/tháng.
- **Mở rộng nguồn dữ liệu:** Kết hợp thêm các node RSS Feed, Google Drive hoặc Gmail để đưa tài liệu nội bộ vào hệ thống RAG Supabase cùng với báo cáo nghiên cứu web.

### 📌 Kết luận
Workflow tạo báo cáo nghiên cứu đa tác nhân này là một "vũ khí tối thượng" giúp các nhà quản lý, đội ngũ chiến lược và chuyên gia nội dung tiết kiệm hàng đống thời gian. Hãy cài đặt ngay lên hệ thống n8n của các sếp để tối ưu hóa năng suất làm việc từ hôm nay!