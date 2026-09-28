---
title: "🚀 Quản lý Streak CRM qua WhatsApp bằng GPT-4 và Gemini trên n8n"
description: "Hướng dẫn xây dựng trợ lý AI tự động hóa Streak CRM trực tiếp qua WhatsApp, hỗ trợ xử lý tin nhắn văn bản, hình ảnh và giọng nói bằng GPT-4 và Google Gemini."
slug: "quan-ly-streak-crm-qua-whatsapp-gpt4-gemini"
tags: [n8n, automation, streak-crm, whatsapp, ai-agent, gpt-4, gemini]
keywords: [n8n workflow, streak crm whatsapp, ai crm assistant, gpt-4 n8n, gemini n8n]
---

# 🚀 Quản lý Streak CRM qua WhatsApp bằng GPT-4 và Gemini

Các sếp có bao giờ cảm thấy mệt mỏi khi phải liên tục chuyển đổi giữa ứng dụng nhắn tin với khách hàng và việc cập nhật thủ công vào Streak CRM? Việc quên cập nhật trạng thái đơn hàng, thông tin khách hàng hay lịch hẹn không chỉ làm giảm hiệu suất mà còn gây bỏ sót cơ hội kinh doanh.

Giải pháp ở đây là gì? Workflow n8n mạnh mẽ này sẽ biến WhatsApp thành một giao diện chat thông minh tích hợp AI (GPT-4 và Gemini). Các sếp chỉ cần nhắn tin văn bản, gửi hình ảnh (như danh thiếp, thẻ công việc) hoặc thậm chí là **gửi tin nhắn thoại (voice note)** qua WhatsApp, AI Agent sẽ tự động phân tích và thực hiện mọi thao tác trên Streak CRM như tạo contact, thêm box vào pipeline, cập nhật stage, tạo task cực kỳ mượt mà.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tương tác đa phương thức:** Nhắn tin văn bản, gửi hình ảnh hoặc ra lệnh bằng giọng nói (voice mail) trực tiếp qua WhatsApp để quản lý CRM.
- **Tự động hóa toàn diện Streak CRM:** Tự động tạo contact, tạo box, cập nhật stage, thêm task và liên kết dữ liệu mà không cần thao tác thủ công trên giao diện web.
- **Trợ lý AI thông minh:** Tích hợp cả GPT-4 và Google Gemini kết hợp với tài liệu API của Streak thông qua Tavily Search, giúp AI hiểu và thực hiện chính xác các yêu cầu phức tạp.
- **Hoạt động 24/7:** Phản hồi khách hàng và cập nhật dữ liệu ngay lập tức mọi lúc mọi nơi.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản WhatsApp Business API** (qua Meta hoặc nhà cung cấp dịch vụ thứ ba) để cấu hình `WhatsApp Trigger` và gửi/nhận tin nhắn.
- **Tài khoản OpenAI API** (dùng cho GPT-4 và xử lý audio/image).
- **Tài khoản Google Gemini API** (Google Palm API).
- **Tài khoản Streak CRM** lấy API Key (Basic Auth).
- **Tài khoản Tavily API** (để AI tra cứu tài liệu Streak CRM khi cần).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này từ n8n.io (Link gốc: [Manage Streak CRM via WhatsApp using GPT-4.1 and Gemini](https://n8n.io/workflows/13218)), sau đó copy toàn bộ JSON và dán trực tiếp vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 29 nodes được chia thành các nhóm xử lý chính. Các sếp cần chú ý cấu hình kỹ các phần sau:

- **WhatsApp Trigger & Send message / Download Nodes:** Kết nối credentials của WhatsApp Business API cho các node `WhatsApp Trigger`, `Send message`, `Download Image`, `Download Voicemail`, `Gets WhatsApp Image Source URL`, `Gets WhatsApp Voicemail Source URL`.
- **AI Models (`OpenAI Chat Model`, `Google Gemini Chat Model`):** Cung cấp API Key của OpenAI và Google để các mô hình ngôn ngữ hoạt động ổn định.
- **Streak CRM Tools (Các node `Streak Tool`):** 
  - Cấu hình `Streak API` credentials (sử dụng API Key của tài khoản Streak dưới dạng Basic Auth).
  - *Lưu ý quan trọng:* Theo hướng dẫn gốc trên canvas, hãy ưu tiên sử dụng các endpoint phiên bản V1 của Streak API cho các HTTP/Tool node, trừ khi tài nguyên đó chỉ có ở phiên bản V2.
- **Tavily Tool (`Streak_Doc`):** Cung cấp `tavilyApi` credentials để AI có thể tự tra cứu tài liệu API của Streak khi cần thực hiện các thao tác phức tạp.
- **Route input Types (`Switch`):** Node này giúp phân loại đầu vào từ WhatsApp (văn bản, hình ảnh hay audio) để chuyển đến các node xử lý tương ứng (`Map text prompt`, `Map image prompt`, hoặc OpenAI Audio/Image translation).

#### 3. Kích hoạt ⚡️
- Gửi thử tin nhắn văn bản mẫu qua WhatsApp tới số cấu hình, ví dụ: *"create contact John Doe"* hoặc gửi một tấm hình danh thiếp để kiểm tra AI Agent.
- Kiểm tra kết quả phản hồi trên WhatsApp và xem dữ liệu đã được cập nhật chính xác trên Streak CRM chưa.
- Bật công tắc **Active** để đưa workflow vào vận hành thực tế.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm kênh thông báo phụ:** Kết nối thêm node Slack hoặc Telegram để gửi thông báo về ban quản lý mỗi khi có deal lớn được tạo hoặc cập nhật trong Streak CRM.
- **Ghi log hoạt động:** Lưu lại lịch sử hội thoại WhatsApp và các thao tác CRM vào Google Sheets để dễ dàng kiểm tra, thống kê hiệu suất làm việc của đội ngũ Sales.
- **Mở rộng công cụ cho AI:** Thêm các tool tùy chỉnh (Custom Operations) nếu các sếp muốn Streak CRM tương tác thêm với các nền tảng khác như Google Calendar hoặc Email Marketing.

### 📌 Kết luận
Với workflow n8n kết hợp giữa WhatsApp, GPT-4 và Streak CRM này, việc quản lý khách hàng trở nên đơn giản hơn bao giờ hết chỉ bằng vài câu lệnh tự nhiên. Hãy triển khai ngay hôm nay để tiết kiệm thời gian và tối ưu hóa quy trình kinh doanh của các sếp!