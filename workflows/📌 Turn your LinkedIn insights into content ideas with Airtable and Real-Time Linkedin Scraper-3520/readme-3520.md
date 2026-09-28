---
title: "🚀 Tự động hóa nội dung từ LinkedIn: Chuyển đổi Insights thành ý tưởng nội dung với Airtable"
description: "Hướng dẫn tự động hóa quy trình chuyển đổi các bài viết LinkedIn bạn thích thành ý tưởng nội dung trong Airtable, tiết kiệm thời gian và tối ưu hóa nội dung cho chiến lược marketing cá nhân."
slug: "tu-dong-hoa-noi-dung-tu-linkedin-voi-airtable"
tags: [n8n, automation, no-code, linkedin, airtable]
keywords: [n8n workflow, tự động hóa nội dung, linkedin insights, airtable content ideas]
---

# 🚀 Tự động hóa nội dung từ LinkedIn: Chuyển đổi Insights thành ý tưởng nội dung với Airtable

[Đoạn mở đầu: Phân tích nỗi đau thực tế của các sếp khi phải thủ công tìm kiếm và lưu trữ ý tưởng nội dung từ LinkedIn. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian: Tự động hóa quy trình tìm kiếm và lưu trữ ý tưởng nội dung
- Tối ưu hóa nội dung: Lọc và tập trung vào những bài viết có giá trị nhất
- Trung tâm hóa thông tin: Tất cả ý tưởng nội dung được lưu trữ trong một bảng Airtable duy nhất
- Tự động hóa liên tục: Workflow chạy định kỳ để luôn cập nhật ý tưởng mới nhất
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản LinkedIn cá nhân
- API Key từ RapidAPI (để truy cập dữ liệu LinkedIn)
- Tài khoản Airtable và một bảng có tên "Content Hub" với bảng con "Ideas"
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào "Templates" ở góc trái màn hình
3. Tìm kiếm workflow "Turn your LinkedIn insights into content ideas with Airtable and Real-Time Linkedin Scraper"
4. Nhấn "Use this template" để import workflow

Hoặc bạn có thể:
1. Truy cập [link workflow gốc](https://n8n.io/workflows/3520)
2. Copy toàn bộ JSON workflow
3. Trong n8n Editor, nhấn vào "Import from Clipboard" và dán JSON vào

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Fetch LinkedIn Likes"**:
   - Cấu hình credentials: Chọn "RapidAPI" trong danh sách credentials
   - Tham số cần điền:
     - `LinkedIn Username`: Tên người dùng LinkedIn của bạn
     - `RapidAPI Key`: API Key từ tài khoản RapidAPI của bạn
     - URL: `https://linkedin-realtime-news-api.p.rapidapi.com/liked-posts`

2. **Node "Save to Airtable"**:
   - Cấu hình credentials: Chọn "Airtable API" trong danh sách credentials
   - Tham số cần điền:
     - `Base ID`: ID của cơ sở dữ liệu Airtable "Content Hub"
     - `Table Name`: "Ideas"
     - `Fields`: Đảm bảo các trường sau được ánh xạ đúng:
       - `Title`: Tiêu đề bài viết
       - `Description`: Mô tả ngắn gọn
       - `Source URL`: Liên kết đến bài viết gốc
       - `Date`: Ngày đăng bài

3. **Node "Schedule Trigger"**:
   - Cấu hình lịch chạy workflow (ví dụ: hàng ngày lúc 9:00 sáng)

#### 3. Kích hoạt ⚡️
1. Nhấn vào nút "Execute Workflow" để test chạy với dữ liệu mẫu
2. Kiểm tra kết quả trong bảng Airtable của bạn
3. Sau khi xác nhận hoạt động đúng, nhấn "Activate" để bật workflow

### ✍️ Mẹo & gợi ý nâng cao
- Kết hợp với Slack/Telegram: Thêm node gửi thông báo khi có ý tưởng nội dung mới
- Phân loại nội dung: Thêm trường "Category" trong Airtable để phân loại ý tưởng
- Tích hợp với Notion: Thay thế Airtable bằng Notion nếu bạn sử dụng công cụ này
- Lọc theo từ khóa: Thêm node lọc nội dung theo từ khóa quan trọng cho ngành nghề của bạn

### 📌 Kết luận
Workflow này giúp các sếp tiết kiệm thời gian quý giá bằng cách tự động hóa quy trình tìm kiếm và lưu trữ ý tưởng nội dung từ LinkedIn. Bằng cách tích hợp với Airtable, bạn có thể dễ dàng quản lý và truy cập lại những ý tưởng nội dung quan trọng trong tương lai. Hãy thử ngay và nâng cao hiệu quả marketing cá nhân của bạn!