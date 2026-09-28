---
title: "🚀 Tự Động Hóa Tạo Bài Blog Từ Video YouTube Với ChatGPT, Google Sheets & WordPress (Không Cần Code)"
description: "Workflow tự động hóa hoàn chỉnh chuyển đổi nội dung video YouTube thành bài blog SEO-optimized, tự động tìm ảnh, viết tiêu đề/miêu tả, và đăng tải lên WordPress chỉ trong vài giây. Giúp các sếp tiết kiệm 10+ giờ công mỗi tuần."
slug: "tieu-dong-hoa-tao-bai-blog-tu-video-youtube"
tags: [n8n, automation, content-creation, ai-chatgpt, wordpress, google-sheets, seo]
keywords: [n8n workflow blog, tự động hóa nội dung, chatgpt tạo bài viết, seo tự động, wordpress automation, video to blog]
---

# 🚀 **Tự Động Hóa Tạo Bài Blog Từ Video YouTube Với AI (ChatGPT + WordPress)**

### **Giải pháp cho các sếp muốn:**
- **Tạo nội dung blog từ video YouTube** mà không cần viết tay?
- **Tiết kiệm 10+ giờ công mỗi tuần** cho việc nghiên cứu và viết bài?
- **Tự động hóa toàn bộ chuỗi từ tìm video → viết bài → đăng tải → quảng bá**?
- **Cải thiện SEO** với tiêu đề, miêu tả và nội dung được tối ưu bởi AI?

