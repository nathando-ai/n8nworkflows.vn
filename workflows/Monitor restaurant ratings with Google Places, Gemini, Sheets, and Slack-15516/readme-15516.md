---
title: "🚀 Tự động giám sát đánh giá nhà hàng với Google Places, Gemini và Slack"
description: "Xây dựng hệ thống theo dõi rating nhà hàng tự động hàng ngày, sử dụng AI Gemini phân tích nguyên nhân review và gửi cảnh báo thông minh qua Slack."
slug: "tu-dong-giam-sat-danh-gia-nha-hang-google-places-gemini-slack"
tags: [n8n, automation, google-places, google-gemini, slack, market-research]
keywords: [n8n workflow, giám sát nhà hàng, google places api, google gemini ai, slack alerts, tự động hóa marketing]
---

# 🚀 Tự động giám sát đánh giá nhà hàng với Google Places, Gemini và Slack

Việc theo dõi thủ công đánh giá (ratings) và phản hồi của khách hàng trên Google Maps cho một hoặc chuỗi nhà hàng là một cơn ác mộng thực sự đối với đội ngũ vận hành và Marketing. Các sếp thường chỉ phát hiện ra điểm số sụt giảm khi khách hàng đã bỏ đi, và việc đọc hàng trăm review để tìm ra nguyên nhân (do phục vụ chậm, đồ ăn mặn, hay giá cao) tốn rất nhiều thời gian.

Workflow n8n **RestaurantPulse** này sinh ra để giải quyết triệt để nỗi đau đó: Tự động hóa 100% quy trình quét dữ liệu, phát hiện biến động, sử dụng AI phân tích nguyên nhân gốc rễ từ review thực tế và bắn tin nhắn cảnh báo phân loại mức độ về Slack cho các sếp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Biết ngay "Tại sao" thay vì chỉ biết "Bao nhiêu":** Không chỉ báo điểm số thay đổi, AI còn đọc review và chỉ ra nguyên nhân cụ thể kèm hành động khắc phục.
- **Phân loại cảnh báo thông minh:** Tự động chia mức độ 🔴 Critical (Nguy cấp), 🟡 Watch (Cần chú ý) và 🟢 Positive (Tích cực) để xử lý đúng trọng tâm.
- **Lưu trữ lịch sử tự động:** Mọi biến động và chẩn đoán của AI được ghi lại gọn gàng vào Google Sheets để làm dữ liệu phân tích xu hướng.
- **Hoạt động 24/7:** Chạy tự động theo lịch trình định sẵn (Schedule Trigger) mà không cần con người nhúng tay.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Google Places API Key** (lấy từ Google Cloud Console)
- **Google Gemini API Key** (hoặc Google Palm API)
- **Tài khoản Google Sheets** (để quản lý danh sách nhà hàng và lịch sử cảnh báo)
- **Tài khoản Slack** (để nhận thông báo cảnh báo)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này và paste trực tiếp vào n8n Editor của mình, hoặc import file JSON tải từ trang chủ n8n.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động mượt mà, các sếp cần cấu hình kỹ các node sau:

- **📊 Read Restaurant List (Google Sheets):** Kết nối tài khoản Google Sheets OAuth2, chọn file chứa danh sách nhà hàng.
  - *Chuẩn bị Google Sheets gồm 2 sheet:*
    - **Sheet 1 (`restaurant_list`):** Các cột gồm `place_id`, `name`, `last_rating`, `last_review_count`, `last_checked`.
    - **Sheet 2 (`alert_history`):** Các cột gồm `timestamp`, `restaurant_name`, `old_rating`, `new_rating`, `rating_diff`, `alert_level`, `ai_diagnosis`, `place_id`.
- **🌐 Fetch Live Data (Google Places API) & 🔄 Loop Over Restaurants:** Dùng HTTP Request gọi đến Google Places API dựa trên `place_id` của từng nhà hàng. Các sếp nhớ cấu hình API Key trong header hoặc query param của request.
- **🧠 Change Detection Engine (Code Node):** Node này dùng Javascript để so sánh điểm số hiện tại với `last_rating` trong Google Sheets, đồng thời kiểm tra các ngưỡng:
  - 🔴 *Critical:* Điểm giảm từ 0.3+ trở lên.
  - 🟡 *Watch:* Điểm giảm 0.1+ HOẶC có thêm 50+ review mới.
  - 🟢 *Positive:* Điểm tăng 0.2+ trở lên.
- **🤖 AI Diagnosis (Google Gemini):** Kết nối Google Gemini API để phân tích các review mới nhận được và đưa ra chẩn đoán nguyên nhân gốc rễ.
- **📡 Alert Routing (Switch) & Slack Nodes (🔴 Critical, 🟡 Watch, 🟢 Positive):** Kết nối Slack OAuth2, chọn Channel nhận thông báo tương ứng cho từng mức độ cảnh báo.
- **💾 Update State & 📜 Log Alert History (Google Sheets):** Node cập nhật lại trạng thái điểm mới nhất vào `restaurant_list` và ghi log chi tiết vào `alert_history`.

#### 3. Kích hoạt ⚡️
- Chạy thử nghiệm thủ công (Test workflow) với 1 nhà hàng mẫu để đảm bảo API Google Places và Gemini trả về dữ liệu chuẩn xác.
- Bật công tắc **Active** để Schedule Trigger tự động hoạt động mỗi ngày.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Chatwork / Zalo / Telegram:** Ngoài Slack, các sếp có thể duplicate các nhánh alert để bắn tin nhắn đồng thời lên group Zalo hoặc Telegram của đội ngũ vận hành cửa hàng.
- **Tự động tạo Task:** Kết hợp thêm node Trello, Asana hoặc Notion để tự động tạo công việc cho quản lý cửa hàng xử lý khi có cảnh báo 🔴 Critical.
- **Báo cáo tuần/tháng:** Tạo thêm một workflow phụ đọc dữ liệu từ `alert_history` trên Google Sheets để tổng hợp báo cáo sức khỏe thương hiệu gửi email cho Ban Giám Đốc định kỳ hàng tuần.

### 📌 Kết luận
RestaurantPulse là một mẫu workflow chuẩn mực kết hợp giữa dữ liệu API thời gian thực và AI tạo sinh (Generative AI). Hãy thiết lập ngay hôm nay để nắm bắt trọn vẹn trải nghiệm của khách hàng và bảo vệ uy tín thương hiệu nhà hàng của các sếp!