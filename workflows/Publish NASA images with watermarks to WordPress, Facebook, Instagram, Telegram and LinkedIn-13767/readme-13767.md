---
title: "🌌 Tự Động Hóa Chia Sẻ Ảnh NASA Với Logo Trang Bài WordPress, Facebook, Instagram, Telegram & LinkedIn - Không Cần Code!"
description: "Workflow tự động hóa lấy ảnh NASA từ RSS Feed, thêm watermark cá nhân hóa, và chia sẻ đồng thời lên WordPress, Facebook, Instagram, Telegram và LinkedIn - tiết kiệm thời gian cho các sếp marketing và content creator 100%."
slug: "tu-dong-hoa-chia-se-anh-nasa"
tags: [n8n, automation, content-creation, social-media, ai-multimodal]
keywords: [n8n workflow NASA, tự động hóa chia sẻ ảnh, watermark tự động, chia sẻ đa nền tảng, AI và n8n]
---

# 🚀 **Tự Động Hóa Chia Sẻ Ảnh NASA Với Logo Trang Bài WordPress, Facebook, Instagram, Telegram & LinkedIn**

### **Giải Pháp Cho Các Sếp Marketing & Content Creator**
Bạn có bao giờ phải mất **giờ đồng hồ** để tìm kiếm, tải xuống, chỉnh sửa và chia sẻ ảnh NASA lên nhiều nền tảng khác nhau? Hay bạn muốn **tự động hóa** quy trình chia sẻ nội dung chất lượng cao mà không cần viết một dòng code nào? Workflow này sẽ **giải phóng thời gian** của các sếp bằng cách tự động:
✅ **Lấy ảnh NASA mới nhất** từ RSS Feed chính thức
✅ **Thêm logo/watermark cá nhân hóa** cho từng ảnh
✅ **Chia sẻ đồng thời lên 5 nền tảng** (WordPress, Facebook, Instagram, Telegram, LinkedIn)
✅ **Tối ưu hóa cho SEO & engagement** với mô tả tự động bằng AI (nếu cần mở rộng)

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **24/7** mà không gián đoạn, các sếp nên **self-host n8n** trên VPS để đảm bảo **tính ổn định và bảo mật cao**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đủ sức mạnh cho workflow này)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần thủ công tìm kiếm, tải xuống và chia sẻ ảnh.
- **Chia sẻ đa nền tảng**: Một workflow duy nhất để quản lý **5 nền tảng** (WordPress, Facebook, Instagram, Telegram, LinkedIn).
- **Cá nhân hóa nội dung**: Thêm logo/watermark tự động cho từng ảnh.
- **Hoạt động liên tục**: Workflow chạy **24/7** mà không cần can thiệp.
- **Nội dung chất lượng cao**: Ảnh NASA được lấy từ **nguồn chính thức**, đảm bảo độ tin cậy.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản WordPress** (API Key hoặc credentials để đăng bài)
✔ **Tài khoản Facebook Developer** (Graph API Access Token)
✔ **Tài khoản Instagram Business** (API Key hoặc OAuth Token)
✔ **Tài khoản Telegram Bot** (Token từ BotFather)
✔ **Tài khoản LinkedIn Developer** (API Key)
✔ **Tài khoản OpenAI (nếu sử dụng AI mô tả)** (API Key)
✔ **Logo/watermark** (định dạng PNG/JPG, kích thước phù hợp)
✔ **VPS n8n** (để self-host workflow)

