---
title: "🚀 Tự động hóa lưu trữ tài liệu lớn trong Vector Store với Supabase và Notion"
description: "Hướng dẫn tự động hóa lưu trữ và truy xuất tài liệu lớn từ Notion vào Vector Store của Supabase bằng n8n, tiết kiệm thời gian và tối ưu hóa quy trình làm việc."
slug: "tu-dong-hoa-luu-tru-tai-lieu-lon-voi-supabase-va-notion"
tags: [n8n, automation, no-code, AI, vector-store]
keywords: [n8n workflow, tự động hóa, vector store, Supabase, Notion, AI]
---

# 🚀 Tự động hóa lưu trữ tài liệu lớn trong Vector Store với Supabase và Notion

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi quản lý và truy xuất tài liệu lớn từ Notion. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa quy trình lưu trữ và truy xuất tài liệu lớn từ Notion vào Vector Store của Supabase.
- Chính xác: Tối ưu hóa việc chia nhỏ và lưu trữ tài liệu để đảm bảo độ chính xác cao trong quá trình tìm kiếm.
- Cá nhân hóa: Tích hợp với OpenAI để tạo và truy xuất embeddings, nâng cao khả năng tìm kiếm và trả lời câu hỏi dựa trên ngữ cảnh.
- Hoạt động liên tục: Tự động cập nhật và quản lý tài liệu mới từ Notion vào Vector Store.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản OpenAI API (để tạo và truy xuất embeddings).
- Tài khoản Supabase (để lưu trữ Vector Store).
- Tài khoản Notion (để truy xuất tài liệu).
- Các credentials tương ứng cho các node: `openAiApi`, `supabaseApi`, `notionApi`.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/2568](https://n8n.io/workflows/2568) để tải file JSON của workflow.
2. Trong n8n Editor, nhấn vào **Import from File** và chọn file JSON đã tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Embeddings OpenAI**: Cấu hình credentials `openAiApi` và chọn model `gpt-4o`.
- **Token Splitter**: Điều chỉnh kích thước chunk và overlap để phù hợp với model `text-embedding-ada-002` (chunk size + overlap ≤ 8191).
- **Loop Over Items**: Đảm bảo chỉ xử lý 1 stream/item để tránh double-processing.
- **Delete old embeddings if exist**: Cấu hình node `supabase` với operation `delete` để xóa các embeddings cũ.
- **Get page blocks**: Cấu hình node `notion` với operation `getAll` và resource `block` để truy xuất tất cả các block của trang.
- **Notion Trigger**: Cấu hình credentials `notionApi` và chọn database chứa Knowledge Base.
- **Supabase Vector Store**: Cấu hình credentials `supabaseApi` để lưu trữ embeddings.
- **Concatenate to single string**: Kết hợp tất cả nội dung thành một chuỗi duy nhất để dễ dàng lưu trữ.

#### 3. Kích hoạt ⚡️
- Test run dữ liệu mẫu để đảm bảo workflow hoạt động đúng.
- Bật Active workflow để tự động hóa quy trình.

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để thông báo khi có tài liệu mới được cập nhật.
- Lưu log các hoạt động để theo dõi và quản lý hiệu suất.
- Gửi báo cáo định kỳ về số lượng tài liệu đã được cập nhật và lưu trữ.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa việc lưu trữ và truy xuất tài liệu lớn từ Notion vào Vector Store của Supabase, tiết kiệm thời gian và tối ưu hóa quy trình làm việc. Hãy áp dụng ngay để nâng cao hiệu suất làm việc!