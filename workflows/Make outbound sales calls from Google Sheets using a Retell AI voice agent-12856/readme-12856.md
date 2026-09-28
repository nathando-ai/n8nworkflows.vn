---
title: "🚀 Tự động gọi điện chăm sóc khách hàng từ Google Sheets bằng Retell AI voice agent"
description: "Hướng dẫn xây dựng hệ thống Outbound Sales Call tự động 100% bằng n8n và Retell AI, tích hợp lọc múi giờ thông minh và cập nhật trạng thái vào Google Sheets."
slug: "tu-dong-goi-dien-sales-google-sheets-retell-ai"
tags: [n8n, automation, retell-ai, google-sheets, ai-voice-agent, lead-nurturing]
keywords: [n8n workflow, retell ai, gọi điện tự động, outbound sales, google sheets automation, ai voice agent]
---

# 🚀 Tự động gọi điện chăm sóc khách hàng từ Google Sheets bằng Retell AI voice agent

Các sếp có đang tốn hàng giờ mỗi ngày để gọi điện cho danh sách khách hàng tiềm năng (leads) đổ về từ Google Sheets không? Việc gọi thủ công không chỉ mất thời gian, dễ bỏ sót mà đôi khi còn gọi nhầm giờ nghỉ ngơi của khách gây khó chịu.

Giải pháp ở đây là gì? Workflow n8n này sẽ tự động hóa toàn bộ quy trình: ngay khi có lead mới, hệ thống tự động làm sạch số điện thoại, kiểm tra múi giờ địa phương (đảm bảo chỉ gọi trong giờ hành chính từ 8h sáng - 5h chiều), thực hiện cuộc gọi qua **Retell AI Voice Agent**, theo dõi kết quả và tự động ghi log chi tiết về Google Sheets. Toàn bộ hoàn toàn tự động, không cần đụng tay!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian telesales:** Không cần bấm số thủ công, AI sẽ gọi và trò chuyện như người thật.
- **Thông minh theo múi giờ:** Hệ thống tự check múi giờ dựa trên số điện thoại, tuyệt đối không gọi phiền khách vào ban đêm.
- **Quản lý dữ liệu tự động:** Trạng thái cuộc gọi, bản ghi (transcript), tóm tắt (summary) và cảm xúc (sentiment) của khách hàng được cập nhật thẳng vào Google Sheets.
- **Hoạt động 24/7:** Chạy ngầm liên tục, cứ có lead mới là hệ thống xử lý ngay lập tức.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản **n8n** (Cloud hoặc Self-hosted).
- Tài khoản **Retell AI** ([Tạo tài khoản miễn phí và nhận $10 credit tại đây](https://dashboard.retellai.com/?ref=retell-n8n)).
- Tài khoản **Google Sheets** có sẵn file quản lý lead.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và paste trực tiếp vào giao diện n8n Editor, hoặc import file JSON tải từ kho lưu trữ.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru, các sếp cần cấu hình các thành phần sau:

- **Tài khoản (Credentials):**
  - Kết nối **Google Sheets OAuth2 API** cho các node `New lead` và `Update Google Sheets with call information`.
  - Tạo **Bearer Auth** credential trong n8n với API Key lấy từ tài khoản Retell AI của các sếp cho node `Get Call Status`.

- **Cấu hình Google Sheet:**
  - Chuẩn bị một Google Sheet với các cột tối thiểu: `Phone Number`, `Name`, `Status`.
  - Đặt trạng thái ban đầu của lead mới là `"Not called"` (để node `Filter numbers we've already called` hoạt động chính xác).

- **Cấu hình Node `Make phone call` (HTTP Request):**
  - `from_number`: Số điện thoại Retell của các sếp (có kèm mã quốc gia, ví dụ `+84...`).
  - `to_number`: Trỏ đến biến `{{ $json['Phone Number'] }}`.
  - `agent_id`: ID của AI Agent đã thiết lập sẵn trên bảng điều khiển Retell AI.

- **Kiểm tra múi giờ & logic phụ:**
  - Node `Get lead's timezone` và `Is it between 8am-5pm for them?`: Giúp lọc thời gian gọi trong khoảng 8h00 - 5h chiều theo giờ địa phương của lead.
  - Các node `Wait` và `Get Call Status`: Dùng để polling (kiểm tra trạng thái) định kỳ cho đến khi cuộc gọi kết thúc trước khi ghi kết quả về Sheet.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (Test step/Test workflow) với một dòng dữ liệu mẫu trong Google Sheets.
- Sau khi thấy hệ thống gọi thành công và cập nhật lại Sheet, gạt công tắc sang **Active** để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa dạng hóa Trigger:** Thay vì dùng Google Sheets Trigger, các sếp có thể đổi thành Webhook nhận lead từ Landing Page, Facebook Lead Ads hoặc CRM (HubSpot, Salesforce).
- **Tích hợp thông báo:** Nối thêm node Slack hoặc Telegram sau bước cập nhật Google Sheets để đội ngũ sales nhận thông báo ngay khi có khách hàng vừa kết thúc cuộc gọi với AI.
- **Mở rộng kịch bản:** Tùy chỉnh Agent ID trên Retell AI cho từng chiến dịch sản phẩm khác nhau.

### 📌 Kết luận
Hệ thống Outbound Sales kết hợp n8n và Retell AI chính là vũ khí giúp doanh nghiệp tối ưu hóa chi phí nhân sự telesales mà vẫn tiếp cận khách hàng cực kỳ chuyên nghiệp. Thiết lập ngay hôm nay để bứt phá doanh thu cùng AI các sếp nhé!