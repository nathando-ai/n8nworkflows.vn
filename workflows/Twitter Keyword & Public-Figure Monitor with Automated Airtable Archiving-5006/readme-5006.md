---
title: "🚀 Tự động lưu trữ Tweets về Narendra Modi vào Airtable mỗi ngày"
description: "Hướng dẫn tự động hóa lưu trữ tweets mới nhất về Narendra Modi vào Airtable hàng ngày, loại bỏ các bản sao trùng lặp một cách hiệu quả."
slug: "tu-dong-luu-tru-tweets-ve-narendra-modi-vao-airtable"
tags: [n8n, automation, no-code, twitter, airtable]
keywords: [n8n workflow, tự động hóa, twitter, airtable, lưu trữ dữ liệu]
---

# 🚀 Tự động lưu trữ Tweets về Narendra Modi vào Airtable mỗi ngày

[Các sếp đang làm việc với dữ liệu từ Twitter nhưng gặp khó khăn khi phải theo dõi và lưu trữ thủ công các tweets mới nhất về một chủ đề cụ thể? Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình này một cách hoàn toàn không cần code.]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Lưu trữ tự động**: Các sếp không cần phải theo dõi thủ công các tweets mới nhất về chủ đề quan tâm.
- **Loại bỏ trùng lặp**: Workflow sẽ tự động kiểm tra và loại bỏ các tweets đã được lưu trữ trước đó.
- **Dữ liệu đầy đủ**: Các sếp sẽ có được đầy đủ thông tin về từng tweet bao gồm nội dung, số lượt thích, ID, URL, tác giả và thời gian đăng.
- **Tự động hóa hoàn toàn**: Workflow sẽ chạy tự động hàng ngày vào lúc 8 AM, không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Twitter Developer với quyền truy cập vào Twitter API.
- Tài khoản Airtable với một cơ sở dữ liệu (base) và một bảng (table) để lưu trữ dữ liệu.
- API keys và credentials cho cả Twitter và Airtable.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể import workflow này vào n8n bằng cách:
1. Truy cập vào n8n Editor.
2. Nhấn vào nút "Import from URL" và dán link sau: [https://n8n.io/workflows/5006](https://n8n.io/workflows/5006).
3. Hoặc tải file JSON từ link trên và import trực tiếp vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần chú ý cấu hình các node sau:

- **Node "Twitter"**:
  - Chọn operation là "search".
  - Cấu hình các tham số tìm kiếm như từ khóa (ví dụ: "Narendra Modi"), số lượng tweets cần lấy (ví dụ: 100).

- **Node "Set_AT_list"**:
  - Cấu hình các trường dữ liệu cần lưu trữ từ tweets vào Airtable. Các trường thông dụng bao gồm:
    - `Text`: Nội dung của tweet.
    - `Likes`: Số lượt thích của tweet.
    - `ID`: ID của tweet.
    - `URL`: URL của tweet.
    - `Author`: Tác giả của tweet.
    - `Timestamp`: Thời gian đăng tweet.

- **Node "get airtable list"**:
  - Chọn operation là "list".
  - Cấu hình các tham số để lấy danh sách các bản ghi hiện có trong bảng Airtable.

- **Node "set twitter data"**:
  - Cấu hình các trường dữ liệu cần lưu trữ từ tweets vào Airtable.

- **Node "Leave only new tweets"**:
  - Cấu hình các tham số để so sánh và loại bỏ các tweets đã tồn tại trong Airtable.

- **Node "Append new tweets to airtable"**:
  - Chọn operation là "append".
  - Cấu hình các tham số để thêm các tweets mới vào bảng Airtable.

- **Node "8 AM"**:
  - Cấu hình thời gian chạy workflow hàng ngày vào lúc 8 AM.

#### 3. Kích hoạt ⚡️
Sau khi cấu hình xong, các sếp cần:
1. Kiểm tra và chạy thử workflow với dữ liệu mẫu để đảm bảo mọi thứ hoạt động đúng.
2. Bật chế độ Active cho workflow để nó chạy tự động hàng ngày vào lúc 8 AM.

### ✍️ Mẹo & gợi ý nâng cao
- **Thay đổi từ khóa**: Các sếp có thể thay đổi từ khóa tìm kiếm trong node "Twitter" để theo dõi các chủ đề khác như tên của các chính trị gia, thương hiệu, hoặc xu hướng mới.
- **Thêm thông báo**: Các sếp có thể cấu hình workflow để gửi thông báo qua email hoặc Slack khi có các tweets mới được lưu trữ.
- **Lưu trữ dữ liệu định kỳ**: Các sếp có thể cấu hình workflow để lưu trữ dữ liệu theo các khoảng thời gian khác nhau (ví dụ: hàng tuần, hàng tháng).
- **Tích hợp với các công cụ khác**: Các sếp có thể tích hợp workflow này với các công cụ khác như Google Sheets, Notion, hoặc các công cụ phân tích dữ liệu khác để mở rộng khả năng sử dụng.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa việc lưu trữ tweets mới nhất về một chủ đề cụ thể vào Airtable hàng ngày, loại bỏ các bản sao trùng lặp một cách hiệu quả. Với việc cấu hình đơn giản và chạy tự động, các sếp có thể tiết kiệm thời gian và tập trung vào các công việc quan trọng hơn. Hãy áp dụng ngay workflow này để tối ưu hóa quy trình làm việc của các sếp!