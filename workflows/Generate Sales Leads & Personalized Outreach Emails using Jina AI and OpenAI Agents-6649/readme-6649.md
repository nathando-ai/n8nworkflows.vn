---
title: "🚀 Tự động hóa tìm kiếm Lead & Viết email cá nhân hóa với Jina AI và OpenAI Agents trên n8n"
description: "Xây dựng hệ thống sales lead generation thông minh chạy tự động: nghiên cứu công ty, tìm người ra quyết định, soạn và chấm điểm email cá nhân hóa rồi lưu về Airtable."
slug: "tu-dong-hoa-sales-lead-jina-ai-openai-n8n"
tags: [n8n, automation, ai-agents, lead-generation, airtable, openai]
keywords: [n8n workflow, tự động hóa sales, Jina AI, OpenAI Agents, Airtable automation, viết email tự động]
---

# 🚀 Tự động hóa tìm kiếm Lead & Viết email cá nhân hóa với Jina AI và OpenAI Agents

Các sếp làm sales hay marketing chắc chắn hiểu cảm giác "khổ sở" khi phải ngồi thủ công tra cứu từng công ty, tìm xem ai là người ra quyết định (Decision Maker), rồi lại vắt óc soạn từng chiếc email cá nhân hóa gửi đi. Vừa tốn thời gian, vừa khó scale (mở rộng quy lượng) mà tỷ lệ phản hồi lại hên xui.

Đừng lo nữa các sếp ơi! Workflow n8n siêu cấp này do chuyên gia **FabioInTech** thiết kế sẽ thay các sếp làm trọn gói từ A-Z: Tự động quét thông tin từ Airtable, dùng **Jina AI** để đào sâu nghiên cứu công ty, giao việc cho các **AI Agents (OpenAI)** phân tích tìm người phù hợp, tự động soạn thảo và đánh giá chất lượng email, sau đó cập nhật ngược lại Airtable cực kỳ mượt mà. 100% tự động, không cần viết code!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không còn cảnh tra cứu thông tin thủ công trên Google hay LinkedIn hàng giờ liền.
- **Cá nhân hóa cực đỉnh:** Email được viết dựa trên dữ liệu thực tế và sâu sắc về doanh nghiệp mục tiêu, giúp tăng tỷ lệ mở email (Open Rate) và chuyển đổi (Conversion Rate).
- **Quy trình chuẩn hóa tự động:** Từ khâu tìm kiếm, phân tích, soạn thảo đến kiểm duyệt chất lượng đều được AI thực hiện tự động trước khi lưu vào database.
- **Hoạt động không nghỉ:** Dễ dàng chạy hàng loạt (batch processing) danh sách hàng trăm lead chỉ với 1 cú click hoặc hẹn giờ định kỳ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị sẵn các tài khoản sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Airtable** kèm theo Base quản lý danh sách lead.
- **Tài khoản Jina AI** và lấy API Key (dùng cho node `Jina_API_Key`).
- **Tài khoản OpenAI** kèm API Key để cấu hình các mô hình AI (`OpenAI o3-mini`, `OpenAI - 4o-mini`, `OpenAI - 4o-mini - low`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow, dán trực tiếp vào n8n Editor hoặc import file JSON thông qua giao diện n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống vận hành chính xác theo ý muốn, các sếp cần chú ý cấu hình kỹ các node sau:

- **Cấu hình Airtable (`Get input records` & `Update record`):** 
  - Tạo một bảng trong Airtable với các trường bắt buộc: `Company_name` (Text), `Company_website` (URL), `Company_email` (Email), và `processed` (Single select gồm 2 giá trị `no` và `yes`).
  - Các trường kết quả trả về để lưu dữ liệu: `lead_name`, `lead_email`, `email_subject`, `email_text`, `email_summary`, `create_date`, `task_result`.
  - Kết nối Airtable Credentials vào hai node này và chọn đúng Base/Table của các sếp.

- **Cấu hình Doanh nghiệp (`Business_Info` node):**
  Điền đầy đủ thông tin về sản phẩm/dịch vụ của các sếp vào node này:
  - `BUSINESS_NAME`: Tên công ty các sếp.
  - `BUSINESS_INFORMATION`: Mô tả ngắn gọn về sản phẩm/dịch vụ.
  - `BUSINESS_KEY_BENEFITS`: 3-6 lợi ích cốt lõi.
  - `LANDING_PAGE_URL`: Đường dẫn trang đích.
  - `LEAD_TARGET_AUDIENCE`: Chân dung khách hàng mục tiêu (ví dụ: "Startups", "SaaS Founders"...).

- **Cấu hình API Key (`Jina_API_Key` & Các node OpenAI):**
  - Dán Jina API Key vào node `Jina_API_Key`.
  - Thiết lập OpenAI Credentials cho các node `OpenAI o3-mini`, `OpenAI - 4o-mini`, `OpenAI - 4o-mini - low`.

#### 3. Kích hoạt ⚡️
- Bấm nút **"Test workflow"** (`When clicking "Test workflow"`) với một bản ghi có trạng thái `processed` là `no` để kiểm tra toàn bộ luồng chạy.
- Sau khi test thành công và kết quả trả về Airtable chuẩn chỉnh, các sếp bật **Active** workflow để hệ thống tự động hóa hoàn toàn.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo Telegram/Slack:** Thêm một node Telegram hoặc Slack ngay sau bước `Update record` để nhận thông báo tức thì mỗi khi AI tìm được lead mới và soạn xong email.
- **Tự động hóa lịch chạy (Cron):** Thay thế node `manualTrigger` bằng node `Schedule Trigger` để workflow tự động quét danh sách lead trên Airtable vào mỗi sáng thứ Hai hàng tuần.
- **Mở rộng lọc dữ liệu:** Thêm bước lọc nâng cao để loại bỏ những công ty không phù hợp trước khi gửi yêu cầu Deep Research đến Jina AI, giúp tiết kiệm tối đa token AI.

### 📌 Kết luận
Workflow này là một "vũ khí tối tân" giúp các đội ngũ sales và marketing tối ưu hóa năng suất gấp nhiều lần. Thay vì tốn hàng giờ mài mòn sức lực cho các tác vụ thủ công, hãy để AI và automation lo phần việc nặng nhọc. Chúc các sếp cài đặt thành công và chốt thật nhiều hợp đồng lớn!