---
title: "🎥 Tự Động Hoạt Động Tạo & Đăng Video Affiliate AI với Sora-2, GPT-4 & YouTube (Không Cần Code)"
description: "Workflow tự động hóa 100% sử dụng n8n để tạo video affiliate chất lượng cao từ mô tả sản phẩm, chuyển đổi thành video AI bằng Sora-2, và tự động đăng lên YouTube. Giúp các sếp tiết kiệm 10-15 giờ/ngày trong content marketing."
slug: "tay-dong-hoat-dong-tao-video-affiliate-ai-sora-2-gpt-4-youTube"
tags: [n8n, automation, content-creation, AI-multimodal, YouTube-automation, Sora-2, GPT-4, affiliate-marketing]
keywords: [tự động hóa video affiliate, Sora-2 n8n, tạo video AI tự động, YouTube automation, affiliate marketing tự động, workflow n8n content creation]
---

# 🚀 **Tự Động Hoạt Động Tạo & Đăng Video Affiliate AI với Sora-2, GPT-4 & YouTube**

### **Giải pháp cho các sếp muốn:**
- **Tiết kiệm 10-15 giờ/ngày** trong việc tạo video affiliate thủ công.
- **Tăng hiệu quả marketing** với video AI chất lượng cao, tự động hóa từ mô tả sản phẩm đến đăng tải trên YouTube.
- **Cá nhân hóa nội dung** cho từng sản phẩm affiliate bằng AI.
- **Hoạt động 24/7** mà không cần can thiệp thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động ổn định và không bị gián đoạn, các sếp nên **self-host n8n** trên một VPS ổn định. Dưới đây là 2 lựa chọn uy tín với mã giảm giá dành riêng cho bạn:

👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Dung lượng lớn, tốc độ cao)

