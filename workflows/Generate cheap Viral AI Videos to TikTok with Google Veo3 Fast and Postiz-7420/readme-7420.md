---
title: "🚀 Tự Động Tạo Video AI Viral Giá Rẻ Với Google Veo3 Fast và Đăng Lên TikTok Qua Postiz"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa hoàn toàn quy trình tạo video AI bằng Google Veo3 Fast, lưu trữ Google Drive, tạo tiêu đề bằng OpenAI và đăng lên TikTok qua Postiz."
slug: "tu-dong-tao-video-ai-viral-tiktok-google-veo3-postiz"
tags: [n8n, automation, ai-video, tiktok, postiz, google-veo, openai]
keywords: [n8n workflow, tạo video ai tự động, google veo3 fast, đăng tiktok tự động, postiz n8n, automation video tiktok]
---

# 🚀 Tự Động Tạo Video AI Viral Giá Rẻ Với Google Veo3 Fast và Đăng Lên TikTok Qua Postiz

Việc sản xuất video ngắn (Reels, TikTok, Shorts) đều đặn mỗi ngày để xây dựng kênh là một "cực hình" đối với các nhà sáng tạo nội dung và nhà marketing khi làm thủ công. Bạn phải nghĩ ý tưởng, viết prompt, tạo video trên các công cụ AI đắt đỏ, tải về, viết caption, rồi lại thủ công đăng lên từng nền tảng.

Giải pháp là đây! Workflow n8n này sẽ tự động hóa toàn bộ quy trình: lấy danh sách prompt từ **Google Sheets**, gọi API tạo video giá rẻ bằng **Google Veo3 Fast** (thông qua Fal.ai), lưu trữ tự động vào **Google Drive**, dùng **OpenAI (GPT-4o)** để viết tiêu đề triệu view, và cuối cùng tự động xuất bản lên **TikTok** thông qua nền tảng quản lý mạng xã hội **Postiz**. Tất cả diễn ra hoàn toàn tự động mà không cần can thiệp thủ công!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 (đặc biệt là các tiến trình chờ xử lý video - `Wait` node), các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Chỉ cần điền ý tưởng (Prompt) vào Google Sheets, hệ thống lo phần còn lại từ A-Z.
- **Tối ưu chi phí:** Sử dụng mô hình Google Veo3 Fast (qua Fal.ai) giúp tiết kiệm đáng kể chi phí tạo video so với các nền tảng khác.
- **Cá nhân hóa & Thông minh:** AI (OpenAI) tự động tạo tiêu đề và caption tối ưu hóa chuẩn SEO cho TikTok.
- **Vận hành liên tục:** Lịch trình tự động (Schedule Trigger) giúp duy trì tần suất đăng bài đều đặn mỗi ngày.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị sẵn các tài khoản và API sau:
- **Tài khoản n8n Self-hosted** (vì workflow sử dụng community node Postiz).
- **Google Sheets & Google Drive**: Tài khoản Google để quản lý bảng dữ liệu và lưu trữ file video.
- **Fal.ai Account**: Lấy API Key để gọi mô hình tạo video Google Veo3 Fast.
- **OpenAI API Key**: Dành cho node `Generate title` (GPT-4o).
- **Postiz Account**: Nền tảng quản lý lịch đăng bài (có bản dùng thử 7 ngày miễn phí) kết nối sẵn với tài khoản TikTok và lấy `ChannelId`.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và dán trực tiếp vào n8n Editor của mình (hoặc import file JSON tải từ nguồn).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 15 nodes, các sếp cần chú ý cấu hình kỹ các điểm sau:

- **Google Sheet (Node: `Get new video` & `Update result`):** 
  - Tạo một Google Sheet theo [mẫu chuẩn này](https://docs.google.com/spreadsheets/d/1pcoY9N_vQp44NtSRR5eskkL5Qd0N0BGq7Jh_4m-7VEQ/edit?usp=sharing).
  - Cột `PROMPT`: Mô tả chi tiết video muốn tạo.
  - Cột `DURATION`: Độ dài video.
  - Cột `VIDEO`: Để trống, hệ thống sẽ tự điền link video sau khi render xong.
  - Kết nối tài khoản Google Sheets OAuth2 cho 2 node này.

- **Tạo Video AI (Node: `Create Video`, `Get status`, `Get Url Video`):**
  - Các node này gọi API tới Fal.ai (`https://fal.ai/`).
  - Cấu hình **Header Auth**: Thêm Header với Name: `Authorization` và Value: `Key YOUR_FAL_AI_API_KEY`.

- **Lưu trữ Google Drive (Node: `Upload Video`):**
  - Kết nối tài khoản Google Drive OAuth2 để tự động lưu video vừa render vào thư mục trên Drive của các sếp.

- **Tạo tiêu đề AI (Node: `Generate title`):**
  - Chọn credential **OpenAI API**, cấu hình model (khuyên dùng `gpt-4o` hoặc `gpt-4o-mini`) để tạo tiêu đề cuốn hút cho video.

- **Đăng TikTok qua Postiz (Node: `TikTok` & `Upload Video to Postiz`):**
  - Tạo tài khoản [Postiz](https://postiz.com/?ref=n3witalia).
  - Vào tab Calendar, bấm **"Add channel"** để kết nối tài khoản TikTok của các sếp.
  - Lấy `ChannelId` của kênh TikTok và thay thế chuỗi `"XXX"` mặc định trong node Postiz.
  - Cấu hình Postiz API Key vào credentials của node.

- **Lịch trình (Node: `Schedule Trigger`):**
  - Mặc định tác giả gợi ý đặt chu kỳ chạy 5 phút/lần để kiểm tra trạng thái render video (`Get status`) và đẩy sang các bước tiếp theo.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm (`Test workflow`) với 1 dòng dữ liệu mẫu trên Google Sheets để kiểm tra toàn bộ chuỗi từ tạo video -> lưu Drive -> viết tiêu đề -> đăng Postiz.
- Khi mọi thứ chạy mượt mà, gạt công tắc **Active** góc trên bên phải để workflow tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm thông báo Telegram/Slack:** Thêm một node Telegram sau khi video đăng thành công lên TikTok để nhận thông báo ngay trên điện thoại.
- **Quản lý lỗi (Error Handling):** Bổ sung nhánh Error Trigger để ghi lại log nếu quá trình render video từ Veo3 Fast gặp sự cố (ví dụ lỗi thiếu quỹ API hoặc prompt vi phạm chính sách).
- **Đa nền tảng:** Ngoài TikTok, Postiz hỗ trợ rất nhiều mạng xã hội khác (Instagram Reels, YouTube Shorts, Facebook). Các sếp có thể nhân bản node Postiz để đăng cùng lúc lên nhiều nền tảng chỉ với 1 lần tạo video!

### 📌 Kết luận
Với workflow n8n kết hợp giữa Google Veo3 Fast, OpenAI và Postiz này, các sếp đã có trong tay một "đội ngũ sản xuất content ảo" hoạt động không lương 24/7. Hãy thiết lập ngay hôm nay để bứt phá lượt xem trên các nền tảng video ngắn!