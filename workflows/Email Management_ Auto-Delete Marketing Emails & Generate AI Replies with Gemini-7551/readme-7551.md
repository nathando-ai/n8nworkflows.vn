---
title: "🚀 Tự động hóa quản lý email: Xóa email rác và tạo phản hồi AI thông minh với Gemini"
description: "Hướng dẫn xây dựng workflow n8n tự động phân loại email đến, xóa email marketing rác và sử dụng Google Gemini để soạn thảo câu trả lời thông minh cho khách hàng."
slug: "tu-dong-hoa-quan-ly-email-gemini-n8n"
tags: [n8n, automation, no-code, gmail, google-gemini, google-sheets]
keywords: [n8n workflow, tự động hóa email, xóa email marketing, google gemini ai, quản lý email tự động]
---

# 🚀 Tự động hóa quản lý email: Xóa email rác và tạo phản hồi AI thông minh với Gemini

Các sếp có bao giờ cảm thấy ngợp thở mỗi sáng mở hộp thư ra và thấy hàng tá email quảng cáo rác, email marketing ngập tràn, trong khi email quan trọng của khách hàng thì lại bị trôi mất? Việc phân loại, xóa rác và ngồi viết email phản hồi thủ công chiếm mất hàng giờ đồng hồ mỗi ngày, làm giảm năng suất làm việc trầm trọng.

Đừng lo, với workflow n8n kết hợp sức mạnh siêu việt của **Google Gemini AI**, các sếp sẽ có ngay một "thư ký ảo" tự động 100%: tự động quét email, nhận diện và xóa sạch email rác, đồng thời soạn thảo sẵn câu trả lời chuyên nghiệp cho khách hàng thực sự. Tất cả được quản lý gọn gàng trên Google Sheets!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian**: Không còn phải lọc thủ công từng email rác hay loay hoay nghĩ câu trả lời cho khách.
- **Phân loại thông minh**: Google Gemini AI tự động phân biệt đâu là email quảng cáo, đâu là email khách hàng thực tế với độ chính xác cao.
- **Tự động hóa toàn diện**: Tự động xóa email marketing và tự động soạn thảo/gửi phản hồi cho khách hàng ngay lập tức khi có email mới.
- **Lưu trữ minh bạch**: Mọi hoạt động (xóa email hay trả lời email) đều được ghi log chi tiết vào Google Sheets để dễ dàng theo dõi và kiểm tra.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn:
- Tài khoản **n8n** (Cloud hoặc Self-hosted).
- Tài khoản **Google Workspace / Gmail** (để đọc, gửi, xóa email và kết nối IMAP).
- Tài khoản **Google Sheets** (để tạo bảng lưu log theo dõi).
- **Google Gemini API Key** (hoặc cấu hình Credential Google Gemini trong n8n).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy đoạn mã JSON của workflow này và paste trực tiếp vào giao diện n8n Editor của mình, hoặc tải file JSON về và import thông qua menu `Import from File`.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà không gặp lỗi, các sếp cần cấu hình chính xác các node quan trọng sau:

- **Email Trigger (IMAP)** hoặc **Get many messages (Gmail)**: Kết nối với tài khoản Gmail của các sếp để hệ thống bắt được email mới đến ngay lập tức.
- **Message a model (Google Gemini)**: Cấu hình API Key của Google Gemini. Node này chịu trách nhiệm đóng vai trò AI phân tích nội dung email:
  - Kiểm tra xem có phải email marketing không -> trả về flag `isMarketing: true/false`.
  - Nếu không phải email marketing -> tự động soạn sẵn nội dung phản hồi khách hàng cực kỳ lịch sự và chuyên nghiệp.
- **AI response formatter (Set)**: Chuẩn hóa lại dữ liệu đầu ra từ AI để các bước tiếp theo dễ dàng xử lý.
- **categories emails (Switch)**: Node rẽ nhánh thông minh dựa trên kết quả của Gemini:
  - Nhánh 1 (Email Marketing): Chuyển đến node **Delete a message** để xóa vĩnh viễn khỏi hòm thư.
  - Nhánh 2 (Email Khách hàng): Chuyển đến node **Reply to a message** để gửi phản hồi tự động.
- **Append or update row in sheet / sheet1 (Google Sheets)**: Kết nối tới file Google Sheets chuẩn bị sẵn để ghi lại lịch sử các email đã xóa hoặc đã trả lời kèm theo tiêu đề email phục vụ việc kiểm tra, kiểm toán (audit).
- **When clicking ‘Execute workflow’ / Manual Trigger**: Dùng để test thủ công khi các sếp muốn chạy thử nghiệm workflow.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** và gửi một vài email mẫu đến hộp thư của các sếp để kiểm tra xem AI phân loại, xóa rác và phản hồi có chính xác chưa.
- Sau khi test ngon lành, hãy bật nút **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo qua Telegram/Slack**: Các sếp có thể gắn thêm node Telegram vào sau bước xử lý của AI để nhận thông báo tức thời ngay khi có khách hàng tiềm năng gửi email đến.
- **Tùy chỉnh Prompt cho Gemini**: Tinh chỉnh lại câu lệnh (prompt) trong node Gemini để AI xưng hô, văn phong phù hợp hơn với sản phẩm hoặc dịch vụ đặc thù của doanh nghiệp các sếp.
- **Báo cáo định kỳ**: Tạo thêm một nhánh chạy theo lịch trình (Schedule Trigger) mỗi tuần để tổng hợp số lượng email marketing đã bị xóa và số lượng khách hàng đã được chăm sóc gửi vào email cá nhân của quản lý.

### 📌 Kết luận
Việc tự động hóa quản lý email chưa bao giờ dễ dàng và thông minh đến thế nhờ sự kết hợp giữa n8n và Google Gemini. Hãy cài đặt ngay workflow này để giải phóng thời gian cho đội ngũ và không bao giờ bỏ lỡ bất kỳ khách hàng quan trọng nào nữa các sếp nhé!