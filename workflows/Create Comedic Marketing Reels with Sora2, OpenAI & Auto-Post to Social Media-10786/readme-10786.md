---
title: "🎬 Tự Động Hóa Video Marketing Hài Hước với Sora2, OpenAI & Auto-Post TikTok/Instagram - Khởi Động Ngay!"
description: "Workflow này tự động tạo video hài hước 12 giây từ AI, upload lên TikTok/Instagram và đăng tự động hàng ngày - tiết kiệm 100% thời gian thủ công cho marketing team!"
slug: "tieu-dong-hoa-video-marketing-hai-huoc-sora2-openai"
tags: [n8n, automation, social-media, ai-multimodal, sora2, tiktok, instagram, openai, no-code]
keywords: [n8n workflow video marketing, tự động hóa tiktok instagram, sora2 ai video, openai caption generator, marketing tự động hóa không code, content ai cho doanh nghiệp]
---

# 🚀 **Tự Động Hóa Video Marketing Hài Hước: Từ AI → Video → TikTok/Instagram Tự Động**

### **Giải pháp cho những sếp marketing mệt mỏi vì phải:**
- **Tạo nội dung video hàng ngày** cho TikTok/Instagram?
- **Tìm kiếm ý tưởng hài hước** để quảng bá sản phẩm/dịch vụ?
- **Chỉnh sửa video** và đăng tải thủ công?
- **Đợi phản hồi** từ khách hàng để điều chỉnh chiến dịch?

