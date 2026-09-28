---
title: "🚀 Tự Động Tạo và Lọc Lead B2B Từ Telegram Kết Hợp Google Maps, Serper, GPT-4o và Gmail"
description: "Khám phá cách tự động hóa quy trình tìm kiếm, xác thực và gửi email chăm sóc khách hàng tiềm năng B2B trực tiếp từ Telegram sử dụng AI và Google Maps."
slug: "tu-dong-tao-va-loc-lead-b2b-tu-telegram-voi-gpt-4o-va-google-maps"
tags: [n8n, automation, no-code, b2b-leads, openai, google-maps, telegram, gmail]
keywords: [n8n workflow, tự động hóa b2b lead, tìm kiếm khách hàng tiềm năng, gpt-4o, serper api, google maps automation]
---

# 🚀 Tự Động Tạo và Lọc Lead B2B Từ Telegram Kết Hợp Google Maps, Serper, GPT-4o và Gmail

Việc tìm kiếm và xác thực khách hàng tiềm năng (B2B leads) theo phương pháp thủ công thường ngốn rất nhiều thời gian của đội ngũ sales: từ việc lướt Google Maps tìm địa điểm, tra cứu thông tin trên web, phân tích xem doanh nghiệp đó có thực sự phù hợp hay không, cho đến việc soạn email chào hàng. 

Đã đến lúc "giải phóng" đội ngũ sales khỏi những công việc lặp đi lặp lại nhàm chán này! Workflow n8n dưới đây là giải pháp tự động hóa 100% không cần code, giúp các sếp nhận yêu cầu tìm lead trực tiếp qua **Telegram**, tự động quét dữ liệu từ **Google Maps & Serper**, nhờ **GPT-4o** phân tích chất lượng lead, và cuối cùng tự động gửi email chăm sóc qua **Gmail**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện**: Chỉ cần ra lệnh qua Telegram, hệ thống sẽ tự động triển khai từ A-Z mà không cần thao tác thủ công.
- **Lọc lead thông minh bằng AI**: GPT-4o sẽ đóng vai trò như một chuyên gia sales, đánh giá tiềm năng và phân loại doanh nghiệp cực kỳ chính xác.
- **Cá nhân hóa nội dung**: Tự động soạn thảo email giới thiệu dịch vụ dựa trên thông tin thực tế của từng doanh nghiệp tìm được.
- **Hoạt động liên tục 24/7**: Không bỏ lỡ bất kỳ cơ hội kinh doanh nào, tiết kiệm hàng chục giờ làm việc mỗi tuần cho đội ngũ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow vận hành trơn tru, các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
1. **Tài khoản Telegram Bot**: Tạo qua BotFather để nhận yêu cầu tìm kiếm lead.
2. **Serper API Key**: Dùng để tìm kiếm thông tin doanh nghiệp qua Google Search API.
3. **OpenAI API Key (GPT-4o)**: Dùng để phân tích dữ liệu và viết email.
4. **Tài khoản Gmail/Google Workspace**: Để gửi email tự động tới khách hàng tiềm năng.
5. **Server n8n**: Đã cài đặt n8n (Self-hosted hoặc n8n Cloud).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow này từ cộng đồng n8n hoặc copy đoạn mã JSON.
- Trong giao diện n8n Editor, nhấn vào dấu **`+`** hoặc chọn **Add workflow** -> **Import from File** / Paste dữ liệu JSON trực tiếp vào màn hình làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Khi import xong, các sếp cần chú ý cấu hình kỹ lưỡng các thành phần cốt lõi sau:
- **Telegram Trigger Node**: Kết nối với Telegram Bot của các sếp để lắng nghe tin nhắn yêu cầu tìm kiếm lead (ví dụ: *"Tìm cho tôi 5 quán cà phê tại Quận 1, TP.HCM"*).
- **HTTP Request / Serper API Node**: Điền Serper API Key để hệ thống gửi truy vấn tìm kiếm doanh nghiệp trên Google.
- **OpenAI (GPT-4o) Node**: Thiết lập credentials OpenAI, cấu hình System Prompt để AI hiểu rõ tiêu chí lọc lead (ví dụ: quy mô, lĩnh vực, vị trí) và yêu cầu định dạng đầu ra chuẩn JSON.
- **Gmail Node**: Cấu hình tài khoản Gmail gửi đi, thiết lập tiêu đề và nội dung email tự động lấy từ kết quả phân tích của GPT-4o.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và gửi một tin nhắn thử nghiệm qua Telegram để kiểm tra luồng dữ liệu chạy qua từng node.
- Sau khi test thành công, gạt công tắc sang trạng thái **Active** để hệ thống tự động hoạt động chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo qua Telegram**: Thêm một node Telegram ở cuối workflow để gửi báo cáo tóm tắt (số lượng lead tìm thấy, tỷ lệ đạt yêu cầu) về thẳng group chat cho sếp hoặc đội ngũ sales theo dõi.
- **Lưu trữ vào Google Sheets**: Thêm node Google Sheets để lưu lại toàn bộ thông tin chi tiết của lead (Tên doanh nghiệp, Website, Email, Đánh giá của AI) phục vụ cho các chiến dịch remarketing sau này.
- **Xử lý trùng lặp**: Kết hợp kiểm tra database trước khi gửi email để tránh gửi trùng một khách hàng nhiều lần.

### 📌 Kết luận
Việc tự động hóa quy trình tìm kiếm và lọc lead B2B bằng n8n, kết hợp với sức mạnh của GPT-4o và Google Maps, sẽ giúp doanh nghiệp tối ưu hóa chi phí vận hành và tăng mạnh tỷ lệ chuyển đổi sales. Hãy triển khai ngay hôm nay để đưa quy trình kinh doanh của các sếp lên một tầm cao mới!