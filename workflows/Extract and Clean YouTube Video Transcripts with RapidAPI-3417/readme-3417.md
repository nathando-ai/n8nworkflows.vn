---
title: "🚀 Tự Động Lấy và Làm Sạch Transcript Video YouTube Bằng RapidAPI và n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động trích xuất, làm sạch và xử lý phụ đề (transcript) từ video YouTube thông qua RapidAPI cực kỳ nhanh chóng."
slug: "tu-dong-lay-va-lam-sach-youtube-transcript-rapidapi-n8n"
tags: [n8n, automation, no-code, youtube, rapidapi, content-marketing]
keywords: [n8n workflow, lay youtube transcript, tu dong hoa youtube, rapidapi youtube, xu ly transcript, n8n viet nam]
---

# 🚀 Tự Động Lấy và Làm Sạch Transcript Video YouTube Bằng RapidAPI

Các sếp làm nội dung, nghiên cứu thị trường hay xây dựng AI Knowledge Base chắc chắn đã từng đau đầu khi phải copy thủ công từng đoạn phụ đề (transcript) từ YouTube, sau đó mất hàng giờ để xóa các mốc thời gian, ký tự thừa và định dạng lại văn bản.

Giải pháp là đây! Workflow n8n này sẽ tự động hóa 100% quy trình: Nhập link YouTube qua Form -> Gọi RapidAPI lấy transcript thô -> Xử lý và làm sạch dữ liệu thành đoạn văn bản hoàn chỉnh, sẵn sàng sử dụng cho các mục đích phân tích hoặc sáng tạo nội dung.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 99% thời gian:** Không còn cảnh tua video, copy dán thủ công từng đoạn transcript rời rạc.
- **Dữ liệu sạch sẽ, chuẩn xác:** Tự động loại bỏ mốc thời gian (timestamps), khoảng trắng thừa và các định dạng rườm rà.
- **Giao diện nhập liệu thân thiện:** Sử dụng Form Trigger giúp dễ dàng dán link video bất kỳ và nhận kết quả ngay.
- **Tích hợp linh hoạt:** Dữ liệu sau khi làm sạch có thể đẩy thẳng vào Google Sheets, Notion, AI (ChatGPT) hoặc gửi về Telegram/Slack.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **RapidAPI Account:** Tài khoản miễn phí trên RapidAPI và đăng ký một dịch vụ lấy YouTube Transcript (như YouTube Transcript API).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy đoạn mã JSON của workflow hoặc tải file JSON từ nguồn, sau đó mở n8n Editor -> Chọn **Add workflow** -> Nhấp vào biểu tượng 3 chấm ở góc trên bên phải -> Chọn **Import from File** hoặc **Import from Clipboard** và dán mã vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 4 nodes chính, các sếp cần cấu hình cẩn thận các điểm sau:

- **Node `YoutubeVideoURL` (Form Trigger):** 
  - Đây là điểm khởi đầu của workflow. Sếp cấu hình giao diện form hiển thị một trường (field) để người dùng dán đường dẫn (URL) của video YouTube vào.
- **Node `extractTranscript` (HTTP Request):** 
  - Cần cấu hình kết nối tới **RapidAPI**. 
  - Điền Endpoint API lấy transcript, truyền tham số `videoId` được lấy từ URL của form ở node trước.
  - Thêm các Headers bắt buộc của RapidAPI vào phần Authentication/Headers (bao gồm `X-RapidAPI-Key` và `X-RapidAPI-Host`).
- **Node `processTranscript` (Function):** 
  - Node này chứa đoạn mã JavaScript (hoặc Code node) dùng để duyệt qua mảng dữ liệu JSON trả về từ API, bóc tách lấy phần nội dung text, loại bỏ các thẻ HTML hoặc ký tự đặc biệt nếu có.
- **Node `cleanedTranscript` (Set):** 
  - Định hình lại cấu trúc dữ liệu đầu ra cuối cùng, gom nhóm các đoạn text đã được làm sạch thành một trường dữ liệu hoàn chỉnh (`cleanText`) để các sếp dễ dàng sử dụng cho các bước tiếp theo.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** và test thử bằng một link video YouTube cụ thể thông qua Form URL để kiểm tra kết quả trả về.
- Sau khi test thành công, bật công tắc **Active** ở góc trên cùng bên phải để đưa workflow vào trạng thái hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp AI (OpenAI / Claude):** Sau node làm sạch transcript, các sếp có thể nối thêm node OpenAI để tự động tóm tắt video, viết bài blog, hoặc tạo danh sách ý chính (bullet points) từ nội dung video đó.
- **Lưu trữ tự động:** Thêm node Google Sheets hoặc Airtable để lưu lại link video gốc kèm theo nội dung transcript đã làm sạch nhằm xây dựng kho tài liệu riêng.
- **Nhận kết quả qua Telegram/Slack:** Thêm node gửi tin nhắn để hệ thống tự động bắn bản transcript hoặc bản tóm tắt về ứng dụng chat ngay khi xử lý xong.

### 📌 Kết luận
Việc khai thác nội dung từ YouTube chưa bao giờ dễ dàng đến thế với workflow tự động hóa này. Hãy thiết lập ngay hôm nay để tối ưu hóa quy trình làm content marketing và nghiên cứu tài liệu của các sếp!