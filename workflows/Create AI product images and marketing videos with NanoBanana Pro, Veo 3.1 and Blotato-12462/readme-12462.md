---
title: "🎨 Tự Động Hóa Sáng Tạo Hình Ảnh & Video Marketing AI với NanoBanana Pro, Veo 3.1 & Blotato (N8N)"
description: "Workflow tự động hóa 100% không code để chuyển đổi hình ảnh sản phẩm thành video marketing AI, xuất bản tự động trên YouTube/TikTok/Instagram. Giảm thời gian sản xuất từ 8h xuống 5 phút!"
slug: "tieu-dong-hoa-sang-tao-hinh-anh-video-marketing-ai"
tags: [n8n, automation, ai-image-generation, video-marketing, no-code, nano-banana-pro, veo-3-1, blotato, google-sheets, openai]
keywords: [n8n workflow tự động hóa hình ảnh video, tạo video marketing AI, nano banana pro n8n, veo 3.1 tự động hóa, xuất bản video blotato, tự động hóa marketing sản phẩm]
---

# 🚀 **Tự Động Hóa Sáng Tạo Hình Ảnh & Video Marketing AI với NanoBanana Pro, Veo 3.1 & Blotato**

Hãy tưởng tượng một ngày mà các sếp chỉ cần **nhấp chuột** là hệ thống tự động:
✅ **Tạo 6 phiên bản hình ảnh sản phẩm** với góc nhìn khác nhau (top-left, top-right, bottom-center...)
✅ **Chuyển đổi hình ảnh thành video marketing AI** với động tác camera tự nhiên
✅ **Xuất bản video lên YouTube/TikTok/Instagram** một cách tự động
✅ **Cập nhật dữ liệu vào Google Sheets** để theo dõi toàn bộ quá trình

