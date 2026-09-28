---
title: "🚀 Tự động hóa thu thập lead và phân loại AI với Typeform, OpenAI & Gmail"
description: "Hướng dẫn tự động hóa quy trình thu thập lead từ Typeform, phân loại bằng AI và gửi phản hồi tự động qua Gmail và Discord"
slug: "tu-dong-hoa-thu-thap-lead-ai-routing-typeform-openai-gmail"
tags: [n8n, automation, no-code, lead-generation, ai-routing]
keywords: [n8n workflow, tự động hóa lead, AI phân loại lead, Typeform, OpenAI]
---

# 🚀 Tự động hóa thu thập lead và phân loại AI với Typeform, OpenAI & Gmail

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi xử lý hàng trăm lead hàng ngày. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa hoàn toàn quy trình thu thập lead từ Typeform
- Phân loại lead bằng AI với độ chính xác cao
- Gửi phản hồi tự động qua Gmail và Discord
- Lưu trữ lead trong Airtable với trạng thái và thông tin phân loại
- Tiết kiệm thời gian xử lý lead từ 80% đến 90%
- Giảm lỗi con người trong quá trình xử lý lead
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Typeform với form ID: UBdasOKD
- Tài khoản Airtable với bảng có các trường: Name, Email, Message, Status, Category, Lead Score, Priority
- Tài khoản OpenAI với API key
- Tài khoản Gmail với quyền gửi email
- Tài khoản Discord với quyền gửi tin nhắn
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor
2. Nhấn vào "Import from URL" và nhập URL: https://n8n.io/workflows/14363
3. Hoặc tải file JSON từ link trên và import vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Typeform Trigger**:
   - Cấu hình credentials cho Typeform
   - Đảm bảo form ID là UBdasOKD

2. **Sanitize Lead Data**:
   - Kiểm tra và điều chỉnh code JavaScript để phù hợp với định dạng dữ liệu của bạn
   - Đặc biệt chú ý đến việc xử lý tên, email và domain

3. **Create a record**:
   - Cấu hình credentials cho Airtable
   - Kiểm tra các trường trong bảng Airtable phải khớp với dữ liệu đầu vào

4. **AI Lead Analyzer**:
   - Cấu hình credentials cho OpenAI
   - Đảm bảo sử dụng model GPT-4o-mini
   - Kiểm tra prompt để đảm bảo phân loại lead phù hợp với nhu cầu kinh doanh

5. **Gmail Nodes**:
   - Cấu hình credentials cho Gmail
   - Kiểm tra các mẫu email để đảm bảo chúng phù hợp với thương hiệu của bạn
   - Đảm bảo các trường dữ liệu được ánh xạ chính xác

6. **Send a message4 (Discord)**:
   - Cấu hình credentials cho Discord
   - Kiểm tra kênh Discord để đảm bảo thông báo được gửi đến đúng vị trí

#### 3. Kích hoạt ⚡️
1. Test run workflow với dữ liệu mẫu
2. Kiểm tra tất cả các bước để đảm bảo chúng hoạt động như mong đợi
3. Bật Active workflow

### ✍️ Mẹo & gợi ý nâng cao
1. **Tích hợp Slack**: Thay thế hoặc bổ sung Discord bằng Slack để nhận thông báo
2. **Lưu log**: Thêm node để lưu log các lead được xử lý
3. **Báo cáo định kỳ**: Thêm node để gửi báo cáo tổng hợp hàng ngày về lead mới
4. **Xử lý lead thất bại**: Thêm bước xử lý lead khi có lỗi xảy ra trong quá trình

### 📌 Kết luận
Workflow này giúp tự động hóa hoàn toàn quy trình thu thập và phân loại lead, giảm thiểu thời gian xử lý và tăng độ chính xác. Bằng cách tích hợp Typeform, OpenAI và Gmail, các sếp có thể tập trung vào những nhiệm vụ quan trọng hơn trong kinh doanh. Hãy áp dụng ngay để tối ưu hóa quy trình làm việc của bạn!