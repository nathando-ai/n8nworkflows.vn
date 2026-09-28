---
title: "🚀 Tự động quét kênh YouTube tiềm năng từ từ khóa với n8n và Google Sheets"
description: "Hướng dẫn xây dựng workflow n8n tự động tìm kiếm, phân tích và lọc các kênh YouTube chất lượng cao từ danh sách từ khóa, sau đó lưu trữ trực tiếp vào Google Sheets."
slug: "tu-dong-quet-kenh-youtube-tu-tu-khoa-voi-n8n"
tags: [n8n, automation, youtube, google-sheets, lead-generation, market-research]
keywords: [n8n workflow, tự động hóa youtube, tìm kiếm creator, quét kênh youtube, google sheets automation]
---

# 🚀 Tự động quét kênh YouTube tiềm năng từ từ khóa với n8n và Google Sheets

Các sếp có đang tốn hàng giờ đồng hồ mỗi ngày để tìm kiếm các kênh YouTube, KOLs, hay các nhà sáng tạo nội dung trong ngách của mình để làm influencer marketing hay nghiên cứu thị trường không? Việc copy-paste thủ công từng từ khóa, xem video, lấy thông tin channel rồi đưa vào file Excel quả thực là một cực hình tốn thời gian và dễ sai sót.

Đừng lo, bài toán đó sẽ được giải quyết triệt để với workflow n8n **"Discover YouTube channels from keywords and save leads to Google Sheets"**. Workflow này sẽ tự động hóa 100% quy trình: lấy từ khóa từ Google Sheets, tìm kiếm video, lọc ra channel chất lượng dựa trên chỉ số (số sub, lượt view, số video) và lưu danh sách leads về file Google Sheets một cách mượt mà!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo sập nguồn hay mất kết nối, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Tự động hoàn toàn từ khâu quét từ khóa, lọc dữ liệu đến lưu trữ mà không cần đụng tay.
- **Dữ liệu chuẩn xác, sạch sẽ:** Tự động loại bỏ các channel trùng lặp, chỉ giữ lại các kênh đạt tiêu chuẩn chất lượng (Subscriber, View, Video count).
- **Cơ sở dữ liệu tự động mở rộng:** Luôn cập nhật danh sách leads mới mỗi ngày, tự động update nếu kênh đã tồn tại trong bảng.
- **Ứng dụng linh hoạt:** Phục vụ đắc lực cho Influencer Marketing, Lead Generation hoặc nghiên cứu ngách (Market Research).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Google Sheets:** 1 file Google Sheets chứa 2 sheet: 1 sheet danh sách từ khóa (`List of Target Keywords`) và 1 sheet lưu kết quả channel.
- **YouTube Data API v3:** Tài khoản Google Cloud Console để tạo YouTube OAuth2 Credentials (hoặc API Key tùy cấu hình HTTP Request).
- **Apify Account (Tùy chọn nâng cao):** Nếu muốn sử dụng Actor của Apify để cào sâu hơn (workflow có tích hợp sẵn node Apify).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy toàn bộ mã JSON từ n8n.
- Trong giao diện n8n Editor, bấm vào menu **Add workflow** -> Chọn **Import from File** hoặc dán trực tiếp (`Ctrl + V`) vào canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy trơn tru, các sếp cần cấu hình chính xác các node trọng điểm sau:

- **Schedule Trigger:** Cài đặt lịch chạy tự động (ví dụ: chạy mỗi giờ, mỗi ngày một lần) tùy thuộc vào số lượng từ khóa và nhu cầu quét dữ liệu của các sếp.
- **List of Target Keywords (Google Sheets):** 
  - Chọn Credentials `googleSheetsOAuth2Api`.
  - Trỏ tới file Google Sheets chứa danh sách từ khóa của các sếp.
- **Get the first keyword & Update Keyword Status -> Processing (Code & Google Sheets):** 
  - Node này lấy từ khóa chưa xử lý đầu tiên trong danh sách và cập nhật trạng thái thành "Processing" để tránh lặp lại ở các lần chạy sau.
- **Search Videos based on Keywords & Get Channel Stats (HTTP Request):**
  - Cần kết nối `youTubeOAuth2Api` để gọi API YouTube tìm kiếm video dựa trên từ khóa và lấy các chỉ số chi tiết của kênh (Subscribers, Total Views, Video Count).
- **Filter based on Criteria (Code):**
  - Tùy chỉnh đoạn code JavaScript trong node này để đặt ngưỡng lọc phù hợp (ví dụ: tối thiểu bao nhiêu subscribers, tổng số view tối thiểu...) để chỉ lọc ra các creator chất lượng nhất.
- **Append or update row in sheet / sheet1 (Google Sheets):**
  - Cấu hình trỏ tới sheet lưu kết quả. Chọn thao tác `appendOrUpdate` để n8n tự động thêm mới nếu chưa có, hoặc cập nhật thông tin nếu kênh YouTube đã tồn tại trong file.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** để test thử với 1-2 từ khóa mẫu xem dữ liệu trả về Google Sheets có chính xác không.
- Nếu mọi thứ xanh mướt (success), gạt công tắc sang **Active** để hệ thống tự động chạy ngầm 24/7!

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node **Telegram** hoặc **Slack** sau bước lưu Google Sheets để nhận thông báo ngay lập tức mỗi khi hệ thống tìm được một kênh YouTube "triệu view" tiềm năng.
- **Chia nhỏ từ khóa:** Nhóm các từ khóa theo chiến dịch (Campaign) để dễ quản lý thứ tự ưu tiên quét dữ liệu.
- **Gửi Email tự động:** Kết hợp với node Gmail để gửi email outreach tự động cho các creators vừa được tìm thấy thỏa mãn tiêu chí.

### 📌 Kết luận
Workflow này chính là "vũ khí bí mật" giúp các marketer, agency và creator tiết kiệm hàng đống thời gian nghiên cứu thị trường. Hãy triển khai ngay lên hệ thống n8n của các sếp để tối ưu hóa quy trình tìm kiếm leads YouTube ngay hôm nay!