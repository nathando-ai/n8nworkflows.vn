---
title: "🚀 Xây dựng hệ thống định tuyến AI thông minh với Dynamic Model Router và OpenRouter trong n8n"
description: "Tự động phân tích câu hỏi của người dùng và chọn model LLM tối ưu nhất qua OpenRouter để tiết kiệm chi phí và nâng cao chất lượng phản hồi."
slug: "dynamic-ai-model-router-openrouter-n8n"
tags: [n8n, automation, no-code, openrouter, ai-agent, llm]
keywords: [n8n workflow, định tuyến AI, openrouter n8n, ai agent dynamic model, tối ưu chi phí llm]
---

# 🚀 Tự động định tuyến AI thông minh với Dynamic Model Router trên n8n

Các sếp có bao giờ đau đầu vì dùng một model AI "khủng" (và đắt đỏ) cho những câu hỏi đơn giản, hoặc ngược lại, dùng model yếu cho các tác vụ phân tích phức tạp? Việc gán cứng một model duy nhất cho mọi tình huống khiến doanh nghiệp vừa tốn kém chi phí API, vừa không đạt hiệu quả tối ưu.

Workflow **Dynamic AI Model Router for Query Optimization with OpenRouter** chính là giải pháp tự động hóa 100% không cần code. Hệ thống sẽ tự động đọc nội dung câu hỏi của người dùng, phân tích độ phức tạp và chọn ra model LLM phù hợp nhất qua OpenRouter để xử lý.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tối ưu chi phí:** Dùng model giá rẻ/nhỏ cho câu hỏi đơn giản và chỉ gọi model cao cấp khi thực sự cần thiết.
- **Nâng cao chất lượng:** Đảm bảo mỗi truy vấn được giải quyết bởi bộ não AI chuyên biệt nhất.
- **Tự động hóa hoàn toàn:** Xử lý linh hoạt hàng ngàn yêu cầu khác nhau mà không cần can thiệp thủ công.
- **Hoạt động 24/7:** Phản hồi người dùng liền mạch thông qua giao diện chat tích hợp.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động.
- Tài khoản và API Key của **OpenRouter** (để truy cập đa dạng các dòng model như Claude, GPT, Llama, Mistral...).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này từ kho lưu trữ n8n hoặc copy trực tiếp và dán vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 6 nodes chính hoạt động nhịp nhàng với nhau. Các sếp cần chú ý các điểm sau:

- **When chat message received (`chatTrigger`):** Điểm khởi đầu nhận tin nhắn từ người dùng. Các sếp có thể tuỳ chỉnh giao diện chat widget hiển thị ra ngoài.
- **OpenRouter Chat Model & OpenRouter Chat Model1 (`lmChatOpenRouter`):** 
  - Cần kết nối credential tài khoản OpenRouter của các sếp.
  - Node thứ hai (`OpenRouter Chat Model1`) có tham số động `model: "={{ $json.output.model }}"` - đây là cốt lõi của việc nhận kết quả phân tích từ bước trước để tự động đổi model linh hoạt.
- **Routing Agent & AI Agent (`agent`):** 
  - *Routing Agent* đóng vai trò như "người gác cổng" phân tích yêu cầu.
  - *AI Agent* thực thi câu trả lời cuối cùng dựa trên model đã được định tuyến động.
- **Structured Output Parser (`outputParserStructured`):** Giúp ép đầu ra của AI định tuyến trả về đúng định dạng JSON chuẩn (chứa tên model) để hệ thống dễ dàng trích xuất và gọi model ở bước sau.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và thử gửi một vài câu hỏi từ dễ đến khó để kiểm tra xem hệ thống có tự động chọn đúng model mong muốn hay không.
- Sau khi test ngon lành, bật công tắc **Active** ở góc trên bên phải để đưa vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp Telegram/Slack:** Thay vì dùng Chat Trigger nội bộ, các sếp có thể đổi thành webhook nhận tin nhắn từ Telegram Bot hoặc Slack để hỗ trợ khách hàng đa kênh.
- **Lưu Log chi tiết:** Thêm node Google Sheets hoặc Supabase để ghi lại lịch sử câu hỏi, model nào đã được chọn và chi phí API tương ứng nhằm dễ dàng kiểm soát tài chính.
- **Bổ sung Fallback:** Cấu hình thêm cơ chế dự phòng (nếu model được chọn bị lỗi API, hệ thống tự chuyển sang model mặc định).

### 📌 Kết luận
Dynamic AI Model Router là một "vũ khí" cực kỳ lợi hại giúp tối ưu hóa chi phí vận hành AI cho các doanh nghiệp vừa và nhỏ. Hãy triển khai ngay hôm nay để tối ưu hóa từng đồng chi phí API mà vẫn mang lại trải nghiệm AI đỉnh cao cho người dùng!