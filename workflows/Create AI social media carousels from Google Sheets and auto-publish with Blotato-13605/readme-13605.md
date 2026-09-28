---
title: "🎨 Tự Động Hóa Tạo Carousel AI + Đăng Bài Tự Động Trên Instagram, Facebook & X (Không Cần Code)"
description: "Workflow tự động hóa hoàn chỉnh từ dữ liệu Google Sheets đến tạo carousel AI với Gemini, định hướng sáng tạo bằng Claude, và đăng bài tự động trên 3 nền tảng xã hội. Giảm thời gian thiết kế từ 60 phút xuống 0 phút, với chi phí chỉ ~50k/carousel."
slug: "tieu-dong-hoa-tao-carousel-ai-va-dang-bai-tu-dong"
tags: [n8n, automation, ai-content-creation, social-media-automation, google-sheets, blotato, gemini, claude-ai]
keywords: [n8n workflow carousel ai, tự động hóa tạo carousel instagram, gemini api n8n, claude ai cho content creation, blotato n8n, tự động đăng bài facebook instagram]
---

# **🚀 Tự Động Hóa Tạo Carousel AI + Đăng Bài Tự Động Trên Instagram, Facebook & X (Không Cần Code)**

### **Giải pháp hoàn chỉnh cho các sếp marketing, content creator, hoặc doanh nghiệp muốn tiết kiệm 100% thời gian thiết kế và đăng bài trên mạng xã hội**

---
### **🎯 Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 60 phút/tháng** cho mỗi carousel: Không cần thiết kế, export, upload, hoặc đăng bài thủ công.
- **Chất lượng chuyên nghiệp** với carousel AI sinh động, đồng nhất về phong cách, và tối ưu hóa cho từng nền tảng.
- **Tự động hóa hoàn chỉnh**: Từ dữ liệu Google Sheets đến đăng bài trên Instagram, Facebook, và X (Twitter) chỉ với một workflow.
- **Chi phí thấp**: ~50k/carousel (tính cả AI và API), so với chi phí thuê designer hoặc mua template.
- **Cá nhân hóa cao**: Hỗ trợ tự động lấy thông tin sản phẩm từ URL, tạo mô tả và hình ảnh phù hợp với từng sản phẩm.
- **Hoạt động 24/7**: Khả năng chạy tự động theo lịch (dựa trên cột `Post Hour` trong Google Sheets).
:::

---
### **🔧 Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** với quyền **read/write** và một bảng dữ liệu có cấu trúc như sau:
   | Brand Logo URL | Product URL | Product Description | Product Image(s) URL | Specification | Post Date | Post Hour | Socials | Status | Post URL |
   |----------------|-------------|---------------------|----------------------|---------------|-----------|-----------|----------|---------|----------|
   - **Lưu ý**:
     - Để trống cột `Product Description` và `Product Image(s) URL` để workflow tự động lấy thông tin từ `Product URL`.
     - Cột `Socials`: Nhập các nền tảng cần đăng bài, cách nhau bởi dấu phẩy (ví dụ: `instagram,facebook,x`).
     - Cột `Post Hour`: Nhập `now` để đăng tức thì hoặc thời gian cụ thể (ví dụ: `14:00`).
     - Cột `Status`: Để trống để workflow tự động cập nhật trạng thái sau khi đăng bài.

2. **API Keys và Credentials**:
   - **Google Sheets OAuth 2.0 API Key**: Để đọc và cập nhật dữ liệu.
   - **Anthropic API Key** (Claude AI): Để tạo định hướng sáng tạo (copy và hệ thống hình ảnh).
   - **Google AI / Gemini API Key**: Để sinh ảnh cho carousel.
   - **Blotato API Key**: Để upload media và đăng bài trên Instagram, Facebook, và X.
   - *(Tùy chọn)* **Telegram Bot Token**: Để nhận thông báo khi workflow hoàn thành.

3. **Blotato Profile IDs**:
   - Các sếp cần thiết lập **Profile IDs** cho từng nền tảng (Instagram, Facebook, X) trong Blotato để workflow biết đăng bài lên đâu.

---
### **🚀 Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Bước 1**: Tải workflow từ [n8n.io/workflows/13605](https://n8n.io/workflows/13605) hoặc copy JSON từ file `.json`.
- **Bước 2**: Mở **n8n Editor** và chọn **Import Workflow** (hoặc **Create New Workflow** và paste JSON).
- **Bước 3**: Chọn **Active** để kích hoạt workflow (sau khi cấu hình xong).

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **4 bước chính**, các sếp cần chú ý cấu hình các node sau:

##### **🔹 Bước 1: Fetch Product Data & Prepare Content**
- **Node `Get Rows` (Google Sheets)**:
  - Chọn **credentials**: `googleSheetsOAuth2Api`.
  - Đặt **Sheet Name** và **Range** (ví dụ: `Sheet1!A1:J100`).
  - **Lưu ý**: Cột `Status` phải trống để workflow biết cần xử lý.

- **Node `Has Description?` (If)**:
  - Kiểm tra xem cột `Product Description` có trống không. Nếu trống, workflow sẽ tự động lấy thông tin từ `Product URL` bằng **Jina.ai**.

##### **🔹 Bước 2: AI Creative Direction & Image Preparation**
- **Node `Scrape Product` (Jina.ai)**:
  - Điền **API Key** trong `credentials`: `jinaAiApi`.
  - **Lưu ý**: Node này sẽ lấy mô tả và hình ảnh từ `Product URL` nếu cột `Product Description` trống.

