---
title: "🚀 Tự Động Hóa Tạo Nội Dung AI + Phê Duyệt & Đăng Video Bulk lên Mạng Xã Hội (TikTok, Instagram, YouTube) - Không Cần Code"
description: "Workflow tự động hóa hoàn chỉnh giúp các sếp tải video từ Google Drive, phân tích nội dung bằng AI Gemini, tự động tạo tiêu đề/miêu tả/hashtag riêng cho mỗi nền tảng, lưu draft vào Google Sheets, và chỉ cần phê duyệt là tự động đăng lên TikTok/Instagram/YouTube theo lịch trình. Tiết kiệm 80% thời gian so với cách làm thủ công!"
slug: "tieu-dong-hoa-tao-noi-dung-ai-va-dang-video-bulk"
tags: [n8n, automation, social-media, ai-gemini, google-drive, google-sheets, upload-post]
keywords: [n8n workflow tự động hóa video, đăng video bulk tiktok instagram youtube, ai tạo nội dung social media, tự động hóa marketing digital, google drive google sheets n8n]
---

# 🚀 **Tự Động Hóa Tạo Nội Dung AI + Phê Duyệt & Đăng Video Bulk lên Mạng Xã Hội**

## **💡 Giải Pháp Cho Nỗi Đau Của Các Sếp Marketing**
Hiện nay, việc tạo nội dung video cho TikTok, Instagram Reels và YouTube Shorts thường phải làm thủ công: tải video từ Google Drive, viết tiêu đề/miêu tả/hashtag riêng cho mỗi nền tảng, sau đó đăng lên từng nền tảng một. **Kết quả?**
- **Tốn thời gian**: Mỗi video mất 30-60 phút để chuẩn bị.
- **Không nhất quán**: Nội dung trên mỗi nền tảng khác nhau, khó theo dõi.
- **Không tự động hóa**: Phải nhớ đăng định kỳ, dễ quên hoặc trễ hạn.
- **Không cá nhân hóa**: Tiêu đề/miêu tả chung cho tất cả nền tảng, giảm engagement.

