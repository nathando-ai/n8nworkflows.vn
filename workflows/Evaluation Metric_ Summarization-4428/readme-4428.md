---
title: "🚀 Đánh giá chất lượng tóm tắt AI (Summarization Metric) tự động trong n8n"
description: "Hướng dẫn cấu hình workflow n8n giúp tự động đo lường độ chính xác, mức độ bám sát nguồn tài liệu gốc (faithfulness) của LLM khi tóm tắt văn bản từ Google Drive."
slug: "danh-gia-chat-luong-tom-tat-ai-summarization-metric-n8n"
tags: [n8n, automation, ai, evaluation, langchain, openai, gemini]
keywords: [n8n workflow, đánh giá AI, summarization metric, llm evaluation, tóm tắt tự động, langchain n8n]
---

# 🚀 Đánh giá chất lượng tóm tắt AI (Summarization Metric) tự động trong n8n

Các sếp đang xây dựng các ứng dụng AI tóm tắt văn bản, báo cáo hay transcript video nhưng luôn đau đầu vì hiện tượng **AI bịa đặt thông tin (hallucination)** hoặc tóm tắt lan man, không bám sát văn bản gốc? Việc kiểm tra thủ công từng bản tóm tắt tốn rất nhiều thời gian và không thể scale lớn.

Workflow n8n tuyệt vời này từ tác giả Jimleuk sẽ giải quyết triệt để vấn đề đó. Nó cung cấp một hệ thống đánh giá tự động (AI Evaluation) chuyên biệt cho tác vụ **Summarization**, giúp đo lường mức độ chính xác và trung thực của mô hình LLM dựa trên tài liệu nguồn lưu trữ tại Google Drive.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa đánh giá:** Chấm điểm tự động độ chính xác của các bản tóm tắt do LLM tạo ra mà không cần con người đọc kiểm tra thủ công.
- **Phát hiện Hallucination:** Nhận diện ngay lập tức các nội dung mà AI tự bịa ra hoặc không xuất hiện trong tài liệu gốc.
- **Tối ưu Prompt & Model:** Dựa vào điểm số (metrics) để biết khi nào cần tinh chỉnh lại câu lệnh (prompt) hoặc đổi model AI phù hợp hơn.
- **Tích hợp linh hoạt:** Kết hợp mượt mà giữa Google Drive, OpenAI, Google Gemini và hệ thống Evaluation Dataset chuyên nghiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Version:** Từ bản `1.94+` trở lên (hỗ trợ đầy đủ các tính năng AI Evaluation và LangChain).
- **Credentials:**
  - **Google Sheets OAuth2 API** (Để đọc dataset mẫu và lưu kết quả đánh giá).
  - **Google Drive OAuth2 API** (Để tải transcript bài viết/video từ Drive).
  - **OpenAI API Key** (Cho mô hình `gpt-4.1-mini`).
  - **Google Palm / Gemini API Key** (Cho mô hình LLM chạy tác vụ chính).
- **Dataset mẫu:** Tham khảo cấu trúc dữ liệu tại [Google Sheet mẫu](https://docs.google.com/spreadsheets/d/1YOnu2JJjlxd787AuYcg-wKbkjyjyZFgASYVV0jsij5Y/edit?usp=sharing).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow (hoặc tải file từ nguồn gốc) và dán trực tiếp vào n8n Editor của mình. Toàn bộ 14 nodes bao gồm các thành phần LangChain, Evaluation Trigger và Google Drive sẽ được thiết lập sẵn sàng.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần chú ý cấu hình các node cốt lõi sau:
- **When fetching a dataset row (`evaluationTrigger`):** Kết nối tài khoản Google Sheets của các sếp và trỏ tới file dataset chứa danh sách URL transcript đầu vào.
- **Download Transcript (`googleDrive`) & Get Gdrive URL (`set`):** Đảm bảo tài khoản Google Drive được cấp quyền để node có thể đọc file transcript dựa trên đường dẫn URL được truyền vào từ dataset.
- **OpenAI Chat Model (`lmChatOpenAi`) & LLM (`lmChatGoogleGemini`):** Nhập API Key chính xác cho OpenAI và Google để các agent thực hiện quá trình sinh tóm tắt và chấm điểm.
- **Set Metrics (`evaluation`):** Cấu hình các thông số đánh giá (`setMetrics`) theo chuẩn template chấm điểm tóm tắt (dựa trên tài liệu chuẩn của Google Vertex AI về Summarization Quality).

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (**Test run**) với một vài dòng dữ liệu mẫu trong Google Sheets để kiểm tra kết quả trả về ở node Output.
- Sau khi mọi thứ hoạt động trơn tru, bật công tắc **Active** để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp cảnh báo:** Thêm node Telegram hoặc Slack ở cuối workflow để nhận thông báo ngay lập tức nếu điểm số tóm tắt của một bản ghi rơi xuống dưới ngưỡng cho phép (ví dụ: điểm faithfulness < 3/5).
- **Lưu lịch sử chi tiết:** Mở rộng workflow để ghi log toàn bộ điểm số và lý do đánh giá của LLM vào một bảng Google Sheets riêng biệt nhằm theo dõi hiệu suất theo thời gian.
- **A/B Testing Model:** Thay đổi linh hoạt giữa các model khác nhau (như GPT-4o-mini, Claude 3.5 Sonnet, Gemini 1.5 Pro) để so sánh xem model nào cho ra kết quả tóm tắt trung thực và bám sát nguồn nhất.

### 📌 Kết luận
Việc kiểm soát chất lượng đầu ra của AI giờ đây đã trở nên đơn giản hơn bao giờ hết với bộ công cụ Evaluation sẵn có trong n8n. Hãy áp dụng ngay workflow này để tối ưu hóa các ứng dụng AI của doanh nghiệp các sếp và loại bỏ hoàn toàn tình trạng AI "nói phét"!