---
title: "🚀 Tự động hóa Chatbot AI đa Agent kết nối Postgres/Supabase và QuickCharts với n8n"
description: "Hướng dẫn chi tiết cách triển khai workflow n8n kết hợp nhiều Agent AI để tương tác với cơ sở dữ liệu Postgres/Supabase và tạo biểu đồ QuickCharts tự động"
slug: "tu-dong-hoa-chatbot-ai-da-agent-postgres-quickcharts-n8n"
tags: [n8n, automation, no-code, ai, chatbot, postgres, supabase, quickcharts]
keywords: [n8n workflow, tự động hóa, chatbot AI, postgres, supabase, quickcharts, langchain]
---

# 🚀 Tự động hóa Chatbot AI đa Agent kết nối Postgres/Supabase và QuickCharts với n8n

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi phải xử lý dữ liệu từ cơ sở dữ liệu và tạo báo cáo trực quan. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code kết hợp nhiều Agent AI.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động hóa tương tác với cơ sở dữ liệu Postgres/Supabase
- Tạo biểu đồ trực quan từ dữ liệu tự động
- Kết hợp nhiều Agent AI để xử lý các yêu cầu phức tạp
- Tiết kiệm thời gian xử lý dữ liệu và tạo báo cáo
- Tăng tính chính xác và nhất quán trong phân tích dữ liệu
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Postgres/Supabase đã cấu hình
- API Key từ OpenAI
- Cơ sở dữ liệu Postgres/Supabase đã có dữ liệu
- Tài khoản n8n đã cài đặt và cấu hình
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấp vào "Import from URL" và dán link: https://n8n.io/workflows/3090
3. Hoặc tải file JSON từ link trên và import trực tiếp vào n8n

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **When chat message received** (chatTrigger):
   - Không cần cấu hình đặc biệt, node này sẽ kích hoạt khi nhận tin nhắn chat

2. **Execute SQL Query** (postgresTool):
   - Cấu hình credentials cho Postgres
   - Đảm bảo kết nối Postgres hoạt động

3. **gpt-4o-mini** và **gpt-4o-mini-2** (lmChatOpenAi):
   - Cấu hình credentials cho OpenAI API
   - Đảm bảo API key hoạt động và có đủ credit

4. **🤖Primary Agent** (agent):
   - Cấu hình prompt cho Agent chính
   - Đảm bảo Agent có quyền truy cập vào các tool cần thiết

5. **🤖Secondary Postgres Agent** và **🤖Secondary QuickChart Agent** (agent):
   - Cấu hình prompt cho các Agent phụ
   - Đảm bảo các Agent có quyền truy cập vào các tool cần thiết

6. **🔀Tool Agent Router** (switch):
   - Cấu hình các điều kiện để định tuyến đến các Agent phụ
   - Đảm bảo các điều kiện định tuyến chính xác

7. **Postgres Chat Memory** (memoryPostgresChat):
   - Cấu hình credentials cho Postgres
   - Đảm bảo bảng lưu trữ lịch sử chat đã được tạo

8. **Create QuickChart** (httpRequest):
   - Đảm bảo endpoint QuickChart.io hoạt động
   - Kiểm tra định dạng JSON đầu vào

9. **QuickChart Object Schema** (outputParserStructured):
   - Cấu hình schema cho QuickChart
   - Đảm bảo schema phù hợp với yêu cầu

#### 3. Kích hoạt ⚡️
1. Test run dữ liệu mẫu để kiểm tra kết nối và chức năng
2. Bật Active workflow để bắt đầu sử dụng

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để tạo chatbot đa kênh
- Thêm node lưu log để theo dõi hoạt động của workflow
- Tạo báo cáo định kỳ từ dữ liệu phân tích
- Kết hợp với các công cụ khác như Google Sheets để lưu trữ dữ liệu
- Tối ưu hóa prompt cho các Agent để tăng tính chính xác

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc tự động hóa tương tác với cơ sở dữ liệu và tạo biểu đồ trực quan từ dữ liệu. Với sự kết hợp của nhiều Agent AI, workflow này có thể xử lý các yêu cầu phức tạp và cung cấp kết quả chính xác. Các sếp nên thử nghiệm với dữ liệu mẫu trước khi triển khai vào sản xuất để đảm bảo hoạt động ổn định.