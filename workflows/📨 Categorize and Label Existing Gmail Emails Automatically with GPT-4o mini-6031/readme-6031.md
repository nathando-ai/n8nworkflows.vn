---
title: "🚀 Tự động phân loại và gắn nhãn email Gmail hiện có bằng GPT-4o mini"
description: "Hướng dẫn chi tiết cách tự động hóa việc phân loại và gắn nhãn email Gmail hiện có bằng AI GPT-4o mini trong n8n. Tiết kiệm thời gian và nâng cao hiệu quả quản lý email."
slug: "tu-dong-phan-loai-va-gan-nhan-email-gmail-bang-gpt-4o-mini"
tags: [n8n, automation, no-code, gmail, ai]
keywords: [n8n workflow, tự động hóa email, gmail automation, gpt-4o-mini, phân loại email]
---

# 🚀 Tự động phân loại và gắn nhãn email Gmail hiện có bằng GPT-4o mini

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp có bao giờ cảm thấy mệt mỏi khi phải phân loại hàng trăm email Gmail thủ công? Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình này chỉ trong vài bước đơn giản, giúp tiết kiệm thời gian quý giá và nâng cao hiệu quả quản lý email.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đáng kể trong việc quản lý email
- Tự động phân loại email chính xác dựa trên nội dung
- Tăng tính tổ chức và dễ dàng tìm kiếm email
- Hoạt động liên tục mà không cần can thiệp thủ công
- Tích hợp AI GPT-4o mini để phân loại thông minh
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Gmail đã kết nối với n8n
- Các nhãn (labels) đã được tạo sẵn trong Gmail
- Tài khoản OpenAI với quyền truy cập GPT-4o mini
- Các node AI Agent và Structured Output Parser trong n8n
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow này vào n8n của bạn, các sếp có thể thực hiện theo các bước sau:

1. Truy cập vào trang workflow gốc: [Categorize and Label Existing Gmail Emails Automatically with GPT-4o mini](https://n8n.io/workflows/6031)
2. Nhấp vào nút "Download" để tải file JSON của workflow
3. Trong n8n Editor, nhấp vào biểu tượng "+" ở góc trái màn hình
4. Chọn "Import from File" và chọn file JSON vừa tải về
5. Hoàn tất quá trình import

Hoặc các sếp cũng có thể copy/paste JSON từ trang workflow gốc vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

1. **Node "Get many messages" (Gmail)**:
   - Chọn credentials Gmail OAuth2 đã được thiết lập
   - Điều chỉnh tham số "Limit" để xác định số lượng email muốn xử lý (mặc định là 50)

2. **Node "Label Checker Filter" (Filter)**:
   - Đảm bảo cấu hình để bỏ qua các email đã có nhãn

3. **Node "Give a Label AI Agent" (Agent)**:
   - Kiểm tra và điều chỉnh prompt AI để phù hợp với nhu cầu phân loại email
   - Đảm bảo các nhãn trong prompt khớp chính xác với nhãn đã tạo trong Gmail

4. **Node "Switch"**:
   - Kiểm tra và cấu hình các điều kiện để chuyển hướng email đến nhãn phù hợp
   - Mỗi nhánh trong Switch node phải khớp với một nhãn email

5. **Các node Gmail (Work, Personal, Finance, Shopping, travel, Newsletters, Others)**:
   - Đảm bảo mỗi node áp dụng đúng nhãn email tương ứng
   - Kiểm tra các credentials Gmail đã được thiết lập chính xác

#### 3. Kích hoạt ⚡️
Sau khi cấu hình xong các node quan trọng:

1. Thực hiện test run với dữ liệu mẫu để kiểm tra hoạt động của workflow
2. Kiểm tra kết quả phân loại email để đảm bảo độ chính xác
3. Bật chế độ Active workflow để chạy tự động khi cần thiết

### ✍️ Mẹo & gợi ý nâng cao
- Các sếp có thể thêm hoặc bớt các danh mục trong prompt AI và node Switch
- Điều chỉnh kích thước batch của email để xử lý nhiều hoặc ít hơn mỗi lần chạy
- Tùy chỉnh prompt AI để phù hợp với loại email mà các sếp nhận (công việc, cá nhân, hỗ trợ khách hàng)
- Kết hợp với Slack/Telegram để nhận thông báo khi workflow hoàn thành
- Lưu log hoạt động của workflow để theo dõi hiệu suất
- Thiết lập gửi báo cáo định kỳ về kết quả phân loại email

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện cho việc tự động hóa phân loại và gắn nhãn email Gmail hiện có. Với tích hợp AI GPT-4o mini, các sếp có thể nâng cao đáng kể hiệu quả quản lý email của mình. Hãy áp dụng ngay để tiết kiệm thời gian và nâng cao năng suất làm việc!