---
title: "🎬 Tự Động Hóa Sáng Tạo Video YouTube Faceless Với Leonardo AI & Creatomate - Không Cần Code!"
description: "Workflow tự động hóa hoàn chỉnh giúp các sếp Content Creator và Marketing tự động tạo video YouTube không cần mặt người, sử dụng AI Leonardo AI và Creatomate. Tiết kiệm thời gian lên đến 90% và tăng hiệu suất content lên 3x!"
slug: "tieu-dong-hoa-sang-tao-video-youtube-faceless"
tags: [n8n, automation, ai, marketing, content-creation, leonardo-ai, youtube-automation]
keywords: [tự động hóa video youtube, faceless video, leonardo ai n8n, tự động hóa content marketing, workflow youtube ai, tạo video youtube không cần code]
---

# 🚀 **Tự Động Hóa Sáng Tạo Video YouTube Faceless Với Leonardo AI & Creatomate**

### **Giải pháp hoàn hảo cho các sếp Content Creator muốn tiết kiệm thời gian và tăng hiệu suất content lên 3x!**

Hãy tưởng tượng một ngày bạn không phải lo lắng về việc **chỉnh sửa video, tìm kiếm hình ảnh, viết script hay lên kế hoạch content** nữa. **Workflow này tự động hóa toàn bộ quy trình sáng tạo video YouTube faceless** (không cần mặt người) bằng cách kết hợp **Leonardo AI** (sáng tạo hình ảnh AI) và **Creatomate** (tạo video từ script), tất cả chỉ với một cú nhấp chuột!

Không cần kỹ năng code, không cần đội ngũ chuyên nghiệp – chỉ cần **n8n** và một chút cấu hình, bạn đã có thể **tạo video chuyên nghiệp, cá nhân hóa và tối ưu SEO** hàng ngày!

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên một VPS chuyên dụng.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ cao cho AI)
:::

---

## 🎯 **Kết quả các sếp nhận được**

:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian lên đến 90%** – Không cần chỉnh sửa video thủ công, tìm kiếm hình ảnh hay viết script.
✅ **Video chuyên nghiệp, cá nhân hóa** – AI tự động chọn hình ảnh, thêm hiệu ứng và tối ưu nội dung.
✅ **Hoạt động liên tục 24/7** – Duy trì lịch trình content ngay cả khi bạn ngủ.
✅ **Tối ưu SEO tự động** – Video được cấu trúc theo best practice, tăng khả năng xếp hạng trên YouTube.
✅ **Không cần kỹ năng code** – Cấu hình đơn giản, chỉ cần copy/paste và chạy.
:::

---

## 🔧 **Yêu cầu cần thiết**

Trước khi bắt đầu, các sếp cần chuẩn bị:

