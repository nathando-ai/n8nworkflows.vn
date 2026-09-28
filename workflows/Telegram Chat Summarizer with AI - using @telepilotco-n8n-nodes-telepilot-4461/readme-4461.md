---
title: "📊 Tự động hóa Telegram Chat với AI - Tóm tắt cuộc trò chuyện bằng n8n"
description: "Hướng dẫn tự động tóm tắt nội dung cuộc trò chuyện Telegram bằng AI trong n8n, tiết kiệm thời gian và nâng cao hiệu quả làm việc"
slug: "tu-dong-hoa-telegram-chat-voi-ai-tom-tat-cuoc-tro-chuyen"
tags: [n8n, automation, no-code, telegram, ai]
keywords: [n8n workflow, tự động hóa, telegram, tóm tắt cuộc trò chuyện, ai]
---

# 📊 Tự động hóa Telegram Chat với AI - Tóm tắt cuộc trò chuyện bằng n8n

[Các sếp đang gặp khó khăn khi phải đọc và tóm tắt thủ công hàng trăm tin nhắn Telegram hàng ngày. Workflow này sẽ giúp các sếp tự động hóa quy trình này bằng công nghệ AI, tiết kiệm thời gian và nâng cao hiệu quả làm việc.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động tóm tắt nội dung cuộc trò chuyện Telegram trong vòng 2 giờ gần nhất
- Tiết kiệm thời gian đọc tin nhắn thủ công
- Nâng cao hiệu quả làm việc với thông tin tổng hợp chính xác
- Hoạt động liên tục 24/7 mà không cần can thiệp
- Tích hợp với hệ thống nhớ của MongoDB để duy trì ngữ cảnh cuộc trò chuyện
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Telegram
- API Key từ OpenRouter (để sử dụng mô hình AI)
- MongoDB để lưu trữ nhớ cuộc trò chuyện
- Cài đặt node @telepilotco/n8n-nodes-telepilot trong n8n
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [workflow gốc trên n8n.io](https://n8n.io/workflows/4461)
2. Click vào nút "Download" để tải file JSON
3. Trong n8n Editor, click vào "Import from File" và chọn file JSON vừa tải về

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Telegram Login"**:
   - Cấu hình credentials cho Telegram
   - Điền thông tin đăng nhập Telegram của bạn

2. **Node "OpenRouter Chat Model"**:
   - Cấu hình credentials với API Key từ OpenRouter
   - Chọn mô hình AI phù hợp (ví dụ: "mistralai/mistral-7b-instruct")

3. **Node "MongoDB Chat Memory"**:
   - Cấu hình kết nối MongoDB
   - Đặt tên collection để lưu trữ nhớ cuộc trò chuyện

4. **Node "Get Chat Id By Name"**:
   - Điền tên chat Telegram bạn muốn tóm tắt (ví dụ: "Nhóm dự án")

5. **Node "Filter Last 2 hours"**:
   - Điều chỉnh bộ lọc thời gian nếu cần (ví dụ: thay đổi thành 1 giờ)

#### 3. Kích hoạt ⚡️
1. Click vào nút "Execute workflow" để test với dữ liệu mẫu
2. Sau khi test thành công, click vào nút "Activate" để kích hoạt workflow
3. Workflow sẽ tự động chạy theo lịch trình đã cài đặt (mặc định là mỗi giờ)

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh tóm tắt**:
   - Chỉnh sửa prompt trong node "AI Agent" để thay đổi cách tóm tắt nội dung
   - Ví dụ: "Tóm tắt cuộc trò chuyện này theo các điểm chính và hành động cần thực hiện"

2. **Kết hợp với Slack**:
   - Thêm node Slack để gửi tóm tắt đến kênh Slack tương ứng

3. **Lưu log hoạt động**:
   - Thêm node Google Sheets để lưu lịch sử tóm tắt

4. **Thông báo khi có lỗi**:
   - Cấu hình gửi email cảnh báo khi workflow gặp sự cố

### 📌 Kết luận
Workflow này sẽ giúp các sếp tiết kiệm hàng giờ mỗi ngày khi đọc và tóm tắt thủ công tin nhắn Telegram. Bằng cách tích hợp công nghệ AI và tự động hóa, các sếp có thể tập trung vào những nhiệm vụ quan trọng hơn. Hãy áp dụng ngay để nâng cao hiệu quả làm việc của mình!