---
title: "🚀 Tự động tạo caption Twitter/X từ hình ảnh Google Drive bằng Cloudinary và GPT-4o-mini"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa hoàn toàn quy trình nhận ảnh từ Google Drive, lưu trữ qua Cloudinary, phân tích bằng Azure OpenAI GPT-4o-mini và gửi kết quả caption qua Email."
slug: "tu-dong-tao-twitter-caption-tu-google-drive-cloudinary-gpt-4o-mini"
tags: [n8n, automation, ai, google-drive, cloudinary, azure-openai, twitter-automation]
keywords: [n8n workflow, tao caption twitter tu dong, google drive cloudinary ai, azure openai gpt-4o-mini, tu dong hoa n8n]
---

# 🚀 Tự động tạo caption Twitter/X từ hình ảnh Google Drive với AI

Các sếp làm nội dung trên mạng xã hội chắc chắn hiểu cảm giác mệt mỏi khi cứ phải ngồi hàng giờ liền nhìn vào hình ảnh, vắt óc nghĩ caption, thêm hashtag sao cho thật thu hút trên Twitter/X. Việc này vừa tốn thời gian, vừa dễ bị "cạn kiệt" ý tưởng vào những ngày nước sôi lửa bỏng.

Thấu hiểu nỗi đau đó, workflow n8n cực đỉnh này do chuyên gia Rahul Joshi thiết kế sẽ giúp các sếp tự động hóa **100%** quy trình: Cứ có ảnh mới đổ vào Google Drive, hệ thống tự động đẩy lên đám mây Cloudinary, gọi AI đa phương thức (GPT-4o-mini) phân tích và viết ngay những chiếc caption cuốn hút kèm hashtag bắt trend, sau đó gửi thẳng vào email cho các sếp lựa chọn! Không cần code phức tạp, chỉ cần thiết lập một lần và để robot làm việc thay các sếp 24/7.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 không lo mất kết nối, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian**: Không còn phải tự viết caption thủ công cho từng bức ảnh.
- **AI thông minh, sáng tạo**: Sử dụng mô hình Azure OpenAI GPT-4o-mini để tạo nội dung chuẩn văn phong mạng xã hội, có kèm hashtag tối ưu.
- **Quy trình liền mạch (Pipeline)**: Tự động từ lúc upload ảnh lên Google Drive đến khi nhận kết quả qua Email.
- **Hoạt động tự động 24/7**: Chạy ngầm liên tục, chỉ cần bỏ ảnh vào thư mục là có ngay nội dung.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI "LÊN ĐỒ"]
- **n8n Instance**: Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Google Drive Account**: Cấp quyền OAuth2 (`googleDriveOAuth2Api`) để theo dõi thư mục và tải tệp.
- **Cloudinary Account**: Tài khoản lưu trữ ảnh với API Key/Secret và `upload_preset` đã được cấu hình.
- **Azure OpenAI Account**: Endpoint và API Key để kết nối với model `gpt-4o-mini`.
- **SMTP Server**: Thông tin cấu hình SMTP để gửi email thông báo kết quả.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow (hoặc tải file JSON từ n8n template), sau đó vào giao diện n8n Editor, chọn **Add workflow** -> Nhấn dấu ba chấm ở góc trên bên phải -> **Import from File / Clipboard** và dán đoạn JSON vào là xong.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 6 nodes chính, các sếp cần cấu hình kỹ các phần sau để hệ thống chạy mượt mà:

- **Get files from drive (`googleDriveTrigger`)**: 
  - Kết nối tài khoản Google Drive qua `googleDriveOAuth2Api`.
  - Chọn thư mục cụ thể trên Drive mà các sếp muốn hệ thống theo dõi (Mỗi khi có ảnh mới up lên thư mục này, workflow sẽ kích hoạt).
- **Download the drive files (`googleDrive`)**: 
  - Cấu hình operation là `download` để lấy dữ liệu thô của hình ảnh phục vụ cho bước tiếp theo.
- **Upload frames to cloudinary (`httpRequest`)**: 
  - Sử dụng phương thức HTTP Request kèm `httpBasicAuth` hoặc API Key của Cloudinary.
  - Đảm bảo truyền đúng file nhị phân từ node Google Drive lên Cloudinary để lấy link URL public (giúp AI có thể truy cập được hình ảnh).
- **Azure OpenAI Chat Model (`lmChatAzureOpenAi`) & Basic LLM Chain (`chainLlm`)**: 
  - Kết nối credential `azureOpenAiApi`.
  - Kiểm tra tham số Model đã chọn sẵn là `gpt-4o-mini`.
  - Tinh chỉnh Prompt trong chuỗi LLM để hướng dẫn AI đóng vai chuyên gia viết content Twitter/X (yêu cầu văn phong ngắn gọn, hấp dẫn, kèm hashtag).
- **Send email (`emailSend`)**: 
  - Kết nối tài khoản SMTP của các sếp (Gmail, SendGrid, Mailgun...).
  - Cấu hình nội dung email nhận về bao gồm: Link ảnh trên Cloudinary và phần Caption do AI vừa tạo.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Test workflow** và thử tải một tấm ảnh lên thư mục Google Drive đã chọn để kiểm tra toàn bộ luồng chạy.
- Nếu email gửi về thành công và nhận được caption xịn sò, các sếp hãy gạt công tắc sang **Active** để workflow chính thức tự động vận hành.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Chat ứng dụng**: Thay vì chỉ nhận Email, các sếp có thể nối thêm node Telegram hoặc Slack để nhận thông báo caption ngay trên điện thoại cực kỳ tiện lợi.
- **Lưu trữ kết quả**: Thêm một node Google Sheets vào cuối luồng để lưu lại lịch sử các caption AI đã tạo, dễ dàng quản lý và tái sử dụng nội dung.
- **Đa dạng hóa mạng xã hội**: Mở rộng prompt để AI tạo đồng thời caption cho cả LinkedIn, Facebook hoặc Instagram chỉ trong một lần chạy.

### 📌 Kết luận
Việc tự động hóa quy trình sáng tạo nội dung chưa bao giờ dễ dàng đến thế với sức mạnh của n8n và AI đa phương thức. Hãy cài đặt ngay workflow này để giải phóng sức lao động và tối ưu hóa hiệu suất làm việc của các sếp ngay hôm nay!