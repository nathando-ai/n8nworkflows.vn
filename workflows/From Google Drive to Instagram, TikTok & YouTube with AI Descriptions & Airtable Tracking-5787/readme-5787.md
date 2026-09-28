---
title: "🚀 Tự động đăng video từ Google Drive lên Instagram, TikTok & YouTube kèm AI Description và Airtable Tracking qua n8n"
description: "Hướng dẫn xây dựng hệ thống tự động hóa đa nền tảng: nhận video từ Google Drive, dùng OpenAI phiên âm và viết caption, đăng tự động lên Instagram, TikTok, YouTube và quản lý trạng thái trên Airtable."
slug: "tu-dong-dang-video-google-drive-len-social-media-ai-airtable"
tags: [n8n, automation, no-code, social-media, ai, open-ai, google-drive, airtable, tiktok, instagram, youtube]
keywords: [n8n workflow, tự động hóa mạng xã hội, đăng video tự động tiktok instagram youtube, ai viết mô tả video, quản lý nội dung airtable, google drive automation]
---

# 🚀 Tự động đăng video từ Google Drive lên Instagram, TikTok & YouTube kèm AI Description và Airtable Tracking

Các sếp có đang cảm thấy mệt mỏi khi mỗi lần xuất video xong phải thủ công ngồi tải lên Google Drive, viết caption cho từng nền tảng (TikTok, Instagram, YouTube), rồi copy paste qua lại và lưu bảng theo dõi không? Việc này vừa tốn thời gian, dễ sót việc lại cực kỳ nhàm chán.

Đừng lo, bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n cực kỳ xịn sò được chia sẻ bởi **Juan Carlos Cavero Gracia**. Hệ thống này sẽ tự động hóa 100% quy trình: Nhận video từ Google Drive -> Dùng AI (OpenAI) phiên âm, viết tiêu đề/mô tả hấp dẫn -> Đăng đồng loạt lên Instagram, TikTok, YouTube và tự động cập nhật trạng thái chi tiết vào bảng quản lý Airtable!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian vận hành**: Chỉ cần thả file video vào Google Drive, mọi việc còn lại hệ thống tự lo.
- **AI thông minh hóa nội dung**: Tự động nghe audio từ video (Whisper) và viết mô tả, hashtag chuẩn SEO cho từng nền tảng xã hội bằng OpenAI.
- **Đa kênh đồng bộ (Omnichannel)**: Đăng tải liền mạch lên cả Instagram, TikTok và YouTube cùng lúc.
- **Quản lý chuyên nghiệp**: Mọi trạng thái thành công hay thất bại đều được log lại chi tiết trên Airtable và gửi cảnh báo qua Telegram nếu có lỗi xảy ra.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động mượt mà, các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **n8n Instance**: Đã cài đặt sẵn sàng.
- **Google Drive Account**: Thư mục chuyên dụng để chứa video đầu vào.
- **OpenAI Account**: Lấy API Key để chạy tính năng phiên âm (Transcribe) và tạo nội dung (Generate Description).
- **Airtable Account**: Tạo sẵn Base và Table quản lý nội dung video.
- **Tài khoản upload-post.com**: Dịch vụ trung gian hỗ trợ API upload video lên các nền tảng mạng xã hội.
- **Telegram Bot (Tùy chọn)**: Để nhận thông báo lỗi (Error Trigger).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể lấy mã JSON gốc từ link n8n chính chủ hoặc copy workflow, sau đó dán trực tiếp vào n8n Editor của mình thông qua tính năng Import từ Clipboard.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import thành công 24 nodes, các sếp tiến hành cấu hình chi tiết các thành phần cốt lõi sau:

- **Set Variables**: Khai báo các biến cấu hình quan trọng như Base ID và Table ID của Airtable để workflow biết nơi đọc/ghi dữ liệu.
- **Google Drive Trigger**: Kết nối tài khoản Google Drive (`googleDriveOAuth2Api`) và trỏ chính xác vào thư mục (Folder) mà các sếp sẽ dùng để upload video thô lên.
- **Google Drive (Download)**: Node thực hiện tải file video từ Drive về hệ thống xử lý.
- **Create Airtable Record**: Kết nối `airtableTokenApi`, cấu hình để thêm một dòng mới khi có video vừa được phát hiện trên Drive. Các trường (fields) cần chuẩn bị trên Airtable gồm: *Video Name, Google Drive Link, File ID, Instagram Status, TikTok Status, YouTube Status, Upload Date, Description*.
- **Get Audio from Video & Generate Description for Videos**: Kết nối `openAiApi`. Node này sẽ dùng mô hình Whisper để chuyển audio thành text, sau đó dùng GPT tạo caption cuốn hút dựa theo prompt tùy chỉnh của các sếp.
- **Update Airtable with Description**: Cập nhật phần mô tả do AI viết ngược lại vào Airtable tương ứng với dòng dữ liệu của video đó.
- **Upload Video to TikTok / Instagram / YouTube**: Các node `httpRequest` sử dụng API từ dịch vụ `upload-post.com` (`httpHeaderAuth`). Các sếp cần cấu hình API Token từ nền tảng này để đẩy video lên các mạng xã hội.
- **Update Status Nodes (Success/TikTok/Instagram/YouTube)**: Các node Airtable cập nhật trạng thái tiến trình upload (Thành công/Thất bại) lên bảng quản lý.
- **Error Trigger & Telegram**: Kết nối Telegram API để nhận tin nhắn cảnh báo ngay lập tức nếu có bất kỳ bước nào trong quy trình gặp sự cố.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và thử nghiệm bằng cách upload một video mẫu vào thư mục Google Drive đã cấu hình để kiểm tra luồng chạy từ đầu đến cuối.
- Kiểm tra lại trên Airtable, OpenAI, các kênh MXH xem dữ liệu đã đồng bộ chuẩn chưa.
- Sau khi test ngon lành, gạt công tắc sang **Active** để hệ thống tự động chạy 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng thông báo**: Thay vì chỉ dùng Telegram khi lỗi, các sếp có thể cấu hình thêm một nhánh gửi thông báo thành công về Slack hoặc nhóm Zalo để team content nắm tình hình.
- **Tùy biến Prompt AI**: Tinh chỉnh prompt trong node OpenAI để AI viết caption chèn thêm các hashtag riêng của thương hiệu hoặc kêu gọi hành động (CTA) phù hợp với sản phẩm.
- **Lọc định dạng file**: Thêm một node `If` kiểm tra định dạng file ở đầu vào (chỉ nhận `.mp4`, `.mov`) để tránh việc người dùng lỡ tay upload file tài liệu hoặc hình ảnh gây lỗi hệ thống.

### 📌 Kết luận
Tự động hóa quy trình sản xuất và đăng tải nội dung chưa bao giờ dễ dàng đến thế với sức mạnh kết hợp giữa n8n, Google Drive, AI và Airtable. Áp dụng ngay workflow này để giải phóng bản thân khỏi các tác vụ thủ công và tập trung vào việc sáng tạo nội dung chất lượng hơn các sếp nhé!