---
title: "📰 Tự động hóa Tin tức Bền vững Châu Âu với RSS, GPT, Gmail, ElevenLabs & Telegram"
description: "Hướng dẫn tự động hóa thu thập, phân loại và gửi tin tức bền vững Châu Âu hàng ngày qua email và tin nhắn thoại qua Telegram"
slug: "tu-dong-hoa-tin-tuc-ben-vung-chau-au"
tags: [n8n, automation, no-code, AI, social media, sustainability]
keywords: [n8n workflow, tự động hóa tin tức, AI phân loại tin, tự động hóa email, tự động hóa Telegram]
---

# 📰 Tự động hóa Tin tức Bền vững Châu Âu với RSS, GPT, Gmail, ElevenLabs & Telegram

[Các sếp] có biết không? Với lượng tin tức hàng ngày về các chính sách và dự án bền vững của Châu Âu, việc theo dõi thủ công là một công việc mệt mỏi và dễ bỏ sót thông tin quan trọng. Workflow này sẽ giúp các sếp tự động hóa toàn bộ quy trình từ thu thập tin tức đến gửi báo cáo qua email và tin nhắn thoại qua Telegram.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động thu thập và phân loại tin tức hàng ngày
- **Chính xác cao**: AI phân loại tin tức dựa trên chủ đề cụ thể
- **Cá nhân hóa**: Nhận báo cáo theo định dạng HTML và tin nhắn thoại
- **Hoạt động liên tục**: Tự động chạy hàng ngày vào lúc 9:00 sáng
- **Tránh trùng lặp**: Kiểm tra và loại bỏ tin tức đã được gửi trước đó
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Gmail để gửi email báo cáo
- API Key từ OpenAI để phân loại tin tức
- API Key từ ElevenLabs để tạo tin nhắn thoại
- Thông tin xác thực Telegram để gửi tin nhắn thoại
- Tạo một bảng dữ liệu (datatable) với các cột: title, link, content, contentSnippet, guid, categories, createDate (kiểu dữ liệu: string)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấn vào nút "Import from URL" và dán link sau: [https://n8n.io/workflows/10961](https://n8n.io/workflows/10961)
3. Hoặc tải file JSON về và import từ file

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Trigger: 09:00 am** - Đảm bảo thời gian chạy phù hợp với nhu cầu của bạn
2. **RSS News EU** - Kiểm tra URL nguồn tin RSS để đảm bảo nó cập nhật liên tục
3. **Topic Config** - Cấu hình chủ đề và mô tả chủ đề trong node này để phù hợp với nhu cầu của bạn
4. **Classify News based on a Topic** - Thêm OpenAI credentials và kiểm tra mô hình được sử dụng (gpt-4.1-mini)
5. **Send the digest** - Cấu hình Gmail credentials và địa chỉ email nhận báo cáo
6. **Generate Voice Message** - Thêm ElevenLabs credentials và kiểm tra giọng đọc phù hợp
7. **Send Voice Summary** - Cấu hình Telegram credentials và Chat ID để gửi tin nhắn thoại
8. **Archived News, Add News, Today's News** - Kết nối tất cả các node này với bảng dữ liệu đã tạo

#### 3. Kích hoạt ⚡️
1. Chạy test với dữ liệu mẫu để kiểm tra toàn bộ quy trình
2. Kích hoạt workflow bằng cách nhấn nút "Active"

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh chủ đề**: Thay đổi chủ đề và mô tả chủ đề trong node Topic Config để phù hợp với nhu cầu cụ thể của bạn
2. **Tùy chỉnh định dạng email**: Chỉnh sửa mã trong node Generate a Digest in HTML để thay đổi định dạng email theo ý muốn
3. **Thêm kênh thông báo**: Kết nối với Slack hoặc Microsoft Teams để nhận báo cáo cùng lúc
4. **Lưu trữ tin tức**: Thêm node lưu trữ tin tức vào cơ sở dữ liệu để phân tích dài hạn

### 📌 Kết luận
Workflow này sẽ giúp các sếp tiết kiệm thời gian quý giá trong việc theo dõi tin tức bền vững Châu Âu hàng ngày. Với sự kết hợp của RSS, AI phân loại, email và tin nhắn thoại, các sếp sẽ nhận được thông tin chính xác và cập nhật một cách tự động. Hãy áp dụng ngay để tối ưu hóa quy trình làm việc của bạn!