**Workflow này sẽ tự động hóa toàn bộ quy trình trong 1 click!** Từ việc **tạo video hài hước 12 giây** bằng Sora2 (AI video tiên tiến), **viết caption hấp dẫn** bằng OpenAI, đến **upload và đăng tự động** lên TikTok/Instagram thông qua Blotato – **không cần code, không cần kỹ thuật!**

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 10+ giờ/ngày** cho team marketing (tạo video, viết caption, đăng tải).
✅ **Nội dung hài hước, cá nhân hóa** phù hợp với brand của doanh nghiệp.
✅ **Hoạt động 24/7** theo lịch trình tự động (ví dụ: đăng video hàng ngày lúc 7h sáng).
✅ **Tăng engagement** với video AI chất lượng cao, caption hấp dẫn.
✅ **Dễ dàng theo dõi & tái sử dụng** ý tưởng video qua Data Table.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản & API Keys:**
   - **OpenAI API Key** (để sử dụng GPT-5 và AI Caption Generator).
   - **Wavespeed/Sora2 API** (để gọi API video AI).
   - **Blotato API Key** (đăng ký tại [blotato.com](https://blotato.com/) để kết nối TikTok/Instagram).
   - **n8n Data Table** (để lưu log prompt video, có thể tạo mới hoặc sử dụng table đã có).

2. **Tài khoản mạng xã hội:**
   - TikTok/Instagram Business Account (đã kết nối với Blotato).

3. **Hệ thống n8n:**
   - **Self-hosted n8n** (khuyến nghị để workflow hoạt động ổn định 24/7).
   - **N8n Community Nodes** (cài đặt các nodes bổ sung như `@n8n/n8n-nodes-langchain` và `@blotato/n8n-nodes-blotato`).
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/10786](https://n8n.io/workflows/10786) (chọn "Export as JSON").
2. **Mở n8n Editor** và nhấn **"Import"** → **"From JSON"** → Chọn file vừa tải.
3. **Xác nhận import** và workflow sẽ hiện lên canvas.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ JSON** từ [n8n.io/workflows/10786](https://n8n.io/workflows/10786) (chọn "Export as JSON").
2. **Mở n8n Editor** → Nhấn **"Import"** → **"From JSON"** → Dán JSON vào và nhấn **"Import"**.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **13 node** quan trọng, các sếp cần **cấu hình kỹ lưỡng** các node sau:

#### **🔹 Node 1: Schedule Trigger (Định thời gian chạy)**
- **Cấu hình:**
  - Chọn **lịch trình** (ví dụ: "Every day at 7:00 PM").
  - **Time Zone:** Chọn múi giờ phù hợp (ví dụ: `Asia/Ho_Chi_Minh`).
- **Lưu ý:** Đảm bảo workflow **không bị trùng chạy** (nếu đã có video đang xử lý).

#### **🔹 Node 2: Video Prompt Agent (Tạo prompt video AI)**
- **Cấu hình:**
  - **Model:** Đã mặc định là `gpt-5` (nếu không có, thêm API Key OpenAI vào n8n).
  - **Prompt:** Sửa đổi để phù hợp với **brand của doanh nghiệp** (ví dụ: thay "coffee shop" thành tên cửa hàng).
  - **Memory Buffer:** Sử dụng `memoryBufferWindow` để lưu trữ prompt trước đó (nếu muốn tái sử dụng).

#### **🔹 Node 3: OpenAI Chat Model (GPT-5)**
- **Cấu hình:**
  - **API Key:** Điền vào **Credentials** của node (nếu chưa có, thêm vào n8n tại `Settings > Credentials`).
  - **Model:** Đảm bảo chọn `gpt-5` (hoặc model khác nếu OpenAI không hỗ trợ).

#### **🔹 Node 4: Sora2 POST Request (Gửi prompt đến Sora2)**
- **Cấu hình:**
  - **URL:** Sử dụng **Wavespeed API** (đăng ký tại [wavespeed.ai](https://wavespeed.ai/)).
  - **Headers:** Thêm `Authorization: Bearer <API_KEY>`.
  - **Body:** Điền `{"prompt": "{{$node["Video Prompt Agent"].json["prompt"]}}", "width": 720, "height": 1280}`.

#### **🔹 Node 5: GET Sora2 Result (Lấy video từ Sora2)**
- **Cấu hình:**
  - **URL:** Sử dụng **endpoint polling** của Sora2 (thường là `https://api.sora.ai/v1/predictions/<prediction_id>`).
  - **Headers:** Thêm `Authorization: Bearer <API_KEY>`.
  - **Lưu ý:** Node này **polling** (kiểm tra) cho đến khi video sẵn sàng (do đó cần **thời gian chờ** sau mỗi request).

#### **🔹 Node 6: Upload media (Upload video lên Blotato)**
- **Cấu hình:**
  - **Credentials:** Điền **Blotato API Key** (tạo tại [blotato.com](https://blotato.com/)).
  - **File:** Chọn `{{$node["GET Sora2 Result"].json["video_url"]}}` (hay `{{$node["GET Sora2 Result"].json["file"]}}` tùy vào cấu trúc API).
  - **Resource:** Chọn `media`.

#### **🔹 Node 7: Create post (Tạo bài đăng TikTok/Instagram)**
- **Cấu hình:**
  - **Caption:** Sử dụng **Caption Generator** (node sau) để tự động tạo caption.
  - **Media:** Chọn video đã upload từ node trước.
  - **Platform:** Chọn TikTok/Instagram (tùy thuộc vào kết nối Blotato).

#### **🔹 Node 8: Caption Generator (Tạo caption AI)**
- **Cấu hình:**
  - **Model:** Sử dụng OpenAI (mặc định là `gpt-4` hoặc `gpt-5`).
  - **Prompt:** Sửa đổi để phù hợp với **brand** (ví dụ: thêm hashtag #CoffeeLovers, #ShopLocal).
  - **Output:** Đảm bảo trả về **caption dạng text** để Blotato sử dụng.

#### **🔹 Node 9: Data Table (Lưu log prompt)**
- **Cấu hình:**
  - **Table ID:** Điền **ID của Data Table** trong n8n (tạo mới tại `Data > Tables`).
  - **Columns:** Đảm bảo có cột `prompt` và `video_url` để lưu trữ.

---
### **3. Kích hoạt ⚡️**
1. **Test Run (Kiểm tra thử):**
   - Chạy **manual test** với dữ liệu mẫu (ví dụ: prompt video đơn giản).
   - Kiểm tra **mỗi node** để đảm bảo không có lỗi (đặc biệt là Sora2 và Blotato).

2. **Bật Active Workflow:**
   - Sau khi test thành công, **bật Active** và **đợi workflow chạy theo lịch trình**.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁCH LÀM NÂNG CAO]
1. **Tái sử dụng prompt:**
   - Sử dụng **Memory Buffer** để lưu trữ prompt cũ và **tái sử dụng** cho video tương tự (giúp tiết kiệm thời gian).

2. **Tăng tính cá nhân hóa:**
   - **Sửa đổi prompt** để phù hợp với **dịp đặc biệt** (ví dụ: "Happy New Year" vào ngày 31/12).
   - **Thêm emoji/hashtag** vào caption theo mùa (ví dụ: `#SummerVibes` vào mùa hè).

3. **Lưu log & báo cáo:**
   - **Kết nối với Google Sheets** (node `dataTable`) để **tạo báo cáo** về số lượng video đăng, engagement.
   - **Gửi báo cáo định kỳ** qua Email (sử dụng node `n8n-nodes-base.email`).

4. **Kết hợp với Slack/Telegram:**
   - **Gửi thông báo** khi video được tạo thành công (ví dụ: "Video mới đã đăng lên TikTok!").
   - **Sử dụng node `n8n-nodes-base.slack`** để alert team.

5. **Optimize Sora2 API:**
   - Nếu video **chậm quá**, giảm **độ phân giải** (ví dụ: từ 720x1280 xuống 480x854).
   - **Tăng thời gian chờ** (node `wait`) nếu Sora2 quá tải.
:::

---
## 📌 **Kết luận**
Workflow này là **công cụ tự động hóa hoàn hảo** cho những sếp marketing muốn:
✔ **Tạo video hài hước hàng ngày** mà không cần kỹ thuật.
✔ **Tiết kiệm thời gian** để tập trung vào chiến lược marketing.
✔ **Tăng engagement** với nội dung AI chất lượng cao.

**👉 Hãy import workflow ngay hôm nay và bắt đầu tự động hóa marketing của mình!**

---
### **🎁 Mã giảm giá VPS cho n8n (Self-hosted)**
:::info[GỢI Ý HẠT ĐẤU]
Để workflow **chạy ổn định 24/7**, các sếp nên **self-host n8n** trên VPS.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

---
**📌 Lưu ý cuối cùng:**
- **Không có workflow nào hoàn hảo 100%**, các sếp cần **test và điều chỉnh** prompt, caption theo brand.
- **Nếu gặp lỗi**, tham khảo [hướng dẫn debug n8n](https://docs.n8n.io/integrations/basic/debugging/) hoặc [community n8n](https://community.n8n.io/).

**Happy automating! 🚀**