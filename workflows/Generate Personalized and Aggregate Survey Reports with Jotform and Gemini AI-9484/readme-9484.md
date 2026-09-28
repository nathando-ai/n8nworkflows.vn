---
title: "🚀 Tự động hóa báo cáo khảo sát với Jotform và Gemini AI trên n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động phân tích phản hồi khảo sát từ Jotform bằng Gemini AI, gửi báo cáo cá nhân hóa cho người dùng và tổng hợp báo cáo hàng tuần cho admin."
slug: "tu-dong-hoa-bao-cao-khao-sat-jotform-gemini-ai"
tags: [n8n, automation, no-code, jotform, ai, gemini, gmail]
keywords: [n8n workflow, jotform automation, gemini ai n8n, tu dong hoa khao sat, tao bao cao tu dong]
---

# 🚀 Tự động hóa báo cáo khảo sát với Jotform và Gemini AI

Các sếp có bao giờ cảm thấy mệt mỏi khi phải thủ công tổng hợp hàng trăm câu trả lời khảo sát từ khách hàng hoặc nhân viên, sau đó lại phải mất hàng giờ viết email cảm ơn kèm theo phân tích cá nhân hóa cho từng người? Việc này không chỉ tốn thời gian mà còn dễ gây chậm trễ, làm giảm trải nghiệm của người tham gia.

Đừng lo, bài toán này sẽ được giải quyết triệt để 100% bằng tự động hóa! Workflow n8n này sẽ giúp các sếp kết hợp sức mạnh của **Jotform** và **Google Gemini AI** để tự động xử lý mọi phản hồi ngay khi được gửi lên, đồng thời lên lịch tổng hợp báo cáo định kỳ mỗi tuần gửi thẳng về email cho Admin.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phản hồi tức thì:** Gửi báo cáo cá nhân hóa, lời khuyên và insights chi tiết cho người trả lời khảo sát chỉ trong vài giây sau khi họ submit form.
- **Báo cáo tổng quan tự động:** Hệ thống tự gom nhóm, phân tích xu hướng và gửi báo cáo thống kê hàng tuần cho Admin mà không cần đụng tay.
- **Ứng dụng AI thông minh:** Tận dụng Google Gemini (qua các node LangChain) để đọc hiểu ngữ nghĩa, trích xuất dữ liệu dạng cấu trúc JSON sạch sẽ.
- **Hoạt động 24/7:** Chạy ngầm liên tục, đảm bảo không bỏ sót bất kỳ phản hồi khảo sát nào.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Self-hosted hoặc Cloud).
- **Tài khoản Jotform** để tạo biểu mẫu khảo sát.
- **Google Gemini API Key** để AI phân tích nội dung khảo sát.
- **Tài khoản Gmail** (hoặc cấu hình SMTP) để gửi email tự động cho người tham gia và Admin.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này hoặc copy trực tiếp mã nguồn JSON, sau đó dán vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình các node cốt lõi sau:

- **Form Submission Trigger (`jotFormTrigger`):** Kết nối tài khoản Jotform của các sếp và chọn đúng Form ID khảo sát muốn theo dõi. Node này đóng vai trò bắt sự kiện khi có người submit form.
- **Weekly Report Scheduler (`scheduleTrigger`):** Cấu hình mốc thời gian (ví dụ: Thứ Hai hàng tuần lúc 8:00 sáng) để kích hoạt quá trình quét toàn bộ phản hồi tuần qua.
- **Fetch Survey Submissions (`httpRequest`):** Điền API Key và Endpoint của Jotform để lấy danh sách toàn bộ submissison khi lịch trình hàng tuần được kích hoạt.
- **Gemini LLM (Personal) & Gemini LLM (`lmChatGoogleGemini`):** Nhập Google Gemini API Credentials cho các node AI Agent. Node này sẽ chịu trách nhiệm viết nội dung phân tích cá nhân hóa cũng như tóm tắt xu hướng tổng quan.
- **Structured Output Parser & Parse Personal Report JSON (`outputParserStructured`):** Thiết lập schema định dạng JSON để đảm bảo AI trả về kết quả chuẩn xác, dễ dàngmapping sang email.
- **Send Personal Report & Send Report to Admin (`gmail`):** Kết nối tài khoản Gmail cá nhân/doanh nghiệp để gửi email HTML chứa báo cáo đến người dùng và quản trị viên.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và test thử bằng cách điền một form mẫu trên Jotform để kiểm tra luồng chạy cá nhân.
- Sau khi kiểm tra mọi thứ hoàn tất, bật công tắc **Active** ở góc trên bên phải để workflow chính thức vận hành tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa dạng hóa kênh thông báo:** Ngoài Gmail, các sếp có thể gắn thêm node Telegram hoặc Slack để bắn tin nhắn thông báo ngay lập tức về điện thoại khi có khách hàng VIP điền khảo sát.
- **Lưu trữ dữ liệu:** Thêm node Google Sheets hoặc Airtable ngay sau bước xử lý để lưu trữ lịch sử khảo sát phục vụ cho việc thống kê dài hạn.
- **Cải tiến Prompt AI:** Tùy biến system prompt trong các AI Agent để văn phong phản hồi phù hợp hơn với lĩnh vực kinh doanh của công ty (Ví dụ: thân thiện, chuyên nghiệp, hài hước...).

### 📌 Kết luận
Workflow tự động hóa khảo sát với Jotform và Gemini AI là giải pháp tuyệt vời giúp tối ưu hóa chăm sóc khách hàng và thu thập feedback thời gian thực. Hãy triển khai ngay hôm nay để tiết kiệm hàng chục giờ làm việc thủ công mỗi tuần cho đội ngũ của bạn!