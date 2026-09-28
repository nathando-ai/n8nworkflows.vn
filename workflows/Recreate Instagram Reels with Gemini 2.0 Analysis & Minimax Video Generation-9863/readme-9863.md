---
title: "🚀 Tự Động Hoá Tạo Bài Video Instagram Reels Mới Từ AI: Phân Tích & Sinh Thành Video Bằng Gemini 2.0 & Minimax"
description: "Workflow này tự động tải xuống video Reels từ Instagram, phân tích chi tiết bằng AI Gemini 2.0, sau đó tái tạo video mới hoàn toàn khác biệt bằng mô hình Minimax Video-01. Giúp content creator tiết kiệm thời gian và tạo nội dung đa dạng chỉ với 1 cú nhấp chuột."
slug: "tay-dong-hoa-tao-bai-video-instagram-reels-tu-ai"
tags: [n8n, automation, ai-video-generation, instagram-reels, gemini-2-0, replicate-minimax]
keywords: [tự động hóa video instagram, tạo video từ ai, gemini 2.0 phân tích video, minimax video generation, workflow n8n ai, content creator tự động]
---

# 🚀 **Tự Động Hoá Tạo Bài Video Instagram Reels Mới Từ AI: Phân Tích & Sinh Thành Video Bằng Gemini 2.0 & Minimax**

## **💡 Giải Pháp Cho Content Creator & Quản Lý Marketing**
Bạn đã bao giờ mệt mỏi phải tạo ra hàng loạt video Reels giống nhau để tối ưu hóa nội dung? Hay muốn biến một video thành công thành nhiều phiên bản khác nhau để thử nghiệm? **Workflow này sẽ tự động hóa toàn bộ quá trình** – từ tải xuống video Reels đến phân tích chi tiết bằng AI, rồi tái tạo video hoàn toàn mới với nội dung độc đáo, chỉ trong vài phút!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### **🎯 Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải quay lại video từ đầu, chỉ cần nhập URL Reels.
- **Nội dung đa dạng**: Tạo ra hàng loạt phiên bản video khác nhau từ 1 video gốc.
- **Phân tích sâu**: AI Gemini 2.0 phân tích từng khung hình, âm thanh, và động tác trong video.
- **Tái tạo sáng tạo**: Mô hình Minimax Video-01 sinh thành video mới với phong cách độc đáo.
- **Hoạt động liên tục**: Workflow tự động kiểm tra trạng thái và xử lý lỗi nếu có.
:::

---

