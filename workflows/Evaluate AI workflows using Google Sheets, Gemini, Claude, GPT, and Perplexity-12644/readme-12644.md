---
title: "🚀 Đánh giá tự động chất lượng AI Workflow bằng Google Sheets, Gemini, Claude, GPT và Perplexity trong n8n"
description: "Hướng dẫn xây dựng hệ thống tự động đánh giá và so sánh hiệu suất các mô hình AI lớn (GPT, Claude, Gemini, Perplexity) kết hợp Google Sheets và n8n."
slug: "danh-gia-tu-dong-ai-workflow-google-sheets-gemini-claude-gpt-perplexity"
tags: [n8n, automation, ai-evaluation, google-sheets, gpt, claude, gemini, perplexity]
keywords: [n8n workflow, đánh giá AI, tự động hóa Google Sheets, OpenAI GPT, Anthropic Claude, Google Gemini, Perplexity AI]
---

# 🚀 Đánh giá tự động chất lượng AI Workflow bằng Google Sheets & Đa mô hình LLM

Việc phát triển và tối ưu các ứng dụng AI đòi hỏi các sếp phải liên tục kiểm thử (testing) và đánh giá chất lượng đầu ra từ nhiều mô hình ngôn ngữ lớn (LLM) khác nhau như GPT, Claude, Gemini hay Perplexity. Tuy nhiên, việc làm thủ công như copy-paste prompt, so sánh kết quả trên Excel hay đánh giá cảm tính tốn rất nhiều thời gian, thiếu khách quan và khó scale.

Giải pháp là gì? Hãy để **n8n** thay các sếp tự động hóa toàn bộ quy trình này! Workflow chuyên nghiệp này giúp kết nối dữ liệu từ Google Sheets, chạy đánh giá tự động thông qua các mô hình AI hàng đầu, xử lý qua Gmail Trigger/Gmail và tổng hợp kết quả một cách chính xác, minh bạch.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **So sánh đa mô hình trực quan:** Tự động gửi cùng một tập dữ liệu/prompt tới GPT, Claude, Gemini và Perplexity để đối chiếu kết quả.
- **Tự động hóa 100%:** Kích hoạt quy trình thông qua `Evaluation Trigger` hoặc `Gmail Trigger` khi có dữ liệu mới.
- **Tiết kiệm 90% thời gian:** Không còn phải thủ công test từng model hay tổng hợp báo cáo bằng tay.
- **Đánh giá chuẩn xác:** Sử dụng các công cụ LangChain, Information Extractor và Evaluation chuyên sâu của n8n để chấm điểm chất lượng đầu ra.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted bản mới nhất hỗ trợ LangChain & AI nodes).
- **Google Sheets:** File chứa danh sách câu hỏi, test cases hoặc prompt cần đánh giá.
- **API Keys / Credentials:** 
  - OpenAI API Key (cho GPT)
  - Anthropic API Key (cho Claude)
  - Google Gemini API Key
  - Perplexity API Key
  - Gmail Credentials (nếu sử dụng trigger hoặc gửi báo cáo qua email)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ nguồn cung cấp.
- Trong giao diện n8n Editor, nhấn vào menu **Add workflow** -> **Import from File** (hoặc copy toàn bộ JSON và dán trực tiếp vào màn hình workflow).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru, các sếp cần cấu hình chính xác các node trọng điểm sau:

- **Evaluation Trigger / Gmail Trigger:** 
  - Chọn đúng tài khoản Gmail hoặc cấu hình điều kiện kích hoạt (`evaluationTrigger`) để hệ thống biết khi nào bắt đầu chạy bộ test.
- **Google Sheets Node:** 
  - Kết nối tài khoản Google của các sếp.
  - Chọn chính xác file Spreadsheet và Sheet Name chứa dữ liệu đầu vào (Prompt / Test Cases).
- **Các Model AI Nodes (`lmChatOpenAi`, `lmChatAnthropic`, `lmChatGoogleGemini`, `perplexityTool`):**
  - Điền các Credentials tương ứng cho từng hãng (OpenAI, Anthropic, Google, Perplexity).
  - Tùy chỉnh tham số Temperature (khuyên dùng `0.2` hoặc `0` để kết quả đánh giá mang tính khách quan, ít ngẫu nhiên).
- **Agent & Information Extractor / Chain Summarization:**
  - Kiểm tra lại các system prompt trong node Agent để đảm bảo tiêu chí chấm điểm, trích xuất thông tin phù hợp với bài toán thực tế của doanh nghiệp.
- **Gmail Node (Gửi kết quả):**
  - Cấu hình địa chỉ email nhận báo cáo tổng hợp sau khi quá trình đánh giá hoàn tất.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử nghiệm (Test Run) với dữ liệu mẫu nhỏ trên Google Sheets.
- Kiểm tra kết quả đầu ra ở từng node để đảm bảo không gặp lỗi xác thực API.
- Sau khi test thành công, gạt công tắc sang **Active** để workflow tự động vận hành.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack / Telegram:** Thay vì chỉ gửi email, các sếp có thể gắn thêm node Slack hoặc Telegram để nhận thông báo ngay lập tức vào group chat khi hoàn thành một phiên đánh giá AI.
- **Lưu lịch sử đánh giá:** Mở rộng workflow để ghi đè hoặc tạo mới một row log kết quả chi tiết vào một Tab riêng trong Google Sheets, giúp theo dõi sự thay đổi chất lượng mô hình qua từng phiên bản cập nhật.
- **Kết hợp trích xuất file:** Sử dụng node `extractFromFile` để tự động đọc các tài liệu PDF/Word tải lên qua email hoặc Google Drive làm nguồn dữ liệu test đầu vào.

### 📌 Kết luận
Việc kiểm thử và đánh giá mô hình AI không còn là bài toán đau đầu nếu các sếp áp dụng ngay workflow tự động hóa này trên n8n. Tiết kiệm thời gian, minh bạch trong kết quả và tối ưu hóa chi phí API là những giá trị thiết thực mà hệ thống mang lại. Hãy triển khai ngay hôm nay!