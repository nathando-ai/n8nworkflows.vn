---
title: "🚀 Tự động hóa trích xuất task từ Google Docs vào GoHighLevel CRM bằng AI GPT-4"
description: "Hướng dẫn cấu hình workflow n8n tự động quét Google Drive, dùng AI trích xuất task từ Google Docs và tạo task trên GoHighLevel CRM, gửi email tổng kết."
slug: "tu-dong-hoa-trich-xuat-task-google-docs-gohighlevel-crm-gpt4"
tags: [n8n, automation, no-code, gpt-4, gohighlevel, google-docs, ai-agent]
keywords: [n8n workflow, trích xuất task, google docs gohighlevel, ai agent ghl, tự động hóa crm]
---

# 🚀 Tự động hóa trích xuất task từ Google Docs vào GoHighLevel CRM bằng GPT-4

Các sếp có bao giờ cảm thấy ngợp thở sau một ngày dài họp hành? Hàng đống ghi chú họp trên Google Docs, các action items (công việc cần làm) bị bỏ sót, việc nhập thủ công vào GoHighLevel (GHL) CRM vừa tốn thời gian lại dễ sai sót. 

Đừng lo, workflow n8n này chính là giải pháp tự động hóa 100% không cần code giúp các sếp giải quyết triệt để bài toán này. Hệ thống sẽ tự động quét thư mục họp mỗi ngày, tổ chức lại tệp, sử dụng AI (GPT-4) thông minh để phân tích ghi chú, tìm kiếm khách hàng trong CRM, tạo task giao việc tự động và gửi email tổng kết báo cáo cho các sếp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không cần phải đọc lại ghi chú dài dòng và gõ tay từng task vào CRM nữa.
- **Không bỏ sót việc:** AI tự động định danh action items, thời hạn (due date) và gắn đúng khách hàng.
- **Tổ chức khoa học:** Tự động phân loại tài liệu họp (Bản ghi âm, Ghi chú, Chat log) vào đúng thư mục trên Google Drive.
- **Báo cáo tức thì:** Nhận email tổng hợp chi tiết qua Gmail ngay sau khi hệ thống chạy xong.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị sẵn các tài khoản và credentials sau:
- **Google Drive OAuth2 API**: Để quét và di chuyển file.
- **Google Docs OAuth2 API**: Để đọc nội dung ghi chú cuộc họp.
- **GoHighLevel OAuth2 API**: Để tìm kiếm contact và tạo task trong CRM.
- **Gmail OAuth2**: Để gửi email báo cáo tổng kết.
- **OpenAI API (GPT-4 / GPT-5 model)**: Bộ não AI thông minh để phân tích nội dung cuộc họp.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này, vào giao diện n8n Editor, chọn **New Workflow** -> Bấm tổ hợp phím `Ctrl + V` (hoặc `Cmd + V`) để dán toàn bộ các node vào màn hình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình lại các thành phần sau để hệ thống chạy đúng ý muốn:

- **DAILY ORGANIZATION TRIGGER**: Node này dùng `scheduleTrigger` để hẹn giờ chạy hàng ngày (ví dụ: cuối ngày làm việc hoặc sáng sớm). Các sếp chỉnh lại khung giờ cho phù hợp.
- **FIND MEETING RECORD FOLDER**: Kết nối tài khoản Google Drive và trỏ tới thư mục chứa các bản ghi/ghi chú họp gốc của các sếp.
- **Các node di chuyển file (MOVE RECORDINGS, MOVE NOTES, MOVE CHAT)**: Cấu hình ID thư mục đích trên Google Drive để tự động gom nhóm file sau khi xử lý xong (Tránh rác thư mục gốc).
- **GET NOTES & FILTER FOR NOTES**: Đảm bảo node lấy đúng nội dung từ Google Docs meeting notes.
- **ORGANIZATION AGENT & SUMMARIZATION AGENT (LangChain Agents + OpenAI Chat Model)**: 
  - Chọn credential OpenAI.
  - Tinh chỉnh System Prompt trong Agent nếu cần để AI hiểu đúng quy chuẩn đặt tên task hoặc định dạng ngày tháng của công ty các sếp.
- **FIND CONTACT IN GHL & CREATE TASKS IN GHL**: Kết nối GoHighLevel OAuth2, chọn đúng Location/Sub-account của các sếp để tool có thể tìm đúng contact và tạo task giao việc.
- **SEND EMAIL TO LEO (Gmail Tool)**: Điền địa chỉ email cá nhân của các sếp vào node này để nhận email HTML tổng kết công việc.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** chạy thử dữ liệu mẫu (Test run) để kiểm tra xem các bước Google Drive -> AI -> GoHighLevel có hoạt động trơn tru không.
- Nếu mọi thứ xanh mướt (success), các sếp bật công tắc **Active** ở góc trên bên phải để workflow tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm ChatOps**: Thay vì chỉ nhận email qua Gmail, các sếp có thể nối thêm node Telegram hoặc Slack để bắn thông báo task trực tiếp vào group chat của team.
- **Lưu log vào Google Sheets**: Thêm một node Google Sheets ở cuối luồng để lưu lại lịch sử các task đã được AI tạo tự động, phục vụ việc kiểm tra chéo (audit) hàng tuần.
- **Mở rộng bộ nhớ AI**: Tận dụng tính năng `Simple Memory` có sẵn trong workflow để AI có ngữ cảnh tốt hơn nếu các cuộc họp liên tiếp có sự liên kết chặt chẽ về mặt nội dung.

### 📌 Kết luận
Tự động hóa quy trình quản lý sau họp chưa bao giờ dễ dàng đến thế với sức mạnh của n8n kết hợp cùng AI Agents. Hãy cài đặt ngay workflow này để giải phóng bản thân khỏi những công việc thủ công nhàm chán và tập trung vào các chiến lược kinh doanh cốt lõi, các sếp nhé!