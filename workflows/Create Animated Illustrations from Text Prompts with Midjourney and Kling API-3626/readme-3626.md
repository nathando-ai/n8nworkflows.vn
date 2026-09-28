---
title: "🎨 Tự Động Tạo Bài Động Vẽ Tự Động Từ Văn Bản (Midjourney + Kling API) - Không Cần Code!"
description: "Workflow tự động hóa hoàn toàn để chuyển đổi văn bản thành bài động vẽ ấn tượng chỉ với một cú nhấp chuột, giúp content creator và marketer tiết kiệm thời gian lên tới 90% trong quá trình tạo nội dung đa phương tiện."
slug: "tay-dong-hoa-tao-bai-dong-ve-tu-van-ban"
tags: [n8n, automation, ai, midjourney, kling-api, design, marketing, no-code]
keywords: [tự động hóa n8n, tạo bài động vẽ tự động, midjourney api, kling api, content creator, marketing automation, workflow n8n design]
---

# 🚀 **Tự Động Tạo Bài Động Vẽ Tự Động Từ Văn Bản (Midjourney + Kling API)**

### **Giải pháp hoàn hảo cho content creator và marketer**
Hãy tưởng tượng: chỉ với một câu văn bản ngắn, bạn có thể tạo ra **bài động vẽ chuyên nghiệp, độc đáo và thu hút** mà không cần phải vẽ tay hay sử dụng phần mềm phức tạp. Đây chính là sức mạnh của **n8n workflow kết hợp Midjourney và Kling API** – một công cụ tự động hóa hoàn toàn **không cần code**, giúp bạn tiết kiệm **thời gian lên tới 90%** trong quá trình tạo nội dung đa phương tiện.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần thiết kế thủ công, chỉ cần nhập văn bản là hệ thống tự tạo bài động vẽ.
- **Nội dung chuyên nghiệp**: Sử dụng AI Midjourney và Kling API để tạo ra **bài động vẽ ấn tượng, phù hợp với mọi chủ đề**.
- **Hoạt động liên tục**: Workflow tự động chạy 24/7, không cần can thiệp của con người.
- **Tối ưu chi phí**: Tránh chi phí thuê designer hoặc mua phần mềm thiết kế đắt đỏ.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
- **Tài khoản PiAPI** (để lấy **x-api-key**) – [Đăng ký tại đây](https://piapi.ai/).
- **API Key của Midjourney** (nếu không có, liên hệ PiAPI để kích hoạt).
- **Thời gian thử nghiệm**: Workflow này **không miễn phí hoàn toàn**, nhưng với chi phí thấp, các sếp có thể tạo ra **nghìn bài động vẽ chất lượng cao**.

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/3626](https://n8n.io/workflows/3626) (chọn **Export as JSON**).
2. Mở **n8n Editor** trên máy chủ của mình.
3. Nhấp vào **Import** và chọn file JSON vừa tải.
4. Workflow sẽ xuất hiện trên canvas.

#### **Phương pháp 2: Copy/Paste JSON**
1. Copy toàn bộ mã JSON từ [n8n.io/workflows/3626](https://n8n.io/workflows/3626).
2. Trong **n8n Editor**, nhấp vào **Import** → **Paste JSON**.
3. Nhấp **Import** để hoàn tất.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **🔹 Cấu hình API Key (QUAN TRỌNG NHẤT!)**
Workflow sử dụng **2 API Key chính**:
- **Midjourney Image Generator** → Điền **x-api-key** từ PiAPI vào **Headers** (`x-api-key: [API_KEY_CỦA_BẠN]`).
- **Kling Video Generator** → Điền **x-api-key** tương tự vào **Headers**.

:::warning[LƯU Ý]
- **Không để trống API Key** → Workflow sẽ **không hoạt động**.
- Nếu không có tài khoản PiAPI, đăng ký tại [piapi.ai](https://piapi.ai/) và lấy API Key từ **Dashboard**.
:::

#### **🔹 Cấu hình "Basic Prompt" (Nội dung văn bản)**
- Node **"Basic Prompt"** là nơi các sếp **nhập văn bản** để tạo bài động vẽ.
- Ví dụ:
  - *"A futuristic city with neon lights and flying cars, cinematic style, 4K, ultra-detailed"*
  - *"A cute cartoon fox wearing a business suit, animated, 3D, vibrant colors"*

#### **🔹 Cấu hình thời gian chờ (Wait Nodes)**
- Workflow có **2 node Wait** để chờ:
  1. **"Wait for Image Generation"** (chờ Midjourney tạo ảnh).
  2. **"Wait for Video Generation"** (chờ Kling tạo video).
- Thời gian mặc định là **30 giây**, nhưng có thể **tăng lên 1-2 phút** nếu cần (điều chỉnh trong **Configuration** của node Wait).

#### **🔹 Kiểm tra "Get Data Status" và "Verify Data Status"**
- Hai node **If** này **lọc dữ liệu** để đảm bảo:
  - Ảnh từ Midjourney đã tạo thành công.
  - Video từ Kling đã hoàn tất.
- Nếu **không có dữ liệu**, workflow sẽ **dừng lại** và báo lỗi.

---

### **3. Kích hoạt ⚡️**
1. **Nhấp vào nút "Test workflow"** để chạy thử.
2. Nhập **văn bản prompt** vào node **"Basic Prompt"**.
3. Chờ **~2-5 phút** (thời gian phụ thuộc vào API).
4. Kiểm tra **output** trong node **"Get Final Video URL"** để lấy liên kết bài động vẽ.
5. **Bật Active** để workflow chạy tự động khi có yêu cầu.

---

## ✍️ **Mẹo & gợi ý nâng cao**

### **🔹 Kết hợp với Slack/Telegram để thông báo kết quả**
- Sử dụng **node Slack/Telegram Webhook** để gửi **liên kết bài động vẽ** ngay khi hoàn tất.
- Cách làm:
  1. Thêm **node HTTP Request** (Slack/Telegram Webhook).
  2. Gửi **Final Video URL** từ node **"Get Final Video URL"** vào payload.

### **🔹 Lưu log để theo dõi quá trình**
- Thêm **node Sticky Note** để ghi lại:
  - **Prompt** được sử dụng.
  - **Thời gian tạo**.
  - **Liên kết kết quả**.
- Giúp các sếp **theo dõi hiệu suất** và **cải thiện nội dung** sau này.

### **🔹 Tạo nhiều biến thể prompt**
- Sử dụng **node Code** để **tạo nhiều biến thể prompt** từ một văn bản gốc.
- Ví dụ:
  - *"A cyberpunk robot in a rainstorm"* → *"A cyberpunk robot in a desert"* → *"A cyberpunk robot in space"*

### **🔹 Tích hợp với Google Drive/Dropbox**
- Sau khi tạo xong, **tự động tải video lên Google Drive/Dropbox** để lưu trữ.
- Cách làm:
  1. Thêm **node Google Drive** (hoặc Dropbox).
  2. Sử dụng **Final Video URL** để tải và lưu file.

---

## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho:
✅ **Content Creator** muốn tạo **bài động vẽ chuyên nghiệp** mà không cần thiết kế.
✅ **Marketer** cần **nội dung đa phương tiện** để quảng bá sản phẩm.
✅ **Doanh nghiệp** muốn **tự động hóa nội dung** mà không tốn chi phí cao.

**Hành động ngay!**
1. **Đăng ký PiAPI** và lấy **API Key**.
2. **Import workflow** vào n8n của mình.
3. **Nhập prompt** và **chờ kết quả** trong vài phút.
4. **Chia sẻ bài động vẽ** trên mạng xã hội hoặc sử dụng trong nội dung marketing!

**🚀 Cùng tự động hóa nội dung của mình ngay hôm nay!** 🚀