### **1. Tài khoản và API Keys**
| Dịch vụ | Yêu cầu |
|---------|---------|
| **Leonardo AI** | [Tạo tài khoản](https://leonardo.ai/) và lấy **API Key** từ Dashboard. |
| **Creatomate** | [Đăng ký miễn phí](https://creatomate.com/) và lấy **API Key**. |
| **YouTube API** | [Bật YouTube Data API v3](https://developers.google.com/youtube/v3/getting-started) và lấy **Client ID & Client Secret**. |
| **OpenAI (ChatGPT API)** | [Lấy API Key](https://platform.openai.com/account/api-keys) (để AI Agent viết script). |
| **Telegram Bot** (tùy chọn) | [Tạo bot Telegram](https://core.telegram.org/bots) và lấy **Token Bot**. |

### **2. Thiết bị & Hạ tầng**
- **VPS self-hosted n8n** (khuyến nghị sử dụng **TinoHost** hoặc **BNIX** như trên).
- **Nút domain** (nếu muốn chạy webhook).
- **Dung lượng lưu trữ** (để lưu video và hình ảnh AI).

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/2971](https://n8n.io/workflows/2971) (chọn **Download JSON**).
2. **Mở n8n Editor** trên VPS của bạn.
3. Nhấn **Import** → Chọn file JSON vừa tải → **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Tải JSON** từ link trên.
2. **Mở n8n Editor** → Nhấn **Import** → Chọn **Paste JSON** → Dán nội dung file → **Import**.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

Workflow này **phức tạp** và có **nhiều node cần cấu hình cẩn thận**. Dưới đây là **các bước quan trọng** để setup:

#### **A. Cấu hình API Keys**
| Node | Yêu cầu cấu hình |
|------|------------------|
| **Leonardo AI** | Điền **API Key** vào `Authorization: Bearer {API_KEY}` trong header của các node `Generate Image X - LeonardoAI`. |
| **Creatomate** | Điền **API Key** vào `Authorization: Bearer {API_KEY}` trong node `Cre - Generate Video1` và `Cre - Get Video`. |
| **OpenAI (ChatGPT)** | Điền **API Key** vào node `OpenAI Chat Model` (trong `n8n-nodes-langchain.lmChatOpenAi`). |
| **YouTube API** | Cấu hình trong node `YouTube` với `Client ID` và `Client Secret`. |
| **Telegram (nếu dùng)** | Điền **Token Bot** vào node `Telegram` để gửi thông báo khi video hoàn thành. |

#### **B. Cấu hình Script & Prompt cho AI Agent**
Node **`AI Agent`** (Loại: `@n8n/n8n-nodes-langchain.agent`) sẽ **tự động viết script** cho video. Các sếp cần:
1. **Điền `Prompt`** để AI hiểu yêu cầu của video (ví dụ: *"Tạo một video faceless về cách học tiếng Anh hiệu quả cho người mới bắt đầu"*).
2. **Cấu hình `Output Parser`** (node `Structured Output Parser`) để AI trả về **dữ liệu có cấu trúc** (script, danh sách hình ảnh cần tạo, tiêu đề, mô tả).

#### **C. Cấu hình Lịch trình (Schedule Trigger)**
Node **`Schedule Trigger`** cho phép workflow chạy **tự động theo lịch**.
- **Chọn ngày giờ** (ví dụ: **mỗi ngày 8h sáng**).
- **Chọn timezone** (Việt Nam: `Asia/Ho_Chi_Minh`).

#### **D. Cấu hình Telegram (nếu muốn nhận thông báo)**
Nếu muốn **nhận tin nhắn Telegram** khi video hoàn thành:
1. Cấu hình node `Telegram` với:
   - **Chat ID** (lấy từ `@username` của bot Telegram).
   - **Message Template** (ví dụ: *"Video mới đã hoàn thành: [Tên Video]"*).

---

### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Run Workflow** và kiểm tra từng node.
   - Đặc biệt kiểm tra:
     - AI Agent có viết script không?
     - Leonardo AI có tạo hình ảnh không?
     - Creatomate có tạo video không?
2. **Bật Active** khi mọi thứ hoạt động ổn.

---

## ✍️ **Mẹo & gợi ý nâng cao**

### **1. Tối ưu hóa video cho SEO**
- **Thêm thẻ mô tả chi tiết** trong node `Edit Fields` (ví dụ: từ khóa, liên kết, hashtag).
- **Cấu hình tiêu đề video** theo **best practice YouTube** (ví dụ: *"Cách Học Tiếng Anh Nhanh Chóng Cho Người Mới Bắt Đầu - Faceless Video"*).

### **2. Kết hợp với Slack/Telegram**
- **Gửi thông báo khi video hoàn thành** qua Slack hoặc Telegram.
- **Tự động chia sẻ video** lên các nhóm cộng đồng (nếu có API).

### **3. Lưu log và theo dõi hiệu suất**
- Sử dụng **node `StickyNote`** để ghi chú các lỗi hoặc cải tiến.
- **Lưu video và hình ảnh** vào **Google Drive** hoặc **AWS S3** thay vì chỉ lưu trên Creatomate.

### **4. Tạo nhiều video cùng lúc**
- **Sử dụng node `Merge`** để chạy nhiều script song song.
- **Tăng tốc độ** bằng cách **tăng số lượng hình ảnh AI** (ví dụ: tạo 6 hình ảnh thay vì 3).

### **5. Cập nhật nội dung định kỳ**
- **Sử dụng `Schedule Trigger`** để tự động cập nhật video theo **lịch trình content**.
- **Cập nhật script** bằng cách thay đổi `Prompt` trong AI Agent.

---

## 📌 **Kết luận**

Workflow này **không chỉ tiết kiệm thời gian mà còn nâng cao chất lượng content** của các sếp Content Creator và Marketing. **Không cần code, không cần đội ngũ chuyên nghiệp** – chỉ cần **n8n + AI**, bạn đã có thể **tạo video YouTube faceless chuyên nghiệp** hàng ngày!

**Hãy thử ngay và xem kết quả như thế nào!** 🚀

---
### **Bước tiếp theo**
1. **Import workflow** theo hướng dẫn trên.
2. **Cấu hình API Keys** và **Prompt AI**.
3. **Bật Schedule Trigger** và **chờ video tự động hoàn thành!**

**Nếu có vấn đề, hãy để lại comment bên dưới!** 👇