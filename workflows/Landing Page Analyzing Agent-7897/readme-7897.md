---
title: "🚀 Xây Dựng AI Agent Phân Tích Landing Page & Tối Ưu CRO Tự Động Trong n8n"
description: "Hướng dẫn chi tiết cách tự động hóa việc phân tích landing page, đánh giá tỷ lệ chuyển đổi CRO và nhận báo cáo chi tiết bằng AI Agent kết hợp Google Gemini."
slug: "landing-page-analyzing-agent-n8n"
tags: [n8n, automation, ai-agent, google-gemini, cro, landing-page]
keywords: [n8n workflow, ai agent phân tích landing page, tối ưu cro tự động, google gemini n8n, tự động hóa marketing]
---

# 🚀 Tự Động Hóa Phân Tích Landing Page & Tối Ưu CRO Với AI Agent

Các sếp làm marketing, sales hay phát triển sản phẩm chắc chắn hiểu cảm giác mệt mỏi khi phải thủ công kiểm tra hàng loạt landing page, đánh giá bố cục, nội dung, và tìm cách tối ưu tỷ lệ chuyển đổi (CRO). Việc này vừa tốn thời gian, vừa dễ bỏ sót các lỗi UX/UI quan trọng.

Giải pháp ở đây là gì? Hãy để **Landing Page Analyzing Agent** làm thay các sếp! Workflow n8n này sẽ tự động nhận URL landing page từ biểu mẫu, cào dữ liệu, và sử dụng sức mạnh của **Google Gemini AI** cùng các mô hình ngôn ngữ lớn để phân tích toàn diện, đưa ra các đề xuất cải thiện CRO sắc bén chỉ trong vài giây.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không cần tự tay đọc và mổ xẻ từng trang web của đối thủ hay sản phẩm của mình.
- **Báo cáo CRO chuyên sâu:** AI Agent tự động đánh giá tiêu đề, lời kêu gọi hành động (CTA), và bố cục trang.
- **Giao diện thân thiện:** Thu thập URL qua form có sẵn và trả kết quả trực quan ngay lập tức.
- **Hoạt động 24/7:** Sẵn sàng phân tích bất cứ lúc nào các sếp cần.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động (Cloud hoặc Self-hosted).
- Tài khoản **Google AI Studio** để lấy **Gemini API Key** (`googlePalmApi`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ kho lưu trữ n8n hoặc copy toàn bộ mã nguồn JSON, sau đó paste trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống vận hành trơn tru, các sếp cần chú ý cấu hình các node sau:
- **Node `Gemini 2.5 Flash` (lmChatGoogleGemini):** Kết nối thông tin xác thực (Credentials) với tài khoản Google Gemini API của các sếp. Nếu chưa có key, hãy lấy miễn phí tại [Google AI Studio](https://aistudio.google.com/apikey).
- **Node `On form submission` (formTrigger):** Đây là điểm khởi đầu, cung cấp một biểu mẫu web để người dùng nhập URL landing page cần phân tích. Các sếp có thể nhúng form này vào website nội bộ.
- **Node `HTTP Request` (httpRequest):** Đảm bảo rằng các URL landing page gửi vào là công khai (publicly accessible) và không nằm sau lớp bảo mật đăng nhập để n8n có thể lấy được mã nguồn/nội dung trang.
- **Node `AI Agent` (agent) & `Information Extractor` (informationExtractor):** Kiểm tra lại System Prompt bên trong AI Agent. Các sếp có thể tinh chỉnh lại hướng dẫn để AI tập trung vào các tiêu chí CRO cụ thể của ngành hàng công ty mình.

#### 3. Kích hoạt ⚡️
- Nhấn **Test step** hoặc **Execute Workflow** để thử nghiệm gửi một URL mẫu qua form.
- Kiểm tra kết quả trả về ở node cuối cùng.
- Khi mọi thứ đã chạy mượt mà, bật công tắc **Active** ở góc trên bên phải để đưa workflow vào hoạt động chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node Telegram hoặc Slack sau node AI để tự động bắn kết quả phân tích về group chat khi có khách hàng hoặc nhân sự submit form.
- **Lưu lịch sử:** Thêm node Google Sheets hoặc Airtable để lưu lại toàn bộ các URL đã phân tích kèm báo cáo của AI phục vụ việc theo dõi chiến dịch.
- **Mở rộng đa ngôn ngữ:** Tùy chỉnh prompt trong AI Agent để cho phép báo cáo đầu ra bằng tiếng Việt hoặc tiếng Anh tùy theo nhu cầu.

### 📌 Kết luận
Landing Page Analyzing Agent là một trợ lý ảo đắc lực giúp các sếp tự động hóa quy trình tối ưu hóa chuyển đổi website. Hãy setup ngay hôm nay để nâng cao hiệu suất marketing của đội ngũ nhé!