---
title: "🚀 Tự động tìm kiếm Reels Instagram hot nhất & lưu Insights vào Notion bằng Gemini AI & Apify"
description: "Hướng dẫn cài đặt workflow n8n tự động cào Instagram Reels hiệu quả cao qua Apify, phân tích nội dung chuyên sâu bằng Google Gemini AI và đồng bộ insights trực quan vào Notion."
slug: "tu-dong-tim-kiem-instagram-reels-luu-notion-gemini-apify"
tags: [n8n, automation, no-code, instagram, apify, gemini-ai, notion, market-research]
keywords: [n8n workflow, tự động hóa instagram, apify instagram reels, gemini ai phân tích video, lưu notion tự động, market research instagram]
---

# 🚀 Tự động tìm kiếm Reels Instagram hot nhất & lưu Insights vào Notion bằng Gemini AI & Apify

Nghiên cứu thị trường và bắt nhịp xu hướng nội dung (Trend Watching) trên Instagram Reels là một công việc cực kỳ tốn thời gian. Các sếp thường phải mất hàng giờ lướt feed, thủ công lọc ra các video triệu view, sau đó phân tích xem vì sao nó viral và ghi chép lại vào Google Sheets hay Notion. 

Quá trình thủ công này vừa nhàm chán, vừa thiếu hệ thống. Workflow n8n siêu việt này sinh ra để giải quyết triệt để vấn đề đó: tự động hóa 100% từ khâu cào dữ liệu Reels qua **Apify**, phân tích video thông minh bằng **Google Gemini AI**, cho đến việc đồng bộ toàn bộ insights đắt giá vào **Notion** để các sếp tha hồ nghiên cứu chiến lược nội dung!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Tự động quét danh sách tài khoản mục tiêu định kỳ mà không cần động tay.
- **Phân tích AI chuyên sâu:** Sử dụng Gemini AI để xem video, phân loại danh mục, nhận diện loại nội dung và đúc kết insights.
- **Kho lưu trữ thông minh:** Tự động tạo trang, cập nhật số liệu thống kê (views, likes, comments) và insights chi tiết trực tiếp vào Notion Database.
- **Hoạt động 24/7:** Chạy ngầm tự động theo lịch trình (Schedule Trigger) hoặc kích hoạt thủ công khi cần thiết.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **n8n Instance:** (Self-hosted hoặc n8n Cloud).
- **Notion Account & API:** Tạo một tích hợp (Integration) trên Notion và cấp quyền truy cập vào Workspace. Tải cấu trúc database chuẩn tại [đây](https://drive.google.com/file/d/1FVaS_-ztp6PDAJbETUb1dkg8IqE4qHqp/view?usp=sharing).
- **Apify Account:** Tài khoản Apify để chạy các Actor cào dữ liệu Instagram Reels (Cần có Apify API Token).
- **Google Gemini (PaLM) API Key:** Dùng cho các HTTP Request nodes gọi đến Gemini API để phân tích video.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy đoạn code JSON từ nguồn gốc.
- Mở n8n Editor, chọn **Add workflow** -> Nhấn vào dấu `...` ở góc trên bên phải -> **Import from File** hoặc **Import from Clipboard** và dán vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node `Get Sources`, `Update Accounts`, `Get Reels`, `Create`, `Update` (Notion):** Kết nối với tài khoản Notion của các sếp. Trỏ tới đúng Database nguồn chứa danh sách tài khoản theo dõi (Sources) và Database đích chứa danh sách Reels.
- **Node `Run an Actor`, `Get Status`, `Get dataset items` (Apify):** Kết nối `apifyApi` credentials. Node này sẽ thực thi Actor chuyên cào dữ liệu Instagram từ Apify.
- **Node `Upload to Gemini`, `Gemini Analyze`, `Get File State` (HTTP Request):** Sử dụng `Google Gemini (PaLM) API` credential với host `https://generativelanguage.googleapis.com` và điền Gemini API Key cá nhân.
- **Node `Variables` (Code):** Cấu hình các tham số phân tích, giới hạn số lượng tài khoản và số Reels cần quét cho mỗi lần chạy (khuyến nghị test với 3-5 tài khoản, mỗi tài khoản 3-5 Reels trước).
- **Node `Set Prompt` (Set):** Tinh chỉnh câu lệnh Prompt AI hướng dẫn Gemini cách phân tích video, phân loại danh mục và đúc kết insights theo mong muốn của doanh nghiệp.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử nghiệm thủ công với dữ liệu mẫu và kiểm tra xem dữ liệu có đổ về Notion suôn sẻ không.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để workflow tự động chạy ngầm theo lịch trình từ node `Schedule Trigger`.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo qua Telegram/Slack:** Thêm một node Telegram hoặc Slack ở cuối luồng để nhận thông báo ngay lập tức mỗi khi hệ thống tìm được một Reel "triệu view" mới.
- **Mở rộng nguồn quét:** Không chỉ quét các tài khoản chỉ định, các sếp có thể kết hợp thêm Apify hashtag scraper để quét các xu hướng mới nổi theo từ khóa ngành nghề.
- **Sao lưu định kỳ:** Kết hợp thêm các node lọc điều kiện (IF) để chỉ tiến hành phân tích sâu với các Reels đạt ngưỡng tương tác tối thiểu (ví dụ > 50k views), giúp tiết kiệm tối đa token Gemini AI.

### 📌 Kết luận
Tự động hóa nghiên cứu thị trường chưa bao giờ dễ dàng đến thế với sự kết hợp hoàn hảo của n8n, Apify và Gemini AI. Hãy cài đặt ngay workflow này để xây dựng một "con bot" nghiên cứu xu hướng Instagram Reels hoạt động 24/7 cho đội ngũ Marketing của các sếp!