---
:::note[LƯU Ý QUAN TRỌNG]
- **Nếu không có VPS**, các sếp có thể dùng **n8n Cloud** (miễn phí cho workflow đơn giản), nhưng **không đảm bảo tính ổn định** như self-host.
- **API Key của các nền tảng** phải được **cập nhật thường xuyên** (đặc biệt là Facebook & Instagram).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể **import workflow** từ file JSON hoặc **copy/paste** JSON vào **n8n Editor**:
1. **Tải workflow** từ [link gốc](https://n8n.io/workflows/13767) (nếu có thể).
2. **Mở n8n Editor** (trên VPS hoặc n8n Cloud).
3. **Nhấn "Import"** và chọn file JSON.
4. **Hoặc copy toàn bộ JSON** và dán vào **Import Workflow** trong Editor.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflows này sử dụng **các node chính** sau. Các sếp cần **cấu hình kỹ lưỡng** như sau:

##### **🔹 Node RSS Feed Read (n8n-nodes-base.rssFeedRead)**
- **URL Feed**: `https://images.nasa.gov/api/discovery/v1/search?q=latest&count=1` (hoặc feed NASA khác)
- **Tham số**:
  - `format`: `json`
  - `fields`: `title,description,link,media_thumbnail`

##### **🔹 Node Edit Image (n8n-nodes-base.editImage)**
- **Tải ảnh từ URL** (trong node RSS Feed).
- **Thêm watermark**:
  - **Logo**: Tải lên từ máy tính (định dạng PNG/JPG).
  - **Vị trí**: Góc phải dưới (hoặc tùy chỉnh).
  - **Độ trong suốt**: 70% (để không che khuất ảnh).
- **Output**: Ảnh đã watermark (sử dụng trong các node chia sẻ sau).

##### **🔹 Node WordPress (n8n-nodes-base.wordpress)**
- **Credentials**: Thiết lập từ **n8n Credentials Manager**.
  - **API Key**: Lấy từ **WordPress REST API**.
  - **Site URL**: Địa chỉ blog WordPress.
- **Tham số**:
  - **Title**: `NASA Image: [Tên ảnh]`
  - **Content**: `Mô tả từ NASA + liên kết ảnh watermark`
  - **Featured Image**: Ảnh đã watermark.

##### **🔹 Node Facebook Graph API (n8n-nodes-base.facebookGraphApi)**
- **Credentials**:
  - **Access Token**: Lấy từ **Facebook Developer** (phải có quyền `publish_pages`).
  - **Page ID**: ID của trang Facebook muốn chia sẻ.
- **Tham số**:
  - **Message**: `Khám phá ảnh NASA mới nhất: [Liên kết ảnh]`
  - **Picture URL**: Ảnh đã watermark.

##### **🔹 Node Instagram (n8n-nodes-base.instagram)**
- **Credentials**:
  - **API Key**: Lấy từ **Instagram Graph API** (phải có tài khoản Business).
  - **Access Token**: Token OAuth 2.0.
- **Tham số**:
  - **Caption**: `NASA Image: [Mô tả]`
  - **Image URL**: Ảnh đã watermark.

##### **🔹 Node Telegram (n8n-nodes-base.telegram)**
- **Credentials**:
  - **Bot Token**: Lấy từ [@BotFather](https://t.me/BotFather).
  - **Chat ID**: ID của nhóm/channel Telegram (lấy bằng cách gửi tin nhắn cho bot `@userinfobot`).
- **Tham số**:
  - **Text**: `🌌 Ảnh NASA mới: [Liên kết ảnh]`
  - **Photo**: Ảnh đã watermark.

##### **🔹 Node LinkedIn (n8n-nodes-base.linkedIn)**
- **Credentials**:
  - **API Key**: Lấy từ **LinkedIn Developer**.
  - **Access Token**: Token OAuth 2.0.
- **Tham số**:
  - **Content**: `Khám phá ảnh NASA mới nhất: [Liên kết ảnh]`
  - **Media URL**: Ảnh đã watermark.

##### **🔹 Node LangChain (n8n-nodes-langchain.lmChatOpenAi) - Tùy chọn**
Nếu muốn **tự động mô tả ảnh** bằng AI (để chia sẻ trên LinkedIn/Telegram):
- **API Key OpenAI**: Điền vào **Credentials**.
- **Prompt**:
  ```plaintext
  "Tóm tắt ngắn gọn về ảnh NASA này (dưới 100 từ) và đề xuất hashtag phù hợp."
  ```
- **Output**: Dùng để **cập nhật mô tả** trong các node chia sẻ.

---
#### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với **dữ liệu mẫu** (nếu có).
2. **Bật Active** workflow.
3. **Monitor** trong **n8n Dashboard** để kiểm tra lỗi (nếu có).

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tự động chia sẻ định kỳ**:
   - Sử dụng **node `n8n-nodes-base.setInterval`** để chạy workflow **mỗi ngày/lần** thay vì chỉ khi có ảnh mới.
2. **Lưu log chia sẻ**:
   - Thêm **node `n8n-nodes-base.stickyNote`** để ghi lại **lịch sử chia sẻ** (dùng cho báo cáo).
3. **Gửi báo cáo tuần/Tháng**:
   - Kết hợp với **node `n8n-nodes-base.email`** để tự động gửi **báo cáo thống kê** (số lượt chia sẻ, nền tảng nào hiệu quả).
4. **Cá nhân hóa mô tả bằng AI**:
   - Sử dụng **LangChain** để **tự động viết mô tả** phù hợp với từng nền tảng (ví dụ: mô tả ngắn cho Instagram, chi tiết cho LinkedIn).
5. **Chia sẻ trên TikTok/YouTube Shorts**:
   - Nếu cần, thêm **node `n8n-nodes-base.youtube`** để chia sẻ video ngắn từ ảnh NASA.

---
### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp marketing và content creator bằng cách **tự động hóa toàn bộ quy trình** từ lấy ảnh đến chia sẻ đa nền tảng. **Không cần viết code**, chỉ cần **cấu hình các API Key** và **cài đặt VPS ổn định**, các sếp đã có một **công cụ tự động hóa hoàn hảo** để **tăng cường engagement** và **tối ưu hóa nội dung**.

**Hãy thử ngay và chia sẻ ảnh NASA của mình trên 5 nền tảng chỉ trong vài giây!** 🚀

---
:::tip[LÀM GÌ TIẾP?]
1. **Đăng ký VPS** để self-host n8n (để workflow chạy 24/7).
2. **Cấu hình các API Key** theo hướng dẫn trên.
3. **Import workflow** và **bật Active**.
4. **Monitor** và **tối ưu hóa** theo nhu cầu!
:::

---
**Cần hỗ trợ?** Đăng ký **hỗ trợ kỹ thuật n8n** tại [n8n Community](https://community.n8n.io/) hoặc liên hệ **SpaGreen Creative** (tác giả workflow). 😊