---
title: "🚀 Tự động tạo bản tóm tắt podcast Apple Podcasts cho Telegram bằng BrowserAct & Gemini"
description: "Workflow n8n hàng ngày lấy top chart Apple Podcasts, dùng Gemini AI tổng hợp nội dung và gửi digest đa phần lên Telegram – không cần viết code."
slug: "tu-dong-tao-bao-tom-podcast-apple-telegram"
tags: [n8n, automation, no-code, podcast, telegram, gemini, browseract]
keywords: [n8n workflow, tự động hóa podcast, AI tạo nội dung, Telegram bot, Apple Podcasts]
---

# 🚀 Tự động tạo bản tóm tắt podcast Apple Podcasts cho Telegram bằng BrowserAct & Gemini

Bạn có bao giờ phải **làm thủ công**: mở Apple Podcasts, sao chép danh sách top chart, đọc qua từng mô tả, rồi tự viết một bản tóm tắt để chia sẻ trên Telegram?  
Công việc này tốn **giờ đồng** mỗi ngày, dễ sai sót, và luôn bị giới hạn độ dài tin nhắn.  

**Workflow này** sẽ **tự động**:
1. **Scrape** top chart podcast từ Apple Podcasts mỗi ngày bằng **BrowserAct**.  
2. **Phân tích** dữ liệu bằng **Google Gemini (PaLM)**, tạo bản tóm tắt HTML chuẩn Telegram, tự chia thành nhiều phần nếu vượt giới hạn ký tự.  
3. **Gửi** từng phần tin nhắn tới kênh/nhóm Telegram một cách **liên tục** và **không bị rate‑limit**.

Kết quả: **tiết kiệm thời gian**, **độ chính xác 100 %**, **nội dung luôn mới** và **được trình bày chuyên nghiệp** – mọi thứ chỉ cần một lần thiết lập, sau đó chạy 24/7.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 2‑3 giờ/ngày**: không còn thao tác copy‑paste, viết tóm tắt thủ công.  
- **Độ chính xác cao**: dữ liệu được lấy trực tiếp từ Apple Podcasts, không có sai sót.  
- **Nội dung chuẩn Telegram**: tự động tính toán ký tự, chia tin thành nhiều phần, tránh “Message too long”.  
- **Hoạt động liên tục**: chạy mỗi ngày vào giờ đã định, không cần giám sát.  
- **Dễ mở rộng**: thêm Slack, Email, hoặc lưu log vào Google Sheets chỉ bằng một node.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **BrowserAct API key** (có template **Top Charts Podcast** trong tài khoản).  
- **Google Gemini (PaLM) API key** (`googlePalmApi` credential).  
- **Telegram Bot API token** và **Chat ID** (kênh hoặc nhóm muốn gửi).  
- **n8n** (cài đặt trên VPS hoặc Docker) với các node: `wait`, `splitOut`, `telegram`, `stickyNote`, `splitInBatches`, `agent`, `scheduleTrigger`, `browserAct`, `lmChatGoogleGemini`, `outputParserStructured`.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở **n8n Editor**.  
2. Nhấn **Import** → **Upload JSON** và chọn file `Create_Telegram_podcast_digests.json` (hoặc copy toàn bộ JSON vào ô **Paste JSON**).  
3. Nhấn **Import**, workflow sẽ xuất hiện trong danh sách.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Mô tả | Cấu hình cần thay đổi |
|------|------|-----------------------|
| **Schedule Daily** | Kích hoạt workflow mỗi ngày. | Chọn **Cron** → `0 8 * * *` (ví dụ 08:00 UTC) hoặc thời gian phù hợp với khán giả. |
| **Run Top Chart Podcast workflow** (BrowserAct) | Gọi template BrowserAct để lấy danh sách podcast. | - **Credentials**: chọn `browserActApi`. <br> - **Template ID**: nhập ID của template **Top Charts Podcast** trong BrowserAct. |
| **Loop Over Items** (splitInBatches) | Duyệt từng podcast thu được. | - **Batch Size**: để `1` (xử lý từng mục một). |
| **Analyze Podcast & Generate Post** (agent) | AI Gemini phân tích và tạo bản tóm tắt. | - **Credentials**: `googlePalmApi`. <br> - **Prompt**: sử dụng prompt mặc định (đã tích hợp) hoặc tùy chỉnh: “Summarize the podcast episode …”. |
| **Google Gemini Chat Model** | Mô hình chat Gemini thực hiện xử lý. | - **Model**: `gemini-pro` (hoặc phiên bản mới nhất). |
| **Structured Output Parser** | Chuyển kết quả Gemini sang JSON có cấu trúc (title, description, link, image). | Không cần thay đổi nếu dùng output schema mặc định. |
| **Split Generated Items** (splitOut) | Tách các phần tin nhắn nếu vượt giới hạn Telegram (4096 ký tự). | Không cần thay đổi. |
| **Avoid Rate Limits** (wait) | Đợi 2‑3 giây giữa các tin để tránh rate‑limit. | - **Delay**: `3000 ms` (có thể tăng lên 5000 ms nếu gặp lỗi). |
| **Send Podcast List to User** (telegram) | Gửi tin nhắn tới Telegram. | - **Credentials**: `telegramApi`. <br> - **Chat ID**: nhập ID kênh/nhóm. <br> - **Message Type**: `HTML`. <br> - **Content**: dùng biểu thức `{{$json["content"]}}` (được tạo bởi node trước). |

> **Lưu ý:** Đảm bảo **tất cả** các credential được tạo trong n8n → **Credentials** → **New Credential** trước khi gán vào node.

#### 3. Kích hoạt ⚡️
1. Nhấn **Execute Workflow** lần đầu để kiểm tra với dữ liệu mẫu.  
2. Kiểm tra kênh Telegram: bạn sẽ nhận được 1‑n phần tin tóm tắt.  
3. Khi mọi thứ ổn, bật **Active** (nút chuyển đổi ở góc trên‑phải) để workflow tự động chạy hàng ngày.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm Slack**: sao chép node `telegram` thành `slack` và cấu hình webhook để đồng thời gửi digest tới Slack.  
- **Lưu log**: dùng node `Google Sheets` hoặc `Airtable` để ghi lại tiêu đề, link và thời gian gửi mỗi podcast.  
- **Báo cáo tuần**: tạo một workflow phụ, dùng `scheduleTrigger` (hàng tuần) để tổng hợp các podcast đã gửi và gửi báo cáo PDF qua email.  
- **Tùy chỉnh Prompt**: nếu muốn nhấn mạnh vào “đánh giá người nghe”, thêm câu “Include listener rating if available” vào prompt của node `agent`.  

### 📌 Kết luận
Với **workflow này**, các sếp sẽ không còn phải tốn công sức vào việc thu thập và biên tập danh sách podcast mỗi ngày. Chỉ cần một lần thiết lập, n8n sẽ tự động **scrape**, **phân tích** và **đăng** bản tóm tắt chất lượng cao lên Telegram, giúp cộng đồng người nghe luôn cập nhật xu hướng mới nhất.  
Hãy **import**, **cấu hình** và **bật chạy** ngay hôm nay – để AI và tự động hóa làm việc cho bạn!