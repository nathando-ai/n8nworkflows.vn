---
title: "🌿 Tự Động Hóa Video AI Tự Nhiên 10s với Sora 2 (Kie AI) + Gemini → Gửi Telegram (N8n)"
description: "Workflow tự động hóa hoàn toàn không code để tạo video tự nhiên 10 giây chất lượng cao từ AI, tự động gửi qua Telegram hàng ngày. Giúp content creator, marketing và giáo dục tiết kiệm 80% thời gian sản xuất video."
slug: "tieu-dong-hoa-video-ai-tu-nhien-10s-kie-ai-gemini-telegram"
tags: [n8n, automation, ai-content-creation, multimodal-ai, telegram-bot, kie-ai, google-gemini]
keywords: [n8n workflow tự động hóa video AI, tạo video tự nhiên với Sora 2, tự động hóa content marketing, AI video generator Telegram, Gemini + Kie AI, tự động hóa sản xuất video không code]
---

# 🚀 **Tự Động Hóa Video AI Tự Nhiên 10s → Gửi Telegram (N8n)**

## **📌 Nỗi Đau Của Các Sếp Và Giải Pháp N8n**
Hiện nay, việc sản xuất video chất lượng cao cho **Instagram Reels, TikTok, YouTube Shorts** hay **bài giảng giáo dục** thường tốn thời gian và chi phí cao. Các sếp phải:
- **Tốn nhiều thời gian** để quay, chỉnh sửa và tạo video từ đầu.
- **Không có sự đa dạng** trong nội dung, dễ bị lặp lại.
- **Phụ thuộc vào kỹ năng** của nhân viên chỉnh sửa.
- **Không thể tự động hóa** quá trình tạo video theo lịch trình.

**Workflow này giải quyết tất cả!** Sử dụng **Google Gemini** để tạo **prompt chi tiết**, **Kie AI (Sora 2)** để sinh video 10s tự nhiên, và **Telegram** để tự động gửi video hàng ngày **không cần can thiệp thủ công**.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 80% thời gian** sản xuất video hàng ngày.
✅ **Video chất lượng cao** với phong cách tự nhiên, đa dạng chủ đề.
✅ **Hoạt động tự động 24/7** theo lịch trình (daily, weekly).
✅ **Gửi video trực tiếp** qua Telegram (cá nhân hoặc nhóm).
✅ **Không cần kỹ năng code** – chỉ cần cấu hình API.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
**1. Tài Khoản & API Keys:**
- **Google Gemini API** (để tạo prompt video).
- **Kie AI API** (để sinh video Sora 2).
- **Telegram Bot Token** (để gửi video).
- **Chat ID Telegram** (cá nhân hoặc nhóm).

**2. Hệ Thống:**
- **n8n Self-hosted** (trên VPS) để workflow hoạt động 24/7.
- **Ngrok** (nếu test trên máy local).

**3. Node Cần Bật:**
- `n8n-nodes-base.wait` (đợi video hoàn thành).
- `@n8n/n8n-nodes-langchain.chainLlm` (Gemini).
- `@n8n/n8n-nodes-langchain.lmChatGoogleGemini` (API Gemini).
- `n8n-nodes-base.telegram` (gửi video Telegram).
:::

---

## **🚀 Cách Import & Cấu Hình Workflow**

