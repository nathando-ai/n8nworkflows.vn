---
title: "🚀 Tự động tạo và giải thích công thức Excel/Google Sheets bằng DeepSeek AI trên n8n"
description: "Hướng dẫn cài đặt và sử dụng workflow n8n tích hợp DeepSeek AI qua OpenRouter để tự động sinh mã hoặc giải thích công thức Excel/Google Sheets một cách thông minh, nhanh chóng."
slug: "tao-va-giai-thich-cong-thuc-excel-google-sheets-deepseek-ai"
tags: [n8n, automation, deepseek, openrouter, excel, google-sheets, ai-agent]
keywords: [n8n workflow, tạo công thức excel, giải thích công thức excel, deepseek ai, openrouter, tự động hóa no-code]
---

# 🚀 Tự động tạo và giải thích công thức Excel/Google Sheets bằng DeepSeek AI

Các sếp có bao giờ cảm thấy đau đầu khi phải mò mẫm viết những hàm Excel phức tạp như `VLOOKUP`, `INDEX/MATCH`, hay `XLOOKUP` lồng nhau không? Hoặc khi nhận được một bảng tính từ đồng nghiệp với những công thức dài dằng dặc mà không tài nào hiểu nổi nó đang tính toán cái gì? 

Việc tra cứu Google hay mò mẫm thủ công vừa tốn thời gian lại dễ xảy ra sai sót. Giải pháp cho các sếp đây: một workflow n8n tự động hóa 100% kết hợp sức mạnh của **DeepSeek AI** (thông qua OpenRouter) giúp tự động tạo công thức theo yêu cầu bằng văn bản tự nhiên, hoặc giải thích chi tiết ý nghĩa của bất kỳ công thức Excel/Google Sheets nào ngay lập tức!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tạo công thức chuẩn xác:** Biến yêu cầu bằng lời nói thành công thức Excel/Google Sheets hoàn chỉnh chỉ trong tích tắc.
- **Giải thích công thức dễ hiểu:** Phân tích chi tiết từng thành phần của công thức giúp người dùng dễ dàng nắm bắt và tối ưu.
- **Tự động hóa hoàn toàn:** Hoạt động qua Webhook, dễ dàng tích hợp vào các ứng dụng nội bộ, chatbot hoặc web app của doanh nghiệp.
- **Tối ưu chi phí:** Sử dụng mô hình DeepSeek AI thông qua OpenRouter với hiệu năng cao và chi phí cực kỳ tiết kiệm.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống **n8n** đã được cài đặt (Self-hosted hoặc n8n Cloud).
- Tài khoản **OpenRouter** và API Key đi kèm để kết nối với mô hình DeepSeek AI.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này từ kho lưu trữ n8n (Link gốc: [n8n.io/workflows/6396](https://n8n.io/workflows/6396)).
- Trong giao diện n8n Editor, bấm vào menu ở góc trên bên phải, chọn **Import from File** hoặc copy và paste trực tiếp đoạn JSON vào workspace của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 9 nodes chính hoạt động nhịp nhàng. Các sếp cần chú ý cấu hình kỹ các node sau:

- **OpenRouter Chat Model & OpenRouter Chat Model1:** 
  - Thêm Credentials loại *OpenRouter API*.
  - Nhập API Key từ tài khoản OpenRouter của các sếp.
  - Chọn model chính xác (khuyến nghị sử dụng các dòng model DeepSeek V3 hoặc DeepSeek R1 để có kết quả tốt nhất).
- **Webhook & Respond to Webhook:** 
  - Cấu hình đường dẫn nhận dữ liệu đầu vào (POST request chứa yêu cầu của người dùng, ví dụ: loại hành động `generate` hay `explain`, và nội dung câu hỏi/công thức).
- **Detect Intent & Intent Switch:** 
  - Kiểm tra logic phân loại ý định người dùng (phân luồng xem yêu cầu là tạo công thức mới hay giải thích công thức có sẵn).
- **Generate Formula & Explain Formula (AI Agent):** 
  - Tinh chỉnh Prompt hệ thống (System Prompt) trong các Agent này nếu các sếp muốn AI trả về kết quả bằng định dạng Markdown, JSON hoặc kèm theo ví dụ cụ thể rõ ràng hơn.
- **Code Node:** 
  - Xử lý dữ liệu đầu ra từ AI trước khi trả về qua Webhook, đảm bảo kết quả hiển thị sạch sẽ, chuẩn cú pháp cho người dùng cuối.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Node** hoặc **Test Workflow** để thử nghiệm gửi một request mẫu đến Webhook.
- Sau khi kiểm tra mọi luồng chạy mượt mà, hãy gạt công tắc sang **Active** để đưa workflow vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Chatbot:** Kết nối Webhook này với Telegram Bot hoặc Slack Workspace để nhân viên trong công ty có thể tra cứu công thức trực tiếp ngay trên khung chat công việc.
- **Lưu lịch sử (Logging):** Thêm một node Google Sheets hoặc Airtable vào sau bước xử lý để lưu lại các câu lệnh và kết quả, giúp đội ngũ quản lý phân tích nhu cầu sử dụng của team.
- **Xây dựng Web App mini:** Kết hợp workflow này với một giao diện No-code đơn giản (như Retool hoặc Softr) để tạo ra trang web "Trợ lý Excel AI" nội bộ cực kỳ chuyên nghiệp.

### 📌 Kết luận
Với workflow tích hợp DeepSeek AI này, việc xử lý các bảng tính Excel và Google Sheets sẽ không còn là cơn ác mộng. Hãy import ngay vào n8n của các sếp để tối ưu hóa năng suất làm việc ngay hôm nay!