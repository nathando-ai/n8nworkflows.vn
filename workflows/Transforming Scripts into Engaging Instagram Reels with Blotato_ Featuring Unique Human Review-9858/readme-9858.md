---
title: "🎥 Tự động hóa tạo Reels Instagram với Blotato + AI Gemini + Xét duyệt người"
description: "Hướng dẫn tự động hóa quy trình tạo video Reels từ script, xử lý bằng AI Gemini và gửi xét duyệt qua email - hoàn toàn không cần code"
slug: "tao-reels-instagram-tu-dong-voi-blotato-ai-gemini"
tags: [n8n, automation, content creation, blotato, ai]
keywords: [tạo reels tự động, blotato workflow, ai tạo video, tự động hóa nội dung]
---

# 🎥 Tự động hóa tạo Reels Instagram với Blotato + AI Gemini + Xét duyệt người

[Các sếp] có biết rằng việc tạo nội dung video cho Instagram đang tốn thời gian và công sức không nhỏ? Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình từ viết kịch bản đến đăng tải video lên Instagram - chỉ với một lần cấu hình duy nhất!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 80% thời gian tạo nội dung video
- Tự động hóa quy trình từ viết kịch bản đến đăng tải
- Đảm bảo chất lượng nội dung với sự kiểm duyệt người
- Tăng khả năng tương tác với khán giả
- Hoạt động liên tục 24/7 không cần can thiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Blotato (đăng ký [tại đây](https://blotato.com/?ref=karne))
- Tài khoản Google Cloud với API Gemini đã kích hoạt
- Tài khoản Gmail để nhận thông báo xét duyệt
- Script mẫu hoặc nguồn dữ liệu đầu vào cho video
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/9858](https://n8n.io/workflows/9858)
2. Click vào nút "Import" ở góc trên bên phải
3. Đăng nhập vào tài khoản n8n của bạn (nếu chưa có, hãy tạo mới)
4. Chọn "Import from URL" và dán link workflow

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "On form submission2"**:
   - Cấu hình form để nhận script video từ người dùng
   - Đảm bảo các trường bắt buộc được điền đầy đủ

2. **Node "Google Gemini Chat Model2"**:
   - Tạo credentials cho Google Palm API trong n8n
   - Điền API Key từ Google Cloud Console
   - Cấu hình prompt để xử lý script video

3. **Node "Create video3"**:
   - Tạo credentials cho Blotato API trong n8n
   - Điền API Key từ tài khoản Blotato
   - Cấu hình các tham số video như độ phân giải, chất lượng...

4. **Node "Send message and wait for response1"**:
   - Tạo credentials cho Gmail OAuth2 trong n8n
   - Cấu hình email nhận thông báo xét duyệt
   - Đảm bảo email có quyền gửi và nhận email từ n8n

5. **Node "Create post2"**:
   - Cấu hình thông tin đăng bài như hashtag, caption...
   - Đảm bảo tài khoản Instagram đã kết nối với Blotato

#### 3. Kích hoạt ⚡️
1. Test run workflow với dữ liệu mẫu
2. Kiểm tra từng node để đảm bảo hoạt động đúng
3. Bật Active workflow sau khi đã kiểm tra kỹ

### ✍️ Mẹo & gợi ý nâng cao
1. Kết hợp với Slack/Telegram để nhận thông báo tức thời
2. Lưu log các video đã tạo để theo dõi hiệu suất
3. Tự động hóa gửi báo cáo hàng tuần về hiệu quả video
4. Kết nối với Google Analytics để theo dõi lượt xem video

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quy trình tạo nội dung video cho Instagram, từ viết kịch bản đến đăng tải - chỉ với một lần cấu hình. Hãy áp dụng ngay để tiết kiệm thời gian và tăng hiệu quả nội dung!