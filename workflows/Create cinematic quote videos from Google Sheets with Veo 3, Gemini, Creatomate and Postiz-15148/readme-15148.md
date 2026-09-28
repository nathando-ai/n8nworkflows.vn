---
title: "🎬 Tự Động Hóa Video Cinematic Từ Google Sheets Với Veo 3 & Gemini"
description: "Biến dữ liệu trong Google Sheets thành video quảng cáo chuyên nghiệp bằng AI Veo 3, render bằng Creatomate và tự động đăng lên TikTok, YouTube, Instagram chỉ với 1 click."
slug: "tu-dong-hoa-video-cinematic-veo-3-gemini"
tags: [n8n, automation, no-code, ai-video, social-media-marketing, veo-3]
keywords: [n8n workflow, tự động hóa video, veo 3, gemini ai, creatomate, postiz]
---

# 🎬 Tự Động Hóa Video Cinematic Từ Google Sheets Với Veo 3 & Gemini

Trong kỷ nguyên của Short-form Video, việc sản xuất nội dung chất lượng cao (Cinematic) thường đòi hỏi đội ngũ quay phim, dựng phim và biên kịch tốn kém. Làm sao để một cá nhân hoặc doanh nghiệp nhỏ có thể tạo ra hàng chục video quảng cáo chuyên nghiệp mỗi ngày mà không cần biết dựng phim?

Workflow này là giải pháp "All-in-One" hoàn hảo. Nó kết hợp sức mạnh của **Google Veo 3** (tạo video AI), **Gemini** (biên kịch & phân tích), **Creatomate** (render video template) và **Postiz** (quản lý mạng xã hội). Các sếp chỉ cần nhập dữ liệu sản phẩm vào Google Sheets, hệ thống sẽ tự động viết kịch bản, tạo video AI, ghép nhạc/đồ họa và đăng tải lên các nền tảng social media một cách hoàn toàn tự động.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, đặc biệt khi xử lý các tác vụ nặng như render video và chờ API AI, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Sản xuất hàng loạt:** Tạo video cinematic chất lượng cao từ dữ liệu thô trong vài phút.
- **Đa nền tảng:** Tự động đăng tải đồng bộ lên YouTube, TikTok và Instagram thông qua Postiz.
- **Cá nhân hóa nội dung:** Gemini AI tự động viết kịch bản và mô tả video dựa trên thông tin sản phẩm cụ thể.
- **Tiết kiệm chi phí:** Loại bỏ nhu cầu thuê đội ngũ quay/dựng phim, chỉ tốn phí API AI và hosting.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị các tài khoản và credentials sau:
1. **Google Account:**
   - Quyền truy cập **Google Sheets** (chứa dữ liệu sản phẩm).
   - Quyền truy cập **Google Cloud Storage** (để lưu trữ video tạm thời).
   - API Key cho **Google Gemini** (dùng cho Agent và Chat Bot).
   - API Key cho **Google Veo 3** (tạo video AI).
2. **Creatomate:**
   - API Key.
   - ID của Template video đã thiết kế sẵn trên Creatomate.
3. **Postiz:**
   - API Key hoặc Token để kết nối.
   - Các nền tảng social media (YouTube, TikTok, Instagram) đã được liên kết trong Postiz.
4. **n8n:**
   - Instance n8n (Cloud hoặc Self-hosted).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.
2. Chọn **Import from URL** và dán link: `https://n8n.io/workflows/15148` HOẶC copy toàn bộ JSON từ file workflow và dán vào editor.
3. Lưu workflow với tên dễ nhớ, ví dụ: `Auto Cinematic Video Generator`.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

Đây là phần quan trọng nhất. Workflow có 25 nodes, nhưng các sếp chỉ cần tập trung cấu hình các điểm mấu chốt sau:

**A. Nguồn dữ liệu & AI Agent**
- **Node `Read from Sheet1`**: 
  - Chọn **Google Sheets credential** của bạn.
  - Chọn đúng **Sheet Name** chứa dữ liệu sản phẩm (cột cần có: Tên sản phẩm, Mô tả, Link hình ảnh, v.v.).
- **Node `Definition AI Agent` & `Gemini Chat Bot`**:
  - Chọn **Google Gemini credential**.
  - Kiểm tra prompt trong node Agent để đảm bảo nó hiểu đúng cấu trúc dữ liệu từ Sheet và yêu cầu Veo 3 tạo video theo phong cách "Cinematic".

**B. Tạo Video AI (Veo 3)**
- **Node `Request Google Token`**: 
  - Đảm bảo đã cấu hình đúng OAuth2 hoặc API Key cho Google Cloud.
