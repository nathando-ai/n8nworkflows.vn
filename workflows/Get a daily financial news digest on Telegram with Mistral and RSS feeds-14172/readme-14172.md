---
title: "🚀 Tự động nhận bản tin tài chính hàng ngày trên Telegram bằng Mistral AI và RSS Feeds"
description: "Hướng dẫn cấu hình workflow n8n tự động tổng hợp tin tức tài chính từ RSS, dùng NVIDIA NIM (Mistral Large) tóm tắt và gửi thẳng vào Telegram, kết hợp lưu log Google Sheets."
slug: "tu-dong-ban-tin-tai-chinh-telegram-mistral-rss-n8n"
tags: [n8n, automation, ai-summarization, telegram, google-sheets, nvidia-nim]
keywords: [n8n workflow, tóm tắt tin tức ai, telegram bot rss, nvidia nim mistral, tự động hóa tài chính]
keywords: [n8n workflow, tóm tắt tin tức ai, telegram bot rss, nvidia nim mistral, tự động hóa tài chính]
---

# 🚀 Tự động nhận bản tin tài chính hàng ngày trên Telegram bằng Mistral AI và RSS Feeds

Các nhà đầu tư, nhà phân tích hay nhà sáng lập thường mất rất nhiều thời gian mỗi ngày để lướt qua hàng chục trang tin tức tài chính, đọc các RSS feed thủ công nhằm nắm bắt thị trường. Việc này vừa nhàm chán, tẻ nhạt lại dễ bỏ sót các thông tin quan trọng.

Giải pháp là đây! Workflow n8n tự động hóa 100% này sẽ thay các sếp cào dữ liệu từ các nguồn RSS tài chính uy tín, chấm điểm, xếp hạng và sử dụng sức mạnh của AI (NVIDIA NIM kết hợp Mistral Large) để cô đọng thành một bản tin ngắn gọn, súc tích gửi thẳng tới Telegram cá nhân hoặc channel mỗi ngày. Đồng thời, mọi hoạt động đều được ghi log chi tiết lên Google Sheets để tiện theo dõi.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tuyệt đối:** Không cần mở hàng tá tab trình duyệt hay đọc tin thủ công mỗi sáng.
- **AI thông minh tổng hợp:** Sử dụng mô hình Mistral Large qua NVIDIA NIM để viết bản tin mạch lạc, đúng trọng tâm ngành tài chính.
- **Tùy biến nguồn tin dễ dàng:** Phân loại theo Tier (Cấp độ ưu tiên) giúp tin quan trọng luôn xuất hiện hàng đầu.
- **Quản trị minh bạch:** Tự động ghi log thành công vào tab `Digest_Log` và lưu vết lỗi vào tab `Error_Log` trên Google Sheets.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một Server n8n đang hoạt động.
- Tài khoản NVIDIA NIM (lấy API Key) dùng cho node `Generate Digest (NIM)`.
- Tài khoản Google Sheets (kết nối OAuth2) để ghi log.
- Telegram Bot Token & Chat ID (hoặc `@channelname`) để nhận tin nhắn.
- Một file Google Sheet được chuẩn bị sẵn 2 tab: `Digest_Log` và `Error_Log`.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã nguồn JSON của workflow này, vào n8n Editor chọn **Add workflow** -> **Import from JSON** và dán vào là xong.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 21 nodes được thiết kế mạch lạc từ lấy dữ liệu -> xử lý AI -> gửi thông báo. Các sếp cần chú ý các điểm sau:

- **Node `📋 RSS Feed Config1`**: 
  - Cập nhật danh sách nguồn tin (`rssFeeds`), giới hạn số tin (`maxStoriesInDigest`), khoảng thời gian quét (`freshnessHours`).
  - Điền `telegramBotToken`, `telegramChatId` và `googleSheetId`.
  - *Mẹo:* Phân loại `tier` (Tier 1 là nguồn quan trọng nhất, Tier 3 là nguồn phụ) để hệ thống tự động ưu tiên xếp hạng.
- **Node `Generate Digest (NIM)`**:
  - Cấu hình Credentials loại **HTTP Header Auth**.
  - Header name: `Authorization`, Value: `Bearer YOUR_NVIDIA_API_KEY`.
  - Đảm bảo endpoint POST trỏ về `https://integrate.api.nvidia.com/v1/chat/completions`.
- **Node `Log Digest to Sheets` & `Log Error to Sheets`**:
  - Chọn Credentials **Google Sheets OAuth2**.
  - Trỏ đúng ID của Google Sheet đã tạo sẵn 2 tab `Digest_Log` và `Error_Log`.
- **Node `Send to Telegram` & `No Stories Alert`**:
  - Các node này sử dụng token và chat ID được truyền trực tiếp từ node cấu hình (`📋 RSS Feed Config1`), không cần tạo credential Telegram riêng.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (Manual Test Run) bằng cách bấm nút **Execute Workflow**.
- Kiểm tra xem bản tin đã bắn về Telegram chưa, đồng thời check lại file Google Sheets xem dòng log đã được ghi nhận ở tab `Digest_Log` chưa.
- Nếu mọi thứ mượt mà, hãy gạt công tắc **Active** ở góc trên bên phải để hệ thống tự động chạy theo lịch trình từ node `⏰ Schedule Trigger1`.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa kênh thông báo:** Có thể nhân bản nhánh gửi Telegram để bắn thêm tin nhắn vào kênh Slack công ty hoặc nhóm Discord nội bộ.
- **Lọc từ khóa thông minh:** Tùy biến đoạn code trong `Tag Articles` để gắn nhãn các chủ đề nóng như *Crypto, AI Stocks, Fed Interest Rate* giúp bản tin phân chia theo chuyên mục rõ ràng hơn.
- **Báo cáo tuần/tháng:** Kết hợp thêm một workflow phụ tổng hợp dữ liệu từ `Digest_Log` trên Google Sheets để vẽ biểu đồ xu hướng tin tức tài chính mỗi cuối tuần.

### 📌 Kết luận
Với workflow n8n này, việc cập nhật tin tức tài chính mỗi ngày đã hoàn toàn tự động hóa, giúp các sếp giải phóng đầu óc để tập trung vào chiến lược kinh doanh cốt lõi. Hãy cài đặt ngay và trải nghiệm sự kỳ diệu của AI kết hợp No-code!