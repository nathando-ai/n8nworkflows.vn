---
title: "🚀 Tự Động Hóa & Tạo Bài Quảng Cáo Facebook Hiệu Quả Từ Đối Thủ Sử Dụng AI Gemini + Apify (Không Code)"
description: "Workflow tự động hóa hoàn toàn miễn phí giúp các sếp clone và tùy chỉnh quảng cáo Facebook thành công của đối thủ, thay thế sản phẩm bằng sản phẩm của mình, tiết kiệm thời gian nghiên cứu lên đến 90% và tăng hiệu quả quảng cáo lên 30%."
slug: "tay-dong-hoa-tao-quang-cao-facebook-tu-doi-thu-su-dung-gemini-apify"
tags: [n8n, automation, no-code, content-creation, ai-multimodal, facebook-ads, gemini-ai, apify]
keywords: [n8n workflow quảng cáo facebook, tự động hóa tạo quảng cáo, clone quảng cáo đối thủ facebook, gemini ai tạo hình ảnh, apify scrap facebook ads, tự động hóa marketing không code]
---

# 🚀 **Tự Động Hóa Tạo Quảng Cáo Facebook Hiệu Quả Từ Đối Thủ Sử Dụng AI Gemini + Apify**

## **Nỗi Đau Của Các Sếp Trong Tạo Quảng Cáo Facebook**
Các sếp thường phải mất **từ 5-10 giờ/lần** để:
✅ **Tìm kiếm** quảng cáo hiệu quả của đối thủ trên Facebook
✅ **Phân tích** thiết kế, nội dung và chiến lược của họ
✅ **Tạo bản sao** (clone) với sản phẩm của mình
✅ **Test A/B** nhiều phiên bản khác nhau để tối ưu hóa

Kết quả? **Chỉ có 10-20% thời gian** dành cho việc **tối ưu hóa và triển khai** quảng cáo thực sự hiệu quả.

