---
title: "🎬 Tự Động Hoá Sáng Tạo Video Faceless Siêu Nhanh Với AI: Từ Script Đến Video Chỉ Với 1 Click"
description: "Workflow n8n này tự động tạo video không cần diện mạo (faceless video) từ khái niệm đến video hoàn chỉnh, kết hợp AI Gemini, ElevenLabs, Leonardo AI và Shotstack. Giúp content creator tiết kiệm 100% thời gian chỉnh sửa, tạo video hàng ngày cho YouTube, TikTok, Reels chỉ trong vài phút."
slug: "tay-dong-hoa-tao-video-faceless-voi-ai"
tags: [n8n, automation, content-creation, ai-multimodal, faceless-video, google-gemini, elevenlabs, leonardo-ai, shotstack]
keywords: [tự động hóa video faceless, n8n workflow faceless video, tạo video không cần diện mạo, ai tạo video tự động, script video tự động, voiceover tự động, video editing tự động]
---

# 🚀 **Tự Động Hoá Sáng Tạo Video Faceless Siêu Nhanh Với AI: Từ Khái Niệm Đến Video Chỉ Với 1 Click**

## **💡 Nỗi Đau Của Các Sếp Content Creator**
Hàng ngày, các sếp phải:
- **Tốn thời gian vô cùng** viết script, chọn hình ảnh, ghép video và chỉnh sửa âm thanh.
- **Khó khăn trong việc tạo nội dung đa dạng** vì thiếu thời gian để nghiên cứu và sáng tạo.
- **Phải thuê đội ngũ chuyên nghiệp** để sản xuất video hàng loạt, tăng chi phí đáng kể.
- **Không thể tối ưu hóa quy trình** vì các công cụ hiện tại yêu cầu kỹ năng kỹ thuật cao.

**Workflow này giải quyết tất cả!** Với **AI + n8n**, các sếp có thể:
✅ **Tạo video faceless hoàn chỉnh** chỉ trong **vài phút** (không cần diện mạo).
✅ **Tự động hóa toàn bộ quy trình** từ viết script đến chỉnh sửa video.
✅ **Tạo video hàng loạt** cho YouTube, TikTok, Reels, quảng cáo mà **không cần biên tập viên**.
✅ **Cá nhân hóa nội dung** cho từng video mà không tốn thời gian.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 20-30 giờ/tuần** so với cách làm thủ công.
- **Video chuyên nghiệp** với âm thanh tự động, hình ảnh AI sinh, và chỉnh sửa thông minh.
- **Tăng sản lượng nội dung** lên **5-10x** mà không tăng chi phí.
- **Hoạt động 24/7** trên VPS, tự động tạo video khi có input mới.
- **Không cần kỹ năng kỹ thuật** – chỉ cần copy/paste và chạy workflow.
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản API** của các dịch vụ sau:
   - **Google Gemini API** (để viết script và tạo prompt hình ảnh).
   - **ElevenLabs API** (để tạo voiceover âm thanh).
   - **OpenAI Whisper API** (để chuyển âm thanh thành văn bản).
   - **Leonardo AI API** (để tạo hình ảnh và video từ text).
   - **Shotstack API** (để chỉnh sửa và ghép video cuối cùng).
   - **Google Drive** (để upload và chia sẻ file âm thanh).
2. **VPS n8n** (để chạy workflow 24/7).
3. **Mã giảm giá VPS** (nếu chưa có):
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** của workflow từ [n8n.io/workflows/6014](https://n8n.io/workflows/6014).
- **Nhấn "Import"** trong n8n Editor và chọn file JSON.
- **Hoặc copy/paste** toàn bộ JSON vào ô "Import Workflow" trong n8n.

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **29 node**, nhưng các sếp chỉ cần chú ý đến **các node quan trọng sau**:

#### **🔹 Node "Fields - Set Idea" (Đặt Khái Niệm Video)**
- **Điền nội dung** vào trường `Idea` (ví dụ: *"Cách tối ưu SEO cho blog năm 2024"*).
- **Lưu ý**: Nếu không điền, workflow sẽ không chạy được.

#### **🔹 Node "Google Gemini Chat Model 1 & 2" (Viết Script & Tạo Prompt)**
- **Kết nối API Google Gemini** (đã có trong danh sách credentials).
- **Không cần chỉnh sửa** nếu đã cấu hình đúng.

#### **🔹 Node "ElevenLabs" (Tạo Voiceover)**
- **Kết nối API ElevenLabs** (đã có trong credentials).
- **Chọn voice** phù hợp (ví dụ: *"Ambient Male"*).

#### **🔹 Node "Upload Audio to Drive" & "Make Audio File Public"**
- **Chọn Google Drive OAuth2** (đã cấu hình trước).
- **Chọn folder** để lưu file âm thanh.

#### **🔹 Node "Shotstack" (Chỉnh Sửa Video)**
- **Kết nối API Shotstack** (đã có trong credentials).
- **Chọn template** chỉnh sửa video (nếu có).

#### **🔹 Node "Wait" (Chờ Xử Lý)**
- **Không cần chỉnh sửa** – workflow tự động chờ thời gian xử lý.

---
### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **"Test Workflow"** và kiểm tra từng node.
   - **Kiểm tra file âm thanh** đã upload lên Google Drive.
   - **Kiểm tra video** đã tạo trên Shotstack.
2. **Bật Active** khi đã kiểm tra xong.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**
:::info[CÁCH LÀM TIẾP THEO]
1. **Tự động hóa gửi video đến Slack/Telegram**:
   - Thêm node **Slack/Telegram Webhook** sau node **"Download Final Video"** để thông báo khi video hoàn tất.
2. **Lưu log hoạt động**:
   - Thêm node **Google Sheets** để ghi lại lịch sử tạo video (topic, thời gian, link download).
3. **Tạo video định kỳ**:
   - Sử dụng **n8n Cron Trigger** để chạy workflow hàng ngày/tuần với input mới.
4. **Thay đổi thời lượng video**:
   - Trong node **"60 Second Script Writer"**, chỉnh sửa prompt để tạo video **30s, 1min, 2min...**.
5. **Sử dụng AI khác**:
   - Thay **Google Gemini** bằng **OpenAI ChatGPT** hoặc **Claude** (cần thay đổi node `lmChatGoogleGemini` thành `lmChatOpenAi`).
6. **Tối ưu hóa hình ảnh**:
   - Thay **Leonardo AI** bằng **DALL·E** hoặc **MidJourney** (cần thay đổi node `Generate Images`).
:::

---
## **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **strategy content** thay vì làm thủ công. **Không cần code, không cần biên tập viên** – chỉ cần **1 click**, video faceless hoàn chỉnh sẽ ra đời!

**🚀 Hãy áp dụng ngay và tạo video hàng loạt cho YouTube, TikTok, Reels chỉ trong vài phút!**

---
### **🔗 Tài Liệu Tham Khảo**
- [Workflow gốc trên n8n.io](https://n8n.io/workflows/6014)
- [Agent Circle - Tác giả workflow](https://www.agentcircle.ai/)
- [Hướng dẫn cài n8n Self-hosted](https://docs.n8n.io/hosting/installation/)