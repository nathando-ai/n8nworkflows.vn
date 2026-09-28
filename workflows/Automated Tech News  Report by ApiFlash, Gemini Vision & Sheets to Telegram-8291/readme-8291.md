---
title: "🚀 Tự Động Hóa Báo Cáo Tin Tech Hàng Ngày Từ APIFlash, Gemini Vision & Sheets Sang Telegram (N8n)"
description: "Workflow tự động hóa thu thập, phân tích tin tức công nghệ hàng ngày từ APIFlash, sử dụng Gemini Vision để tóm tắt và gửi báo cáo định kỳ qua Telegram. Giúp các sếp tiết kiệm thời gian theo dõi xu hướng thị trường, đồng thời cá nhân hóa thông tin theo nhu cầu."
slug: "tieu-dong-hoa-bao-cao-tin-tech-hang-ngay"
tags: [n8n, automation, no-code, ai-multimodal, google-sheets, telegram-bot, gemini-ai]
keywords: [n8n workflow tự động hóa, báo cáo tin tức công nghệ, Gemini Vision, APIFlash, Telegram bot, tự động hóa market research]
---

# 🚀 **Tự Động Hóa Báo Cáo Tin Tech Hàng Ngày Từ APIFlash, Gemini Vision & Sheets Sang Telegram**

### **Giải pháp cho các sếp muốn theo dõi xu hướng công nghệ mà không tốn thời gian thủ công**
Hàng ngày, các sếp phải mất nhiều giờ để tra cứu, đọc và tổng hợp tin tức công nghệ từ nhiều nguồn khác nhau để đưa ra quyết định kinh doanh. Workflow này **tự động hóa toàn bộ quy trình** bằng cách:
- **Thu thập tin tức** từ APIFlash (nguồn tin tức công nghệ uy tín).
- **Phân tích hình ảnh và nội dung** bằng Gemini Vision (AI multimodal của Google).
- **Tóm tắt và gửi báo cáo** định kỳ qua Telegram, giúp các sếp **nhận thông tin cập nhật nhanh chóng** mà không cần mở nhiều tab hoặc ứng dụng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần thủ công tra cứu tin tức hàng ngày.
- **Tóm tắt thông tin chi tiết**: Gemini Vision phân tích hình ảnh và nội dung, đưa ra báo cáo ngắn gọn.
- **Cá nhân hóa thông tin**: Gửi báo cáo qua Telegram với định dạng dễ đọc.
- **Hoạt động liên tục**: Workflow chạy tự động theo lịch trình đã thiết lập.
- **Dữ liệu lưu trữ**: Tất cả báo cáo được ghi vào Google Sheets để theo dõi lịch sử.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản APIFlash** (để thu thập tin tức công nghệ).
2. **API Key của Google Sheets** (để đọc và ghi dữ liệu).
3. **Bot Telegram** (để gửi báo cáo tự động).
4. **API Key của Google Gemini** (để phân tích hình ảnh và văn bản).
5. **Google Sheet** (để lưu trữ lịch sử báo cáo).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/8291](https://n8n.io/workflows/8291) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ link trên và dán vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **15 node**, các bước quan trọng cần chú ý:

##### **A. Cấu hình Schedule Trigger (Định thời gian chạy)**
- Node **Schedule Trigger** sẽ kích hoạt workflow theo lịch trình (ví dụ: hàng ngày lúc 8h sáng).
- **Cấu hình**:
  - Chọn **Cron expression** phù hợp (ví dụ: `0 8 * * *` để chạy lúc 8h hàng ngày).
  - **Active**: Bật để workflow chạy tự động.

##### **B. Cấu hình HTTP Request (Thu thập tin tức từ APIFlash)**
- Node **HTTP Request** gọi API của APIFlash để lấy tin tức công nghệ mới nhất.
- **Cấu hình**:
  - **Method**: `GET`
  - **URL**: `https://apiflash.com/documents/tech-news` (hoặc URL API khác của APIFlash).
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer YOUR_APIFLASH_API_KEY"
    }
    ```
  - **Response Format**: Chọn `JSON`.

##### **Cấu hình Google Sheets (Đọc và ghi dữ liệu)**
- **Node "Read entire Sheet"**:
  - **Google Sheets Credentials**: Chọn tài khoản đã kết nối với Google Sheets.
  - **Sheet Name**: Tên sheet chứa dữ liệu (ví dụ: `TechNewsReport`).
  - **Range**: `A1:Z1000` (để đọc toàn bộ sheet).
- **Node "Append row in sheet"**:
  - **Sheet Name**: Tên sheet để ghi dữ liệu mới.
  - **Range**: `A1` (để thêm hàng mới).

##### **C. Cấu hình Gemini Vision (Phân tích hình ảnh và văn bản)**
- **Node "Analyze image"**:
  - **Model**: Chọn `gemini-pro-vision`.
  - **Prompt**: Cung cấp câu hỏi phân tích (ví dụ: *"Tóm tắt tin tức này và cho biết điểm nổi bật"*).
  - **Image URL**: Lấy từ tin tức thu thập được.
- **Node "AI Trend Report"**:
  - **Model**: Chọn `gemini-pro`.
  - **Prompt**: Cấu hình để tóm tắt báo cáo (ví dụ: *"Tóm tắt tin tức công nghệ trong ngày và đưa ra xu hướng thị trường"*).

##### **D. Cấu hình Telegram (Gửi báo cáo)**
- **Node "Send a photo message"**:
  - **Telegram Credentials**: Chọn bot Telegram đã kết nối.
  - **Chat ID**: ID chat của cá nhân hoặc nhóm.
  - **Photo URL**: Lấy từ kết quả phân tích của Gemini Vision.
- **Node "Send a text message"**:
  - **Text**: Dùng kết quả từ Gemini Vision để tạo nội dung báo cáo.

##### **E. Các node khác cần chú ý**
- **Node "Filter"**: Lọc tin tức theo tiêu chí (ví dụ: chỉ lấy tin tức mới nhất).
- **Node "Aggregate"**: Kết hợp dữ liệu từ nhiều nguồn.
- **Node "Code"**: Sử dụng JavaScript để xử lý logic phức tạp (nếu cần).

#### **3. Kích hoạt ⚡️**
- **Test Run**: Chạy workflow với dữ liệu mẫu để kiểm tra kết quả.
- **Active Workflow**: Sau khi kiểm tra thành công, bật **Active** để workflow chạy tự động.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tùy chỉnh lịch trình**: Thay đổi **Schedule Trigger** để chạy workflow vào giờ phù hợp (ví dụ: sáng sớm).
2. **Lưu log**: Sử dụng **Google Sheets** để lưu trữ tất cả báo cáo, giúp theo dõi xu hướng dài hạn.
3. **Kết hợp với Slack**: Thay vì Telegram, các sếp có thể gửi báo cáo qua Slack bằng node **Slack**.
4. **Cập nhật API Key**: Đảm bảo **API Key của APIFlash và Google Gemini** không hết hạn.
5. **Tự động cảnh báo**: Sử dụng **If-Then** để gửi thông báo nếu có tin tức quan trọng (ví dụ: ra mắt sản phẩm mới).

---

### 📌 **Kết luận**
Workflow này **giúp các sếp tự động hóa việc theo dõi tin tức công nghệ**, tiết kiệm thời gian và nhận thông tin cập nhật nhanh chóng. **Chỉ cần import, cấu hình và bật Active**, workflow sẽ hoạt động 24/7 mà không cần can thiệp thủ công.

🚀 **Hãy áp dụng ngay và bắt đầu theo dõi xu hướng công nghệ một cách thông minh!**