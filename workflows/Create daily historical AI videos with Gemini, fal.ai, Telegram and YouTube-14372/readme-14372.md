---
title: "🎬 **Tự Động Hóa Sáng Tạo & Phát Hành Video Lịch Sử AI Hàng Ngày Với Gemini, fal.ai, Telegram & YouTube**"
description: "Workflow tự động hóa 100% không code giúp các sếp tạo và phát hành video lịch sử AI hàng ngày lên YouTube với sự phê duyệt thông qua Telegram. Tiết kiệm 10+ giờ công sức mỗi tuần, tối ưu hóa nội dung và tăng cường tương tác với khán giả."
slug: "tieu-dong-hoa-tao-phat-hanh-video-lich-su-ai"
tags: [n8n, automation, content-creation, multimodal-ai, youtube-automation, telegram-bot, google-gemini, fal-ai]
keywords: [n8n workflow lịch sử AI, tự động hóa video YouTube, Gemini + fal.ai, Telegram phê duyệt nội dung, tự động hóa content creator]
---

# 🚀 **Tự Động Hóa Video Lịch Sử AI Hàng Ngày: Từ Script Đến YouTube Với Phê Duyệt Telegram**

Hãy tưởng tượng một ngày không cần phải ngồi trước máy tính từ sáng sớm để viết script, tạo video, hoặc chờ đợi quá trình render kéo dài. **Workflow này tự động hóa toàn bộ quy trình sáng tạo và phát hành video lịch sử AI hàng ngày**, từ việc chọn lựa sự kiện lịch sử đến việc upload lên YouTube với sự phê duyệt thông qua Telegram. **Không cần code, không cần kỹ năng kỹ thuật cao** – chỉ cần một vài bước cấu hình và workflow sẽ hoạt động 24/7, giúp các sếp tiết kiệm **10+ giờ công sức mỗi tuần** và tối ưu hóa nội dung cho kênh YouTube.

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm thời gian**: Tự động hóa toàn bộ quy trình từ sáng tạo đến phát hành, chỉ cần phê duyệt 1 lần/ngày.
- **Nội dung cá nhân hóa**: Video lịch sử được tạo động dựa trên sự kiện ngày hôm đó, phù hợp với khán giả mục tiêu.
- **Chất lượng chuyên nghiệp**: Sử dụng AI Gemini và fal.ai để tạo video cinematic, đẹp mắt và chuyên nghiệp.
- **Phê duyệt linh hoạt**: Sử dụng Telegram để kiểm soát chất lượng trước khi upload lên YouTube.
- **Hoạt động liên tục**: Workflow được trigger hàng ngày tại 1 AM, không cần can thiệp thủ công.
- **Tăng cường tương tác**: Video được chia sẻ tự động qua Telegram với link YouTube, giúp tăng độ phủ.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[**CHUẨN BỊ**]
Để workflow hoạt động, các sếp cần chuẩn bị các tài khoản và API keys sau:
1. **Tài khoản n8n**:
   - Cài đặt n8n **Self-hosted** (khuyến nghị) trên VPS để workflow hoạt động 24/7 ổn định.
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

