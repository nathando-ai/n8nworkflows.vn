---
title: "🍽️ Tự Động Hóa Chia Sẻ Ảnh Ăn Uống Đạt Điểm Cao lên Pinterest Với AI GPT-3.5 + Google Sheets"
description: "Workflow tự động hóa chia sẻ ảnh ẩm thực cao điểm từ Google Sheets lên Pinterest với caption AI, tiết kiệm thời gian và tối ưu hóa nội dung hàng ngày. Khắc phục vấn đề phải làm thủ công, mất thời gian và không đảm bảo tính nhất quán."
slug: "tu-dong-hoa-chia-se-anh-am-thuc-len-pinterest"
tags: [n8n, automation, social-media, ai-gpt, google-sheets, pinterest]
keywords: [tự động hóa pinterest, chia sẻ ảnh ẩm thực tự động, ai viết caption, google sheets + pinterest, workflow n8n social media]
---

# 🚀 **Tự Động Hóa Chia Sẻ Ảnh Ăn Uống Đạt Điểm Cao lên Pinterest Với AI GPT-3.5 + Google Sheets**

### **🔥 Nỗi Đau Của Các Sếp Và Giải Pháp Tự Động Hóa**
Các sếp quản lý tài khoản **ẩm thực** hay **ẩm thực du lịch** thường phải:
- **Làm thủ công** mỗi ngày để chọn ảnh ẩm thực có điểm cao từ Google Sheets.
- **Viết caption** một cách nhất quán, nhưng thường bị mất thời gian và không đảm bảo tính hấp dẫn.
- **Chia sẻ lên Pinterest** một cách rời rạc, không có lịch trình tự động.
- **Quên cập nhật trạng thái** sau khi đã chia sẻ, dẫn đến trùng lặp nội dung.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Lấy ảnh ẩm thực** từ Google Sheets với điểm ≥ 4 sao và chưa được chia sẻ.
✅ **Sử dụng AI GPT-3.5** để tạo **caption hấp dẫn** dưới 100 ký tự, phù hợp với Pinterest.
✅ **Chia sẻ lên Pinterest** một cách tự động qua API.
✅ **Cập nhật trạng thái** trong Google Sheets để tránh trùng lặp.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần chọn ảnh, viết caption hoặc chia sẻ thủ công hàng ngày.
- **Nội dung chuyên nghiệp**: Caption AI được tối ưu hóa cho Pinterest, tăng tương tác.
- **Tự động hóa hoàn toàn**: Workflow chạy theo lịch trình, không phụ thuộc vào thời gian làm việc.
- **Tránh trùng lặp**: Cập nhật trạng thái trong Google Sheets để không chia sẻ lại ảnh cũ.
- **Tăng độ phủ**: Chia sẻ ảnh ẩm thực hàng ngày, tăng cơ hội thu hút khách hàng.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets**:
   - Một **Google Sheet** chứa dữ liệu ảnh ẩm thực với các cột:
     - `Image URL` (đường dẫn ảnh)
     - `Feedback` (đánh giá khách hàng)
     - `Rating` (điểm số, ví dụ: 4.5 sao)
     - `Posted` (trạng thái: `false` nếu chưa chia sẻ, `true` nếu đã chia sẻ).
   - **API Key Google Sheets**: Tạo tại [Google Cloud Console](https://console.cloud.google.com/).
2. **Tài khoản OpenAI**:
   - **API Key OpenAI**: Tạo tại [OpenAI Platform](https://platform.openai.com/).
3. **Tài khoản Pinterest**:
   - **API Key Pinterest**: Tạo tại [Pinterest Developer Portal](https://developers.pinterest.com/).
   - **Header Auth** (nếu sử dụng API Business).
4. **n8n Self-hosted**:
   - Cài đặt n8n trên VPS (khuyến nghị dùng [TinoHost](https://tino.vn/) hoặc [BNIX](https://my.bnix.one/)).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/5989](https://n8n.io/workflows/5989).
- **Import vào n8n Editor**:
  - Mở n8n Dashboard → **Create Workflow** → **Import from JSON**.
  - Chọn file và nhấn **Import**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **6 node chính**, các sếp cần cấu hình kỹ lưỡng như sau:

##### **🔹 Node 1: Daily Post Scheduler (scheduleTrigger)**
- **Cấu hình**:
  - **Schedule**: Chọn `Daily` và thời gian phù hợp (ví dụ: 8h sáng).
  - **Time Zone**: Đặt theo múi giờ của doanh nghiệp.
- **Lưu ý**: Workflow sẽ chạy tự động theo lịch trình đã thiết lập.

##### **🔹 Node 2: Fetch Food Photos from Sheet (googleSheets)**
- **Cấu hình**:
  - **Credentials**: Chọn `googleApi` (đã tạo trước).
  - **Spreadsheet ID**: Tìm trong URL của Google Sheet (ví dụ: `https://docs.google.com/spreadsheets/d/SPREADSHEET_ID/edit`).
  - **Range**: Đặt là `Sheet1!A:Z` (hoặc tên sheet cụ thể).
  - **Operation**: Đặt là `get`.
- **Lưu ý**: Đảm bảo sheet có cột `Rating` và `Posted` để workflow lọc được.

##### **🔹 Node 3: Filter 4+ Star Dishes (if)**
- **Cấu hình**:
  - **Condition**: Kiểm tra `$.Rating >= 4` **và** `$.Posted === false`.
  - **Output**: Chỉ giữ lại các dòng đáp ứng điều kiện.
- **Lưu ý**: Nếu không có dữ liệu đáp ứng, workflow sẽ không tiếp tục.

##### **🔹 Node 4: AI Caption Generator (openAi)**
- **Cấu hình**:
  - **Credentials**: Chọn `openAiApi`.
  - **Model**: Đặt là `gpt-3.5-turbo`.
  - **Prompt**:
    ```plaintext
    Generate a concise, engaging Pinterest caption for a food photo based on this customer feedback: '{{$node['Google Sheets'].json['Feedback']}}'. Keep it under 100 characters and include a positive tone.
    ```
  - **Max Tokens**: Đặt là `100` (để caption ngắn gọn).
- **Lưu ý**:
  - Đảm bảo cột `Feedback` trong Google Sheet có dữ liệu.
  - Nếu OpenAI trả về caption quá dài, điều chỉnh prompt để ngắn hơn.

##### **🔹 Node 5: Upload to Pinterest (httpRequest)**
- **Cấu hình**:
  - **Credentials**: Chọn `httpHeaderAuth` (nếu sử dụng API Business).
  - **Method**: `POST`.
  - **URL**: API endpoint của Pinterest (ví dụ: `https://api.pinterest.com/v5/business/boards/{board-id}/pins`).
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer YOUR_PINTEREST_API_KEY",
      "Content-Type": "application/json"
    }
    ```
  - **Body**:
    ```json
    {
      "image_url": "{{$node['Fetch Food Photos from Sheet'].json['Image URL']}}",
      "description": "{{$node['AI Caption Generator'].json['choices'][0].text}}"
    }
    ```
- **Lưu ý**:
  - Thay thế `YOUR_PINTEREST_API_KEY` bằng API Key thực tế.
  - Kiểm tra `board-id` của board Pinterest bạn muốn chia sẻ.

##### **🔹 Node 6: Mark as Posted in Sheet (googleSheets)**
- **Cấu hình**:
  - **Credentials**: Chọn `googleApi`.
  - **Spreadsheet ID**: Giống Node 2.
  - **Range**: Đặt là `Sheet1!A:Z` (hoặc tên sheet).
  - **Operation**: `update`.
  - **Values**: Cập nhật cột `Posted` thành `true` cho các dòng đã chia sẻ.
- **Lưu ý**: Đảm bảo cột `Posted` có kiểu dữ liệu là `BOOLEAN`.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Execute Workflow** để kiểm tra dữ liệu mẫu.
   - Kiểm tra:
     - AI có tạo caption không?
     - Ảnh có được chia sẻ lên Pinterest không?
     - Trạng thái `Posted` có được cập nhật không?
2. **Bật Active**:
   - Sau khi test thành công, nhấn **Active** để workflow chạy tự động theo lịch trình.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram` để thông báo khi chia sẻ thành công.
   - Ví dụ: Gửi tin nhắn `"📸 Ảnh [Dish Name] đã được chia sẻ lên Pinterest!"`.

2. **Lưu Log Dữ Liệu**:
   - Thêm node `n8n-nodes-base.set` hoặc `n8n-nodes-base.chronicle` để lưu lịch sử chia sẻ.
   - Giúp theo dõi hiệu suất và phân tích hiệu quả.

3. **Báo Cáo Định Kỳ**:
   - Sử dụng node `n8n-nodes-base.googleSheets` để tạo báo cáo thống kê (ví dụ: số ảnh chia sẻ/tháng).
   - Gửi báo cáo qua email tự động bằng node `n8n-nodes-base.email`.

4. **Tối Ưu Hóa Caption**:
   - Thử nghiệm các prompt khác nhau trong node `openAi` để caption phù hợp hơn với brand.
   - Ví dụ: Thêm từ khóa như `#FoodieVietnam` hoặc `#AmThucDuLich`.

5. **Xử Lý Lỗi**:
   - Thêm node `n8n-nodes-base.error` để bắt lỗi và gửi thông báo khi workflow thất bại.
   - Ví dụ: Nếu OpenAI trả về lỗi, gửi email cảnh báo.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp quản lý nội dung ẩm thực, đồng thời **tăng cường hiệu quả chia sẻ** trên Pinterest với caption AI chuyên nghiệp. **Không cần code**, chỉ cần cấu hình và chạy tự động hàng ngày!

**Hành động ngay**:
1. **Chuẩn bị Google Sheet** và API keys.
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Bật Active** và để AI làm việc cho bạn!

👉 **Bạn có thể tùy chỉnh workflow này để phù hợp với nhiều loại nội dung khác** như chia sẻ ảnh du lịch, sản phẩm, hoặc nội dung cá nhân. **Hãy thử ngay và chia sẻ kết quả với chúng tôi!** 🚀

---