---
title: "🚀 Tự động hóa Humanize văn bản AI với Rephrasy chỉ viết lại câu bị phát hiện"
description: "Hướng dẫn sử dụng workflow n8n tích hợp Rephrasy API để phân tích, phát hiện và chỉ viết lại các câu có dấu hiệu AI, giữ nguyên vẹn giọng văn tự nhiên."
slug: "humanize-ai-text-rephrasy-n8n"
tags: [n8n, automation, ai-humanizer, rephrasy, content-creation, ai-detector]
keywords: [n8n workflow, humanize ai text, rephrasy api, viết lại văn bản ai, tự động hóa nội dung]
---

# 🚀 Tự động hóa Humanize văn bản AI với Rephrasy thông minh

Các sếp có bao giờ đau đầu vì nội dung tạo ra từ ChatGPT hay Claude quá "máy móc", dễ dàng bị các công cụ AI Detector phát hiện? Việc thuê nhân sự sửa lại toàn bộ bài viết thì tốn kém, mà dùng các công cụ humanize thông thường lại làm hỏng cấu trúc hoặc sai lệch ý nghĩa của bài viết gốc.

Workflow n8n tuyệt vời này được tác giả **Davide Boizza** thiết kế để giải quyết triệt để bài toán đó. Thay vì viết lại toàn bộ văn bản, workflow sẽ **phân tích chi tiết từng câu**, chỉ chọn ra những câu có điểm số AI cao (> 50) để đưa qua **AI Humanizer** viết lại, trong khi các câu mang giọng văn tự nhiên của con người sẽ được giữ nguyên bản tuyệt đối!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Bảo toàn ngữ nghĩa:** Chỉ can thiệp chỉnh sửa những câu bị đánh dấu là AI, giữ nguyên vẹn ý tưởng cốt lõi và văn phong tự nhiên của các câu còn lại.
- **Tiết kiệm chi phí API:** Tối ưu hóa số lượng token/request gọi đến AI Humanizer bằng cách lọc bỏ các câu đã mang tính "người".
- **Vượt qua AI Detector dễ dàng:** Biến văn bản cứng nhắc thành nội dung mượt mà, tự nhiên chuẩn SEO.
- **Hỗ trợ đa ngôn ngữ:** Hoạt động tốt với tiếng Anh, Đức, Pháp, Tây Ban Nha, Ý, Bồ Đào Nha, Hà Lan, Ba Lan, Nhật Bản.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản và API Key từ **Rephrasy** (hoặc dịch vụ AI Detector/Humanizer tương ứng) để cấu hình HTTP Bearer Auth.
- n8n Instance (Cloud hoặc Self-hosted).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tạo một workflow mới trong n8n của các sếp, sau đó copy toàn bộ mã JSON của workflow này và Paste trực tiếp vào giao diện n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node `Set text`**: Điền đoạn văn bản gốc mà các sếp muốn kiểm tra và humanize vào đây. (Hoặc có thể thay thế node kích hoạt này bằng Webhook, Google Sheets, Form trigger tùy ý).
- **Node `AI Detector` & `AI Humanizer`**: 
  - Tạo credential kiểu **HTTP Bearer Auth** và điền **Rephrasy API Key** của các sếp vào.
  - Kiểm tra lại trường `language` trong payload của node `AI Humanizer` xem đã khớp với ngôn ngữ văn bản đầu vào hay chưa.
- **Node `> 50?` (IF condition)**: Node này đóng vai trò quyết định lọc câu. Nếu điểm AI của câu > 50, nó sẽ được đẩy sang bộ phận Humanize; ngược lại sẽ đi thẳng qua nhánh `Continue...` (giữ nguyên).

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** với dữ liệu mẫu trong node Set Text để test thử nghiệm luồng chạy.
- Sau khi kiểm tra kết quả trả về tại node **Aggregate Text** đã hoàn chỉnh, các sếp gạt công tắc sang **Active** để đưa vào sử dụng chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp Google Sheets / Airtable:** Thay vì nhập tay ở node Set text, hãy kết nối với Google Sheets để tự động quét hàng loạt các bài viết draft và cập nhật lại bài hoàn chỉnh.
- **Tích hợp Telegram/Slack:** Thêm một thông báo qua chat ngay sau khi workflow hoàn tất để sếp nhận được văn bản đã được humanize tức thì.
- **Lưu trữ Log:** Lưu lại lịch sử điểm số AI trước và sau khi humanize để đánh giá hiệu quả cải thiện nội dung.

### 📌 Kết luận
Workflow này là một "vũ khí bí mật" cực kỳ mạnh mẽ cho anh em làm Content Marketing, SEO và AI Automation. Áp dụng ngay hôm nay để tối ưu hóa chất lượng nội dung tự động một cách thông minh và tiết kiệm nhất!