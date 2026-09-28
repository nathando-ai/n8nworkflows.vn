---
title: "🚀 Tự động tạo bản tóm tắt cuộc họp AI với Google Calendar, GPT-4 và MadKudu MCP"
description: "Hướng dẫn xây dựng trợ lý AI tự động nghiên cứu khách mời, công ty đối tác và tạo meeting brief cực kỳ chuyên nghiệp ngay trên Google Calendar bằng n8n."
slug: "tu-dong-tao-tom-tat-cuoc-hop-ai-google-calendar-gpt-4-madkudu"
tags: [n8n, automation, no-code, google-calendar, openai, ai-agent, crm]
keywords: [n8n workflow, tự động hóa google calendar, gpt-4 meeting brief, madkudu mcp, ai agent nghiên cứu khách hàng]
---

# 🚀 Tự động tạo bản tóm tắt cuộc họp AI với Google Calendar, GPT-4 và MadKudu MCP

Các sếp có từng mệt mỏi vì phải lục lọi LinkedIn, CRM hay Google để tìm thông tin về khách hàng trước mỗi cuộc họp quan trọng không? Việc tra cứu thủ công này tốn rất nhiều thời gian mà đôi khi vẫn bỏ sót thông tin cốt lõi. 

Giải pháp ư? Workflow n8n này sẽ đóng vai trò như một **Trợ lý AI chuẩn bị họp (Meeting Prep AI Assistant)** tự động 100%. Hệ thống sẽ tự quét lịch họp hàng giờ, lọc ra các cuộc gặp với đối tác/khách hàng bên ngoài, sử dụng AI kết hợp **MadKudu MCP** để nghiên cứu sâu về khách mời và tự động cập nhật bản tóm tắt chi tiết vào lịch của các sếp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm hàng giờ tra cứu:** Không cần thủ công tìm kiếm thông tin khách hàng trên Google hay LinkedIn trước giờ họp.
- **Tự tin "chốt sales":** Nắm bắt toàn bộ bối cảnh công ty, lịch sử tương tác và thông tin về người tham dự ngay trong phần mô tả sự kiện.
- **Bảo mật tuyệt đối:** Bản tóm tắt được thêm vào sự kiện riêng tư trên lịch của chính các sếp, đối tác sẽ không nhìn thấy.
- **Hoạt động tự động 24/7:** Chạy ngầm liên tục hàng giờ để chuẩn bị sẵn sàng cho mọi lịch trình sắp tới.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Cloud hoặc Self-hosted).
- Tài khoản **Google Account** (có quyền truy cập Google Calendar).
- Tài khoản **OpenAI API** (để sử dụng model `gpt-4.1-mini`).
- Tài liệu / kết nối tới **MadKudu MCP (Model Context Protocol)** để truy vấn dữ liệu công ty và khách hàng.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trong n8n, sau đó copy toàn bộ mã nguồn JSON của workflow (hoặc tải file từ trang chủ n8n) và dán trực tiếp vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động mượt mà, các sếp cần cấu hình chính xác các node trọng điểm sau:

- **Schedule Trigger**: Node này được cấu hình chạy định kỳ mỗi giờ để quét các cuộc họp diễn ra trong 1 giờ tới. Các sếp có thể điều chỉnh lại tần suất nếu lịch họp thưa hơn.
- **Get many events (Google Calendar)**: Kết nối tài khoản Google Calendar thông qua `Google Calendar OAuth2 API` để lấy danh sách sự kiện sắp tới.
- **Keep meetings with external attendees (Filter)**: 
  - Các sếp cần đặt biến công ty `my_company_domain` (ví dụ: `acme.com`) trong phần n8n Variables.
  - Node này dùng để lọc và **chỉ giữ lại các cuộc họp có ít nhất 1 khách mời bên ngoài** (có tên miền email khác với công ty của các sếp), giúp tránh lãng phí tài nguyên AI cho các cuộc họp nội bộ.
- **OpenAI Model & AI Agent - Research Attendees**: 
  - Kết nối `OpenAI API Credentials`.
  - Chọn model AI là `gpt-4.1-mini`.
  - AI Agent sẽ phối hợp cùng **MadKudu MCP** để thực hiện phân tích sâu về profile khách hàng và tổng hợp thông tin.
- **Send summary as event (Google Calendar)**: Tạo một sự kiện riêng tư trùng thời gian với cuộc họp gốc, đính kèm toàn bộ bản tóm tắt AI (Meeting Brief) vào phần mô tả (Description).

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** với một mốc thời gian giả lập để test xem luồng chạy có suôn sẻ không.
- Sau khi kiểm tra dữ liệu trả về chuẩn chỉnh, gạt công tắc sang **Active** để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh chat:** Thay vì chỉ lưu trên Calendar, các sếp có thể nối thêm một node Telegram hoặc Slack để bot chủ động "gõ cửa" báo cáo thông tin tóm tắt trước giờ họp 15 phút.
- **Lưu trữ lịch sử CRM:** Kết nối thêm HubSpot hoặc Salesforce để ghi nhận lịch sử chuẩn bị họp tự động.
- **Mở rộng nguồn dữ liệu MCP:** Tích hợp thêm các công cụ MCP khác ngoài MadKudu để AI có góc nhìn đa chiều hơn về khách hàng tiềm năng.

### 📌 Kết luận
Với workflow n8n này, các sếp đã sở hữu ngay một trợ lý AI đắc lực, giúp nâng tầm chuyên nghiệp trong mọi cuộc gặp gỡ đối tác mà không tốn một giọt mồ hôi nghiên cứu thủ công. "Lên đồ" ngay cho hệ thống n8n của mình thôi nào các sếp!