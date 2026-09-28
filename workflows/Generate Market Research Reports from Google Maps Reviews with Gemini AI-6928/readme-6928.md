---
title: "🚀 Tự động tạo báo cáo nghiên cứu thị trường từ Google Maps Reviews với Gemini AI"
description: "Hướng dẫn xây dựng workflow n8n tự động cào dữ liệu Google Maps, phân tích đánh giá khách hàng bằng Gemini AI và gửi báo cáo chi tiết qua Gmail."
slug: "tao-bao-cao-nghien-cuu-thi-truong-google-maps-gemini-ai"
tags: [n8n, automation, google-maps, gemini-ai, market-research, ai-summarization]
keywords: [n8n workflow, nghiên cứu thị trường, google maps reviews, gemini ai, tự động hóa n8n, serpapi]
---

# 🚀 Tự động tạo báo cáo nghiên cứu thị trường từ Google Maps Reviews với Gemini AI

Các sếp có bao giờ tốn hàng giờ liền để lướt qua hàng trăm đánh giá trên Google Maps của đối thủ cạnh tranh, cố gắng gom góp xem khách hàng đang phàn nàn cái gì hay thích thú điểm nào chưa? Công việc thủ công này cực kỳ tốn thời gian, nhàm chán và rất dễ bỏ sót các insight quan trọng.

Đừng lo, workflow n8n này sẽ thay các sếp làm trọn gói từ A-Z: tự động tìm kiếm địa điểm trên Google Maps, bóc tách toàn bộ đánh giá (reviews), dùng sức mạnh của **Google Gemini AI** để phân tích sâu, và cuối cùng là gửi thẳng một bản báo cáo nghiên cứu thị trường cực kỳ chuyên nghiệp vào hộp thư Gmail của các sếp! 100% tự động, không cần viết code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo lỗi timeout hay sập vặt, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Thay vì mất vài ngày cào dữ liệu và tổng hợp thủ công, workflow chạy xong trong vài phút.
- **Insight khách hàng sắc bén:** Gemini AI sẽ phân tích điểm mạnh, điểm yếu, xu hướng và nhu cầu ẩn giấu của khách hàng từ hàng trăm đánh giá thực tế.
- **Báo cáo tận nơi:** Nhận ngay báo cáo nghiên cứu thị trường chi tiết, trình bày đẹp mắt ngay trong email cá nhân.
- **Hoạt động liên tục:** Có thể lên lịch chạy định kỳ (cron job) để theo dõi đối thủ hàng tuần/hàng tháng tự động.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động mượt mà, các sếp cần chuẩn bị sẵn các tài khoản sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **SerpAPI Key:** Dùng để lấy dữ liệu Google Maps (có gói miễn phí 100 lượt tìm kiếm/tháng tại [SerpAPI](https://serpapi.com/google-maps-reviews-api)).
- **Google AI Studio API Key:** Dùng cho mô hình Gemini AI phân tích.
- **Tài khoản Gmail:** Để cấu hình node gửi email báo cáo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này, vào giao diện n8n Editor, chọn **Add workflow** -> **Import from JSON** và dán vào là xong.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, hệ thống gồm 14 nodes sẽ xuất hiện. Các sếp cần cấu hình chính xác các điểm sau:

- **Node `User Input Configuration` (Loại `Set`):** 
  Đây là nơi các sếp thiết lập từ khóa tìm kiếm và khu vực muốn nghiên cứu. Sửa lại các thông số cho phù hợp với nhu cầu:
  ```json
  {
    "search_query": "restaurants downtown",
    "search_location": "@40.7589,-73.9851,12z",
    "language_code": "en",
    "analysis_focus": "restaurant",
    "city_name": "New York City"
  }
  ```
  *(Gợi ý: Dùng trang [LatLong.net](https://www.latlong.net/) để lấy tọa độ `search_location` chuẩn xác).*

- **Node `Dynamic Search Places` & `Get Reviews Content` (Loại `HTTP Request`):**
  Thay thế chuỗi `YOUR_SERPAPI_KEY_HERE` bằng API Key thật của các sếp lấy từ SerpAPI.

- **Node `Google Gemini Chat Model` (Loại `lmChatGoogleGemini`):**
  Tạo và kết nối credentials sử dụng `Google Palm/Gemini API Key` lấy từ [Google AI Studio](https://ai.google.dev/gemini-api/docs/api-key).

- **Node `Send Email Report` (Loại `Gmail`):**
  Kết nối tài khoản Gmail của các sếp qua OAuth2 và đổi địa chỉ email nhận báo cáo thành email cá nhân hoặc email công việc của các sếp.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** tại node `Start Workflow` (Manual Trigger) để chạy thử nghiệm lần đầu và kiểm tra dữ liệu trả về ở từng bước.
- Sau khi test thành công, bật công tắc **Active** ở góc trên cùng bên phải để workflow sẵn sàng hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack/Telegram:** Thêm node gửi thông báo qua Telegram hoặc Slack ngay sau node `Send Email Report` để team cùng nắm được kết quả phân tích ngay lập tức.
- **Lưu trữ vào Google Sheets:** Thêm một node Google Sheets trước bước gửi email để lưu lại toàn bộ lịch sử nghiên cứu thị trường làm cơ sở dữ liệu dài hạn.
- **Tự động hóa định kỳ:** Thay thế node `Start Workflow` bằng node `Schedule Trigger` để n8n tự động quét và gửi báo cáo cho các sếp mỗi sáng thứ Hai hàng tuần.

### 📌 Kết luận
Workflow này là một "vũ khí bí mật" cực mạnh cho các đội ngũ Sales, Marketing và Chủ doanh nghiệp muốn nhanh chóng nắm bắt thị hiếu thị trường và đối thủ cạnh tranh mà không tốn nhiều công sức. Hãy cài đặt ngay hôm nay và để AI làm thay những việc lặp đi lặp lại cho các sếp!