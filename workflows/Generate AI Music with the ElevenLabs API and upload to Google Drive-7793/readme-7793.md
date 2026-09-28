---
title: "🚀 Tự động sáng tác nhạc AI với ElevenLabs và Google Drive qua n8n"
description: "Hướng dẫn xây dựng workflow n8n giúp tạo nhạc độc quyền bằng AI từ mô tả văn bản sử dụng ElevenLabs API, lưu trữ tự động trên Google Drive và hiển thị trực tiếp."
slug: "tao-nhac-ai-elevenlabs-google-drive-n8n"
tags: [n8n, automation, elevenlabs, google-drive, ai-music, content-creation]
keywords: [n8n workflow, tạo nhạc ai, elevenlabs api, google drive automation, tự động hóa n8n]
---

# 🚀 Tự động sáng tác nhạc AI với ElevenLabs và Google Drive qua n8n

Các sếp có bao giờ cần một đoạn nhạc nền, giai điệu độc đáo cho video, podcast hay dự án sáng tạo nhưng lại mất quá nhiều thời gian tìm kiếm hoặc chi phí thuê nhạc sĩ không? Việc tự tạo nhạc thủ công vừa tốn kém lại chẳng mấy linh hoạt.

Giải pháp ở đây là gì? Workflow n8n này sẽ giúp các sếp xây dựng một hệ thống tạo nhạc tự động 100% bằng AI. Chỉ cần điền mô tả ý tưởng vào một biểu mẫu web đơn giản, ElevenLabs AI sẽ lo phần sáng tác, file MP3 sẽ tự động được lưu vào Google Drive của các sếp và hiển thị kết quả ngay lập tức mà không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tạo nhạc theo yêu cầu:** Biến mọi ý tưởng thành âm thanh chỉ bằng văn bản mô tả.
- **Tự động lưu trữ:** File nhạc MP3 được đồng bộ trực tiếp lên thư mục Google Drive gọn gàng.
- **Giao diện thân thiện:** Cung cấp Form web trực quan để nhập yêu cầu và nghe lại thành quả ngay sau khi xử lý xong.
- **Tiết kiệm tối đa:** Không cần tốn kém chi phí bản quyền hay thời gian chờ đợi producer.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản n8n (Cloud hoặc Self-hosted).
- Tài khoản **ElevenLabs** kèm API Key (Lấy tại [ElevenLabs account](https://try.elevenlabs.io/api-music)).
- Tài khoản **Google Drive** để cấp quyền OAuth2 cho n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này và dán trực tiếp vào n8n Editor của mình, hoặc sử dụng tính năng import file JSON.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 6 nodes chính, các sếp cần cấu hình kỹ các điểm sau để hệ thống chạy mượt mà:

- **AI Music Generator (`formTrigger`):** Node này tạo ra một Web Form để người dùng nhập yêu cầu mô tả âm nhạc. Sau khi kích hoạt workflow, các sếp sẽ nhận được một URL công khai của form này.
- **API Key (`set`):** Các sếp cần dán ElevenLabs API Key của mình vào node này để hệ thống có quyền gọi API tạo nhạc.
- **elevenlabs_api (`httpRequest`):** Node này chịu trách nhiệm gửi yêu cầu tạo nhạc tới ElevenLabs dựa trên prompt từ form người dùng.
- **Upload mp3 (`googleDrive`):** Cần kết nối tài khoản Google Drive thông qua **GoogleDriveOAuth2Api** và chọn thư mục đích để lưu trữ các file nhạc MP3 được tạo ra.
- **prepare reponse (`html`):** Node này định dạng lại nội dung hiển thị kết quả bằng HTML.
- **display mp3 (`form` - completion):** Hoàn tất quy trình và hiển thị giao diện thành công kèm link nghe nhạc cho người dùng.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Test workflow** và thử nhập một mô tả bất kỳ trên Form để kiểm tra xem nhạc có được tạo và đẩy lên Google Drive thành công không.
- Nếu mọi thứ mượt mà, hãy bật nút **Active** ở góc trên bên phải để đưa workflow vào hoạt động chính thức 24/7.

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống xịn xò hơn nữa, các sếp có thể mở rộng workflow với các ý tưởng sau:
- **Thông báo qua Telegram/Slack:** Thêm node gửi tin nhắn tự động về group chat mỗi khi có một bài hát mới được tạo thành công.
- **Gửi Email tự động:** Tích hợp node Gmail để gửi file nhạc hoặc link Google Drive thẳng đến email của người yêu cầu.
- **Lưu lịch sử vào Google Sheets:** Ghi lại prompt, thời gian tạo và link file Drive để dễ dàng quản lý kho nhạc cá nhân.

### 📌 Kết luận
Với workflow n8n kết hợp ElevenLabs và Google Drive này, việc sản xuất âm nhạc bằng AI chưa bao giờ dễ dàng đến thế. Hãy áp dụng ngay vào dự án của các sếp để tối ưu hóa thời gian sáng tạo nội dung nhé!