### **1. Import Workflow 📥**
- **Tải JSON** từ [link gốc](https://n8n.io/workflows/10371) hoặc copy/paste JSON vào **n8n Editor**.
- **Nhấn "Import"** để thêm workflow vào hệ thống.

### **2. Các Bước Cấu Hình BẮT BUỘC**
#### **🔹 1. Cấu Hình Google Gemini (Prompt Video)**
- **Node:** `Gemini Prompt Model` (type: `lmChatGoogleGemini`).
- **Tham số cần thiết:**
  - **Credentials:** Chọn `googlePalmApi` (đã cấu hình trước).
  - **Model:** Chọn `gemini-1.5-flash` (hoặc `pro`).
  - **Prompt Template:**
    ```plaintext
    Tạo một prompt chi tiết cho video 10s tự nhiên với chủ đề: {theme}.
    Cấu trúc:
    - Mô tả cảnh: {description}
    - Phong cách: {style} (chất lượng 4K, tự nhiên, không CGI)
    - Kỹ thuật quay: {camera_tech} (phong cảnh rộng, zoom tự nhiên)
    - Âm nhạc: {music} (âm thanh tự nhiên, không nhạc nền)
    ```
  - **Example Input:**
    ```json
    {
      "theme": "rừng mây buổi sáng",
      "description": "Cây tre xanh mướt giữa sương mù, ánh nắng chiếu qua lá",
      "style": "chất lượng 4K, tự nhiên, không CGI",
      "camera_tech": "phong cảnh rộng, zoom tự nhiên từ xa đến gần",
      "music": "âm thanh chim hót, gió thổi qua lá"
    }
    ```

#### **🔹 2. Cấu Hình Kie AI API (Sinh Video)**
- **Node:** `Submit Video Generation` (type: `httpRequest`).
- **Tham số cần thiết:**
  - **Credentials:** Chọn `httpHeaderAuth` (đã cấu hình `Authorization: Bearer {API_KEY}`).
  - **URL:** `https://kie.ai/api/v1/video` (hoặc URL chính thức của Kie AI).
  - **Headers:**
    ```json
    {
      "Content-Type": "application/json",
      "Authorization": "Bearer {API_KEY}"
    }
    ```
  - **Body (JSON):**
    ```json
    {
      "prompt": "${{ $json["prompt"] }}", // Dữ liệu từ node Gemini
      "aspect_ratio": "portrait",
      "frames": 10,
      "model": "sora-2-text-to-video"
    }
    ```

#### **🔹 3. Cấu Hình Telegram (Gửi Video)**
- **Node:** `Deliver Video to Telegram` (type: `telegram`).
- **Tham số cần thiết:**
  - **Credentials:** Chọn `telegramApi` (đã cấu hình `bot token`).
  - **Chat ID:** Điền **ID chat Telegram** (cá nhân hoặc nhóm).
    - **Lấy Chat ID:**
      - Gửi tin nhắn cho bot: `/get_id`.
      - Bot trả về ID (vd: `-100123456789`).
  - **File Video:** Chọn `${{ $node["Download Generated Video"].json }}` (từ node tải video).

#### **🔹 4. Cấu Hình Lịch Trình (Schedule Trigger)**
- **Node:** `Schedule Trigger` (type: `scheduleTrigger`).
- **Tham số cần thiết:**
  - **Cron Expression:** `0 9 * * *` (chạy hàng ngày lúc 9h sáng).
  - **Time Zone:** Chọn múi giờ phù hợp (vd: `Asia/Ho_Chi_Minh`).

---

### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chạy node `Generate Video Prompt` → Kiểm tra prompt có logic không.
   - Chạy node `Submit Video Generation` → Kiểm tra API Kie AI trả về status `success`.
   - Chạy node `Deliver Video to Telegram` → Kiểm tra video có gửi được không.
2. **Bật Active** workflow.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**
### **1. Tối Ưu Hóa Prompt Gemini**
- **Thêm biến chủ đề** (mùa xuân, mùa đông, biển cả, rừng rậm).
- **Sử dụng template động** để tạo nhiều video khác nhau:
  ```json
  {
    "themes": ["biển buổi chiều", "rừng mây", "hoang mạc", "thành phố đêm"],
    "description": "Cảnh {theme} với ánh sáng {light} (mặt trời, trăng, đèn phố)",
    "style": "chất lượng 4K, không CGI, tự nhiên"
  }
  ```

### **2. Lưu Log & Theo Dõi Lỗi**
- **Thêm node `StickyNote`** để ghi log lỗi:
  ```json
  {
    "error": "${{ $json["error"] }}",
    "status": "${{ $json["status"] }}",
    "timestamp": "${{ $node["Poll Video Status"].date }}"
  }
  ```
- **Kết hợp với Google Sheets** để theo dõi lịch sử.

### **3. Gửi Video qua Slack/Email**
- **Thêm node `Slack`** để thông báo khi video hoàn thành.
- **Thêm node `Email`** để gửi video cho khách hàng.

### **4. Tăng Tốc Đối với Kie AI**
- **Sử dụng polling** thay vì webhook nếu API Kie AI không ổn định.
- **Cấu hình timeout** cho node `wait` (vd: 30 phút).

---

## **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **strategy content** thay vì sản xuất video thủ công. **Chỉ cần 10 phút cấu hình**, bạn đã có **một robot video tự động** hoạt động 24/7!

**👉 Hãy áp dụng ngay và tiết kiệm 80% thời gian sản xuất video!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**💡 Bạn có thể tùy chỉnh chủ đề video theo nhu cầu cụ thể của doanh nghiệp!** Ví dụ:
- **Marketing:** Video quảng cáo sản phẩm với phong cách tự nhiên.
- **Giáo dục:** Video minh họa sinh học về hệ sinh thái.
- **Giải trí:** Video clip ngắn cho TikTok/Reels.