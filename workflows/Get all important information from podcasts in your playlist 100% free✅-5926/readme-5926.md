---
title: "🚀 Tự động tóm tắt Podcast từ Playlist YouTube 100% miễn phí với n8n & AI"
description: "Hướng dẫn xây dựng workflow n8n tự động trích xuất nội dung, lấy transcript và tóm tắt toàn bộ video podcast từ YouTube playlist vào Google Sheets sử dụng AI Groq miễn phí."
slug: "tu-dong-tom-tat-podcast-youtube-playlist-n8n"
tags: [n8n, automation, youtube, ai-agent, groq, google-sheets, no-code]
keywords: [n8n workflow, tóm tắt podcast youtube, tự động hóa n8n, groq ai agent, supadata transcript, google sheets automation]
---

# 🚀 Tự động tóm tắt Podcast từ Playlist YouTube 100% miễn phí với n8n & AI

Các sếp có đang gặp tình trạng lưu hàng đống video podcast, chuỗi bài giảng hoặc video dài trên YouTube vào danh sách "Xem sau" (Watch Later) hay Playlist nhưng mãi không có thời gian xem hết? Việc ngồi nghe từng video dài 1-2 tiếng để chắt lọc ý chính thực sự là "nỗi ác mộng" ngốn rất nhiều thời gian quý báu.

Đừng lo, giải pháp ở đây rồi! Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ mạnh mẽ do tác giả **ARRE** thiết kế. Workflow này sẽ tự động hóa toàn bộ quy trình: quét toàn bộ video trong một YouTube Playlist, lấy transcript (bản ghi lời thoại), sử dụng AI siêu tốc của **Groq (Llama 3)** để tóm tắt và tự động đổ toàn bộ dữ liệu (Tiêu đề, URL, Script, Tóm tắt) thẳng vào **Google Sheets** mà không tốn một đồng chi phí API nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Thay vì mất hàng chục giờ nghe podcast, AI sẽ đọc và tóm tắt gọn gàng chỉ trong vài phút.
- **Lưu trữ khoa học:** Tự động đồng bộ toàn bộ tiêu đề, đường dẫn, transcript và bản tóm tắt vào Google Sheets một cách ngăn nắp.
- **100% Miễn phí:** Kết hợp YouTube API, Supadata (gói Free) và Groq AI (cung cấp API miễn phí cực nhanh) giúp tối ưu chi phí tối đa.
- **Vận hành tự động:** Chạy hàng loạt (Batch processing) qua từng video trong playlist mà không sợ bị tràn bộ nhớ hay lỗi rate-limit.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản sau:
1. **n8n Instance:** (Self-hosted hoặc n8n Cloud).
2. **YouTube Account / Google Cloud Console:** Để kết nối node `YouTube Playlist` (OAuth2).
3. **Google Sheets:** Tạo sẵn một file Google Sheet có sẵn các cột để lưu trữ (Tiêu đề, URL, Script, Tóm tắt...).
4. **Supadata API Key:** Đăng ký tài khoản miễn phí tại Supadata để lấy API lấy transcript video YouTube.
5. **Groq API Key:** Đăng ký miễn phí tại [Groq Console](https://console.groq.com/) để sử dụng mô hình AI `llama-3.1-8b-instant`.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ n8n template hoặc copy trực tiếp đoạn JSON, sau đó dán (Paste) trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình các thành phần sau để workflow chạy mượt mà:

- **📺 YouTube Playlist:** 
  - Chọn Credentials tài khoản YouTube của các sếp.
  - Thay đổi `playlistId` thành ID của danh sách phát YouTube mà các sếp muốn quét.
- **🔗 titles/URL (Function Node) & 🆔 video ID (Code Node):** 
  - Các node này xử lý việc bóc tách URL và trích xuất Video ID từ dữ liệu YouTube trả về. (Không cần sửa code trừ khi muốn custom thêm trường).
- **📝 supadata (HTTP Request Node):** 
  - Thêm API Key của Supadata vào header của request để lấy transcript chính xác từ YouTube.
- **🔄 Loop Over Items1 (Split In Batches) & Split Out:** 
  - Giúp chia nhỏ lượng video xử lý theo từng batch để không bị quá tải hệ thống.
- **🤖 Groq Chat Model (LLM Node) & AI Agent1:** 
  - Kết nối `Groq API` credentials.
  - Chọn model: `llama-3.1-8b-instant`.
  - Tùy chỉnh Prompt trong AI Agent nếu các sếp muốn AI tập trung tóm tắt theo một format riêng (ví dụ: gạch đầu dòng 5 ý chính, rút ra bài học thực tế...).
- **📊 Google Sheets3:** 
  - Kết nối Google Sheets Credentials.
  - Trỏ tới file Google Sheet và Sheet Name đã chuẩn bị từ trước, map các trường dữ liệu (Title, URL, Script, Summary) vào đúng các cột tương ứng.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** (chạy thủ công với nút `When clicking 'Execute workflow'`) để test thử với 1-2 video đầu tiên xem dữ liệu đẩy vào Google Sheets có chuẩn không.
- Sau khi test thành công, bấm **Active** để bật workflow chạy tự động theo lịch trình (nếu các sếp đổi Trigger thành Cron/Schedule) hoặc chạy theo yêu cầu.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Thông báo:** Thêm node **Telegram** hoặc **Slack** ở cuối vòng lặp để mỗi khi AI tóm tắt xong một video mới, hệ thống sẽ bắn một tin nhắn thông báo kèm link Google Sheets về điện thoại cho các sếp.
- **Lọc video ngắn/dài:** Thêm một node `If` sau node YouTube Playlist để lọc ra các video có thời lượng quá ngắn (ví dụ dưới 3 phút) hoặc quá dài nếu không cần thiết.
- **Lưu trữ vector:** Có thể kết hợp thêm Vector Store (như Pinecone hoặc Qdrant) vào AI Agent để sau này có thể "chat" trực tiếp với toàn bộ nội dung kho tàng podcast của các sếp.

### 📌 Kết luận
Workflow này là một "vũ khí tối thượng" cho những ai ghiền học hỏi từ podcast nhưng lại thiếu thời gian. Hãy cài đặt ngay lên VPS của mình, kết nối API Groq và tận hưởng việc để AI làm "thư ký" đọc sách, nghe podcast thay cho các sếp nhé! Chúc các sếp thành công!