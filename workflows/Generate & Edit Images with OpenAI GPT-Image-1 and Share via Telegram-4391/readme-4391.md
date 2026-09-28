---
title: "🚀 Tự động Tạo và Chỉnh sửa Ảnh bằng OpenAI GPT-Image và Chia sẻ qua Telegram với n8n"
description: "Hướng dẫn chi tiết workflow n8n tự động hóa quy trình tạo ảnh gốc, chỉnh sửa ảnh (image-to-image) bằng OpenAI, lưu trữ trên Google Drive/ImgBB và gửi trực tiếp qua Telegram."
slug: "tu-dong-tao-va-chinh-sua-anh-openai-telegram-n8n"
tags: [n8n, automation, no-code, openai, telegram, google-drive, ai-image-generation]
keywords: [n8n workflow, tạo ảnh ai, openai gpt-image, telegram bot automation, chỉnh sửa ảnh ai, google drive api, imgbb upload]
---

# 🚀 Tự động Tạo và Chỉnh sửa Ảnh bằng OpenAI GPT-Image & Gửi Telegram

Các sếp trong ngành Marketing, thiết kế hay sáng tạo nội dung chắc hẳn đã tốn rất nhiều thời gian để viết prompt, tạo ảnh, chỉnh sửa đi chỉnh sửa lại rồi tải về máy và gửi cho khách hàng hoặc team qua Telegram/Zalo. Quy trình thủ công này vừa ngốn thời gian, vừa đứt gãy mạch sáng tạo.

Hôm nay, em xin giới thiệu workflow n8n cực kỳ xịn sò giúp tự động hóa toàn bộ quy trình: **Nhận yêu cầu qua Form -> Tạo/Chỉnh sửa ảnh bằng OpenAI AI -> Lưu trữ trên Google Drive hoặc ImgBB -> Gửi kết quả thẳng đến Telegram** mà không cần đụng một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Chỉ cần điền Form, hệ thống tự lo phần còn lại từ sinh ảnh đến trả kết quả.
- **Linh hoạt chọn chế độ:** Hỗ trợ cả tạo ảnh mới (Text-to-Image) lẫn chỉnh sửa ảnh có sẵn (Image-to-Image).
- **Lưu trữ đa nền tảng:** Tự động lưu lên Google Drive (cấp quyền chia sẻ công khai) hoặc đẩy lên Imgbb để lấy link nhanh.
- **Thông báo tức thì:** Gửi ảnh hoàn thiện trực tiếp vào nhóm hoặc chat cá nhân qua Telegram Bot.
:::

### 🚀 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **OpenAI API Key** (Có quyền truy cập mô hình tạo ảnh GPT-Image).
- **Telegram Bot Token** (Tạo qua `@BotFather`).
- **Google Drive Credentials** (OAuth2 hoặc Service Account để upload và chia sẻ file).
- **ImgBB API Key** (Tùy chọn nếu muốn lưu ảnh lên Imgbb).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này, vào giao diện n8n chọn **Add workflow** -> **Import from JSON** và dán vào là xong.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node cốt lõi sau:

- **On form submission (`formTrigger`):** Điền thông tin bảo mật (`httpBasicAuth`) nếu cần thiết và thiết kế các trường nhập liệu như: Prompt tạo ảnh, URL ảnh gốc (nếu dùng chế độ chỉnh sửa), và chế độ hoạt động.
- **Switch Mode (`switch`):** Node này dùng để phân luồng xem các sếp muốn tạo ảnh mới từ đầu hay chỉnh sửa ảnh dựa trên ảnh có sẵn.
- **SETUP API KEY & Các node OpenAI (`Image Generation`, `Edit Image (OpenAI)`):** 
  - Thêm `openAiApi` credentials của các sếp vào.
  - Kiểm tra endpoint gọi tới OpenAI: `/v1/images/generations` (tạo ảnh) hoặc `/v1/images/edits` (chỉnh sửa ảnh) sử dụng model `gpt-image-1`.
- **Chuyển đổi định dạng (`Convert json binary to File`, `Convert json binary to File final`):** Các node này chuyển đổi dữ liệu base64 trả về từ OpenAI thành định dạng file ảnh nhị phân (binary PNG) chuẩn để upload.
- **Lưu trữ ảnh (`Upload Result Image to Google Drive`, `Set Access Permissions`):**
  - Kết nối `googleApi` credentials.
  - Cấu hình thư mục đích trên Google Drive để lưu ảnh.
  - Node `Set Access Permissions` sẽ tự động cấu hình quyền chia sẻ file công khai để lấy link gửi đi.
- **Gửi Telegram (`Send to Telegram`):**
  - Kết nối `telegramApi` credentials (Token Bot).
  - Điền Chat ID của cá nhân hoặc group Telegram muốn nhận ảnh kết quả.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và test thử bằng cách điền form mẫu.
- Sau khi test thành công và ảnh đã bay về Telegram êm ái, các sếp bật công tắc **Active** ở góc trên bên phải để workflow chạy tự động 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Google Sheets:** Lưu lại lịch sử các câu lệnh (prompt) và link ảnh đã tạo để làm báo cáo hoặc tra cứu sau này.
- **Mở rộng kênh thông báo:** Kết hợp thêm node Slack hoặc Discord để gửi ảnh đồng thời đến nhiều kênh làm việc của công ty.
- **Tự động tạo log lỗi:** Thêm nhánh xử lý lỗi (Error Trigger) để nếu OpenAI lỗi API hay quá hạn mức, hệ thống sẽ báo ngay về Telegram cho các sếp xử lý.

### 📌 Kết luận
Workflow này là một "vũ khí" cực mạnh mẽ giúp tối ưu hóa công việc sáng tạo nội dung hình ảnh bằng AI. Hãy cài đặt ngay hôm nay để giải phóng sức lao động và tăng tốc độ triển khai chiến dịch marketing của các sếp nhé!