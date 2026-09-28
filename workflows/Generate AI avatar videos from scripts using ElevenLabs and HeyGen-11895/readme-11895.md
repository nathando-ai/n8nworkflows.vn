---
title: "🚀 Tự động tạo video AI Avatar từ kịch bản với ElevenLabs và HeyGen bằng n8n"
description: "Hướng dẫn chi tiết xây dựng workflow n8n tự động hóa quy trình tạo video AI avatar chuyên nghiệp từ kịch bản văn bản sử dụng giọng đọc ElevenLabs và công nghệ tạo video HeyGen."
slug: "tu-dong-tao-video-ai-avatar-elevenlabs-heygen-n8n"
tags: [n8n, automation, no-code, AI, ElevenLabs, HeyGen, Content Creation]
keywords: [n8n workflow, tạo video ai, elevenlabs heygen, tự động hóa video, ai avatar n8n]
---

# 🚀 Tự động tạo video AI Avatar từ kịch bản với ElevenLabs và HeyGen

Việc sản xuất video ngắn, video marketing hay video đào tạo với người đại diện ảo (AI Avatar) đang trở thành xu hướng giúp tiết kiệm chi phí nhân sự và thời gian quay dựng. Tuy nhiên, nếu làm thủ công qua từng nền tảng — từ việc tạo giọng đọc ở ElevenLabs, tải file âm thanh lên HeyGen, tạo video, chờ đợi render rồi tải về Google Drive — các sếp sẽ mất rất nhiều thao tác lặp đi lặp lại.

Được thiết kế bởi chuyên gia tự động hóa **Rahul Joshi**, workflow n8n này sẽ giải quyết triệt để bài toán trên. Hệ thống sẽ tự động hóa từ đầu đến cuối: nhận kịch bản, tạo giọng đọc siêu thực, tổng hợp thành video AI Avatar, lưu trữ trên Google Drive và gửi thông báo hoàn tất qua Slack. Tất cả diễn ra hoàn toàn tự động mà không cần can thiệp thủ công!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow xử lý các tác vụ nặng (như render và tải video từ HeyGen) chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%**: Biến văn bản thành video AI hoàn chỉnh chỉ thông qua một yêu cầu Webhook duy nhất.
- **Chất lượng đỉnh cao**: Kết hợp công nghệ lồng tiếng siêu thực của ElevenLabs và công nghệ AI Avatar chuyển động mượt mà từ HeyGen.
- **Lưu trữ tự động**: Video sau khi xuất xưởng sẽ được tự động lưu trữ gọn gàng lên Google Drive để dễ dàng chia sẻ hoặc sử dụng tiếp.
- **Giám sát thông minh**: Tích hợp cơ chế kiểm tra trạng thái render video (Polling), chờ đợi thông minh và gửi cảnh báo qua Slack khi có lỗi xảy ra.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và thông tin xác thực (Credentials) sau:
1. **n8n Instance**: Đã cài đặt n8n (Cloud hoặc Self-hosted).
2. **ElevenLabs API Key**: Tài khoản ElevenLabs để tạo giọng đọc AI chất lượng cao.
3. **HeyGen API Key**: Tài khoản HeyGen để tạo video AI Avatar.
4. **Google Drive Credentials**: Tài khoản GoogleOAuth2 để lưu trữ video.
5. **Slack Bot Token**: (Tùy chọn) Để nhận thông báo trạng thái hoặc lỗi qua Slack.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ kho lưu trữ n8n.
- Trong giao diện n8n, chọn **Add workflow** -> Nhấp vào biểu tượng ba chấm ở góc trên bên phải -> Chọn **Import from File** và chọn file JSON đã tải.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 16 nodes hoạt động nhịp nhàng. Các sếp cần cấu hình kỹ các node trọng điểm sau:

- **Webhook - Receive Request**: Node điểm khởi đầu nhận kịch bản/dữ liệu đầu vào từ hệ thống của các sếp (hoặc từ form, CRM). Hãy copy URL Webhook để cấu hình gửi request.
- **Parse Request Parameters (Set)**: Đảm bảo các tham số đầu vào như kịch bản (`script`), ID giọng đọc ElevenLabs (`voice_id`), và Avatar ID của HeyGen được map chính xác.
- **Generate Audio with ElevenLabs (HTTP Request)**: Cấu hình API Endpoint của ElevenLabs, gắn `Credential` API Key và truyền nội dung kịch bản để tạo file âm thanh.
- **Upload Audio to HeyGen & Create Avatar Video with Audio (HTTP Request)**: Kết nối API HeyGen bằng Credentials tương ứng, truyền file audio vừa tạo kết hợp với Avatar ID có sẵn trong tài khoản HeyGen của các sếp.
- **Poll Video Status & Check If Completed (HTTP Request & IF)**: Node này kiểm tra xem video trên HeyGen đã render xong chưa. Node **Wait 5 Seconds** giúp giãn cách thời gian gọi API tránh bị chặn rate-limit.
- **Download Video & Upload to Google Drive**: Cấu hình thư mục đích trên Google Drive để lưu video thành phẩm.
- **Error Handler Trigger & Send a message (Slack)**: Cấu hình kênh Slack để nhận thông báo khẩn cấp nếu quá trình tạo video gặp lỗi (ví dụ hết quota ElevenLabs hoặc HeyGen lỗi render).

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và gửi một request mẫu tới Webhook để test toàn bộ luồng chạy.
- Kiểm tra kết quả trên Google Drive và Slack.
- Nếu mọi thứ mượt mà, hãy gạt nút **Active** ở góc trên bên phải để đưa workflow vào vận hành chính thức 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo**: Thay vì chỉ dùng Slack, các sếp có thể bổ sung thêm node Telegram hoặc Zalo OA để nhận link video ngay trên điện thoại.
- **Tích hợp Google Sheets**: Thêm bước lưu log kịch bản, thời gian tạo và link video Google Drive vào một bảng tính Google Sheets để dễ dàng quản lý chiến dịch nội dung.
- **Tự động đăng social**: Kết nối thêm node Facebook, TikTok hoặc YouTube để tự động đăng tải video ngay khi upload lên Google Drive thành công.

### 📌 Kết luận
Workflow tích hợp ElevenLabs và HeyGen này là một "vũ khí" cực kỳ mạnh mẽ giúp các nhà sáng tạo nội dung và doanh nghiệp tối ưu hóa quy trình sản xuất video bằng AI. Hãy cài đặt ngay hôm nay để tiết kiệm hàng chục giờ làm việc thủ công mỗi tuần!