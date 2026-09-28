---
title: "🚀 Tự động hóa: Chuyển đổi tin tức từ Gmail thành bài đăng LinkedIn thông minh với OpenAI"
description: "Hướng dẫn tự động hóa chuyển đổi tin tức từ email tin tức thành bài đăng LinkedIn hấp dẫn bằng n8n và OpenAI, tiết kiệm thời gian và tăng tương tác"
slug: "tu-dong-hoa-tin-tuc-gmail-sang-linkedin-openai"
tags: [n8n, automation, no-code, marketing, openai]
keywords: [n8n workflow, tự động hóa, marketing, openai, linkedin]
---

# 🚀 Tự động hóa: Chuyển đổi tin tức từ Gmail thành bài đăng LinkedIn thông minh với OpenAI

[Các sếp đang mệt mỏi với việc phải đọc hàng chục email tin tức hàng ngày và viết tay từng bài đăng LinkedIn? Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình từ lọc tin tức đến tạo nội dung và đăng bài một cách chuyên nghiệp, tiết kiệm thời gian đáng kể.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động xử lý hàng chục email tin tức mỗi ngày
- **Nội dung chuyên nghiệp**: Sử dụng AI tạo bài đăng hấp dẫn, phù hợp với thương hiệu
- **Tăng tương tác**: Bài đăng được tối ưu hóa với thông tin chính xác và góc nhìn độc đáo
- **Hoạt động liên tục**: Không cần can thiệp thủ công, chạy tự động 24/7
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Gmail với quyền truy cập email tin tức
- Tài khoản LinkedIn với quyền đăng bài
- API Key từ OpenAI (có thể dùng tài khoản miễn phí)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/3509)
2. Click vào nút "Copy to clipboard" để sao chép JSON workflow
3. Trong n8n Editor, click vào "Import from Clipboard" và dán JSON đã sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node Gmail**:
   - Đảm bảo đã cấu hình credentials "gmailOAuth2" với quyền truy cập đầy đủ
   - Thay đổi tham số "operation" thành "getAll" nếu cần lấy tất cả email
   - Thêm bộ lọc để chỉ lấy email từ địa chỉ tin tức mong muốn

2. **Node Extract News Items (OpenAI)**:
   - Cấu hình credentials "openAiApi" với API Key hợp lệ
   - Tùy chỉnh prompt để trích xuất thông tin chính xác từ email tin tức
   - Ví dụ prompt có thể là: "Tóm tắt các tin tức chính từ email này, mỗi tin tức trên một dòng"

3. **Node Create LinkedIn Posts (OpenAI)**:
   - Sử dụng cùng credentials "openAiApi" với node trước
   - Tùy chỉnh prompt để tạo nội dung bài đăng phù hợp với thương hiệu
   - Ví dụ prompt có thể là: "Viết một bài đăng LinkedIn hấp dẫn từ nội dung này, sử dụng ngôn ngữ chuyên nghiệp và góc nhìn độc đáo"

4. **Node LinkedIn**:
   - Cấu hình credentials "linkedInOAuth2Api" với quyền đăng bài
   - Đảm bảo tài khoản LinkedIn có quyền đăng bài công khai hoặc theo nhóm

#### 3. Kích hoạt ⚡️
1. Click vào nút "Test workflow" để kiểm tra với dữ liệu mẫu
2. Sau khi kiểm tra thành công, click vào nút "Active workflow" để kích hoạt chạy tự động

### ✍️ Mẹo & gợi ý nâng cao
1. **Lọc email hiệu quả hơn**: Thêm bộ lọc ngày tháng hoặc từ khóa để chỉ xử lý email mới nhất
2. **Tùy chỉnh nội dung**: Sử dụng các node Function để thêm định dạng đặc biệt vào bài đăng
3. **Thông báo kết quả**: Kết nối với node Slack hoặc Telegram để nhận thông báo khi workflow chạy xong
4. **Lưu trữ nội dung**: Thêm node Google Sheets để lưu trữ lịch sử các bài đăng đã tạo

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quy trình chuyển đổi tin tức từ email thành bài đăng LinkedIn chuyên nghiệp, tiết kiệm thời gian đáng kể và nâng cao hiệu quả marketing. Hãy thử ngay và thấy sự khác biệt trong cách tiếp cận nội dung của các sếp!