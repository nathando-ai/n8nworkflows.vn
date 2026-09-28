---
title: "🚀 Tự động giám sát thương hiệu 24/7 với GPT, Brave Search và Google Sheets"
description: "Hướng dẫn cài đặt workflow n8n tự động tìm kiếm brand mention qua Brave Search, lọc thông minh bằng AI, đồng bộ Google Sheets và gửi email thông báo hàng ngày."
slug: "tu-dong-giam-sat-thuong-hieu-n8n-brave-search-gpt"
tags: [n8n, automation, ai-summarization, market-research, openai, google-sheets]
keywords: [n8n workflow, giám sát thương hiệu, brand monitoring, brave search api, openai gpt, tự động hóa marketing]
---

# 🚀 Tự động giám sát thương hiệu 24/7 với GPT, Brave Search và Google Sheets

Các sếp có đang tốn hàng giờ mỗi ngày để "lục tung" internet xem khách hàng, báo chí hay mạng xã hội đang nhắc gì về thương hiệu của mình không? Việc tìm kiếm thủ công vừa mất thời gian, dễ bỏ sót thông tin, lại chẳng thể duy trì liên tục. 

Giải pháp đây rồi! Workflow n8n siêu việt này sẽ thay các sếp "canh gác" không gian mạng 24/7. Sử dụng **Brave Search API** để quét thông tin, kết hợp sức mạnh phân tích ngữ cảnh của **OpenAI (GPT)** để lọc bỏ tin rác, sau đó tự động lưu vào **Google Sheets** và gửi báo cáo qua **Gmail** mỗi ngày. Tự động hóa 100%, không tốn một phút làm thủ công!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần tra cứu thủ công từng từ khóa mỗi ngày.
- **AI thông minh lọc nhiễu:** GPT giúp phân biệt chính xác bài viết nói về thương hiệu của bạn hay chỉ là trùng tên/chủ đề khác.
- **Chống trùng lặp tuyệt đối:** Hệ thống tự động đối chiếu với Google Sheets lịch sử để chỉ báo cáo các bài viết **mới tinh**.
- **Chủ động nắm bắt thông tin:** Nhận email tổng hợp Brand Mention mỗi ngày một cách gọn gàng, chuyên nghiệp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n (Cloud hoặc Self-hosted).
- Tài khoản **Brave Search API** (để lấy khóa API tìm kiếm).
- Tài khoản **OpenAI API** (để sử dụng mô hình GPT xác thực nội dung).
- Tài khoản **Google Sheets & Gmail** (kết nối qua OAuth2).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này hoặc copy toàn bộ mã nguồn JSON, sau đó paste trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình các thông số quan trọng sau trong các node tương ứng:

- **Node `Set Config` & `Set keyword and description`**: Nơi các sếp định nghĩa từ khóa thương hiệu (`Keyword`), mô tả chi tiết ngữ cảnh (`Keyword Description`), các biến thể tìm kiếm (`Dorky` - mảng các câu lệnh search) và danh sách tên miền cần loại trừ (`Banned Domains`).
- **Node `Brave Search`**: Kết nối credentials của Brave Search API để cho phép workflow thực hiện lệnh tìm kiếm trong 24 giờ qua.
- **Node `Message a model` (OpenAI)**: Chọn credentials OpenAI API và thiết lập System/User Prompt để AI đóng vai trò thẩm định bài viết có thực sự liên quan đến thương hiệu không.
- **Node `Check & Log to Sheet` & `InsertSentRows` (Google Sheets)**: 
  - Kết nối tài khoản Google Sheets OAuth2.
  - Trỏ tới file Google Sheet dùng làm bộ nhớ lịch sử (để check trùng URL) và lưu các bài viết mới đã gửi.
- **Node `Send Email` (Gmail)**: Kết nối tài khoản Gmail cá nhân/doanh nghiệp để gửi bản tin tóm tắt kết quả mới mỗi ngày.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** để chạy thử thủ công (Test run) với dữ liệu từ trigger `Every Day`.
- Kiểm tra kết quả trả về ở Google Sheets và Email xem đã mượt mà chưa.
- Sau khi test thành công, gạt công tắc sang **Active** để hệ thống tự động chạy ngầm mỗi ngày.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa kênh thông báo:** Ngoài Gmail, các sếp có thể gắn thêm node Telegram hoặc Slack ở cuối luồng để nhận thông báo "nóng" ngay lập tức khi có bài viết lớn nhắc đến thương hiệu.
- **Tùy biến tần suất:** Thay vì `Every Day` (Schedule Trigger), các sếp có thể chỉnh chạy theo giờ (`Every X hours`) nếu thương hiệu của các sếp có độ phủ sóng cực lớn và cần update liên tục.
- **Mở rộng nguồn quét:** Có thể kết hợp thêm các node RSS feed hoặc Social Listening API khác đổ về chung một luồng xử lý AI của n8n.

### 📌 Kết luận
Một workflow hoàn hảo cho các Marketer, Founder hay PR Agency muốn tối ưu hóa quy trình theo dõi sức khỏe thương hiệu (Brand Monitoring) bằng AI. Thiết lập một lần, chạy êm ái trọn đời. Chúc các sếp cài đặt thành công!