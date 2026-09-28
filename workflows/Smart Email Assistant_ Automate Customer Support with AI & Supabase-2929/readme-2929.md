---
title: "🚀 Trợ lý Email thông minh: Tự động hóa hỗ trợ khách hàng với AI & Supabase"
description: "Tự động phân loại, xử lý và trả lời email khách hàng với AI, giảm thời gian xử lý tới 90% và cải thiện trải nghiệm khách hàng"
slug: "tro-ly-email-thong-minh-tu-dong-hoa-ho-tro-khach-hang-voi-ai-supabase"
tags: [n8n, automation, no-code, AI, support]
keywords: [n8n workflow, tự động hóa, AI, hỗ trợ khách hàng, email]
---

# 🚀 Trợ lý Email thông minh: Tự động hóa hỗ trợ khách hàng với AI & Supabase

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Giảm thời gian xử lý email tới 90%
- Tự động phân loại và ưu tiên email quan trọng
- Trả lời email khách hàng nhanh chóng với nội dung chính xác
- Tích hợp dữ liệu từ Google Drive vào hệ thống hỗ trợ
- Tự động hóa toàn bộ quy trình xử lý email
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Gmail (để theo dõi và gửi email)
- Tài khoản Google Drive (để lưu trữ tài liệu hỗ trợ)
- Tài khoản Supabase (để lưu trữ vector embeddings)
- API Key từ OpenAI (để sử dụng các tính năng AI)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/2929)
2. Nhấn nút "Import" và chọn "Import from URL"
3. Dán link workflow vào ô nhập liệu
4. Nhấn "OK" để hoàn tất import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Email Monitor (gmailTrigger)**
   - Cấu hình credentials cho Gmail
   - Thiết lập bộ lọc email (ví dụ: chỉ theo dõi email từ khách hàng)

2. **AI Email Classifier (openAi)**
   - Cấu hình credentials cho OpenAI
   - Thiết lập prompt để phân loại email (ví dụ: "Phân loại email này thành: Hỗ trợ, Hỏi giá, Khiếu nại")

3. **Route Email (switch)**
   - Thiết lập các điều kiện chuyển hướng email dựa trên kết quả phân loại

4. **AI Response Generator (agent)**
   - Cấu hình các công cụ hỗ trợ (ví dụ: Vector Store Tool)
   - Thiết lập prompt cho AI tạo phản hồi

5. **Supabase Vector Store (vectorStoreSupabase)**
   - Cấu hình credentials cho Supabase
   - Thiết lập tên bảng để lưu trữ vector embeddings

6. **File Created/File Updated (googleDriveTrigger)**
   - Cấu hình credentials cho Google Drive
   - Thiết lập thư mục theo dõi

7. **Extract Document Text (extractFromFile)**
   - Thiết lập các định dạng file cần trích xuất (PDF, DOCX, TXT)

8. **Recursive Character Text Splitter (textSplitterRecursiveCharacterTextSplitter)**
   - Thiết lập kích thước chunk và overlap

9. **Embeddings OpenAI (embeddingsOpenAi)**
   - Cấu hình credentials cho OpenAI
   - Thiết lập model embeddings (ví dụ: text-embedding-ada-002)

10. **Create Draft (gmailTool)**
    - Cấu hình credentials cho Gmail
    - Thiết lập template email mẫu

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu.
- Bật Active workflow.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để thông báo khi có email quan trọng
- Thiết lập báo cáo hàng ngày về số lượng email đã xử lý
- Tích hợp với hệ thống CRM để lưu trữ thông tin khách hàng
- Thêm tính năng ghi âm thoại để xử lý email bằng giọng nói
- Tích hợp với các nền tảng thanh toán để xử lý đơn hàng trực tiếp từ email

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quy trình hỗ trợ khách hàng qua email, giảm thời gian xử lý và cải thiện trải nghiệm khách hàng. Với sự kết hợp của AI và Supabase, hệ thống có thể học hỏi và cải thiện liên tục dựa trên dữ liệu lịch sử. Hãy thử ngay để thấy sự khác biệt trong cách làm việc của bạn!