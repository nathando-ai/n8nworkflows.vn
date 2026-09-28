---
title: "🚀 Tự động hóa tin tức hàng ngày với AI: Tổng hợp RSS, Gemini và Slack/Gmail"
description: "Hướng dẫn chi tiết cách tự động tổng hợp tin tức từ RSS, tóm tắt bằng AI Gemini và gửi định kỳ qua Slack/Gmail - giải pháp tiết kiệm thời gian cho các sếp nghiên cứu thị trường."
slug: "tu-dong-hoa-tin-tuc-hang-ngay-voi-ai-gemini-slack-gmail"
tags: [n8n, automation, no-code, ai, market-research]
keywords: [n8n workflow, tự động hóa tin tức, ai tóm tắt, gemini api, slack automation, gmail automation]
---

# 🚀 Tự động hóa tin tức hàng ngày với AI: Tổng hợp RSS, Gemini và Slack/Gmail

[Các sếp làm nghiên cứu thị trường] chắc hẳn đã mệt mỏi với việc phải theo dõi hàng chục nguồn tin tức hàng ngày, lọc thông tin quan trọng và tóm tắt nội dung. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quá trình này với công nghệ AI tiên tiến, tiết kiệm thời gian đáng kể và nhận được thông tin chất lượng cao mỗi sáng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động tổng hợp tin tức từ nhiều nguồn trong 1 lần chạy
- **Thông tin chất lượng cao**: AI Gemini tóm tắt và đánh giá mức độ quan trọng của mỗi bài viết
- **Truy cập đa kênh**: Nhận thông tin qua cả Slack và Gmail
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công sau khi cài đặt
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Cloud với API Gemini đã kích hoạt
- Tài khoản Slack với quyền gửi tin nhắn vào kênh
- Tài khoản Gmail với quyền gửi email
- Danh sách URL nguồn tin RSS (Tech News, Hacker News...)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/13674](https://n8n.io/workflows/13674)
2. Click vào nút "Import" ở góc trên bên phải
3. Copy toàn bộ JSON workflow và dán vào n8n Editor của bạn

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node "Morning Schedule"**: Chỉnh thời gian chạy hàng ngày phù hợp với lịch làm việc của các sếp
- **Nodes "Tech News Feed" và "Hacker News Feed"**: Thay đổi URL nguồn tin RSS theo sở thích
- **Node "Gemini Chat Model"**:
  - Tạo credentials cho Google Gemini trong n8n
  - Điền API Key và chọn model phù hợp (ví dụ: gemini-pro)
- **Node "Post to Slack"**:
  - Tạo credentials cho Slack trong n8n
  - Chọn channel để gửi tin nhắn
- **Node "Email Digest"**:
  - Tạo credentials cho Gmail trong n8n
  - Điền địa chỉ email người nhận

#### 3. Kích hoạt ⚡️
1. Click vào nút "Execute Workflow" để test với dữ liệu mẫu
2. Sau khi test thành công, bật chế độ Active workflow

### ✍️ Mẹo & gợi ý nâng cao
- Thêm các nguồn tin RSS khác bằng cách sao chép và sửa đổi nodes "Tech News Feed" và "Hacker News Feed"
- Điều chỉnh prompt trong node "Summarize and Score" để phù hợp với lĩnh vực nghiên cứu của các sếp
- Thêm node lọc để chỉ gửi những bài viết có điểm số quan trọng cao hơn ngưỡng đã đặt
- Kết hợp với workflow khác để tự động phân tích cảm xúc của tin tức
- Thiết lập báo cáo định kỳ hàng tuần/tháng từ dữ liệu tổng hợp

### 📌 Kết luận
Workflow này không chỉ giúp các sếp tiết kiệm thời gian đáng kể mà còn nâng cao chất lượng thông tin nhận được. Với sự kết hợp của công nghệ AI tiên tiến và khả năng tự động hóa của n8n, các sếp có thể tập trung vào những nhiệm vụ quan trọng hơn trong công việc nghiên cứu thị trường. Hãy thử ngay và trải nghiệm cách làm việc thông minh hơn!