*Lưu ý:* N8n cần tối thiểu **4GB RAM** và **2 vCore** để xử lý các node AI (Sora-2, GPT-4) hiệu quả.
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian:** Tự động hóa toàn bộ quy trình từ tìm kiếm sản phẩm đến đăng video lên YouTube.
✅ **Nội dung AI chất lượng cao:** Sử dụng **Sora-2** (AI video) và **GPT-4** để tạo video chuyên nghiệp từ mô tả sản phẩm.
✅ **Tối ưu SEO:** Video được tự động bổ sung **meta data** và **thẻ tag** phù hợp với YouTube.
✅ **Hoạt động liên tục:** Workflow chạy tự động hàng ngày, không cần can thiệp thủ công.
✅ **Cá nhân hóa nội dung:** Mỗi video được tạo riêng cho từng sản phẩm affiliate, tăng tỷ lệ chuyển đổi.
✅ **Báo cáo tự động:** Kết quả được ghi lại trên **Google Sheets**, giúp theo dõi hiệu suất dễ dàng.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
### **1. Tài khoản & API Keys**
| **Dịch vụ**               | **Thông tin cần thiết**                                                                 | **Lưu ý**                                                                 |
|---------------------------|---------------------------------------------------------------------------------------|---------------------------------------------------------------------------|
| **Google Sheets**         | - Tài khoản Google (đăng ký [Google Workspace](https://workspace.google.com/))       | Cần **bảng Google Sheets** để lưu trữ danh sách sản phẩm affiliate.       |
|                           | - **API Key** (nếu sử dụng Google Sheets API)                                         | Nếu không muốn dùng API, chỉ cần chia sẻ bảng với n8n.                     |
| **OpenAI (GPT-4 & Sora-2)** | - **API Key** từ [OpenAI Platform](https://platform.openai.com/)                      | Cần **tài khoản Pro** để sử dụng Sora-2 và GPT-4.                          |
| **YouTube**              | - **Tài khoản YouTube** (đăng ký [YouTube Studio](https://studio.youtube.com/))       | Cần **tài khoản Business** để tự động upload video.                       |
|                           | - **OAuth 2.0 Client ID & Secret** (tạo từ [Google Cloud Console](https://console.cloud.google.com/)) | Dùng để xác thực API YouTube.                                           |
| **Telegram (optional)**   | - **Token Bot** từ [@BotFather](https://t.me/BotFather)                               | Dùng để nhận thông báo lỗi hoặc tiến trình từ workflow.                   |

### **2. Bảng Google Sheets chuẩn bị**
Các sếp cần tạo **1 bảng Google Sheets** với cấu trúc sau (tên cột chính):
- `Product Name` (Tên sản phẩm)
- `Product URL` (Link sản phẩm)
- `Affiliate Link` (Link affiliate)
- `Status` (Trạng thái: "Active" hoặc "Inactive")
- `Published` (Trạng thái: "No" hoặc "Yes")
- `Video URL` (Link video sau khi tạo, nếu có)

*Ví dụ:*
| Product Name | Product URL                          | Affiliate Link                     | Status   | Published | Video URL          |
|--------------|---------------------------------------|------------------------------------|----------|-----------|--------------------|
| iPhone 15 Pro | https://example.com/iphone-15-pro    | https://affiliate.com/iphone-15-pro | Active   | No        | -                  |

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [link gốc](https://n8n.io/workflows/10372) (chọn **Download JSON**).
2. **Mở n8n Editor** (trên trang web hoặc self-hosted).
3. Nhấn **Import** → Chọn file JSON vừa tải → Nhấn **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Mở n8n Editor**.
2. Nhấn **Import** → Chọn **Paste JSON** → Dán nội dung JSON từ file.
3. Nhấn **Import**.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này **không hoạt động ngay** sau khi import. Các sếp cần cấu hình **các node quan trọng** sau:

#### **A. Cấu hình Schedule Trigger**
- Node: **"Schedule Trigger"**
- **Cài đặt:**
  - **Frequency:** Chọn **"Daily"** (hoặc **"Weekly"** nếu muốn chạy tuần 1 lần).
  - **Time:** Chọn giờ phù hợp (ví dụ: **6h sáng** để tránh thời gian cao điểm).
  - **Time Zone:** Chọn **Asia/Ho Chi Minh** (hoặc khu vực của bạn).

#### **B. Cấu hình Google Sheets**
- Node: **"Get row(s) in sheet"**, **"Update row in sheet"**
- **Cài đặt:**
  - **Credentials:** Chọn **Google Sheets** (đã cấu hình trước).
  - **Sheet Name:** Nhập tên **bảng Google Sheets** bạn đã tạo.
  - **Range:** Nhập **A1:F1000** (hoặc phạm vi phù hợp).
  - **Filter:** Chỉ lấy dòng có **Status = "Active"** và **Published = "No"**.

#### **C. Cấu hình OpenAI (GPT-4 & Sora-2)**
- Node: **"OpenAI Chat Model1"**, **"OpenAI Chat Model"**, **"Sora2 Prompt Generator"**
- **Cài đặt:**
  - **Credentials:** Chọn **OpenAI** (đã cấu hình API Key).
  - **Model:** Chọn **gpt-4** (hoặc **gpt-4-turbo** nếu có).
  - **API Key:** Điền **API Key OpenAI** của bạn.
  - **Prompt:** Các node này **sử dụng prompt mặc định** từ tác giả. Các sếp có thể **cập nhật** trong node **"Set"** (nếu cần).

#### **D. Cấu hình YouTube**
- Node: **"Upload a video"**, **"Update Youtube Meta Data"**
- **Cài đặt:**
  - **Credentials:** Chọn **YouTube** (đã cấu hình OAuth 2.0).
  - **Channel ID:** Nhập **ID kênh YouTube** của bạn (thường là số sau `https://www.youtube.com/channel/UCxxxxxxxx`).
  - **Default Playlist:** Chọn **playlist** muốn upload video (ví dụ: "Affiliate Videos").
  - **Video Metadata:** Các node này sẽ tự động lấy **tên, mô tả, thẻ tag** từ AI (GPT-4).

#### **E. Cấu hình Telegram (nếu muốn nhận thông báo)**
- Node: **"Send message and wait for response"**
- **Cài đặt:**
  - **Credentials:** Chọn **Telegram** (đã cấu hình Token Bot).
  - **Chat ID:** Nhập **ID chat** của bạn (lấy từ [@userinfobot](https://t.me/userinfobot)).
  - **Message:** Cấu hình nội dung thông báo (ví dụ: `"Video [PRODUCT_NAME] đã tạo thành công!"`).

#### **F. Cấu hình Sora-2 (Text to Video)**
- Node: **"Text to Video2"**, **"Get Video4"**, **"Download Video"**
- **Lưu ý:**
  - **Sora-2 là API mới** của OpenAI, có thể **tạm thời không hoạt động** nếu OpenAI chưa mở rộng API.
  - Nếu gặp lỗi, các sếp có thể **thay thế bằng MidJourney API** (nếu có) hoặc **node HTTP Request** để gọi API video khác.
  - **Tham số quan trọng:**
    - **Prompt:** Node **"Sora2 Prompt Generator"** sẽ tự động tạo prompt từ mô tả sản phẩm.
    - **API Endpoint:** Điền **URL API Sora-2** (nếu có) hoặc **API video khác** (ví dụ: Runway ML).

---
### **3. Kích hoạt ⚡️**
1. **Test Run (Kiểm tra trước khi chạy thực tế):**
   - Chọn **1 dòng sản phẩm** trong Google Sheets (ví dụ: iPhone 15 Pro).
   - Nhấn **Run Workflow** (chọn dòng đó).
   - Kiểm tra **các node** sau:
     - **"Get Product Details"** → Đã lấy thông tin sản phẩm chưa?
     - **"Sora2 Prompt Generator"** → Prompt có hợp lý không?
     - **"Text to Video2"** → Video có tạo thành công không?
     - **"Upload a video"** → Video có upload lên YouTube không?

2. **Bật Active Workflow:**
   - Sau khi test thành công, chuyển **Schedule Trigger** sang **Active**.
   - Workflow sẽ chạy **tự động hàng ngày** theo lịch đã thiết lập.

---

## ✍️ **Mẹo & gợi ý nâng cao**
### **1. Tối ưu Prompt cho Sora-2**
- Nếu video tạo ra **không chất lượng**, các sếp có thể **cập nhật prompt** trong node **"Sora2 Prompt Generator"**.
- **Ví dụ prompt hiệu quả:**
  ```
  "Create a 15-second promotional video for [PRODUCT_NAME].
  Style: Professional, cinematic, high-quality, 4K.
  Showcase key features: [FEATURES].
  Background music: Upbeat, modern.
  Text overlay: Bold, white font, subtitles in Vietnamese.
  Avoid: Blurry images, low resolution, irrelevant objects."
  ```

### **2. Thêm Log & Báo cáo**
- **Node "StickyNote"** (nếu có) được sử dụng để **ghi chú lỗi**.
- Các sếp có thể **thêm node "Set"** sau **"Update row in sheet"** để **ghi log lỗi** vào Google Sheets:
  ```json
  {
    "jsonata": "$['error'] ? { 'Status': 'Error', 'Error Message': $['error'] } : { 'Status': 'Success' }"
  }
  ```

### **3. Kết hợp với Slack/Telegram**
- Thay vì chỉ Telegram, các sếp có thể **thêm node Slack** để nhận thông báo lỗi:
  ```json
  {
    "type": "n8n-nodes-base.slack",
    "name": "Send Slack Alert",
    "options": {
      "webhookUrl": "YOUR_SLACK_WEBHOOK_URL",
      "message": "⚠️ Error in workflow: {{ $json.error }}"
    }
  }
  ```

### **4. Chạy workflow cho nhiều kênh affiliate**
- Nếu các sếp có **nhiều bảng Google Sheets** (ví dụ: Amazon, Shopee, Lazada), có thể:
  - **Tạo nhiều workflow** riêng.
  - **Sử dụng node "Set"** để **lấy dữ liệu từ nhiều bảng** và xử lý song song.

### **5. Tự động chia sẻ video trên Facebook/Instagram**
- Sau khi upload lên YouTube, các sếp có thể **thêm node Facebook/Instagram** để chia sẻ tự động:
  ```json
  {
    "type": "n8n-nodes-base.facebook",
    "name": "Share on Facebook",
    "options": {
      "accessToken": "YOUR_FACEBOOK_ACCESS_TOKEN",
      "message": "🚀 Xem video mới về [PRODUCT_NAME]: {{ $json.videoUrl }}",
      "link": "{{ $json.videoUrl }}"
    }
  }
  ```

---

## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tự động hóa toàn bộ quy trình tạo video affiliate** mà không cần viết code. Với sự kết hợp giữa **Sora-2 (AI video)**, **GPT-4 (AI text)**, và **YouTube Automation**, các sếp có thể:
✔ **Tiết kiệm thời gian** lên đến **15 giờ/ngày**.
✔ **Tăng hiệu quả marketing** với video AI chất lượng cao.
✔ **Hoạt động 24/7** mà không cần can thiệp thủ công.

**Hành động ngay hôm nay:**
1. **Chuẩn bị tài khoản & API Keys** (Google Sheets, OpenAI, YouTube).
2. **Tạo bảng Google Sheets** theo cấu trúc đã hướng dẫn.
3. **Import workflow** và **cấu hình các node quan trọng**.
4. **Test Run** trước khi kích hoạt.
5. **Bật Active** và **nhận video affiliate tự động hàng ngày!**

---
**💡 Mẹo cuối:** Nếu gặp khó khăn trong quá trình cấu hình, các sếp có thể **li