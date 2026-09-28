---
title: "🎬 Tự Động Hoà Video AI Với Nền Hình Tạo Bằng Gemini & VideoBGRemover - Không Cần Code!"
description: "Workflow tự động hóa hoàn chỉnh tạo video chuyên nghiệp với nền hình AI sinh tổng hợp từ Gemini và công nghệ VideoBGRemover, lưu kết quả lên Google Drive. Giúp các sếp tiết kiệm thời gian 100% trong sản xuất nội dung marketing, demo sản phẩm hoặc video AI avatar."
slug: "tự-dộng-hoa-video-ai-nen-hinh-gemini-video-bg-remover"
tags: [n8n, automation, ai-image-generation, video-editing, google-drive, gemini-api, videobgremover]
keywords: [tự động hóa video AI, nền hình AI cho video, gemini nano banana, video bg remover n8n, tự động hóa nội dung marketing, tự động hóa demo sản phẩm]
---

# 🚀 **Tự Động Hoà Video AI Với Nền Hình Tạo Bằng Gemini & VideoBGRemover**

## **🔥 Giải Phóng Tay Các Sếp Từ Công Việc Tạo Video Chuyên Nghiệp!**

Hãy tưởng tượng: chỉ với một cú nhấp chuột, các sếp có thể tạo ra những video **chuyên nghiệp, cá nhân hóa** với nền hình **AI sinh tổng hợp** từ những mô tả văn bản, mà không cần phải cài phần mềm, chỉnh sửa thủ công hay tìm kiếm hình ảnh phù hợp. Đây chính là **công cụ tự động hóa video AI** mà workflow này mang lại!

Thay vì mất **giờ đồng hồ** để tìm kiếm, chỉnh sửa và ghép nền hình cho video, các sếp chỉ cần cung cấp:
✅ **URL video** (AI avatar, demo sản phẩm, video marketing...)
✅ **Mô tả nền hình** (ví dụ: *"Căn phòng văn phòng hiện đại với ánh sáng tự nhiên và cảnh nhìn thành phố"*)
✅ **Tỉ lệ khung hình** (16:9, 1:1, 9:16...)

Workflow sẽ tự động:
✔ **Tạo nền hình AI** từ mô tả bằng **Gemini Nano Banana** (mô hình sinh ảnh tiên tiến của Google).
✔ **Xóa nền video gốc** bằng công nghệ **VideoBGRemover** (AI phân tích và loại bỏ nền hiệu quả).
✔ **Ghép video vào nền hình mới** với khung hình chuyên nghiệp.
✔ **Lưu kết quả lên Google Drive** với liên kết chia sẻ trực tiếp.

**Kết quả?** Video **chuyên nghiệp, độc đáo và hoàn toàn tự động hóa** – chỉ trong **2-4 phút**!

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm thời gian**: Không cần tìm kiếm, chỉnh sửa hình ảnh thủ công.
- **Nền hình cá nhân hóa**: Tạo video với **bối cảnh độc đáo** phù hợp với thương hiệu.
- **Chất lượng chuyên nghiệp**: Video có **khung hình cân đối, nền hình mượt mà**.
- **Hoạt động 24/7**: Chạy tự động qua **webhook** hoặc **manual trigger**.
- **Lưu trữ an toàn**: Kết quả được **lưu trên Google Drive** với liên kết chia sẻ.
- **Dễ dàng mở rộng**: Kết hợp với **Slack, Telegram, hoặc Google Sheets** để tự động hóa batch.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI BẮT ĐẦU**]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Google Drive** (để lưu video kết quả).
2. **API Key Gemini** (dùng để sinh ảnh AI).
3. **API Key VideoBGRemover** (dùng để xóa nền và ghép video).
4. **URL video công khai** (các sếp có thể upload lên YouTube hoặc Google Drive và chia sẻ liên kết công khai).
5. **Mô tả nền hình chi tiết** (càng cụ thể, nền hình càng chân thực).

