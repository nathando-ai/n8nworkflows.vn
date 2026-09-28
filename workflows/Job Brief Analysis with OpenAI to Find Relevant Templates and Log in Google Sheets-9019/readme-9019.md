---
title: "🚀 Tự động phân tích Job Brief bằng OpenAI và lưu Template phù hợp vào Google Sheets"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa việc phân tích bản mô tả công việc (job brief), tìm kiếm template phù hợp bằng AI và lưu trữ kết quả trực tiếp vào Google Sheets."
slug: "tu-dong-phan-tich-job-brief-openai-google-sheets"
tags: [n8n, automation, no-code, openai, google-sheets, ai-agent]
keywords: [n8n workflow, phân tích job brief, tự động hóa openai, google sheets automation, ai agent n8n]
---

# 🚀 Tự động phân tích Job Brief bằng OpenAI và tìm kiếm Template phù hợp

Các sếp làm trong ngành sáng tạo nội dung, tuyển dụng hay quản lý dự án chắc chắn đã quá quen thuộc với cảnh tượng: Nhận một bản mô tả công việc (job brief) dài dằng dặc, sau đó phải lục tung kho tài liệu, template cũ kỹ để tìm xem có mẫu nào phù hợp để tái sử dụng hay không. Công việc thủ công này vừa tốn thời gian, vừa dễ bỏ sót ý tưởng hay.

Đừng lo, giải pháp ở đây rồi! Với workflow n8n kết hợp giữa **AI Agent (OpenAI)** và **Google Sheets**, các sếp có thể tự động hóa 100% quy trình này: Gửi job brief vào khung chat, AI sẽ tự động bóc tách từ khóa, tìm kiếm các template liên quan thông qua API và lưu toàn bộ kết quả vào Google Sheets một cách ngăn nắp. Không cần code phức tạp, chỉ cần vài phút cấu hình!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và không lo bị gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** AI tự động đọc hiểu brief và tìm template thay vì phải search thủ công từng từ khóa.
- **Độ chính xác cao:** Trích xuất chính xác 5 từ khóa cốt lõi từ nội dung yêu cầu công việc.
- **Hệ thống hóa dữ liệu:** Tự động lưu trữ thông tin template, đường dẫn (URL), mô tả trực tiếp vào Google Sheets để dễ dàng tra cứu.
- **Hoạt động tự động 24/7:** Kích hoạt ngay lập tức qua giao diện chat bất cứ khi nào có brief mới.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **OpenAI API Key:** Để sử dụng model GPT-4.1-mini thông qua node `OpenAI Chat Model`.
- **Google Account:** Tài khoản Google để kết nối và ghi dữ liệu vào Google Sheets.
- **Template API URL:** Endpoint hoặc API nguồn để tìm kiếm template (hoặc sử dụng API thư viện template tương ứng).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này, sau đó vào giao diện n8n -> Chọn **Add workflow** -> Nhấn dấu `...` (Options) ở góc trên bên phải -> Chọn **Import from File** hoặc **Import from Clipboard** và dán đoạn JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà không báo lỗi, các sếp cần cấu hình chính xác các điểm sau:

- **Node `OpenAI Chat Model`**: 
  - Chọn hoặc thêm mới **OpenAI credentials** của các sếp.
  - Đảm bảo model được chọn là `gpt-4.1-mini` (hoặc model tương thích tùy ý).
- **Các node Google Sheets (`Append row in sheet2`, `Get row(s) in sheet`, `Update row in sheet`)**:
  - Kết nối với tài khoản Google thông qua **Google Sheets OAuth2 API**.
  - Chuẩn bị sẵn một Google Sheet với các cột bắt buộc: `Template ID`, `Name`, `User`, `Description`, `URL`.
- **Cấu hình biến chung (Config)**:
  - Thiết lập các biến môi trường hoặc cấu hình trực tiếp các tham số `GOOGLE_SHEETS_DOC_ID`, `GOOGLE_SHEET_NAME`, và `N8N_TEMPLATES_API_URL` để workflow biết chính xác vị trí ghi dữ liệu và nguồn API tìm kiếm.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và thử gửi một đoạn job brief mẫu qua node `When chat message received` để kiểm tra kết quả.
- Nếu dữ liệu đổ về Google Sheets chuẩn chỉnh, các sếp chỉ cần gạt công tắc sang **Active** để bật chế độ tự động chạy 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh chat thực tế:** Thay vì dùng chat trigger mặc định của n8n, các sếp có thể đổi thành Webhook từ **Telegram Bot** hoặc **Slack** để nhận brief trực tiếp từ nhóm chat của công ty.
- **Báo cáo tự động:** Thêm một node gửi thông báo qua Slack/Email sau khi ghi dữ liệu thành công vào Google Sheets để team nắm bắt tiến độ.
- **Mở rộng lưu trữ:** Nếu không thích Google Sheets, các sếp có thể dễ dàng thay thế bằng **Airtable** hoặc **Notion** chỉ với vài thao tác đổi node.

### 📌 Kết luận
Workflow này là một "trợ lý ảo" cực kỳ đắc lực giúp tối ưu hóa khâu xử lý job brief và quản lý tài nguyên template cho các agency hoặc đội ngũ nội dung. Hãy áp dụng ngay hôm nay để giải phóng sức lao động cho team của mình các sếp nhé!