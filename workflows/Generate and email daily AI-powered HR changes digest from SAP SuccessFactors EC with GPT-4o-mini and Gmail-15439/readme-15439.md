---
title: "🚀 Tự động hóa bản tin nhân sự hàng ngày từ SAP SuccessFactors bằng AI và n8n"
description: "Hướng dẫn cài đặt workflow n8n tự động lấy dữ liệu biến động nhân sự từ SAP SuccessFactors, tổng hợp bằng GPT-4o-mini và gửi báo cáo qua Gmail mỗi sáng."
slug: "tu-dong-hoa-ban-tin-nhan-su-sap-successfactors-ai-n8n"
tags: [n8n, automation, sap-successfactors, ai-summarization, gmail, hr]
keywords: [n8n workflow, sap successfactors ec, gpt-4o-mini, tự động hóa nhân sự, hr digest email]
---

# 🚀 Tự động hóa bản tin nhân sự hàng ngày từ SAP SuccessFactors bằng AI và n8n

Trong các doanh nghiệp lớn, đội ngũ Nhân sự (HR) thường phải tốn hàng giờ mỗi ngày để rà soát các biến động nhân sự như nhân viên mới, nghỉ việc, thuyên chuyển nội bộ hay thay đổi địa chỉ trên hệ thống SAP SuccessFactors Employee Central (EC). Việc tổng hợp thủ công này vừa nhàm chán, tốn thời gian lại dễ xảy ra sai sót.

Workflow n8n này sinh ra để giải quyết triệt để "nỗi đau" đó! Hệ thống sẽ tự động quét dữ liệu từ SAP SuccessFactors vào mỗi buổi sáng, dùng **GPT-4o-mini** để phân tích, cô đọng thông tin thành một bản tin (digest) súc tích, chuyên nghiệp và gửi thẳng tới hộp thư của ban lãnh đạo hoặc đội ngũ HR qua **Gmail** hoàn toàn tự động.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tuyệt đối**: Thay vì thủ công tra cứu 4-5 báo cáo khác nhau trên SAP SF, bản tin tổng hợp xuất hiện sẵn sàng trong email vào 6:30 sáng mỗi ngày.
- **Báo cáo thông minh bằng AI**: GPT-4o-mini giúp lọc bỏ thông tin rườm rà, làm nổi bật các biến động quan trọng kèm theo văn phong chuyên nghiệp.
- **Giám sát lỗi tự động**: Workflow có cơ chế kiểm tra lỗi hệ thống (Critical Errors) và tự động gửi email cảnh báo cho quản trị viên nếu kết nối SAP SF gặp sự cố.
- **Vận hành bền vững 24/7**: Kết hợp lịch trình tự động (Schedule Trigger) và khả năng kích hoạt thủ công (Manual Trigger) khi cần test.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động mượt mà, các sếp cần chuẩn bị sẵn:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản SAP SuccessFactors (EC)** với quyền API để gọi dữ liệu (New Hires, Terminations, Transfers, Address Changes). Chuẩn bị thông tin Base URL và phương thức xác thực (Basic Auth hoặc OAuth 2.0).
- **OpenAI API Key** (Sử dụng model `gpt-4o-mini` tiết kiệm và thông minh).
- **Tài khoản Gmail** đã cấu hình Credentials trên n8n để gửi email báo cáo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc sao chép mã nguồn JSON.
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File** / **Paste Workflow JSON** để đưa toàn bộ 19 nodes lên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần tinh chỉnh các node cốt lõi sau để hệ thống chạy đúng môi trường thực tế:
- **Node `Set Config Variables`**: Cập nhật lại các biến cấu hình cơ bản như Base URL của SAP SuccessFactors, email người nhận bản tin (Digest Recipient) và email nhận cảnh báo lỗi (Error Recipient).
- **Các node gọi API SAP SF (`Fetch New Hires`, `Fetch Terminated Employees`, `Fetch Internal Transfers`, `Fetch Address Changes`)**: 
  - Cấu hình Credentials kết nối đến SAP SuccessFactors (Basic Auth hoặc token tương ứng).
  - Kiểm tra lại các OData API Endpoint/Entity phù hợp với cấu trúc SuccessFactors của công ty các sếp.
- **Node `Request AI Completion`**: 
  - Cung cấp OpenAI API Key.
  - Kiểm tra lại Model Name (mặc định là `gpt-4o-mini`) và prompt truyền vào trong node `Create AI Prompt` để đảm bảo văn phong báo cáo đúng ý muốn.
- **Các node Gmail (`Email Digest via Gmail` & `Email Error Report via Gmail`)**:
  - Chọn Credentials Gmail đã được cấp quyền OAuth2 hoặc App Password trên n8n để gửi email thành công.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** ở chế độ thủ công (thông qua node `When Triggered Manually`) để test một vòng xem dữ liệu có kéo về thành công từ SAP SF và AI có sinh ra bản tin đúng hạn không.
- Sau khi test xanh mướt, gạt công tắc **Active** tại góc trên bên phải để kích hoạt lịch chạy tự động lúc 06:30 sáng mỗi ngày từ node `When 06:30AM Daily`.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh liên lạc nội bộ**: Thay vì chỉ nhận email, các sếp có thể nối thêm node **Slack** hoặc **Telegram** sau bước `Draft Digest Email` để đẩy bản tin nhân sự trực tiếp lên group chat chung của ban lãnh đạo.
- **Lưu lịch sử vào Google Sheets**: Thêm node Google Sheets vào nhánh `Log Digest Summary` để lưu trữ lịch sử các biến động nhân sự hàng ngày phục vụ cho việc thống kê, phân tích dữ liệu dài hạn (HR Analytics).
- **Tùy chỉnh lịch chạy**: Có thể điều chỉnh node `ScheduleTrigger` thành nhiều mốc thời gian khác nhau trong ngày nếu công ty có nhu cầu cập nhật realtime liên tục.

### 📌 Kết luận
Workflow tự động hóa bản tin nhân sự từ SAP SuccessFactors kết hợp GPT-4o-mini này là một "vũ khí" lợi hại giúp tự động hóa khâu báo cáo nhân sự, giảm tải công việc thủ công cho đội ngũ HR và mang lại trải nghiệm chuyên nghiệp cho ban lãnh đạo. Hãy tiến hành import và cấu hình ngay hôm nay để tối ưu hóa vận hành doanh nghiệp các sếp nhé!