👉 **Lưu ý:** Video phải là **liên kết công khai** (public URL) để VideoBGRemover có thể xử lý.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n.io](https://n8n.io/) và đăng nhập vào tài khoản.
2. Nhấp vào **"Import"** và chọn file JSON (hoặc paste JSON từ [link gốc](https://n8n.io/workflows/9821)).
3. Chọn **"Import"** để tải workflow vào hệ thống.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này có **22 node**, nhưng các node quan trọng nhất cần cấu hình kỹ là:

##### **🔑 Cấu Hình API Keys (BẮT BUỘC)**
Workflow sử dụng **hai API key** để hoạt động:
- **Gemini API Key** (dùng để sinh ảnh AI).
- **VideoBGRemover API Key** (dùng để xóa nền và ghép video).

**Cách thiết lập:**
1. Truy cập **Settings → Variables** trong n8n.
2. Thêm hai biến mới:
   - **Tên:** `GEMINI_KEY`
     **Giá trị:** API Key từ [Google AI Studio](https://aistudio.google.com/apikey).
   - **Tên:** `VIDEOBGREMOVER_KEY`
     **Giá trị:** API Key từ [VideoBGRemover](https://videobgremover.com/api-management).

⚠️ **Lưu ý:** Đảm bảo **không chia sẻ API Key** với ai!

##### **📥 Cấu Hình Google Drive**
Workflow sẽ **lưu video kết quả lên Google Drive**:
1. Trong node **"2. Save Background Image to Drive"**, nhấp **"Connect"** và đăng nhập tài khoản Google.
2. Chọn **folder lưu trữ** (có thể là **My Drive** hoặc folder tùy chỉnh).

##### **📝 Cấu Hình Inputs (Dữ liệu đầu vào)**
Workflow hỗ trợ **hai cách kích hoạt**:
- **Manual Trigger** (test thủ công).
- **Webhook Trigger** (tự động hóa qua API).

**Cách cấu hình:**
1. **Manual Trigger:**
   - Mở node **"Sample Inputs (Edit Here)"** và điền:
     - `video_url`: Liên kết video công khai (ví dụ: YouTube hoặc Google Drive).
     - `background_prompt`: Mô tả nền hình (ví dụ: *"Căn phòng văn phòng hiện đại với ánh sáng tự nhiên"*).
     - `aspect_ratio`: Tỉ lệ khung hình (ví dụ: `16:9`).
   - Nhấp **"Execute Workflow"** để chạy.

2. **Webhook Trigger:**
   - Mở node **"Webhook Trigger"** và sao chép **URL webhook**.
   - Gửi **POST request** với dữ liệu JSON:
     ```json
     {
       "video_url": "https://example.com/video.mp4",
       "background_prompt": "A modern office with city skyline at golden hour",
       "aspect_ratio": "16:9"
     }
     ```
   - Workflow sẽ tự động xử lý và trả về kết quả.

##### **🔄 Cấu Hình Node "Is Complete?" và "Has Failed?"**
- Node **"Is Complete?"** (kiểu `if`) kiểm tra xem video đã xử lý xong chưa.
- Node **"Has Failed?"** (kiểu `if`) xử lý trường hợp lỗi (ví dụ: video không tải được).
- **Không cần chỉnh sửa** nếu các sếp đã điền đúng API Key và URL video.

##### **⏳ Cấu Hình Node "Wait 20s"**
- Node này **đợi 20 giây** giữa các bước xử lý để tránh quá tải API.
- **Không cần chỉnh sửa** (n8n sẽ tự động điều chỉnh).

---

#### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** (để kiểm tra lỗi):
   - Chạy workflow với **manual trigger** và kiểm tra kết quả trên Google Drive.
2. **Bật Active**:
   - Nhấp vào **toggle "Active"** ở góc trên bên phải của canvas.
   - Nếu dùng **webhook**, đảm bảo **URL webhook** được bảo mật.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[**CÁCH DÙNG HIỆU QUẢ HƠN**]
1. **Tự động hóa qua Google Sheets/Airtable:**
   - Kết nối với **Google Sheets** để **batch processing** (xử lý nhiều video cùng lúc).
   - Ví dụ: Tạo một sheet với cột `video_url`, `background_prompt`, `aspect_ratio`, rồi kết nối với workflow.

2. **Gửi kết quả qua Slack/Telegram:**
   - Sử dụng **node Slack** hoặc **Telegram Bot** để thông báo khi video hoàn thành.
   - Ví dụ: Khi video xong, gửi tin nhắn: *"Video đã hoàn thành! Link: [Google Drive Link]"*.

3. **Lưu log xử lý:**
   - Thêm **node "Set"** sau node **"8. Upload Video to Drive"** để lưu **metadata** (tên video, thời gian xử lý, trạng thái).
   - Có thể kết nối với **Google Sheets** để theo dõi lịch sử.

4. **Tối ưu chi phí:**
   - Gemini có **giá $0.03/ảnh**, VideoBGRemover **$0.50-$2.00/phút video**.
   - Nếu xử lý nhiều video, **lựa chọn video ngắn** (dưới 30 giây) để tiết kiệm chi phí.

5. **Tạo template nền hình:**
   - Sử dụng **mô tả nền hình tiêu chuẩn** (ví dụ: *"Căn phòng văn phòng hiện đại"* cho tất cả video).
   - Điều này giúp **tạo ra sự nhất quán** trong branding.
:::

---

### 📌 **Kết Luận: Tự Động Hoà Video AI – Giải Pháp Chuyên Nghiệp Cho Các Sếp!**

Workflow này không chỉ **giúp các sếp tiết kiệm thời gian** mà còn **mang lại video chuyên nghiệp, cá nhân hóa** mà không cần kỹ năng chỉnh sửa. Dù là **marketing, demo sản phẩm, hoặc video AI avatar**, các sếp đều có thể tạo ra nội dung **độc đáo và hiệu quả** chỉ trong **2-4 phút**.

**Hành động ngay!**
1. **Cài đặt n8n trên VPS** (để workflow chạy 24/7).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

2. **Import workflow** và bắt đầu tự động hóa!
3. **Kết nối với Google Drive, Gemini và VideoBGRemover** theo hướng dẫn.

**Chúc các sếp thành công với video AI chuyên nghiệp!** 🚀

---
**📌 Lưu ý cuối cùng:**
- Nếu gặp lỗi, kiểm tra **API Key** và **URL video công khai**.
- Đối với video **dài hơn 30 giây**, chi phí VideoBGRemover sẽ tăng.