Workflow này **không chỉ tự động hóa việc chuyển đổi video thành bài viết**, mà còn **tìm ảnh miễn phí từ Pexels**, **tối ưu SEO với YOAST**, và **cập nhật Google Sheets** để theo dõi tiến trình. **Không cần code, chỉ cần copy/paste và chạy!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ cao, phù hợp với AI)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Chuyển đổi video thành bài blog chỉ trong **vài giây** thay vì nhiều giờ.
✅ **Nội dung SEO-optimized**: Tiêu đề, miêu tả và bài viết được **tối ưu bởi AI** (ChatGPT).
✅ **Tự động tìm ảnh**: Sử dụng **Pexels API** để lấy ảnh miễn phí phù hợp với bài viết.
✅ **Quản lý trung tâm**: Tất cả bài viết được **cập nhật vào Google Sheets** để theo dõi.
✅ **Hoạt động liên tục**: **Schedule Trigger** cho phép chạy workflow **tự động hàng ngày**.
✅ **Cá nhân hóa**: **ChatGPT Agent** giúp viết bài theo phong cách riêng của brand.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
### **1. Tài khoản & API Keys**
| Dịch vụ/API | Mô tả | Làm thế nào để lấy? |
|-------------|--------|----------------------|
| **Google Sheets** | Để lưu trữ danh sách video và bài viết | Tạo file Google Sheets mới và chia sẻ cho n8n |
| **WordPress** | Đăng tải bài viết tự động | API Key từ plugin **WP REST API** |
| **ChatGPT (OpenAI)** | Tạo nội dung, tối ưu SEO | [Tạo API Key tại OpenAI](https://platform.openai.com/account/api-keys) |
| **Gmail** | Gửi thông báo lỗi/hoàn thành | Tạo **App Password** nếu sử dụng 2FA |
| **Pexels API** | Tải ảnh miễn phí | [Đăng ký tại Pexels](https://www.pexels.com/api/) |

### **2. File Google Sheets chuẩn**
Workflow yêu cầu **1 file Google Sheets** với **các sheet sau**:
- **`video_db`**: Danh sách video YouTube (cột: `video_url`, `title`, `date_added`).
- **`blog_db`**: Danh sách bài viết đã tạo (cột: `blog_url`, `status`, `keywords`).
- **`keywords_db`**: Danh sách từ khóa (cột: `keyword`, `intent`).

📌 **Mẫu file mẫu**: [Tải template Google Sheets](https://docs.google.com/spreadsheets/d/1EXAMPLE/edit) *(sẽ cập nhật link thực tế sau)*

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/7376](https://n8n.io/workflows/7376) (chọn **Export as JSON**).
2. **Đăng nhập n8n** (self-hosted hoặc n8n.cloud).
3. **Nhấn "Import"** và chọn file JSON vừa tải.
4. **Chọn "Create new workflow"** và đặt tên (ví dụ: `YouTube-to-Blog-Automation`).

#### **Phương pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ JSON** từ [n8n.io/workflows/7376](https://n8n.io/workflows/7376).
2. **Mở n8n Editor** → **Nhấn "Import"** → **Paste JSON** → **Create**.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow có **65 node**, nhưng chỉ **5 node quan trọng** cần cấu hình kỹ lưỡng:

#### **🔹 Node 1: Google Sheets (GET Video Used)**
- **Credentials**: Chọn **Google Sheets** đã tạo trước.
- **Sheet Name**: `video_db`
- **Range**: `A2:D` (đảm bảo cột `video_url` có dữ liệu).

#### **🔹 Node 2: OpenAI (AI Generator Post)**
- **Credentials**: Chọn **OpenAI API Key** đã tạo.
- **Model**: `gpt-4` (hoặc `gpt-3.5-turbo` nếu tiết kiệm chi phí).
- **Prompt**: **Không chỉnh sửa**, để AI tự động viết bài theo cấu trúc đã định.

#### **🔹 Node 3: WordPress (Create a post)**
- **Credentials**: Chọn **WordPress API Key** từ plugin **WP REST API**.
- **Post Type**: `post` (hoặc `page` nếu muốn tạo trang).
- **Status**: `publish` (bài viết sẽ đăng tải ngay).

#### **🔹 Node 4: Pexels (Download Pexels Image)**
- **API Key**: Nhập **API Key Pexels** từ [pexels.com/api](https://www.pexels.com/api/).
- **Query**: `{{$node["GET Video Used"].jsonpath("$.title")}}` (tự động lấy tiêu đề video).

#### **🔹 Node 5: Schedule Trigger**
- **Cron Expression**: `0 0 * * *` (chạy **lúc 00:00 hàng ngày**).
- **Time Zone**: Chọn **UTC** hoặc khu vực phù hợp.

---
### **3. Kích hoạt ⚡️**
1. **Test Run** với **1 video mẫu**:
   - Chọn **Manual Trigger** → Nhập **URL video YouTube**.
   - Kiểm tra **các node quan trọng** (OpenAI, WordPress, Pexels) có hoạt động không.
2. **Bật Active**:
   - Nhấn **Active** trên workflow.
   - **Kiểm tra email** (nếu cấu hình Gmail) để nhận thông báo lỗi.

---

## ✍️ **Mẹo & gợi ý nâng cao**
### **1. Tối ưu SEO thêm bằng YOAST**
Workflow đã tích hợp **meta description & title SEO**, nhưng các sếp có thể:
- **Sử dụng node `meta desc and title gen`** để AI viết lại tiêu đề miêu tả.
- **Kết hợp với plugin All in One SEO** để tự động hóa thêm.

### **2. Gửi báo cáo định kỳ qua Slack/Telegram**
- **Thêm node `httpRequest`** để gửi thông báo khi bài viết được đăng tải.
- **Cấu hình webhook** từ Slack/Telegram vào node này.

### **3. Lọc video theo chủ đề**
- **Thêm node `custom filter`** để chỉ lấy video từ **những channel cụ thể**.
- **Ví dụ**: Chỉ chạy cho video từ **YouTube Channel Marketing**.

### **4. Lưu log hoạt động**
- **Thêm node `stickyNote`** để ghi lại **lịch sử lỗi** và **thành công**.
- **Dùng Google Sheets** để theo dõi **tỉ lệ thành công**.

### **5. Tích hợp với Apify (nếu cần)**
Nếu muốn **tự động tìm video mới** từ YouTube:
- **Sử dụng node `httpRequest`** để gọi API Apify.
- **Cấu hình cron** để chạy **hàng ngày**.

---

## 📌 **Kết luận**
Workflow này **giải phóng các sếp khỏi công việc viết blog thủ công**, đồng thời **tối ưu hóa SEO và tự động hóa toàn bộ quy trình**. **Chỉ cần 5 phút setup**, sau đó **AI sẽ làm tất cả**!

🚀 **Hành động ngay**:
1. **Import workflow** theo hướng dẫn trên.
2. **Cấu hình Google Sheets & API Keys**.
3. **Bật Schedule Trigger** và **đợi AI làm việc**.

**Nếu gặp vấn đề**, để lại comment bên dưới hoặc liên hệ **tôi** để hỗ trợ!

---
**#TựĐộngHóaBlog #ChatGPTTạoNộiDung #WordPressAutomation #SEOAutomated**