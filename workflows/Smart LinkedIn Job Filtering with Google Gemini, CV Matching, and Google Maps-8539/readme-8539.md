---
title: "🚀 Tự động lọc việc làm LinkedIn thông minh với Google Gemini, so khớp CV và Google Maps"
description: "Workflow n8n tự động hóa việc tìm kiếm việc làm trên LinkedIn, lọc theo tiêu chí cá nhân, tính thời gian di chuyển và so khớp CV bằng AI, gửi thông báo qua Telegram"
slug: "tu-dong-loc-viec-lam-linkedin-voi-google-gemini"
tags: [n8n, automation, no-code, linkedin, google-maps, ai, google-gemini]
keywords: [n8n workflow, tự động hóa, tìm kiếm việc làm, linkedin, google maps, google gemini, so khớp cv]
---

# 🚀 Tự động lọc việc làm LinkedIn thông minh với Google Gemini, so khớp CV và Google Maps

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp thường gặp khó khăn khi phải:
- Xem hàng trăm tin tuyển dụng trên LinkedIn mỗi ngày
- Lọc thủ công theo tiêu chí cá nhân (ngôn ngữ, cấp bậc, vị trí làm việc...)
- Tính thời gian di chuyển cho các công việc không làm từ xa
- So khớp CV với yêu cầu công việc một cách chính xác

Workflow này giúp các sếp tự động hóa toàn bộ quy trình này với 21 nodes n8n, kết hợp sức mạnh của Google Gemini và Google Maps.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm 2-3 giờ mỗi ngày khi không phải lọc thủ công
- Chỉ nhận thông báo về các công việc phù hợp hoàn toàn với tiêu chí cá nhân
- Tự động tính thời gian di chuyển chính xác cho các công việc không làm từ xa
- So khớp CV với yêu cầu công việc một cách chính xác bằng AI
- Nhận thông báo chi tiết qua Telegram khi có công việc phù hợp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản LinkedIn (để lấy dữ liệu tuyển dụng)
- API Key từ Google Maps (để tính thời gian di chuyển)
- API Key từ Google Gemini (để phân tích nội dung tuyển dụng)
- Tài khoản Supabase (để lưu trữ dữ liệu)
- Tài khoản Telegram (để nhận thông báo)
- CV/resume đầy đủ (để so khớp với yêu cầu công việc)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/8539](https://n8n.io/workflows/8539)
2. Click vào nút "Download" để tải file JSON
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node Config (set)**
   - Thêm CV/resume đầy đủ vào trường "MyCV"
   - Cấu hình các tiêu chí lọc:
     - JobKeywords: Từ khóa tìm kiếm (ví dụ: "engineer", "product manager")
     - JobsToScrape: Số lượng công việc cần lấy mỗi lần chạy (ví dụ: 20)
     - HomeLocation: Địa điểm nhà (ví dụ: "Hà Nội, Việt Nam")
     - MaxCommuteMinutes: Thời gian di chuyển tối đa (ví dụ: 45)
     - TargetLanguage: Ngôn ngữ mong muốn (ví dụ: "Tiếng Việt")
     - ExperienceLevel: Cấp bậc mong muốn (ví dụ: "mid_senior")
     - Under10Applicants: Chỉ lấy công việc có ít hơn 10 ứng viên (true/false)

2. **Node Scrape LinkenIn Jobs (httpRequest)**
   - Cấu hình credentials "httpBearerAuth" với token LinkedIn của bạn

3. **Node Google Gemini (lmChatGoogleGemini)**
   - Cấu hình credentials "googlePalmApi" với API Key Google Gemini
   - Đảm bảo tài khoản Google có đủ credit để sử dụng API

4. **Node Get Commute Time (httpRequest)**
   - Cấu hình credentials "httpQueryAuth" với API Key Google Maps

5. **Node Save Data (supabase)**
   - Cấu hình credentials "supabaseApi" với thông tin kết nối Supabase

6. **Node Send a Notification (telegram)**
   - Cấu hình credentials "telegramApi" với thông tin bot Telegram

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong tất cả các node, click vào nút "Activate" để kích hoạt workflow
2. Để test workflow, bạn có thể:
   - Chạy thủ công bằng cách click vào nút "Execute Workflow" trong n8n Editor
   - Hoặc chờ workflow tự động chạy theo lịch trình đã cấu hình

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh thông báo Telegram**: Bạn có thể chỉnh sửa nội dung thông báo trong node "Send a Notification" để phù hợp với nhu cầu cá nhân
2. **Thêm bộ lọc**: Bạn có thể thêm các tiêu chí lọc khác trong node "Config" để phù hợp hơn với nhu cầu tìm việc
3. **Tích hợp với các công cụ khác**: Bạn có thể kết nối workflow này với các công cụ khác như Slack, Email để nhận thông báo
4. **Lưu log hoạt động**: Bạn có thể thêm node để lưu log hoạt động của workflow để theo dõi hiệu suất

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian đáng kể trong quá trình tìm kiếm việc làm. Bằng cách tự động hóa quá trình lọc, tính thời gian di chuyển và so khớp CV, các sếp có thể tập trung vào các công việc thực sự phù hợp với tiêu chí cá nhân. Hãy áp dụng ngay để nâng cao hiệu suất tìm việc của mình!