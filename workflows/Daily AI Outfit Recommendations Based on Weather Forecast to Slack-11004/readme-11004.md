---
title: "🌤️ [Tự Động Hóa Gợi Ý Áo Phục AI Theo Dự Báo Thời Tiêu Trên Slack - Khởi Động Ngày Hàng Ngày] 👕✨"
description: "Workflow tự động hóa hàng ngày gửi gợi ý trang phục phù hợp với thời tiết qua Slack, giúp các sếp tiết kiệm thời gian và bắt đầu ngày mới với phong cách cá nhân hóa. Dữ liệu thời tiết chính xác từ OpenWeatherMap kết hợp với trí tuệ nhân tạo OpenRouter để tạo ra những lời khuyên thời trang thực tế."
slug: "tieu-dong-hoa-gi-gi-y-ao-phuc-ai-theo-thoi-tieu"
tags: [n8n, automation, no-code, ai-personal-assistant, slack-integration, openweathermap, langchain]
keywords: [n8n workflow thời tiết, tự động hóa trang phục AI, gợi ý áo phục hàng ngày, Slack + AI, OpenWeatherMap API, OpenRouter AI]
---

# 🚀 **Tự Động Hóa Gợi Ý Áo Phục AI Theo Dự Báo Thời Tiêu Trên Slack**

### **🔥 Nỗi Đau Của Các Sếp Hàng Ngày**
Mỗi sáng, các sếp phải mất **5-10 phút** để:
- **Tra cứu thời tiết** trên Google hoặc ứng dụng thời tiết.
- **Tìm kiếm gợi ý trang phục** phù hợp trên Pinterest, TikTok, hoặc hỏi bạn bè.
- **Chọn đồ** nhưng vẫn lo lắng "Có phù hợp không?" với nhiệt độ, độ ẩm, hoặc mưa gió.
- **Quên hoặc không kịp** chuẩn bị đồ phù hợp khi thời tiết thay đổi bất ngờ.

**Kết quả?** Thời gian bị lãng phí, trang phục không phù hợp, và cảm giác "không tự tin" khi ra ngoài.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
Sau khi áp dụng workflow này, các sếp sẽ:
✅ **Tiết kiệm 10+ phút mỗi sáng** – Không cần tra cứu thời tiết hay tìm gợi ý trang phục.
✅ **Áo phục phù hợp 100%** – AI phân tích thời tiết và gợi ý trang phục **cá nhân hóa**, từ áo khoác cho ngày mưa đến quần áo mát mẻ cho ngày nắng nóng.
✅ **Hình ảnh thời tiết + gợi ý trang phục** được **tự động tạo và gửi** lên Slack, giúp bắt đầu ngày một cách **sáng tạo và hiệu quả**.
✅ **Hoạt động 24/7** – Workflow chạy tự động **lúc 6h sáng hàng ngày**, không cần can thiệp thủ công.