2. **Tài khoản fal.ai**:
   - Đăng ký tại [fal.ai](https://fal.ai/) và lấy **API Key** để gửi yêu cầu tạo video.
   - **Lưu ý**: fal.ai sử dụng mô hình Hunyuan LoRA, phù hợp với video ngắn.

3. **Google Gemini API**:
   - Đăng ký tại [Google AI Studio](https://aistudio.google/) và lấy **API Key** cho Google Palm API.

4. **Tài khoản YouTube**:
   - Tạo **OAuth2 API Key** cho YouTube để upload video tự động.
   - Cài đặt **YouTube Data API v3** và kích hoạt quyền upload.

5. **Tài khoản Telegram**:
   - Tạo **Bot Telegram** và lấy **API Token**.
   - Thiết lập **Chat ID** của bot hoặc cá nhân để nhận thông báo phê duyệt.

6. **Nguồn dữ liệu lịch sử**:
   - Workflow mặc định lấy dữ liệu từ API lịch sử, nhưng các sếp có thể thay thế bằng nguồn dữ liệu riêng (ví dụ: API của riêng mình hoặc Google Sheets).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Bước 1**: Tải workflow từ [n8n.io/workflows/14372](https://n8n.io/workflows/14372) hoặc sử dụng file JSON đã cung cấp.
- **Bước 2**: Mở **n8n Editor** và chọn **Import Workflow** → Chọn file JSON hoặc copy/paste JSON từ file.
- **Bước 3**: Workflow sẽ được import với **23 nodes** và cấu trúc đã sẵn sàng.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này bao gồm nhiều node quan trọng cần cấu hình cẩn thận. Dưới đây là hướng dẫn chi tiết:

##### **A. Cấu hình Credentials**
1. **Telegram Bot**:
   - Tạo **Bot Telegram** tại [@BotFather](https://t.me/BotFather) và lấy **API Token**.
   - Thiết lập **credentials** cho Telegram trong n8n:
     - **Name**: `telegramApi`
     - **Token**: Paste API Token từ BotFather.
     - **Chat ID**: Thiết lập **Chat ID** của bot hoặc cá nhân (không hardcode, sử dụng biến hoặc Set node).

2. **fal.ai API**:
   - Tạo **HTTP Header Auth** trong n8n:
     - **Name**: `httpHeaderAuth`
     - **Authentication Type**: `Bearer Token`
     - **Token**: Paste API Key từ fal.ai.

3. **Google Gemini API**:
   - Thiết lập **credentials** cho Google Palm API:
     - **Name**: `googlePalmApi`
     - **API Key**: Paste API Key từ Google AI Studio.

4. **YouTube OAuth2**:
   - Tạo **YouTube OAuth2 API** trong n8n:
     - **Name**: `youTubeOAuth2Api`
     - **Client ID** và **Client Secret**: Lấy từ Google Cloud Console.
     - **Refresh Token**: Lấy sau khi authorize ứng dụng.

##### **B. Cấu hình Node Quản Lý**
1. **Node "Select Random Historical Event"**:
   - Node này sử dụng **HTTP Request** để lấy dữ liệu lịch sử. Các sếp có thể thay thế bằng nguồn dữ liệu riêng (ví dụ: API của riêng mình hoặc Google Sheets).
   - **Lưu ý**: Đảm bảo API trả về dữ liệu JSON có định dạng phù hợp.

2. **Node "Generate Cinematic Script with AI"**:
   - Node này sử dụng **Google Gemini** để tạo script. Các sếp có thể tùy chỉnh **prompt** trong node **Code** trước đó để điều chỉnh phong cách script (ví dụ: thêm thông tin chi tiết hơn về sự kiện).

3. **Node "Submit to fal.ai"**:
   - Đảm bảo **URL API** và **headers** được cấu hình chính xác. Tham khảo [fal.ai API Docs](https://fal.ai/docs) để lấy thông tin chi tiết.
   - **Lưu ý**: fal.ai có giới hạn số lượng yêu cầu/ngày, các sếp nên kiểm tra tài khoản để tránh bị chặn.

4. **Node "Upload to YouTube"**:
   - Đảm bảo **credentials YouTube OAuth2** được thiết lập đúng.
   - **Lưu ý**: Video phải có độ dài ≤ 15 phút và định dạng phù hợp (MP4, MOV).

5. **Node "Check Retry Limit"**:
   - Workflow mặc định cho phép **3 lần retry** nếu video bị từ chối. Các sếp có thể điều chỉnh số lần retry trong node **Code** này.

##### **C. Cấu hình Schedule Trigger**
- Node **"Schedule (Daily at 1 AM)"** được thiết lập để trigger workflow hàng ngày tại 1 AM.
- **Lưu ý**: Nếu muốn thay đổi thời gian trigger, chỉnh sửa **cron expression** trong node này (ví dụ: `0 0 1 * * ?` để trigger tại 1 AM hàng ngày).

#### **3. Kích hoạt ⚡️**
- **Bước 1**: Chạy **Test Run** với dữ liệu mẫu để kiểm tra workflow.
- **Bước 2**: Kiểm tra các node quan trọng như:
  - **"Select Random Historical Event"**: Đảm bảo lấy được dữ liệu lịch sử.
  - **"Generate Cinematic Script with AI"**: Kiểm tra script được tạo có logic hay không.
  - **"Submit to fal.ai"**: Kiểm tra video được tạo có tải xuống được không.
  - **"Upload to YouTube"**: Kiểm tra video được upload thành công.
- **Bước 3**: Nếu tất cả node hoạt động bình thường, **bật Active workflow**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::info[**TỐT HƠN HƠN**]
1. **Tăng cường tương tác với khán giả**:
   - Thêm node **Slack** hoặc **Email** để thông báo video mới được upload.
   - Ví dụ: Sử dụng node **Slack Webhook** để gửi thông báo đến nhóm nội dung.

2. **Lưu log hoạt động**:
   - Thêm node **Sticky Note** hoặc **Google Sheets** để lưu lịch sử video đã tạo và phê duyệt.
   - Ví dụ: Lưu thông tin video (tiêu đề, link, ngày tạo, trạng thái) vào Google Sheets để theo dõi.

3. **Tùy chỉnh video theo chủ đề**:
   - Sử dụng node **Code** để thay đổi **prompt** cho Gemini dựa trên chủ đề (ví dụ: lịch sử Việt Nam, lịch sử thế giới).
   - Ví dụ: Thêm điều kiện trong node **If** để chọn chủ đề khác nhau.

4. **Tối ưu hóa chất lượng video**:
   - Thay đổi **tham số video** trong node **Submit to fal.ai** (ví dụ: độ phân giải, tốc độ frame).
   - Tham khảo [fal.ai API Docs](https://fal.ai/docs) để tìm hiểu các tùy chọn.

5. **Tự động chia sẻ video trên mạng xã hội**:
   - Thêm node **Twitter**, **Facebook**, hoặc **LinkedIn** để chia sẻ video tự động sau khi upload lên YouTube.
   - Ví dụ: Sử dụng node **Twitter Post** để tweet link video mới.

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa quy trình sáng tạo và phát hành video lịch sử AI hàng ngày. **Không cần code, không cần kỹ thuật cao** – chỉ cần một vài bước cấu hình, workflow sẽ hoạt động 24/7, tiết kiệm thời gian và tối ưu hóa nội dung cho kênh YouTube.

**Hành động ngay hôm nay**:
1. **Cài đặt n8n Self-hosted** trên VPS để workflow hoạt động ổn định.
2. **Import workflow** và cấu hình các credentials theo hướng dẫn.
3. **Test Run** và kích hoạt workflow.
4. **Tận hưởng** video lịch sử AI được tạo và phát hành tự động hàng ngày!

**🚀 Cùng tự động hóa nội dung của mình ngay bây giờ!**