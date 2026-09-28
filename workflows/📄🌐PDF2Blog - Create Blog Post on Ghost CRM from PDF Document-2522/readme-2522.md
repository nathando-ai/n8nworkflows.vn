---
title: "🚀 Tự động tạo bài viết Blog từ PDF với Ghost và AI - Workflow n8n"
description: "Hướng dẫn tự động hóa quy trình chuyển đổi PDF thành bài viết blog trên Ghost CRM bằng công nghệ AI, tiết kiệm thời gian và nâng cao hiệu quả nội dung"
slug: "tu-dong-tao-bai-viet-blog-tu-pdf-voi-ghost-va-ai"
tags: [n8n, automation, no-code, ai, marketing]
keywords: [n8n workflow, tự động hóa, ghost cms, pdf to blog, ai content creation]
---

# 🚀 Tự động tạo bài viết Blog từ PDF với Ghost và AI - Workflow n8n

[Các sếp đang gặp khó khăn khi phải chuyển đổi thủ công các tài liệu PDF thành bài viết blog trên Ghost CRM. Workflow này sẽ giúp tự động hóa toàn bộ quy trình này bằng công nghệ AI, tiết kiệm thời gian và nâng cao hiệu quả nội dung.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động chuyển đổi PDF thành bài viết blog hoàn chỉnh trên Ghost CRM
- Tiết kiệm thời gian xử lý từ 80% trở lên
- Đảm bảo nội dung nhất quán và chuyên nghiệp
- Tự động hóa toàn bộ quy trình từ upload đến xuất bản
- Tích hợp công nghệ AI để tối ưu hóa nội dung
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Ghost CRM với quyền tạo bài viết
- API Key của Ghost Admin API
- Tài khoản OpenAI với API Key (để sử dụng mô hình GPT-4o-mini)
- File PDF chứa nội dung cần chuyển đổi
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Click vào "Import from URL" và nhập link: https://n8n.io/workflows/2522
3. Hoặc copy/paste JSON workflow vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Upload PDF" (formTrigger)**:
   - Đảm bảo đường dẫn "path" được đặt là "pdf"

2. **Node "Extract Text" (extractFromFile)**:
   - Đảm bảo "operation" được đặt là "pdf"

3. **Node "Post to Ghost" (ghost)**:
   - Thêm credentials "ghostAdminApi" với API Key của bạn
   - Đảm bảo "operation" được đặt là "create"

4. **Node "gpt-4o-mini" (lmChatOpenAi)**:
   - Thêm credentials "openAiApi" với API Key của bạn
   - Đảm bảo "model" được đặt là "gpt-4o-mini-2024-07-18"

5. **Node "Create Structured Blog Post" (agent)**:
   - Cấu hình prompt phù hợp với nội dung của bạn
   - Đảm bảo output được định dạng đúng theo yêu cầu

#### 3. Kích hoạt ⚡️
1. Test run workflow với một file PDF mẫu
2. Kiểm tra kết quả trên Ghost CRM
3. Bật Active workflow sau khi đã kiểm tra kỹ

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram để nhận thông báo khi bài viết được xuất bản
- Lưu log các bài viết đã xuất bản để theo dõi hiệu suất
- Tự động gửi báo cáo hàng tuần về số lượng bài viết đã xuất bản
- Tích hợp với các công cụ SEO như Ahrefs hoặc SEMrush để tối ưu hóa bài viết

### 📌 Kết luận
Workflow này sẽ giúp các sếp tự động hóa hoàn toàn quy trình chuyển đổi PDF thành bài viết blog trên Ghost CRM, tiết kiệm thời gian và nâng cao hiệu quả nội dung. Hãy áp dụng ngay để tối ưu hóa quy trình làm việc của bạn!