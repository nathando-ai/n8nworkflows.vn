---
title: "🚀 Tự động tạo Video Sales Letter bằng Google VEO3, Creatomate & Facebook Publishing với n8n"
description: "Xây dựng hệ thống tự động hóa toàn diện từ form đầu vào, sinh kịch bản AI, tạo video bằng Google VEO3, chèn phụ đề Creatomate và tự động xuất bản lên Facebook."
slug: "tu-dong-tao-video-sales-letter-google-veo3-creatomate-facebook"
tags: [n8n, automation, ai-video, google-veo, facebook-marketing, content-creation]
keywords: [n8n workflow, tạo video AI, google veo3, creatomate captions, facebook publishing, tự động hóa marketing]
---

# 🚀 Tự động hóa sản xuất Video Sales Letter (VSL) và đăng bài Facebook với AI

Các sếp có đau đầu khi mỗi lần muốn chạy chiến dịch quảng cáo hoặc làm nội dung video ngắn (UGC/VSL) đều phải tốn hàng giờ viết kịch bản, dựng hình, gắn phụ đề rồi lại thủ công đăng lên mạng xã hội? Công việc lặp đi lặp lại này ngốn rất nhiều thời gian và ngân sách nhân sự.

Giải pháp ở đây chính là workflow n8n được thiết kế bởi chuyên gia LukaszB. Workflow này sẽ giúp các sếp **tự động hóa 100% quy trình sản xuất video sales letter** từ một form thông tin đơn giản, kết hợp sức mạnh của OpenAI, Google VEO3, Creatomate và tự động đăng tải lên Facebook mà không cần đụng tay vào khâu chỉnh sửa phức tạp.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Chỉ cần điền Form, hệ thống tự lo phần kịch bản, tạo video, chèn sub và publish lên Facebook.
- **Tiết kiệm 90% thời gian:** Không còn cảnh chờ đợi render thủ công hay thuê biên tập viên cho các video mẫu cơ bản.
- **AI thông minh:** Sử dụng OpenAI để viết kịch bản chuyển đổi cao và tối ưu hóa prompt hình ảnh sản phẩm.
- **Chất lượng chuyên nghiệp:** Tích hợp công cụ tạo video tiên tiến và tự động gắn phụ đề bắt mắt (Captions) giữ chân người xem.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI BẮT ĐẦU]
- **n8n Instance:** Đã cài đặt n8n (Phiên bản hỗ trợ LangChain và các node HTTP).
- **Tài khoản OpenAI:** Lấy API Key để chạy các node AI phân tích, viết kịch bản và sinh prompt.
- **Google Cloud Storage (GCS):** Lưu trữ tạm thời các file hình ảnh/video để có URL công khai phục vụ cho các API khác.
- **Google VEO3 & Creatomate Credentials:** API/Token xác thực để gọi dịch vụ tạo video và chèn phụ đề.
- **Facebook Page:** Quyền kết nối và đăng bài qua node Upload Post.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ nguồn cấp hoặc copy toàn bộ mã JSON.
- Trong giao diện n8n, chọn **Workflows** -> **Import from File** hoặc dán trực tiếp vào vùng làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống vận hành trơn tru, các sếp cần chú ý cấu hình các node cốt lõi sau:
- **On form submission & Form Input:** Cài đặt giao diện form đầu vào để thu thập thông tin sản phẩm, ý tưởng hoặc hình ảnh từ người dùng.
- **SET Credentials:** Nơi lưu trữ các khóa API cấu hình chung cho toàn hệ thống. Hãy đảm bảo điền chính xác các biến môi trường.
- **OpenAI Chat Model, Content writer, Product Image Describing, VeoPrompt, UGC.Formulator:** Kết nối tài khoản OpenAI của bạn. Cấu hình prompt chi tiết nếu muốn điều chỉnh giọng văn (tone of voice) của kịch bản video.
- **Upload to GCS (To be accessible via URL):** Cấu hình kết nối Google Cloud Storage để upload file ảnh/video và lấy public URL phục vụ cho bước sinh video.
- **Generate Video1, Fetch Status, Wait:** Cấu hình gọi API tới dịch vụ Google VEO3 kèm cơ chế vòng lặp kiểm tra trạng thái render video (`Fetch Status` và `Wait`).
- **Add Captions, Captions added?:** Tích hợp với dịch vụ Creatomate để tự động thêm phụ đề chạy theo lời thoại.
- **Upload Post:** Kết nối với trang Facebook đích để tự động xuất bản video hoàn thiện cùng nội dung text đi kèm.

#### 3. Kích hoạt ⚡️
- Nhấn **Test step** hoặc **Execute Workflow** với dữ liệu mẫu trên Form để kiểm tra từng chặng (từ kịch bản -> render video -> chèn sub).
- Sau khi test thành công không báo lỗi, gạt công tắc sang **Active** để đưa workflow vào trạng thái vận hành tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm bước thông báo:** Tích hợp thêm node Telegram hoặc Slack sau node `Upload Post` để nhận thông báo ngay khi video đã lên sóng thành công.
- **Lưu trữ database:** Đẩy toàn bộ thông tin kịch bản, link video GCS và link Facebook Post vào Google Sheets hoặc Airtable để dễ dàng quản lý kho nội dung.
- **Mở rộng nền tảng:** Nhân bản node xuất bản để ngoài Facebook, video còn được tự động đẩy lên TikTok, YouTube Shorts hoặc Instagram Reels cùng lúc.

### 📌 Kết luận
Workflow tạo Video Sales Letter tự động này là mảnh ghép hoàn hảo cho các đội ngũ marketing hiện đại muốn tối ưu hóa hiệu suất sản xuất nội dung video ngắn. Hãy triển khai ngay hôm nay để bứt phá doanh thu và tiết kiệm tối đa nguồn lực!