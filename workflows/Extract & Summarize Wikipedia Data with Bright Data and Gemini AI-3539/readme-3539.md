---
title: "🚀 Tự động trích xuất và tóm tắt dữ liệu Wikipedia với Bright Data và Gemini AI"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình cào dữ liệu Wikipedia thông qua Bright Data và sử dụng sức mạnh Gemini AI để trích xuất, tóm tắt nội dung cực kỳ nhanh chóng."
slug: "trich-xuat-va-tom-tat-wikipedia-bright-data-gemini-ai"
tags: [n8n, automation, ai, gemini, bright-data, web-scraping]
keywords: [n8n workflow, trích xuất dữ liệu wikipedia, tóm tắt ai, bright data, gemini ai, n8n automation]
---

# 🚀 Tự động trích xuất và tóm tắt dữ liệu Wikipedia với Bright Data và Gemini AI

Các sếp có bao giờ cảm thấy ngợp trước những bài viết Wikipedia dài dằng dặc, cần đọc hiểu và tóm tắt nhanh nhưng lại mất quá nhiều thời gian copy-paste thủ công? Hoặc việc cào dữ liệu từ các trang web lớn thường xuyên gặp tình trạng bị chặn IP, gây gián đoạn công việc nghiên cứu và tổng hợp thông tin?

Đừng lo, giải pháp tự động hóa 100% không cần code dưới đây sẽ giúp các sếp giải quyết triệt để vấn đề này! Workflow n8n kết hợp giữa **Bright Data** (giải pháp cào dữ liệu vượt tường lửa thông minh) và **Google Gemini AI** sẽ tự động thực hiện từ A-Z: gọi dữ liệu, làm sạch nội dung HTML, trích xuất văn bản dễ đọc và tạo ra bản tóm tắt súc tích trong chớp mắt.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Chỉ cần nhập URL Wikipedia và kích hoạt, mọi việc còn lại để AI lo.
- **Vượt rào cản cào dữ liệu:** Sử dụng Bright Data Zone để đảm bảo yêu cầu lấy dữ liệu từ Wikipedia luôn thành công mà không sợ bị chặn.
- **Trích xuất thông minh:** Node `LLM Data Extractor` chuyển đổi dữ liệu HTML thô thành văn bản sạch sẽ, chuẩn ngữ nghĩa người đọc.
- **Tóm tắt chuyên sâu:** Node `Concise Summary Generator` sử dụng Google Gemini AI để chắt lọc những ý chính đắt giá nhất.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Bright Data Account:** Cần có tài khoản và cấu hình Zone để thực hiện `Wikipedia Web Request`.
- **Google Gemini API Key:** Tài khoản Google AI Studio để kết nối với các mô hình ngôn ngữ lớn (LLM).
- **Webhook Endpoint (Tùy chọn):** URL nhận thông báo kết quả từ `Summary Webhook Notifier`.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp hãy copy đoạn mã JSON của workflow này và dán trực tiếp vào n8n Editor của mình, hoặc sử dụng tính năng import file JSON từ giao diện chính.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống vận hành trơn tru, các sếp cần chú ý cấu hình các node cốt lõi sau:

- **Set Wikipedia URL with Bright Data Zone:** 
  - Cập nhật lại đường dẫn URL Wikipedia mục tiêu và cấu hình thông số kết nối thông qua Bright Data Zone của sếp.
- **Wikipedia Web Request (HTTP Request):** 
  - Thiết lập thông tin xác thực (`httpHeaderAuth`) tương ứng với tài khoản Bright Data để gửi request mượt mà.
- **Google Gemini Chat Model For Summarization & Model 2:** 
  - Thêm Credentials `googlePalmApi` bằng cách điền API Key lấy từ Google AI Studio. (Các sếp hoàn toàn có thể đổi sang OpenAI hoặc các nhà cung cấp LLM khác nếu muốn).
- **Summary Webhook Notifier (HTTP Request):** 
  - Cập nhật URL Webhook đích của các sếp (ví dụ: Discord, Slack, Make, hoặc hệ thống nội bộ) để nhận bản tóm tắt tự động.

#### 3. Kích hoạt ⚡️
- Nhấn **‘Test workflow’** bằng tay (`When clicking ‘Test workflow’`) để kiểm tra toàn bộ chuỗi xử lý dữ liệu từ đầu đến cuối.
- Kiểm tra kết quả trả về ở các node AI và Webhook, sau đó gạt công tắc **Active** để đưa workflow vào hoạt động chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh nhận tin:** Thay vì chỉ dùng Webhook HTTP Request đơn thuần, các sếp có thể tích hợp thêm node Telegram hoặc Slack để bắn kết quả tóm tắt trực tiếp vào group chat công việc.
- **Lưu trữ dữ liệu tự động:** Nối thêm một node Google Sheets hoặc Airtable vào cuối luồng để lưu lại lịch sử các bài viết đã được tóm tắt phục vụ cho việc tra cứu sau này.
- **Tùy chỉnh Prompt cho AI:** Tùy biến prompt bên trong các LangChain nodes để AI tóm tắt theo phong cách ngắn gọn, dạng bullet-point hoặc theo định dạng báo cáo chuyên nghiệp tùy theo nhu cầu doanh nghiệp.

### 📌 Kết luận
Workflow tích hợp Bright Data và Gemini AI này là một "vũ khí" cực kỳ lợi hại giúp tối ưu hóa thời gian xử lý thông tin, nghiên cứu thị trường hoặc tổng hợp tài liệu học tập, truyền thông. Hãy cài đặt ngay hôm nay để giải phóng sức lao động thủ công cho đội ngũ của mình các sếp nhé!