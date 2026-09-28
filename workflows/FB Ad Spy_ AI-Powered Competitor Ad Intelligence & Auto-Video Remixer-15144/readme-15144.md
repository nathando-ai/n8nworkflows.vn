---
title: "🚀 Tự động hóa Facebook Ad Spy & Remix Video bằng AI cực đỉnh với n8n"
description: "Khám phá workflow n8n đỉnh cao giúp cào dữ liệu Facebook Ad Library, phân tích đối thủ bằng AI đa phương thức và tự động tạo lại video quảng cáo."
slug: "fb-ad-spy-ai-video-remixer-n8n"
tags: [n8n, automation, ai, facebook-ads, marketing, openai, gemini]
keywords: [n8n workflow, fb ad spy, ai video remixer, facebook ad library, tự động hóa marketing, openai n8n]
keywords: [n8n workflow, fb ad spy, ai video remixer, facebook ad library, tự động hóa marketing, openai n8n]
---

# 🚀 Tự động hóa Facebook Ad Spy & Remix Video bằng AI cực đỉnh với n8n

Việc nghiên cứu đối thủ cạnh tranh trên Facebook Ad Library (Ad Spy) thủ công thường ngốn rất nhiều thời gian của các nhà quảng cáo và Marketer: từ việc lướt tìm kiếm từng mẫu quảng cáo, tải video, phân tích xem vì sao mẫu đó lại thu hút nhiều tương tác, cho đến việc lên ý tưởng kịch bản mới dựa trên insight đó. 

Hiểu được nỗi đau này, workflow **"FB Ad Spy: AI-Powered Competitor Ad Intelligence & Auto-Video Remixer"** do tác giả *Koulikas Giannis (Coreflow Automation)* thiết kế sẽ thay thế hoàn toàn sức người. Hệ thống này tự động hóa từ A-Z: cào dữ liệu quảng cáo, phân tích nội dung text/hình ảnh/video bằng AI (OpenAI & Gemini), lưu trữ vào Google Sheets, cho đến việc tự động dựng lại và chỉnh sửa video quảng cáo mới tối ưu hơn!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow quy mô lớn với các tác vụ đa phương thức (Multimodal AI) chạy ổn định 24/7 mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian nghiên cứu:** Tự động thu thập hàng loạt mẫu quảng cáo hiệu suất cao từ Facebook Ad Library mà không cần copy/paste thủ công.
- **Phân tích sâu bằng AI đa phương thức:** Tận dụng sức mạnh của OpenAI và Gemini để giải mã kịch bản, cấu trúc hình ảnh và thông điệp của đối thủ.
- **Tự động hóa Remix video:** Chuyển đổi và xử lý định dạng video (tỷ lệ 9:16, chèn phụ đề tự động) để tái sử dụng làm ý tưởng quảng cáo riêng cho thương hiệu.
- **Quản lý tập trung thông minh:** Mọi dữ liệu phân tích, chỉ số tương tác và file media đều được đồng bộ gọn gàng lên Google Sheets và Google Drive / Cloud Storage.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **n8n Instance:** Đã cài đặt n8n (khuyến nghị bản self-hosted mới nhất).
- **OpenAI API Key:** Dùng cho các node phân tích văn bản, hình ảnh và tạo prompt video (`Summarize Text with AI`, `Create Video Prompt with AI`,...).
- **Google Gemini API / Cloud Account:** Phục vụ cho việc tải và phân tích video dung lượng lớn (`Submit Video to Gemini`, `Analyze Video in Gemini`).
- **Google Drive & Google Sheets Credentials:** Để lưu trữ file video và ghi nhận bảng dữ liệu báo cáo.
- **Google Cloud Storage Credentials:** Lưu trữ file video đầu ra sau khi xử lý.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ nguồn cung cấp.
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File** và tải file JSON lên, hoặc copy toàn bộ mã JSON và dán trực tiếp vào không gian làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow sở hữu hệ thống 54 nodes cực kỳ mạnh mẽ, các sếp cần chú ý cấu hình kỹ các điểm sau để chạy mượt mà:
- **Node `Scrape Ad Library Data` & `Download Video Content` (HTTP Request):** Cấu hình đường dẫn API cào dữ liệu từ Facebook Ad Library hoặc bên thứ ba cung cấp dữ liệu Ad Library mà các sếp đang sử dụng.
- **Các node AI (`Summarize Video with AI`, `Analyze Image with AI`, `Create Video Prompt with AI`):** Kết nối đúng OpenAI API Credential và kiểm tra lại System Prompt cho phù hợp với ngành hàng sản phẩm của doanh nghiệp.
- **Các node Google Services (`Save Video to Google Drive`, `Record Video Data in Sheets`, `Save File to Cloud Storage`):** 
  - Chọn đúng tài khoản Google OAuth2 của sếp.
  - Trỏ đúng ID của Google Sheet dùng để lưu trữ dữ liệu thông tin quảng cáo (Text, Image, Video).
- **Các node xử lý video (`Transform Video to 9:16 Ratio`, `Insert Video Captions`):** Đảm bảo cấu hình đúng các endpoint API xử lý video hoặc dịch vụ render video bên thứ ba mà hệ thống đang tích hợp qua HTTP Request.

#### 3. Kích hoạt ⚡️
- Nhấn nút **`On Manual Start`** để chạy thử nghiệm (Test Run) với một vài dữ liệu mẫu.
- Kiểm tra các nhánh `Filter by Ad Likes`, `Batch Video Ads Processing` xem dữ liệu có chảy qua mượt mà hay không.
- Sau khi test thành công, bật công tắc **Active** góc trên cùng bên phải để workflow tự động hoạt động theo lịch trình hoặc sự kiện kích hoạt.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo Telegram/Slack:** Thêm một node Telegram hoặc Slack ở cuối luồng phân tích để hệ thống tự động bắn tin nhắn báo cáo về "Hot Ad" mới tìm được mỗi ngày.
- **Tự động hóa theo lịch (Cron):** Thay thế node `On Manual Start` bằng node `Schedule Trigger` để hệ thống tự động đi "thám thính" đối thủ vào 0h mỗi tuần.
- **Lưu trữ Log lỗi:** Kết hợp nhánh Error Trigger để ghi lại các lỗi khi API cào dữ liệu quá tải, giúp dễ dàng debug.

### 📌 Kết luận
Workflow **FB Ad Spy & Auto-Video Remixer** là một giải pháp tự động hóa toàn diện, giúp các đội ngũ Marketing và Agency nắm bắt xu hướng quảng cáo của đối thủ nhanh gấp 10 lần. Hãy cài đặt ngay hôm nay để tối ưu hóa quy trình sáng tạo nội dung quảng cáo của doanh nghiệp các sếp nhé!