- **Node `Basic LLM Chain` (Claude AI)**:
  - Chọn **model**: `claude-sonnet-4-5-20250929` (đã cấu hình sẵn).
  - **Prompt**: Workflow sẽ tự động tạo hệ thống hình ảnh và copy cho carousel dựa trên dữ liệu sản phẩm.
  - **Lưu ý**: Các sếp có thể chỉnh sửa **system prompt** trong node này để thay đổi phong cách carousel (ví dụ: chuyên nghiệp, trẻ trung, minimalist...).

- **Node `Nano Banana Pro` (Gemini API)**:
  - Chọn **credentials**: `googlePalmApi`.
  - **Lưu ý**: Node này sẽ sinh ảnh cho carousel. Các sếp cần đảm bảo API Key có đủ credit.

##### **🔹 Bước 3: Generate Slides with Visual Consistency Loop**
- **Node `Loop Over Items` (Split in Batches)**:
  - Workflow sẽ tạo **3 slide** (có thể chỉnh sửa trong prompt Claude).
  - **Node `Add Previous Slides` (Code)**: Đảm bảo các slide có tính đồng nhất về phong cách.

- **Node `Convert to File`**:
  - Chuyển dữ liệu ảnh thành file binary để upload lên Blotato.

##### **🔹 Bước 4: Publish**
- **Node `Switch`**:
  - Chọn **credentials**: `blotatoApi`.
  - **Lưu ý**: Cấu hình **Profile IDs** cho từng nền tảng (Instagram, Facebook, X) trong cột `Socials` của Google Sheets.

- **Node `instagram`, `facebook`, `x` (Blotato)**:
  - Workflow sẽ đăng bài lên các nền tảng đã chọn.

- **Node `Set Processing` (Google Sheets)**:
  - Cập nhật cột `Status` thành `Done` và `Post URL` vào Google Sheets.

#### **3. Kích hoạt ⚡️**
- **Test Run**:
  - Chọn **Execute Workflow** và nhập **1 row** từ Google Sheets để kiểm tra.
  - Kiểm tra các slide được tạo và đăng bài có đúng không.
- **Bật Active**:
  - Sau khi test thành công, chuyển workflow sang **Active** và chọn **Schedule Trigger** để chạy tự động theo lịch.

---
### **✍️ Mẹo & gợi ý nâng cao**
:::info[CÁCH TĂNG CƯỜNG HIỆU QUẢ]
1. **Thay đổi AI Model**:
   - Thay thế **Claude Sonnet** bằng **Claude Instant** (rẻ hơn) trong node `Anthropic Chat Model`.
   - Thay đổi **Gemini Pro** bằng **Gemini Nano** (nếu muốn tiết kiệm chi phí).

2. **Tăng số lượng slide**:
   - Chỉnh sửa **system prompt** trong node `Basic LLM Chain` để yêu cầu thêm slide (ví dụ: 5 slide thay vì 3).

3. **Thêm bước xác nhận**:
   - Chèn **node `Wait`** giữa bước tạo carousel và đăng bài để người dùng xác nhận trước khi đăng.

4. **Lưu log hoạt động**:
   - Thêm **node `Set`** sau `Blotato Upload` để lưu thông báo thành công/lỗi vào Google Sheets.

5. **Tích hợp Telegram Bot**:
   - Thêm **node `httpRequest`** để gửi thông báo khi workflow hoàn thành.

6. **Chuyển đổi hosting hình ảnh**:
   - Thay thế **Blotato Upload** bằng **Cloudinary** hoặc **AWS S3** nếu muốn tự quản lý media.

7. **Tự động hóa theo lịch**:
   - Sử dụng **node `scheduleTrigger`** để chạy workflow vào thời gian cụ thể (ví dụ: 8h sáng hàng ngày).
:::

---
### **💰 Chi phí ước tính (theo 1 carousel)**
| Dịch vụ               | Chi phí (tính theo token/API call) | Chi phí ước tính (VND) |
|-----------------------|-----------------------------------|------------------------|
| **Claude (creative direction)** | ~8K tokens                     | ~20.000 VND            |
| **Gemini (3 slide images)**      | ~3 API calls                    | ~30.000 VND            |
| **Blotato (upload + publish)**   | Phụ thuộc plan                 | ~10.000 VND            |
| **Tổng**               |                                   | **~60.000 VND**        |

---
### **📌 Kết luận**
Workflow này là **giải pháp hoàn chỉnh** để các sếp tự động hóa **tất cả quy trình tạo và đăng bài carousel** trên mạng xã hội, từ lấy dữ liệu đến sinh ảnh AI và đăng bài tự động. Với chi phí thấp và hiệu quả cao, các sếp có thể **tiết kiệm thời gian, nâng cao chất lượng nội dung, và mở rộng hoạt động marketing một cách dễ dàng**.

**🚀 Hành động ngay**:
1. **Cài đặt n8n trên VPS** để workflow chạy 24/7 (khuyến nghị dùng [TinoHost](https://tino.vn/vps-n8n?affid=388) với mã giảm giá **VPSN8N**).
2. **Import workflow** và cấu hình các API Key.
3. **Test với 1-2 row** trước khi kích hoạt chế độ tự động.
4. **Bắt đầu tự động hóa** và giảm thiểu công việc thủ công!

---
**🔗 Tài liệu tham khảo**:
- [Tutorial chi tiết trên YouTube (NoCodeHack)](https://youtube.com/@nocodehack)
- [Blotato API Docs](https://blotato.com/docs)
- [Google AI / Gemini API](https://ai.google.dev)

**📩 Liên hệ hỗ trợ**:
- [LinkedIn: ing.Seif](https://www.linkedin.com/in/ing-seif/)
- [YouTube: NoCodeHack](https://youtube.com/@nocodehack)