### **🔧 Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **API Key RapidAPI** (để tải video Reels):
   - Đăng ký tại [RapidAPI](https://rapidapi.com) và mua gói "Instagram Reels Downloader API".
   - Copy API Key và thay thế `YOUR_RAPIDAPI_KEY_HERE` trong workflow.

2. **API Key Google AI Studio** (để phân tích video bằng Gemini 2.0):
   - Đăng ký tại [Google AI Studio](https://aistudio.google.com/apikey).
   - Tạo API Key và thay thế `YOUR_GOOGLE_API_KEY_HERE` (xuất hiện 2 lần trong workflow).

3. **API Key Replicate** (để sinh thành video mới bằng Minimax):
   - Đăng ký tại [Replicate](https://replicate.com).
   - Tạo API Token tại **Account Settings → API Tokens** và thay thế `YOUR_REPLICATE_API_KEY_HERE` (xuất hiện 3 lần).

4. **Tài khoản n8n** (Self-hosted hoặc n8n.cloud) để chạy workflow.
:::

---

### **🚀 Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link workflow gốc](https://n8n.io/workflows/9863) hoặc copy/paste JSON từ trang này vào **n8n Editor**.
- **Cách import**:
  1. Mở n8n Editor → Nhấn **"Import"** → Chọn file JSON hoặc dán JSON.
  2. Nhấn **"Import"** để hoàn tất.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **13 node** với các bước chính sau. Các sếp cần chú ý **cấu hình API Key** ở các node sau:

| **Node**                     | **Loại Node**               | **Lưu ý cấu hình**                                                                 |
|------------------------------|-----------------------------|------------------------------------------------------------------------------------|
| **When chat message received** | `chatTrigger`               | **Không cần cấu hình** – tự động nhận URL từ chat.                              |
| **Reel Downloader**          | `httpRequest`               | Thay thế `YOUR_RAPIDAPI_KEY_HERE` trong **Headers → `x-rapidapi-key`**.          |
| **Download Reel**             | `httpRequest`               | **Không cần cấu hình** – tự động tải video từ URL.                               |
| **Upload the video to model** | `httpRequest`               | Thay thế `YOUR_GOOGLE_API_KEY_HERE` trong **URL parameter**.                      |
| **Analyse the Video**        | `httpRequest`               | Thay thế `YOUR_GOOGLE_API_KEY_HERE` trong **URL parameter**.                      |
| **Create the Video**         | `httpRequest`               | Thay thế `YOUR_REPLICATE_API_KEY_HERE` trong **Headers → `Authorization`**.      |
| **Get Status of the Video**  | `httpRequest`               | Thay thế `YOUR_REPLICATE_API_KEY_HERE` trong **Headers → `Authorization`**.      |
| **Fetches the Video Output** | `httpRequest`               | Thay thế `YOUR_REPLICATE_API_KEY_HERE` trong **Headers → `Authorization`**.      |

:::note[Cách thay thế API Key]
- Mở node cần cấu hình → Nhấn **"Edit"** → Tìm phần **URL** hoặc **Headers**.
- Thay thế tất cả các chuỗi `YOUR_API_KEY_HERE` bằng API Key thực tế.
- **Lưu ý**: API Key Google và Replicate xuất hiện nhiều lần → **đảm bảo thay thế đầy đủ**.
:::

#### **3. Kích hoạt ⚡️**
1. **Test run dữ liệu mẫu**:
   - Nhập **URL của một video Reels** vào chat trigger (ví dụ: `https://www.instagram.com/reel/...`).
   - Nhấn **"Run"** để kiểm tra workflow.
   - Nếu gặp lỗi, kiểm tra lại API Key và kết nối mạng.

2. **Bật Active workflow**:
   - Sau khi test thành công, nhấn **"Active"** để workflow chạy tự động khi nhận được URL.

---

### **✍️ Mẹo & gợi ý nâng cao**
:::tip[CÁCH SỬ DỤNG HIỆU QUẢ NHẤT]
1. **Tích hợp với Slack/Telegram**:
   - Sau khi video được tạo, thêm node **`httpRequest`** gửi kết quả về Slack/Telegram thông báo hoàn tất.
   - Ví dụ: Gửi link video mới vào channel nội dung.

2. **Lưu log và báo cáo**:
   - Thêm node **`set`** để lưu thông tin video (tên, URL, thời gian tạo) vào **Google Sheets** hoặc **Notion**.
   - Dùng node **`email`** gửi báo cáo định kỳ cho team.

3. **Tối ưu thời gian chờ**:
   - Nếu video thường mất hơn 2 phút, tăng thời gian chờ trong node **`Wait`** từ 2 phút lên 3-5 phút.

4. **Tạo nhiều phiên bản**:
   - Sau khi có video mới, thêm node **`httpRequest`** để tải video về và lưu vào **Google Drive** hoặc **AWS S3**.
   - Sau đó, dùng node **`set`** để tạo danh sách URL video và chia sẻ cho team.
:::

---

### **📌 Kết luận**
Workflow này là **công cụ mạnh mẽ** giúp content creator và quản lý marketing:
✅ **Tạo video mới từ 1 video gốc** chỉ trong vài phút.
✅ **Phân tích sâu** từng khung hình bằng AI Gemini 2.0.
✅ **Tái tạo nội dung sáng tạo** với mô hình Minimax Video-01.
✅ **Hoạt động tự động** 24/7 trên VPS.

**Hành động ngay!**
- **Import workflow** và thử nghiệm với video Reels của mình.
- **Tích hợp với Slack/Telegram** để nhận thông báo khi video hoàn tất.
- **Tối ưu hóa** bằng cách thêm node lưu log hoặc chia sẻ tự động.

**🚀 Chỉ cần 1 cú nhấp chuột – AI sẽ làm tất cả!**