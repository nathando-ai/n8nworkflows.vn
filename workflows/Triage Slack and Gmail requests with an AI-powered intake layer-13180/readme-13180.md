---
title: "🚀 Tự động hóa Triage Yêu cầu từ Slack và Gmail bằng AI - Workflow n8n"
description: "Tự động phân loại và xử lý yêu cầu từ Slack và Gmail bằng AI, tiết kiệm thời gian cho HR và đội ngũ hỗ trợ"
slug: "tu-dong-hoa-triage-yeu-cau-slack-gmail-ai"
tags: [n8n, automation, no-code, AI, HR, ticket-management]
keywords: [n8n workflow, tự động hóa HR, AI triage, quản lý yêu cầu, Slack Gmail]
---

# 🚀 Tự động hóa Triage Yêu cầu từ Slack và Gmail bằng AI - Workflow n8n

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa 100% quy trình triage yêu cầu từ Slack và Gmail
- Tiết kiệm thời gian xử lý yêu cầu lên đến 80%
- Phân loại và ưu tiên yêu cầu một cách chính xác nhờ AI
- Tạo ticket tự động trong Notion cho việc theo dõi
- Thông báo ngay trong Slack cho các yêu cầu quan trọng
- Tránh xử lý trùng lặp yêu cầu nhờ cơ chế lưu trữ ID đã xử lý
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Slack với quyền truy cập kênh cần theo dõi
- Tài khoản Gmail với quyền truy cập vào hộp thư cần theo dõi
- Tài khoản Notion với cơ sở dữ liệu đã tạo sẵn cho ticket
- API Key từ OpenAI để sử dụng các mô hình ngôn ngữ
- Bảng dữ liệu (Data Table) trong n8n để lưu trữ ID đã xử lý
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào "Import from URL" và dán link: https://n8n.io/workflows/13180
3. Hoặc tải file JSON về và chọn "Import from File"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Fetch recent Slack messages"**:
   - Chọn credentials Slack của bạn
   - Chỉ định kênh Slack cần theo dõi
   - Điều chỉnh tham số thời gian lấy tin nhắn (mặc định là 1 phút)

2. **Node "Watch inbound Gmail messages"**:
   - Chọn credentials Gmail của bạn
   - Thiết lập bộ lọc email (ví dụ: chỉ xử lý email từ các địa chỉ cụ thể)
   - Chỉ định hộp thư cần theo dõi (INBOX hoặc hộp thư khác)

3. **Node "Skip already processed items"**:
   - Tạo một bảng dữ liệu mới trong n8n
   - Thêm cột "uniqueID" để lưu trữ ID của các yêu cầu đã xử lý
   - Kết nối bảng dữ liệu này với node này

4. **Node "LLM for message normalization" và "LLM for triage agent"**:
   - Chọn credentials OpenAI của bạn
   - Đảm bảo chọn mô hình phù hợp (gpt-4.1-mini cho normalization, gpt-5.2 cho triage)
   - Điều chỉnh prompt nếu cần thiết để phù hợp với ngữ cảnh công việc của bạn

5. **Node "Create Notion ticket"**:
   - Chọn credentials Notion của bạn
   - Chỉ định cơ sở dữ liệu Notion để lưu trữ ticket
   - Đảm bảo các thuộc tính trong Notion khớp với đầu ra từ node "Parse triage JSON"

6. **Node "Notify in Slack"**:
   - Chọn credentials Slack của bạn
   - Chỉ định kênh Slack để gửi thông báo
   - Điều chỉnh thông điệp thông báo theo nhu cầu của bạn

7. **Node "Only high importance items"**:
   - Điều chỉnh ngưỡng mức độ quan trọng để lọc các yêu cầu cần thông báo
   - Mặc định là 7/10, có thể điều chỉnh từ 1-10

#### 3. Kích hoạt ⚡️
1. Thực hiện test run với dữ liệu mẫu để đảm bảo workflow hoạt động đúng
2. Kiểm tra các ticket được tạo trong Notion và thông báo trong Slack
3. Bật Active workflow sau khi đã kiểm tra kỹ

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với các công cụ khác**:
   - Thêm node để gửi email thông báo cho các yêu cầu quan trọng
   - Kết nối với hệ thống CRM để tự động tạo lead từ yêu cầu
   - Thêm node để lưu trữ log xử lý yêu cầu

2. **Tối ưu chi phí**:
   - Giới hạn số lượng ký tự được gửi đến LLM để giảm chi phí
   - Sử dụng mô hình nhỏ hơn cho các tác vụ đơn giản
   - Thiết lập lịch chạy workflow vào giờ làm việc để tiết kiệm tài nguyên

3. **Mở rộng nguồn yêu cầu**:
   - Thêm các node để theo dõi yêu cầu từ các nền tảng khác (Microsoft Teams, Discord...)
   - Tích hợp với các hệ thống ticket khác (Zendesk, Freshdesk...)

4. **Tự động hóa phản hồi**:
   - Thêm node để tự động gửi phản hồi cho các yêu cầu đơn giản
   - Sử dụng LLM để tạo nội dung phản hồi phù hợp với từng loại yêu cầu

### 📌 Kết luận
Workflow này mang lại giải pháp toàn diện cho việc tự động hóa quy trình triage yêu cầu từ Slack và Gmail, giúp các đội ngũ HR và hỗ trợ tiết kiệm thời gian và tập trung vào các yêu cầu quan trọng hơn. Bằng cách tích hợp AI và tự động hóa, các sếp có thể nâng cao hiệu suất làm việc và cải thiện trải nghiệm khách hàng. Hãy áp dụng ngay workflow này để tối ưu hóa quy trình làm việc của bạn!