**Workflow này giải quyết tất cả vấn đề trên bằng cách:**
✔ **Tự động scrape** 20 quảng cáo thành công nhất từ Facebook Ad Library của đối thủ
✔ **Phân tích AI** thiết kế, màu sắc, bố cục và nội dung của họ
✔ **Tạo bản clone** với sản phẩm của bạn, giữ nguyên hiệu quả ban đầu
✔ **Lưu trữ tự động** tất cả tài liệu tham khảo và bản clone lên Google Drive
✔ **Hoàn thành trong 10-30 giây/quảng cáo**, không cần code

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian lên đến 90%** so với phương pháp thủ công
- **Tăng hiệu quả quảng cáo lên 30%** nhờ clone thiết kế thành công của đối thủ
- **Không cần kỹ năng code** – chỉ cần copy/paste và cấu hình nhanh
- **Tự động lưu trữ** tất cả tài liệu tham khảo và bản clone lên Google Drive
- **Hoàn thành nhanh** (10-30 giây/quảng cáo) để test A/B hiệu quả
- **Áp dụng cho nhiều ngành hàng** (eCommerce, SaaS, Dịch vụ, Thương mại điện tử...)
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Apify** (để scrape quảng cáo Facebook)
   - [Đăng ký Apify miễn phí](https://apify.com/)
   - **API Key** (tìm trong **Settings > API > API Token**)
2. **Tài khoản Google Gemini API** (để phân tích và tạo hình ảnh)
   - [Đăng ký Google AI Studio](https://makersuite.google.com/app/apikey)
   - **API Key** (tìm trong **API Key** của Google Cloud)
3. **Tài khoản Google Drive** (để lưu trữ quảng cáo tham khảo và bản clone)
   - [Đăng ký Google Drive](https://drive.google.com/)
   - **OAuth 2.0 Credentials** (cấu hình trong n8n)
4. **URL Facebook Ad Library** của đối thủ (để scrape)
   - Ví dụ: `https://www.facebook.com/[competitor]/ads/?adset_id=[adset_id]`
5. **Hình ảnh sản phẩm** (để thay thế đối thủ trong bản clone)
   - Kích thước khuyến nghị: **1080x1080px**, định dạng **JPEG/PNG**
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow bằng **2 cách**:
- **Tải file JSON** từ [n8n.io/workflows/8415](https://n8n.io/workflows/8415) và import vào n8n Editor.
- **Copy JSON** từ trang trên và dán vào **Import Workflow** trong n8n.

:::note[Lưu ý khi import]
- **Không chỉnh sửa tên node** (nếu không muốn workflow bị lỗi).
- **Không xóa node** (trừ khi hiểu rõ chức năng của nó).
:::

---

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Sau khi import, các sếp cần **cấu hình chi tiết** các node quan trọng:

##### **A. Node `scrape_ads` (Apify)**
- **Credentials**: Chọn `apifyOAuth2Api` (đã cấu hình trước khi import).
- **Parameters**:
  - `actorId`: `facebook-ad-library-scraper` (không cần thay đổi).
  - `startUrl`: Điền **URL Facebook Ad Library** của đối thủ (ví dụ: `https://www.facebook.com/companyX/ads/`).
  - `maxItems`: **20** (lấy tối đa 20 quảng cáo).
  - `runMode`: `runOnce` (chạy một lần duy nhất).

##### **B. Node `generate_ad_image_prompt` & `generate_ad_image` (Gemini AI)**
- **Credentials**: Chọn `httpHeaderAuth` (đã cấu hình trước khi import).
- **Headers**:
  - `Authorization`: `Bearer [API_KEY_GOOGLE_GEMINI]` (thay thế bằng API Key của bạn).
  - `Content-Type`: `application/json`.
- **Body (Request)**:
  ```json
  {
    "model": "gemini-2.5-pro",
    "prompt": "Analyze the competitor ad image and create a detailed prompt for generating a new ad image with my product instead. Keep the original style, colors, and layout."
  }
  ```
  *(Cấu hình chi tiết trong node `build_prompt` sau này.)*

##### **C. Node `build_prompt` (Set)**
- **Expression**:
  ```javascript
  {
    prompt: `Analyze the competitor ad image ({{ $json["image_url"] }}) and create a detailed prompt for generating a new ad image with my product instead. Keep the original style, colors, layout, and text placement. The new image should feature my product: {{ $json["product_image"] }}. The final image should be in 1080x1080 resolution, high quality, and optimized for Facebook ads.`,
    image_url: $node["scrape_ads"]["$nodeHistory[0]["json"]["image_url"]"],
    product_image: $node["convert_product_image_to_base64"]["$nodeHistory[0]["json"]["binary"]"]
  }
  ```

##### **D. Node `upload_ad_reference` & `upload_image` (Google Drive)**
- **Credentials**: Chọn `googleDriveOAuth2Api` (đã cấu hình trước khi import).
- **Folder ID**:
  - **Reference Ads**: `1AbCdEfGhIjKlMnOpQrStUvWxYz` (thay bằng ID folder của bạn).
  - **Generated Ads**: `1AbCdEfGhIjKlMnOpQrStUvWxYz` (thay bằng ID folder khác).
- **File Metadata**:
  - `name`: `competitor_ad_{{ $node["scrape_ads"]["$nodeHistory[0]["json"]["id"]"] }}.jpg`
  - `mimeType`: `image/jpeg`

##### **E. Node `check_if_prohibited` (If)**
- **Condition**:
  ```javascript
  $node["generate_ad_image"]["json"]["prohibited"] === true
  ```
  *(Nếu Gemini AI từ chối tạo hình ảnh, workflow sẽ bỏ qua và chuyển sang quảng cáo tiếp theo.)*

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Điền **URL Facebook Ad Library** và **hình ảnh sản phẩm** vào form trigger.
   - Chạy **Test Execution** để kiểm tra workflow.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, **bật workflow** để tự động chạy khi có dữ liệu mới.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Slack/Telegram Notifications**
   - Sử dụng node **Slack** hoặc **Telegram Bot** để thông báo khi workflow hoàn thành.
   - Cấu hình trong node **Set** trước khi upload image.

2. **Lưu Log Tự Động**
   - Thêm node **Google Sheets** để ghi lại tất cả quảng cáo scrape và clone.
   - Cấu hình trong node **Set** với dữ liệu:
     ```json
     {
       "competitor_ad_id": $node["scrape_ads"]["$nodeHistory[0]["json"]["id"]"],
       "competitor_ad_url": $node["scrape_ads"]["$nodeHistory[0]["json"]["url"]"],
       "generated_ad_url": $node["upload_image"]["$nodeHistory[0]["json"]["url"]"],
       "status": $node["check_if_prohibited"]["json"]["prohibited"] ? "Failed" : "Success"
     }
     ```

3. **Tối Ưu Hóa Prompt AI**
   - Thay đổi **node `build_prompt`** để nhấn mạnh yếu tố nào trong quảng cáo (ví dụ: **màu sắc**, **bố cục**, **nội dung text**).
   - Ví dụ:
     ```javascript
     prompt: `Focus on the color scheme and layout of the competitor ad when generating the new image. The product should be placed in the same position as the competitor's product, but with my branding.`
     ```

4. **Thêm Text Overlay**
   - Sử dụng **node `set`** để thêm **chữ nhấn mạnh** (CTA) vào hình ảnh clone.
   - Ví dụ:
     ```javascript
     {
       "text_overlay": "🔥 MUA NGAY - GIÁ TỐT NHẤT THÁNG 2024! 🔥",
       "font_size": 48,
       "font_color": "#FFFFFF"
     }
     ```

5. **Áp Dụng Cho Nhiều Ngành Hàng**
   - Thay đổi **prompt** để phù hợp với ngành hàng (eCommerce, SaaS, Dịch vụ...).
   - Ví dụ cho **SaaS**:
     ```javascript
     prompt: `Generate a professional ad image for a SaaS product. Keep the minimalist design, clean fonts, and modern color scheme from the competitor ad.`
     ```

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** của các sếp để tập trung vào **strategy và tối ưu hóa quảng cáo** thay vì mất công phân tích và tạo bản clone thủ công.

**Hành động ngay:**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với URL Facebook Ad Library** của đối thủ.
3. **Tải xuống bản clone** và sử dụng trong chiến dịch A/B test.

**Kết quả?** **Quảng cáo hiệu quả hơn 30% chỉ trong vài phút!**

---
🔗 **Xem video hướng dẫn chi tiết** của tác giả Lucas Walter:
[🎥 YouTube: Clone & Customize Competitor Facebook Ads with Gemini AI and Apify](https://www.youtube.com/watch?v=example)

💡 **Cần hỗ trợ?** Đăng câu hỏi trên [Community n8n](https://community.n8n.io/) hoặc liên hệ tác giả qua [LinkedIn](https://www.linkedin.com/in/lucaswalter/).