**Workflow này giải quyết hoàn toàn vấn đề thủ công, tốn thời gian và không nhất quán** trong việc tạo nội dung marketing cho sản phẩm. Thay vì mất **8 giờ** để tạo 1 video marketing thủ công, các sếp chỉ cần **5 phút** để hệ thống tự động hoàn thành toàn bộ quy trình!

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Giảm 90% thời gian sản xuất nội dung marketing.
- **Chất lượng cao**: Hình ảnh và video được tạo bởi AI với độ chính xác cao.
- **Tự động hóa hoàn chỉnh**: Từ hình ảnh đầu vào đến xuất bản video trên mạng xã hội.
- **Cá nhân hóa**: Tạo nhiều phiên bản hình ảnh và video khác nhau từ 1 input.
- **Theo dõi dễ dàng**: Dữ liệu được cập nhật tự động vào Google Sheets.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản và API Key**:
   - [NanoBanana Pro](https://fal.ai/) (API endpoint: `https://fal.ai/models/fal-ai/nano-banana-pro/edit/api`)
   - [Veo 3.1](https://fal.ai/) (API endpoint: `https://fal.ai/models/fal-ai/veo3.1/first-last-frame-to-video`)
   - [Blotato](https://blotato.com/) (Đăng ký với mã giới thiệu: `firas`)
   - [Google Sheets](https://docs.google.com/spreadsheets) (Sử dụng [bảng mẫu này](https://docs.google.com/spreadsheets/d/130hio-ntnPCZbGzmp1R3ROHXSpKQBUC0I_iM0uQPPi4/copy))
   - [OpenAI API](https://platform.openai.com/) (Để phân tích hình ảnh và tạo prompt)

2. **Credentials trong n8n**:
   - **HTTP Request (Bearer Token)**: NanoBanana Pro & Veo 3.1
   - **Blotato API**: Tên credential `Blotato account`
   - **Google Sheets OAuth2**: Tên credential `Google Sheets account`
   - **OpenAI API**: Tên credential `openAiApi`

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải file JSON từ [đây](https://n8n.io/workflows/12462) hoặc sao chép toàn bộ JSON từ link trên.
2. Mở **n8n Editor** và nhấp vào **Import** → Dán JSON và nhấn **Import**.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **72 node** và được chia thành 3 phần chính: **Tạo hình ảnh**, **Tạo video**, và **Xuất bản video**. Dưới đây là các bước cấu hình quan trọng:

#### **A. Cấu hình NanoBanana Pro (Tạo hình ảnh)**
1. **Node "NanoBanana: Create Image"**:
   - Điền **API Key** của NanoBanana Pro vào `Authorization` header.
   - Cấu hình **prompt** để tạo hình ảnh sản phẩm (ví dụ: `A high-quality product image of a smartphone, realistic, 8K, cinematic lighting`).
   - Thêm tham số `width=1024` và `height=1024` để đảm bảo độ phân giải cao.

2. **Node "Crop Top Left/Top Center/..."**:
   - Các node này sẽ **crop** hình ảnh thành 6 phiên bản khác nhau.
   - Đảm bảo **tham số `x`, `y`, `width`, `height`** được cấu hình chính xác theo tỉ lệ mong muốn (ví dụ: `x=0`, `y=0`, `width=512`, `height=512` cho `Top Left`).

3. **Node "Upload to Google Drive"**:
   - Chọn **credentials** `googleDriveOAuth2Api` đã cấu hình trước.
   - Đặt tên file theo định dạng: `product_{product_id}_top_left.jpg`.

#### **B. Cấu hình Veo 3.1 (Tạo video)**
1. **Node "Veo Generation"**:
   - Điền **API Key** của Veo 3.1 vào `Authorization` header.
   - Cấu hình **prompt** để tạo video (ví dụ: `A dynamic product showcase video, 16:9 aspect ratio, smooth camera motion, cinematic lighting`).
   - Thêm tham số `first_frame` và `last_frame` để Veo biết đầu và cuối video.

2. **Node "Merge 3 Videos"**:
   - Đây là bước **ghép 3 video** thành 1 video cuối cùng.
   - Đảm bảo các **URL video** từ Veo được truyền vào node này.

#### **C. Cấu hình Blotato (Xuất bản video)**
1. **Node "Upload Video to BLOTATO"**:
   - Chọn **credentials** `blotatoApi`.
   - Đảm bảo **file video** đã được tải lên trước khi upload.

2. **Node "Youtube"**:
   - Chọn **tài khoản mạng xã hội** muốn xuất bản (YouTube, TikTok, Instagram...).
   - Cấu hình **tiêu đề, mô tả, thẻ** cho video.

#### **D. Cập nhật Google Sheets**
1. **Node "Append row in sheet"**:
   - Chọn **Google Sheets OAuth2** và **bảng mẫu** đã copy.
   - Cấu hình **cột** để lưu trữ:
     - URL hình ảnh (6 phiên bản)
     - URL video
     - Thông tin sản phẩm (ID, tên...)

2. **Node "Update url image_top_left"**:
   - Cập nhật **URL hình ảnh** cho từng phiên bản vào Google Sheets.

---

### **3. Kích hoạt ⚡️**
1. **Test run dữ liệu mẫu**:
   - Nhấp vào **Execute Workflow** và chọn **Manual Trigger**.
   - Đính kèm **1 hình ảnh sản phẩm** vào workflow để test.
   - Kiểm tra kết quả:
     - Hình ảnh đã được crop thành 6 phiên bản.
     - Video đã được tạo và xuất bản.
     - Dữ liệu đã cập nhật vào Google Sheets.

2. **Bật Active workflow**:
   - Sau khi test thành công, chuyển workflow sang **Active**.

---

## ✍️ **Mẹo & gợi ý nâng cao**
1. **Tối ưu hóa prompt**:
   - Sử dụng **OpenAI GPT-4** để tự động tạo prompt cho NanoBanana và Veo.
   - Ví dụ: `Prompt: "Create a product showcase video for {product_name}, highlight feature {feature}, style {style}"`.

2. **Lưu log hoạt động**:
   - Thêm **node `stickyNote`** để ghi lại lỗi hoặc thông tin debug.
   - Ví dụ: `Error: {error.message}` nếu tạo hình ảnh thất bại.

3. **Gửi báo cáo định kỳ**:
   - Sử dụng **node `scheduleTrigger`** để chạy workflow hàng ngày và gửi báo cáo qua **Slack/Email**.
   - Ví dụ: `Gửi báo cáo video mới tạo vào Slack channel #marketing`.

4. **Kết hợp với CRM**:
   - Cập nhật **Google Sheets** vào **CRM** (HubSpot, Salesforce...) để theo dõi hiệu suất video.

---

## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa toàn bộ quy trình từ **tạo hình ảnh đến xuất bản video marketing** một cách nhanh chóng và hiệu quả. Bằng cách sử dụng **NanoBanana Pro, Veo 3.1 và Blotato**, các sếp không chỉ tiết kiệm thời gian mà còn nâng cao **chất lượng nội dung** với độ chính xác cao.

**Hãy áp dụng ngay workflow này và bắt đầu tự động hóa marketing sản phẩm của mình!** 🚀

---
**🔗 [Tải workflow nguyên bản](https://n8n.io/workflows/12462)**
**📖 [Tài liệu chi tiết](https://automatisation.notion.site/Generate-product-images-with-NanoBanana-Pro-to-Veo-videos-and-Blotato-2dc3d6550fd980dc81adea10a5df6b28)**