---
### **🔧 Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
🔹 **API Key OpenWeatherMap** – Để lấy dữ liệu thời tiết chính xác.
🔹 **API Key OpenRouter** – Để sử dụng mô hình AI chatbot (OpenRouter).
🔹 **Credentials Slack** – Để upload file hình ảnh vào channel Slack.
🔹 **Thiết bị VPS** – Để chạy workflow 24/7 (không cần máy tính cá nhân).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/11004](https://n8n.io/workflows/11004) (chọn "Download JSON").
2. **Mở n8n Editor** trên VPS hoặc máy tính.
3. **Nhấn "Import"** và chọn file JSON vừa tải.
4. **Chọn "Import"** để workflow xuất hiện trên canvas.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Tải file JSON** từ link trên.
2. **Mở n8n Editor** và nhấn **"Import"** → **"Paste JSON"**.
3. **Dán toàn bộ nội dung JSON** vào ô và nhấn **"Import"**.

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

#### **🔹 Node 1: "Daily 6AM Trigger" (scheduleTrigger)**
- **Không cần chỉnh sửa** – Workflow tự động chạy lúc 6h sáng hàng ngày.

#### **🔹 Node 2: "Get Weather Data" (openWeatherMap)**
- **Thêm API Key OpenWeatherMap**:
  - Mở node này → **Credentials** → Chọn **"Add"** → Nhập **API Key** từ tài khoản OpenWeatherMap.
  - **Chỉnh sửa thành phố**:
    - Trong **Parameters** → **City** → Nhập tên thành phố (ví dụ: "Hà Nội" hoặc "TP.HCM").
    - **Lưu ý**: Nếu muốn lấy thời tiết theo vị trí GPS, có thể sử dụng **lat/lng** thay vì tên thành phố.

#### **🔹 Node 3: "OpenRouter Chat Model" (lmChatOpenRouter)**
- **Thêm API Key OpenRouter**:
  - Mở node này → **Credentials** → Chọn **"Add"** → Nhập **API Key** từ tài khoản OpenRouter.
  - **Chọn mô hình AI** (nếu cần):
    - Trong **Parameters** → **Model** → Chọn mô hình phù hợp (ví dụ: `mistral-tiny`, `llama3`).

#### **🔹 Node 4: "Upload a file" (slack)**
- **Thêm Credentials Slack**:
  - Mở node này → **Credentials** → Chọn **"Add"** → Nhập **Token OAuth** từ Slack (tạo ở [Slack API](https://api.slack.com/apps)).
- **Chọn Channel**:
  - Trong **Parameters** → **Channel** → Nhập **#channel-name** (ví dụ: `#personal-assistant`).
- **Tên file**:
  - Trong **Parameters** → **File Name** → Đặt tên file (ví dụ: `outfit_recommendation_${date}.png`).

#### **🔹 Node 5: "Create Image Card" (editImage)**
- **Không cần chỉnh sửa** – Workflow tự động tạo hình ảnh từ dữ liệu thời tiết và gợi ý trang phục.

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** (để kiểm tra workflow hoạt động):
   - Nhấn **"Run Workflow"** trên canvas.
   - Kiểm tra **Slack channel** đã có hình ảnh gợi ý trang phục chưa.
2. **Bật Active**:
   - Nhấn **"Active"** trên nút ở góc trên bên phải của workflow.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **🔹 Tích Hợp với Google Calendar**
- **Gợi ý trang phục trước khi đi làm**:
  - Sử dụng **node Google Calendar** để lấy lịch hẹn và kết hợp với thời tiết để gợi ý trang phục phù hợp cho mỗi hoạt động.

### **🔹 Lưu Log Lịch Sử Gợi Ý**
- **Sử dụng node StickyNote** để lưu lịch sử gợi ý trang phục:
  - Mở node **"Store Advice Text"** → Thêm **StickyNote** để lưu dữ liệu.
  - Sau đó, có thể **xem lại lịch sử** để so sánh với thời tiết trước đó.

### **🔹 Gửi Báo Cáo Hàng Tuần**
- **Tạo báo cáo tuần** về thời tiết và trang phục:
  - Sử dụng **node ScheduleTrigger** để chạy workflow vào **thứ Bảy sáng**.
  - **Tạo một file PDF** tổng hợp gợi ý trang phục trong tuần và gửi lên Slack.

### **🔹 Kết Hợp với Telegram**
- **Gửi gợi ý trang phục qua Telegram** thay vì Slack:
  - Thay thế node **Slack** bằng **Telegram Bot Node**.
  - Cài đặt **Bot Telegram** và thêm **API Key** vào node mới.

---

## **📌 Kết Luận**
Workflow **Daily AI Outfit Recommendations** là **giải pháp hoàn hảo** cho các sếp muốn:
✔ **Tiết kiệm thời gian** mỗi sáng.
✔ **Áo phục luôn phù hợp** với thời tiết.
✔ **Bắt đầu ngày một cách sáng tạo** với hình ảnh thời trang cá nhân hóa.

**Hành động ngay!**
1. **Cài đặt n8n trên VPS** (nếu chưa có).
2. **Import workflow** và **cấu hình API Keys**.
3. **Bật Active** và **nhận gợi ý trang phục hàng ngày**!

**🚀 Chúc các sếp có những ngày mới hiệu quả và thời trang hơn!** 👕🌦️