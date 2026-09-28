---
title: "🚀 Tự động tìm kiếm và chấm điểm LinkedIn Leads bằng GPT-4 AI và lưu vào Google Sheets"
description: "Hướng dẫn xây dựng hệ thống tự động tìm kiếm khách hàng tiềm năng trên LinkedIn qua Ghost Genius API, chấm điểm bằng AI GPT-4 và lưu trữ vào Google Sheets CRM."
slug: "tim-kiem-va-cham-diem-linkedin-leads-voi-gpt4-ai-google-sheets"
tags: [n8n, automation, no-code, lead-generation, ai, openai, google-sheets]
keywords: [n8n workflow, linkedin leads, gpt-4 ai scoring, ghost genius api, google sheets crm, tự động hóa bán hàng]
---

# 🚀 Tự động tìm kiếm và chấm điểm LinkedIn Leads bằng GPT-4 AI và lưu vào Google Sheets

Việc tìm kiếm và phân loại khách hàng tiềm năng (Lead Generation) trên LinkedIn theo cách thủ công thường tốn rất nhiều thời gian: từ việc lướt tìm công ty, lọc thông tin, đánh giá độ phù hợp cho đến việc copy/paste vào file quản lý. Điều này không chỉ gây mệt mỏi mà còn làm lỡ mất cơ hội tiếp cận khách hàng vàng.

Workflow n8n này sẽ giải quyết triệt để vấn đề đó bằng cách tự động hóa 100% quy trình: Tìm kiếm công ty trên LinkedIn, lấy thông tin chi tiết, lọc các tiêu chí chất lượng, nhờ AI (GPT-4) chấm điểm mức độ tiềm năng dựa trên sản phẩm/dịch vụ của bạn, và tự động lưu vào Google Sheets CRM mà không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Des kỹ VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Thu thập hàng loạt công ty từ LinkedIn theo từ khóa, ngành nghề, vị trí mong muốn.
- **AI thông minh phân loại**: GPT-4 tự động đọc thông tin công ty và chấm điểm (Score) mức độ phù hợp với dịch vụ của doanh nghiệp bạn.
- **Chống trùng lặp dữ liệu**: Tự động kiểm tra xem công ty đã tồn tại trong CRM chưa trước khi thêm mới.
- **Vận hành an toàn**: Cơ chế chia batch (lô) và độ trễ thông minh giúp tuân thủ tuyệt đối giới hạn API của LinkedIn và Google Sheets.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- Tài khoản và API Key tại **Ghost Genius API** (dùng để trích xuất dữ liệu LinkedIn).
- **OpenAI API Key** (để chạy node AI Company Scoring).
- File **Google Sheets** làm CRM (sử dụng bản sao từ [Google Sheet mẫu](https://docs.google.com/spreadsheets/d/1hlBAeFV17wBYDntwoJP6MMv5CuZbUtl63Z4jbTtv3gw/edit?usp=sharing)).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này và import trực tiếp vào giao diện n8n Editor của các sếp, hoặc copy toàn bộ JSON và paste trực tiếp vào màn hình làm việc của n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy mượt mà, các sếp cần cấu hình chính xác các node quan trọng sau:

- **Node `Set Variables`**: 
  - Đây là nơi quan trọng nhất để định nghĩa từ khóa tìm kiếm, ngành nghề, quy mô nhân sự, vị trí địa lý.
  - Tùy chỉnh prompt hệ thống cho phần AI Lead Scoring sao cho phù hợp nhất với sản phẩm/dịch vụ thực tế của công ty bạn.
- **Node `Search Companies` & `Get Company Info` (HTTP Request)**:
  - Cần tạo **Header Auth** credential với thông tin:
    - **Name**: `Authorization`
    - **Value**: `Bearer YOUR_TOKEN_HERE` (thay bằng API Key từ Ghost Genius).
- **Node `AI Company Scoring` (OpenAI)**:
  - Kết nối OpenAI API Key thông qua n8n Credentials.
  - Chọn model GPT-4 hoặc model phù hợp để hệ thống chấm điểm chính xác.
- **Node `Check If Company Exists` & `Add Company to CRM` (Google Sheets)**:
  - Kết nối tài khoản Google Drive/Sheets của bạn.
  - Trỏ đúng tới file Google Sheet CRM đã tạo bản sao và chọn đúng sheet `Companies`.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** với một vài dữ liệu mẫu ở node `Start` (Manual Trigger) để kiểm tra xem dòng dữ liệu chạy có mượt không.
- Sau khi test thành công, gạt công tắc sang **Active** để workflow chạy tự động theo lịch hoặc theo ý muốn.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo**: Thêm node **Slack** hoặc **Telegram** ngay sau node `Add Company to CRM` để nhận tin nhắn thông báo tức thì mỗi khi hệ thống tìm được một Lead chất lượng cao (ví dụ: Điểm AI > 8/10).
- **Báo cáo định kỳ**: Kết hợp node **Cron (Schedule Trigger)** kết hợp gửi email tổng hợp danh sách các Lead mới tìm được trong tuần qua Gmail.
- **Quản lý giới hạn tìm kiếm**: Mỗi lần tìm kiếm Ghost Genius trả về tối đa 1.000 kết quả. Nếu thị trường mục tiêu quá lớn, hãy chia nhỏ theo khu vực (Location ID) để thu thập dữ liệu chi tiết và tránh quá tải.

### 📌 Kết luận
Workflow "Find & Score LinkedIn Leads with GPT-4 AI and Export to Google Sheets CRM" là trợ thủ đắc lực giúp đội ngũ sales và marketing tiết kiệm hàng chục giờ làm việc thủ công mỗi tuần. Hãy thiết lập ngay hôm nay để đưa quy trình tìm kiếm khách hàng tiềm năng lên một tầm cao mới!