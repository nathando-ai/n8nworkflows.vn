---
title: "✍️ Tự động tạo bài đăng LinkedIn từ Blog với AI GPT-4o"
description: "Hướng dẫn tự động hóa tạo nội dung LinkedIn từ blog bằng n8n và GPT-4o, tiết kiệm thời gian và tối ưu nội dung"
slug: "tu-dong-tao-bai-dang-linkedin-tu-blog-voi-ai-gpt-4o"
tags: [n8n, automation, no-code, linkedin, marketing]
keywords: [n8n workflow, tự động hóa, linkedin, marketing, ai, gpt-4o]
---

# ✍️ Tự động tạo bài đăng LinkedIn từ Blog với AI GPT-4o

[Các sếp] có biết không? Việc tạo nội dung cho LinkedIn từ blog đang tốn thời gian và công sức của các chuyên viên marketing. Bạn phải:
- Đọc từng bài viết
- Tìm hiểu nội dung
- Viết bài đăng phù hợp
- Đảm bảo tính nhất quán

Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình này trong vòng 5 phút!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động tạo nội dung trong vài giây thay vì vài giờ
- **Nội dung nhất quán**: Đảm bảo định dạng và phong cách thống nhất
- **Tối ưu SEO**: Nội dung được tối ưu hóa cho LinkedIn
- **Tự động lưu trữ**: Tất cả bài đăng được lưu trong Google Sheets
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Ghost (hoặc WordPress với plugin Ghost)
- Tài khoản OpenAI (để sử dụng GPT-4o)
- Tài khoản Google (để lưu trữ trong Google Sheets)
- API keys cho các dịch vụ trên
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/3500](https://n8n.io/workflows/3500)
2. Click vào nút "Import" trên trang workflow
3. Hoặc copy toàn bộ JSON workflow và paste vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Extract Blog Posts"**:
   - Thêm credentials cho tài khoản Ghost của bạn
   - Chọn số lượng bài viết muốn lấy (mặc định là 10)

2. **Node "AI Agent"**:
   - Thêm credentials cho tài khoản OpenAI
   - Chỉnh sửa system prompt để phù hợp với phong cách viết của bạn
   - Đảm bảo chọn model là "gpt-4o-mini"

3. **Node "Record the posts"**:
   - Thêm credentials cho tài khoản Google
   - Chọn file Google Sheets để lưu trữ
   - Chọn sheet cụ thể trong file
   - Map các trường dữ liệu (title, url, content, linkedin_post)

#### 3. Kích hoạt ⚡️
1. Click vào nút "Test workflow" để kiểm tra với dữ liệu mẫu
2. Sau khi kiểm tra thành công, click vào nút "Active" để kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node Slack/Telegram để thông báo khi có bài đăng mới
- Tự động đăng lên LinkedIn bằng node "LinkedIn"
- Lập lịch chạy workflow hàng ngày để cập nhật nội dung mới nhất
- Thêm node "Email" để gửi báo cáo hàng tuần về các bài đăng đã tạo

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa việc tạo nội dung LinkedIn từ blog, tiết kiệm thời gian và đảm bảo tính nhất quán. Hãy thử ngay và nâng cao hiệu quả marketing của bạn!