**Workflow này giải quyết tất cả!** Với **AI Gemini Pro**, nó tự động phân tích video và tạo **tiêu đề, miêu tả, hashtag riêng cho TikTok, Instagram và YouTube**. Sau đó, chỉ cần **phê duyệt trên Google Sheets**, nó sẽ tự động đăng lên các nền tảng theo lịch trình đã thiết lập.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 80% thời gian** so với cách làm thủ công.
✅ **Nội dung cá nhân hóa** cho mỗi nền tảng (TikTok, Instagram, YouTube).
✅ **Tự động đăng theo lịch trình** (không cần nhớ).
✅ **Phê duyệt đơn giản** trên Google Sheets (chỉ cần đổi trạng thái từ "draft" sang "approved").
✅ **Duy trì nhất quán** với AI phân tích video và tạo nội dung chuyên nghiệp.
✅ **Hoạt động 24/7** (không cần can thiệp người).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google** (để kết nối Google Drive, Google Sheets và Google Gemini API).
2. **Tài khoản Upload-Post** (để đăng video lên TikTok, Instagram, YouTube).
   - [Tải ứng dụng Upload-Post](https://upload-post.com/) và tạo tài khoản.
3. **File Google Drive** chứa video cần đăng (định dạng MP4).
4. **Google Sheet mẫu** (sẽ được hướng dẫn copy).
5. **API Key Google Gemini** (miễn phí trong giới hạn).
6. **Thời gian zone** và **lịch trình đăng** (ví dụ: đăng 3 video/tuần, bắt đầu từ ngày X).
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Cách 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/11638](https://n8n.io/workflows/11638) (chọn "Export as JSON").
2. Trên n8n Editor, nhấn **"Import"** và chọn file JSON vừa tải.
3. Chọn **"Import"** để hoàn tất.

#### **Cách 2: Copy/Paste JSON**
1. Copy toàn bộ JSON từ [n8n.io/workflows/11638](https://n8n.io/workflows/11638) (chọn "Export as JSON").
2. Trên n8n Editor, nhấn **"Import"** > **"Paste JSON"**.
3. Chọn **"Import"** để hoàn tất.

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **2 Flow chính**:
- **Flow 1**: Tải video từ Google Drive → Phân tích bằng AI → Tạo nội dung → Lưu draft vào Google Sheets.
- **Flow 2**: Kiểm tra Google Sheets mỗi 15 phút → Nếu trạng thái = "approved" → Tải video và đăng lên các nền tảng.

#### **🔹 Cấu Hình Cần Thiết Trong Flow 1**
| **Node**               | **Lưu Ý Cần Chỉnh**                                                                 | **Tham Khảo**                                                                 |
|------------------------|------------------------------------------------------------------------------------|------------------------------------------------------------------------------|
| **Start Campaign**     | Chọn **"Form Trigger"** để bắt đầu workflow.                                      | -                                                                           |
| **Campaign Settings**  | Điền thông tin:                                                                     |                                                                              |
| - Drive Folder ID      | ID của folder Google Drive chứa video (lấy từ liên kết folder).                 | Ví dụ: `1AbCdEfGhIjKlMnOpQrStUvWxYz` (trong `https://drive.google.com/drive/folders/1AbCdEfGhIjKlMnOpQrStUvWxYz`) |
| - Upload-Post Username | Tên tài khoản Upload-Post (để đăng video).                                       | Lấy từ ứng dụng Upload-Post.                                                |
| - Platforms Enabled    | Chọn nền tảng muốn đăng (TikTok, Instagram, YouTube).                            |                                                                              |
| - Timezone             | Chọn múi giờ của doanh nghiệp (ví dụ: `Asia/Ho_Chi_Minh`).                          | [Danh sách múi giờ](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones). |
| - Start Date           | Ngày bắt đầu đăng video.                                                          | Ví dụ: `2024-07-01`.                                                        |
| - Cadence              | Lịch trình đăng (ví dụ: `3 videos/week`).                                         |                                                                              |
| - Publish Hour         | Giờ đăng video (ví dụ: `18:00`).                                                  |                                                                              |
| - Sheet ID             | ID của Google Sheet mẫu (sẽ được hướng dẫn copy).                              |                                                                              |
| **Fetch Videos from Drive** | Chọn **credentials**: `googleDriveOAuth2Api`.                                  | -                                                                           |
| **Video Files Only**   | Node **Filter** này sẽ giữ lại chỉ video (loại bỏ file khác).                   | -                                                                           |
| **AI Video Analysis**  | Chọn **credentials**: `googlePalmApi` (API Key Google Gemini).                     | -                                                                           |
| **Generate Social Copy** | Node **Agent** này sẽ tạo tiêu đề/miêu tả/hashtag cho mỗi nền tảng.          | -                                                                           |
| **Gemini Pro**         | Chọn **credentials**: `googlePalmApi`.                                            | -                                                                           |
| **Structured Output Parser** | Đảm bảo output là JSON đúng định dạng.          | -                                                                           |
| **Save Draft to Sheet** | Chọn **credentials**: `googleSheetsOAuth2Api`.                                   | -                                                                           |
| - Sheet Name           | Tên sheet trong Google Drive (ví dụ: `VideosTable`).                              |                                                                              |

#### **🔹 Cấu Hình Cần Thiết Trong Flow 2**
| **Node**               | **Lưu Ý Cần Chỉnh**                                                                 | **Tham Khảo**                                                                 |
|------------------------|------------------------------------------------------------------------------------|------------------------------------------------------------------------------|
| **15 mins check**      | Node **Schedule Trigger** này chạy mỗi 15 phút để kiểm tra Google Sheets.         | -                                                                           |
| **Only Approved**      | Node **Filter** này chỉ lấy video có trạng thái = `"approved"`.                    | -                                                                           |
| **Schedule TikTok/Instagram/YouTube** | Chọn **credentials**: `uploadPostApi`.          | -                                                                           |
| - Upload-Post Profile  | Chọn profile Upload-Post đã cấu hình.                                             |                                                                              |
| **Mark as Scheduled** | Cập nhật trạng thái từ `"approved"` sang `"scheduled"` khi đăng thành công.      | -                                                                           |

---

### **3. Kích Hoạt ⚡️**
1. **Test Run với dữ liệu mẫu**:
   - Nhấn **"Run Workflow"** và điền thông tin mẫu vào form.
   - Kiểm tra Google Sheets xem draft được tạo không.
   - Đổi trạng thái từ `"draft"` sang `"approved"` và chờ Flow 2 đăng video.

2. **Bật Active Workflow**:
   - Sau khi kiểm tra thành công, nhấn **"Active"** để workflow chạy tự động.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[TIPS THỰC TẾ]
🔹 **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram** để thông báo khi video được đăng thành công.
   - Ví dụ: Sau khi đăng video, gửi tin nhắn: *"Video [Tên Video] đã đăng lên TikTok/Instagram/YouTube!"*.

🔹 **Lưu log hoạt động**:
   - Thêm node **Google Sheets** hoặc **Google Drive** để lưu lịch sử hoạt động (thành công/thất bại).

🔹 **Báo cáo định kỳ**:
   - Sử dụng node **Google Sheets** để tạo báo cáo thống kê (số video đăng, engagement, thời gian đăng).

🔹 **Tự động tạo thumbnail**:
   - Nếu video dài, có thể thêm node **AI Image Generator** (ví dụ: DALL·E) để tạo thumbnail tự động.

🔹 **Phân tích hiệu quả**:
   - Kết hợp với **Google Analytics** hoặc **Upload-Post Analytics** để theo dõi performance.
:::

---

## 📌 **Kết Luận**
Workflow này là **giải pháp hoàn chỉnh** cho các sếp marketing muốn tự động hóa toàn bộ quy trình từ **tải video → tạo nội dung AI → phê duyệt → đăng bulk lên TikTok/Instagram/YouTube**. **Không cần code, không cần chuyên gia AI**, chỉ cần cấu hình đúng như hướng dẫn.

**🚀 Hành động ngay!**
1. **Chuẩn bị tài khoản** (Google Drive, Google Sheets, Upload-Post, Google Gemini).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Test run** và bật **Active** để tự động hóa ngay!

**🎁 Đăng ký VPS TinoHost để chạy n8n 24/7 (Self-hosted):**
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

**🔗 Xem workflow gốc:** [n8n.io/workflows/11638](https://n8n.io/workflows/11638)
**📝 Tác giả:** [Juan Carlos Cavero Gracia](https://www.linkedin.com/in/juan-carlos-cavero-gracia/) (LinkedIn)

---
**💬 Cần hỗ trợ? Hãy để lại comment bên dưới!**