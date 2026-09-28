---
title: "🚀 Tự động hóa giám sát và phân tích quảng cáo Facebook đối thủ bằng Apify, GPT-4o, Gemini & Google Sheets"
description: "Xây dựng hệ thống tự động cào Facebook Ad Library, phân tích thông minh hình ảnh, video, văn bản quảng cáo bằng AI và lưu trữ kết quả vào Google Sheets."
slug: "tu-dong-hoa-giam-sat-quang-cao-facebook-doi-thu-apify-ai"
tags: [n8n, automation, facebook-ads, apify, openai, gemini, google-sheets]
keywords: [n8n workflow, cào facebook ads, phân tích quảng cáo đối thủ, apify n8n, openai gpt-4o, google sheets automation]
---

# 🚀 Tự động hóa giám sát và phân tích quảng cáo Facebook đối thủ với AI

Các sếp có đang tốn hàng giờ mỗi tuần để mò mẫm trong **Facebook Ad Library** nhằm nghiên cứu chiến lược của đối thủ? Việc theo dõi thủ công từng mẫu quảng cáo, tải video, phân tích góc tiếp cận (angles) và lưu vào Excel không chỉ tốn thời gian mà còn khiến các sếp bỏ lỡ những xu hướng thị trường quan trọng.

Giải pháp ở đây là gì? Workflow n8n tự động hóa 100% này sẽ thay thế hoàn toàn đội ngũ thao tác thủ công, giúp các sếp cào dữ liệu quảng cáo, lọc đối thủ tiềm năng, dùng AI (GPT-4o và Gemini) mổ xẻ thông điệp/creative và tự động đồng bộ hóa vào Google Sheets.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Cào và phân tích quảng cáo đối thủ định kỳ mà không cần đụng tay.
- **Lọc nhiễu thông minh:** Tự động loại bỏ các nhà quảng cáo nhỏ lẻ, chỉ tập trung vào các đối thủ lớn có độ tín hiệu cao (dựa trên lượng Like của Page).
- **Mổ xẻ chuyên sâu bằng AI:** GPT-4o và Gemini phân tích chi tiết từng định dạng (Video, Hình ảnh, Văn bản), trích xuất chiến lược, góc tiếp cận và tạo gợi ý viết lại (rewrite prompts).
- **Cơ sở dữ liệu tập trung:** Toàn bộ dữ liệu cấu trúc được lưu gọn gàng vào Google Sheets, tự động chống trùng lặp theo ID quảng cáo.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động mượt mà, các sếp cần chuẩn bị sẵn:
- Tài khoản **Apify** (để cào dữ liệu Facebook Ad Library).
- Tài khoản **OpenAI** (API Key cho GPT-4o để phân tích ảnh và văn bản).
- Tài khoản **Google Gemini (Google Palm)** (để phân tích video nặng).
- Tài khoản **Dropbox** (lưu trữ tạm thời video/hình ảnh quảng cáo để AI xử lý).
- Tài khoản **Google Sheets** (nơi lưu trữ kết quả cuối cùng).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này từ n8n.io và import trực tiếp vào n8n Editor của các sếp, hoặc tạo mới một workflow và dán toàn bộ cấu trúc JSON vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình các thành phần quan trọng sau:
- **Apify (`Run an Actor and get dataset`, `Scrape Facebook Ad Library`)**: Kết nối tài khoản Apify và cấu hình Actor chuyên dụng cào Facebook Ad Library.
- **Bộ lọc tín hiệu (`Filter High-Signal Pages (>5k Likes)`)**: Điều chỉnh ngưỡng số lượng Like của Page (mặc định >5k Likes) tùy thuộc vào ngách thị trường của các sếp.
- **Định tuyến nội dung (`Detect Ad Creative Type`)**: Node Switch sẽ phân tách dữ liệu thành 3 nhánh xử lý riêng biệt: **Video**, **Image**, và **Text**.
- **Xử lý AI (`Analyze Image`, `Output Image/Text Summary`, `Analyze video`)**: Kết nối credentials OpenAI và Gemini. Đảm bảo các prompt yêu cầu AI trích xuất đúng cấu trúc chiến lược quảng cáo.
- **Lưu trữ (`Add as Type = Video/Image/Text`, Google Sheets)**: Trỏ tới file Google Sheet của các sếp và map chính xác các trường dữ liệu (Ad ID, Copy, Angle, Summary, Link...) vào các cột tương ứng.
- **Lưu trữ tạm (`Upload a file`, `Download a file` - Dropbox)**: Cấu hình thư mục lưu trữ trên Dropbox để phục vụ việc truyền tải video/hình ảnh sang AI phân tích.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** trên node `When clicking ‘Execute workflow’` để test chạy thử với một lượng dữ liệu nhỏ.
- Kiểm tra kết quả trả về trong Google Sheets.
- Bật công tắc **Active** để workflow tự động chạy theo lịch trình (Schedule) mong muốn.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Thêm node Slack hoặc Telegram ở cuối workflow để bắn thông báo ngay về máy mỗi khi có mẫu quảng cáo "triệu view" mới của đối thủ xuất hiện.
- **Tự động hóa lịch chạy:** Thiết lập Schedule Trigger chạy hàng tuần thay vì chỉ chạy thủ công.
- **Mở rộng nền tảng:** Kết hợp thêm các nguồn cào dữ liệu mạng xã hội khác như TikTok Ad Library để có góc nhìn toàn diện hơn.

### 📌 Kết luận
Việc nghiên cứu đối thủ chưa bao giờ dễ dàng và tự động hóa đến thế. Hãy cài đặt ngay workflow này để tối ưu hóa năng suất làm chiến lược marketing và "vượt mặt" đối thủ trên đường đua doanh số!