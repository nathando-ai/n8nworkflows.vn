---
title: "🚀 Tự động tạo video marketing UGC cho thương mại điện tử với Sora 2 và Gemini trên n8n"
description: "Hướng dẫn xây dựng hệ thống n8n tự động hóa hoàn toàn việc tạo video quảng cáo UGC chân thực từ ảnh sản phẩm bằng OpenAI Sora 2 và Google Gemini."
slug: "tu-dong-tao-video-ugc-sora-2-gemini-n8n"
tags: [n8n, automation, ai-video, sora2, gemini, ecommerce, nocode]
keywords: [n8n workflow, tao video ugc tu dong, sora 2 api, gemini pro, ai marketing ecommerce]
---

# 🚀 Tự động tạo video marketing UGC cho thương mại điện tử với Sora 2 và Gemini

Các sếp kinh doanh eCommerce chắc chắn hiểu rằng video UGC (User-Generated Content) đang là "vũ khí tối thượng" để chốt đơn trên TikTok, Reels và YouTube Shorts. Tuy nhiên, việc thuê creator quay dựng, lên kịch bản và test A/B tốn rất nhiều thời gian, chi phí và nhân lực.

Giải pháp là gì? Hãy để tự động hóa lo! Bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n cực đỉnh, kết hợp sức mạnh của **OpenAI Vision**, **Google Gemini 2.5 Pro** và **Sora 2 API** để tự động biến một bức ảnh sản phẩm đơn thuần thành chuỗi video quảng cáo UGC chuyên nghiệp chỉ bằng vài cú click.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, xử lý các tác vụ AI nặng và render video, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% chi phí sản xuất:** Không cần thuê KOC/KOL hay ekip quay phim phức tạp vẫn có video review sản phẩm chân thực.
- **Sản xuất hàng loạt biến thể (A/B Testing):** Tự động tạo nhiều kịch bản và góc quay khác nhau từ một hình ảnh sản phẩm duy nhất.
- **Tối ưu hóa đa nền tảng:** Video xuất ra định dạng 9:16 (720x1280) chuẩn chỉnh, tự động lưu trữ gọn gàng lên Google Drive.
- **Vận hành tự động 24/7:** Chỉ cần upload ảnh qua Form, hệ thống sẽ tự động phân tích, viết kịch bản, tạo frame, gọi API render video và báo cáo kết quả.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (bản Cloud hoặc Self-hosted).
- **OpenAI API Key:** Cần có tài khoản OpenAI được cấp quyền truy cập Sora 2 API và GPT-4 Vision.
- **Google Gemini API Key (Google Palm/Gemini API):** Dùng cho node `gemini-2.5-pro` để viết kịch bản và xử lý hình ảnh.
- **Google Drive Account:** Tài khoản Google kết nối OAuth2 để tự động lưu video hoàn thiện.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow từ n8n template hoặc copy đoạn JSON, sau đó paste trực tiếp vào giao diện n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống mượt mà vận hành, các sếp cần chú ý cấu hình các node cốt lõi sau:
- **`analyze_product` (OpenAI Node):** Chọn credential OpenAI API, node này sử dụng Vision API để phân tích chi tiết sản phẩm từ hình ảnh.
- **`gemini-2.5-pro` & `extract_prompts` (Gemini & LangChain Nodes):** Kết nối Google Gemini API credential. Đảm bảo model được cấu hình đúng để nhận diện persona khách hàng và viết kịch bản UGC 12 giây chuẩn xác.
- **`generate_video`, `get_video_status`, `get_video` (HTTP Request Nodes):** Cấu hình đúng endpoint của Sora 2 API cùng với OpenAI API Key để gửi lệnh render video, kiểm tra trạng thái render (polling mỗi 15 giây) và tải file về.
- **`upload_video` (Google Drive Node):** Chọn Google Drive OAuth2 credential và trỏ tới thư mục (Folder ID) cụ thể trên Drive để lưu trữ video tự động.
- **`resize_image` (Edit Image Node):** Tùy chỉnh kích thước khung hình video (mặc định 720x1280 cho dọc mobile) tùy theo nhu cầu chiến dịch.

#### 3. Kích hoạt ⚡️
- Chạy thử (Test run) bằng một sản phẩm mẫu thông qua giao diện `form_trigger`.
- Kiểm tra quá trình xử lý qua từng node (Vision -> Gemini script -> Sora 2 generation -> Google Drive upload).
- Bật công tắc **Active** để đưa workflow vào hoạt động chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Thêm node Telegram hoặc Slack ở cuối workflow để gửi thông báo trực tiếp kèm link Google Drive ngay khi video render xong.
- **Đa dạng hóa phong cách:** Tinh chỉnh prompt trong node `set_build_video_prompts` để tạo các style video khác nhau (Review háo hức, Unboxing bí ẩn, Mẹo vặt đời sống...).
- **Tự động thêm phụ đề:** Kết hợp thêm các API biên tập video hoặc Whisper để tự động chèn sub vào video UGC tăng tỷ lệ giữ chân người xem.

### 📌 Kết luận
Việc sản xuất video marketing chưa bao giờ dễ dàng và tự động đến thế với sự kết hợp của AI thế hệ mới (Sora 2 & Gemini) và n8n. Hãy thiết lập ngay workflow này để tối ưu hóa chiến dịch quảng cáo eCommerce của các sếp ngay hôm nay!