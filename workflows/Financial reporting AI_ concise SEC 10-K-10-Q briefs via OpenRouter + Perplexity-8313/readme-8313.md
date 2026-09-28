---
title: "🚀 Tự động hóa báo cáo tài chính SEC 10-K & 10-Q với AI Agent, OpenRouter và Perplexity trong n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động tóm tắt báo cáo tài chính SEC 10-K và 10-Q siêu tốc, kết hợp AI Agent, OpenRouter và Perplexity."
slug: "tu-dong-hoa-bao-cao-tai-chinh-sec-openrouter-perplexity-n8n"
tags: [n8n, automation, no-code, ai-agent, openrouter, perplexity, finance]
keywords: [n8n workflow, bao cao tai chinh sec, ai summarization, openrouter n8n, perplexity tool n8n, tu dong hoa no-code]
---

# 🚀 Tự động hóa báo cáo tài chính SEC 10-K & 10-Q với AI Agent cực đỉnh

Các sếp làm trong lĩnh vực tài chính, đầu tư hay phân tích thị trường chắc chắn hiểu rõ nỗi đau: Việc đọc hiểu các bản cáo bạch, báo cáo tài chính SEC 10-K (báo cáo thường niên) hay 10-Q (báo cáo hàng quý) dài hàng trăm trang là một cơn ác mộng tốn cực kỳ nhiều thời gian và chất xám. 

Thay vì phải "bơi" trong biển dữ liệu khô khan đó thủ công, workflow n8n này sẽ thay các sếp "nhai" tài liệu, phân tích thông tin cốt lõi và tóm tắt thành các bản brief súc tích, chuyên nghiệp nhờ sự kết hợp giữa **AI Agent**, **OpenRouter** và **Perplexity**. Giải pháp tự động hóa 100% không cần code giúp tối ưu hóa hiệu suất đầu tư ngay lập tức!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Rút ngắn thời gian phân tích từ vài tiếng đọc tài liệu xuống chỉ vài phút nhận báo cáo tóm tắt.
- **Độ chính xác cao:** Khai thác dữ liệu thời gian thực từ Perplexity kết hợp khả năng suy luận sắc bén của mô hình AI qua OpenRouter.
- **Định dạng chuyên nghiệp:** Tự động chuẩn hóa nội dung thành Markdown, HTML hoặc lưu trữ trực tiếp tiện lợi.
- **Hoạt động linh hoạt:** Nhận câu hỏi và trả kết quả thông qua giao diện chat trực quan bất cứ lúc nào các sếp cần.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống n8n đã được cài đặt (Cloud hoặc Self-hosted).
- **OpenRouter API Key:** Để kết nối với các mô hình ngôn ngữ lớn (LLM) thông qua node OpenRouter Chat Model.
- **Perplexity API Key:** Cung cấp công cụ tìm kiếm và truy vấn thông tin tài chính thời gian thực.
- Tài khoản/API liên quan nếu muốn lưu trữ kết quả qua HTTP Request (Google Docs, Notion, v.v.).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ nguồn chính thức hoặc copy trực tiếp mã JSON và dán vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà không gặp lỗi "missing credential", các sếp cần chú ý cấu hình các node cốt lõi sau:

- **When chat message received (`chatTrigger`):** Điểm khởi đầu nhận yêu cầu từ người dùng (ví dụ: *"Tóm tắt báo cáo tài chính quý gần nhất của Apple"*).
- **AI Agent (`agent`):** Bộ não trung tâm điều phối luồng xử lý câu hỏi và kết hợp các công cụ.
- **OpenRouter Chat Model (`lmChatOpenRouter`):** Cần điền OpenRouter API Key và chọn model AI phù hợp (ví dụ: Claude 3.5 Sonnet hoặc GPT-4o) để đảm bảo chất lượng phân tích tài chính sâu sắc.
- **Message a model in Perplexity (`perplexityTool`):** Cung cấp API Key của Perplexity để AI Agent có thể gọi công cụ này tìm kiếm thông tin mới nhất từ các hồ sơ SEC.
- **CreateGoogleDoc (`httpRequest`) & Format_HTML (`code`):** Tùy chỉnh các node này nếu các sếp muốn xuất kết quả tóm tắt ra Google Docs hoặc định dạng lại HTML theo ý muốn.

#### 3. Khởi động ⚡️
- Nhấn nút **Execute Workflow** và thử gửi một câu hỏi mẫu qua chat trigger để test dữ liệu.
- Sau khi kiểm tra kết quả trả về hoàn hảo, các sếp hãy gạt nút **Active** để đưa workflow vào trạng thái vận hành tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack / Telegram:** Thêm node gửi tin nhắn để mỗi khi có báo cáo tóm tắt hoàn thành, hệ thống sẽ tự động push thẳng vào nhóm chat công việc của team đầu tư.
- **Lưu trữ Log Google Sheets:** Mở rộng workflow bằng cách ghi lại lịch sử các mã cổ phiếu và câu hỏi đã tra cứu vào Google Sheets để dễ dàng tra cứu lại.
- **Lập lịch tự động (Schedule Trigger):** Thay vì hỏi thủ công qua chat, các sếp có thể đổi trigger thành Schedule để tự động tóm tắt báo cáo tài chính của một danh sách mã cổ phiếu yêu thích mỗi khi có thông tin mới từ SEC.

### 📌 Kết luận
Việc phân tích tài chính chưa bao giờ dễ dàng và nhanh chóng đến thế khi kết hợp sức mạnh của AI và tự động hóa n8n. Hãy "lên đồ" workflow này ngay hôm nay để tối ưu hóa năng suất và nắm bắt cơ hội đầu tư nhanh hơn đối thủ!