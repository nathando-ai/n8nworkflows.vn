---
title: "🚀 Tự động hóa tạo hình ảnh và video bất động sản bằng OpenAI và Google Drive trong n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa quy trình biến ý tưởng thô thành hình ảnh và video marketing bất động sản chuyên nghiệp qua OpenAI, Google Drive và hệ thống phê duyệt qua email."
slug: "tu-dong-hoa-tao-anh-video-bat-dong-san-openai-google-drive"
tags: [n8n, automation, ai, openai, google-drive, real-estate, content-creation]
keywords: [n8n workflow, tạo ảnh ai, video bất động sản, openai api, google drive automation, ai agent n8n]
---

# 🚀 Tự động hóa tạo hình ảnh & video bất động sản với AI trong n8n

Các sếp làm trong ngành bất động sản hoặc Agency marketing chắc chắn hiểu rõ nỗi đau: Việc tạo ra các ấn phẩm hình ảnh và video 360 độ chất lượng cao cho hàng loạt dự án tốn rất nhiều thời gian, chi phí thuê designer và thiếu tính đồng bộ. 

Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ mạnh mẽ (gồm 22 nodes kết hợp AI Agent, OpenAI, Google Drive, Gmail và Google Sheets) giúp tự động hóa 100% quy trình: Từ một ý tưởng sơ khai trên form → AI viết lại prompt tối ưu → Sinh ảnh/video → Lưu trữ Cloud và gửi email xin phê duyệt tự động!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa toàn diện:** Biến 1 dòng mô tả ý tưởng thô thành ảnh/video sắc nét, sẵn sàng chạy quảng cáo.
- **Tối ưu hóa Prompt bằng AI:** Sử dụng AI Agent kết hợp GPT-4o-mini để nâng cấp prompt thô thành các prompt chi tiết, chuyên nghiệp cho AI sinh ảnh/video.
- **Quy trình phê duyệt thông minh:** Tự động gửi email kèm file kết quả và chờ phản hồi (Approve/Reject) trực tiếp từ quản lý/khách hàng.
- **Quản lý dữ liệu tập trung:** Mọi yêu cầu, prompt cải tiến và link file đều được lưu vết tự động trên Google Sheets và Google Drive.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **Tài khoản OpenAI:** Cần có API Key và số dư để sử dụng GPT-4o-mini, Image Generation và Video Generation.
- **Google Account:** 
  - Kết nối Google Sheets (Credentials OAuth2) kèm [Template Google Sheets mẫu](https://docs.google.com/spreadsheets/d/1NEtQvs2hlcqmrFfSC6e1cReC25g2FEvxTiqdXOgtnjM/edit?usp=sharing).
  - Kết nối Google Drive để lưu trữ và chia sẻ file.
  - Kết nối Gmail để gửi email tương tác và nhận phê duyệt.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tải file JSON của workflow từ [n8n Template #14134](https://n8n.io/workflows/14134), sau đó chọn **Import from File** hoặc copy và paste trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà không gặp lỗi "Credentials Error", các sếp cần cấu hình chính xác các node sau:
- **On form submission & Form:** Cấu hình form thu thập ý tưởng (phong cách, loại hình bất động sản, yêu cầu đặc biệt).
- **Google Sheets Nodes (`Append row in sheet`, `Append or update row in sheet`...):** Chọn đúng Credentials Google Sheets, liên kết tới File Sheet quản lý và ánh xạ (map) đúng các cột dữ liệu theo template chuẩn.
- **AI Agent & OpenAI Chat Model:** Chọn credential OpenAI API và đảm bảo mô hình LLM được trỏ đúng vào `gpt-4.1-mini` (hoặc `gpt-4o-mini`).
- **Generate an image2 & Generate a video:** Kiểm tra lại prompt binding `={{ $json['Improved Prompt'] }}` và `={{ $('AI Agent1').item.json.output }}` để đảm bảo dữ liệu từ AI truyền sang chính xác.
- **Google Drive Nodes (`Upload file`, `Share file`...):** Chọn thư mục đích (Folder ID) trên Drive để lưu trữ ảnh và video tự động sinh ra.
- **Gmail Nodes (`Send message and wait for response`, `Send a message`):** Cấu hình Credentials Gmail và thiết lập email người nhận để hệ thống thực hiện luồng chờ phê duyệt (Approval Flow).

#### 3. Kích hoạt ⚡️
- Thực hiện **Test workflow** bằng cách điền thông tin thử nghiệm lên Form thu thập ý tưởng.
- Kiểm tra từng bước (Trigger -> AI -> Drive -> Gmail) xem dữ liệu trả về chính xác chưa.
- Bật nút **Active** để đưa workflow vào vận hành thực tế 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack/Telegram:** Thêm node thông báo qua Telegram hoặc Slack ngay khi có một yêu cầu mới được gửi từ form hoặc khi file được phê duyệt thành công.
- **Lưu trữ Log chi tiết:** Bổ sung các nhánh bắt lỗi (Error Trigger) để tự động gửi cảnh báo về Telegram nếu quá trình tạo video/ảnh qua OpenAI API gặp sự cố.
- **Mở rộng đa kênh:** Tự động đăng tải (Auto-post) các hình ảnh/video đã được phê duyệt trực tiếp lên Fanpage Facebook, Instagram hoặc kênh TikTok của dự án bất động sản.

### 📌 Kết luận
Workflow tự động hóa tạo nội dung bất động sản này là mảnh ghép hoàn hảo giúp đội ngũ marketing tiết kiệm 90% thời gian triển khai ý tưởng thành các ấn phẩm trực quan. Hãy áp dụng ngay vào hệ thống của các sếp để tối ưu hóa năng suất vận hành ngay hôm nay!