- **Node `Initiate Video Generation`**:
  - Đây là node gọi API Veo 3. Kiểm tra tham số `prompt` được truyền từ Agent.
  - **Lưu ý:** Veo 3 có thể mất thời gian xử lý. Workflow đã có node `Wait 20 Seconds` và `Check Video Status` để polling kết quả.

**C. Render Video (Creatomate)**
- **Node `Create HTTP Payload for Creatomate`**:
  - Đây là node Code. Các sếp cần kiểm tra logic tại đây để đảm bảo dữ liệu (video AI, nhạc, text) được map đúng vào các biến của Template Creatomate.
- **Node `Submit Creatomate Render`**:
  - Chọn **Creatomate credential**.
  - Điền **Template ID** của bạn. *Mẹo: Hãy tạo một template mẫu trên Creatomate với các biến động (dynamic fields) như `{{video_url}}`, `{{title}}`, `{{music_url}}`.*
- **Node `Check Render Status` & `Await Render Completion`**:
  - Workflow sẽ tự động chờ cho đến khi Creatomate render xong. Không cần chỉnh gì thêm nếu template không quá phức tạp.

**D. Đăng tải Social Media (Postiz)**
- **Node `Fetch Postiz Integrations`**:
  - Chọn **Postiz credential**.
- **Node `Route by Platform`**:
  - Đây là node Switch. Nó sẽ phân loại video để gửi đến đúng nền tảng (YouTube, TikTok, Instagram).
  - Các sếp có thể chỉnh sửa điều kiện ở đây nếu muốn bỏ qua một nền tảng nào đó.
- **Node `Post to [Platform]`**:
  - Đảm bảo các node này nhận đúng payload từ Postiz.

**E. Lưu trữ & Xử lý file**
- **Node `Upload to Google Cloud`**:
  - Chọn **Google Cloud Storage credential**.
  - Điền đúng **Bucket Name**. Video AI và file render sẽ được lưu tạm tại đây.
- **Node `Convert Data to File`**:
  - Đảm bảo format file (MP4) được giữ nguyên để tương thích với Creatomate và các nền tảng social.

#### 3. Kích hoạt ⚡️
1. **Test Run:** 
   - Nhấn vào node `Manual Trigger` và chọn **Execute Workflow**.
   - Theo dõi từng bước: Đọc Sheet -> Gemini viết kịch bản -> Veo tạo video -> Creatomate render -> Postiz đăng bài.
   - *Lưu ý:* Quá trình này có thể mất 5-15 phút tùy thuộc vào độ phức tạp của video và tốc độ API.
2. **Bật Active:**
   - Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải.
   - *Gợi ý:* Nếu muốn chạy tự động theo lịch, các sếp có thể thay thế `Manual Trigger` bằng `Schedule Trigger` (ví dụ: chạy mỗi sáng 8h).

### ✍️ Mẹo & gợi ý nâng cao

1. **Tối ưu Template Creatomate:** 
   - Đừng chỉ dùng video AI thô. Hãy thiết kế template trên Creatomate với hiệu ứng chuyển cảnh, logo thương hiệu, và nhạc nền bắt tai. Điều này giúp video trông chuyên nghiệp hơn gấp nhiều lần.
2. **A/B Testing Kịch bản:**
   - Sử dụng Gemini để tạo 2-3 biến thể kịch bản khác nhau cho cùng một sản phẩm. Workflow hiện tại chỉ lấy 1 kết quả, các sếp có thể thêm logic để chọn kịch bản tốt nhất hoặc tạo nhiều video.
3. **Tích hợp thêm Telegram/Slack:**
   - Thêm node `Telegram` hoặc `Slack` sau bước `Download Final Video` để gửi thông báo cho team khi video đã sẵn sàng, kèm link xem trước.
4. **Lưu Log vào Google Sheets:**
   - Thêm node `Google Sheets` ở cuối workflow để ghi lại: Thời gian tạo, Link video, Nền tảng đã đăng, và Trạng thái. Điều này giúp các sếp dễ dàng theo dõi hiệu suất nội dung.

### 📌 Kết luận

Workflow này là một "vũ khí" cực mạnh cho các sếp làm Content Marketing. Thay vì tốn hàng giờ để quay và dựng video, các sếp chỉ cần nhập dữ liệu và để AI lo phần còn lại. Với sự kết hợp của Veo 3, Gemini và Creatomate, chất lượng video sẽ không thua kém gì các agency chuyên nghiệp.

Hãy bắt đầu ngay hôm nay để chiếm lĩnh thị trường Short-form Video! 🚀