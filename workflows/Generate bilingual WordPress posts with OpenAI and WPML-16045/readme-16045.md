---
title: "🌍 Tự Động Hóa Sáng Tạo Bài Blog WordPress Song Ngữ Với OpenAI & WPML (Không Cần Code)"
description: "Workflow này tự động tạo bài viết blog WordPress song ngữ (Việt-English) bằng AI OpenAI, kết nối với WPML, tạo hình ảnh bìa AI và gán tự động - tiết kiệm 80% thời gian so với thủ công."
slug: "tieu-dong-hoa-tao-bai-blog-song-ngu-wordpress-openai-wpml"
tags: [n8n, automation, content-creation, ai-multimodal, wordpress, wpml, openai, no-code]
keywords: [tự động hóa blog song ngữ, n8n workflow wordpress, tạo bài viết blog bằng ai, wpml automation, openai chatgpt wordpress, tự động hóa nội dung đa ngôn ngữ]
---

# 🚀 **Tự Động Hóa Sáng Tạo Bài Blog WordPress Song Ngữ Với OpenAI & WPML**

## **📌 Giới Thiệu: Giải Pháp Cho Người Sáng Tạo Nội Dung Đa Ngôn Ngữ**
Bạn là một **nhà quản trị website, blogger, hoặc chuyên gia marketing** phải viết bài blog cho **hai ngôn ngữ (Việt-English) hàng tuần**? Hoặc bạn đang **phải duy trì nội dung song ngữ** cho website quốc tế nhưng lại **khó khăn với thời gian và chính xác**? Workflow này sẽ **tự động hóa toàn bộ quy trình** từ **sáng tạo nội dung** đến **cập nhật hình ảnh bìa** trên WordPress, giúp bạn **tiết kiệm 80% thời gian** và **giảm thiểu lỗi nhân sự**.

Với **OpenAI GPT-5 Mini** và **WPML**, workflow này sẽ:
✅ **Tạo bài viết song ngữ** (Việt-English) một lần, tự động phân tách sang hai ngôn ngữ.
✅ **Tạo hình ảnh bìa AI** phù hợp với tiêu đề bài viết.
✅ **Tự động đăng bài** lên WordPress và **gắn liên kết dịch** thông qua WPML.
✅ **Cập nhật hình ảnh bìa** cho cả hai phiên bản ngôn ngữ.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** so với viết thủ công.
- **Chính xác 100%** với AI OpenAI, không lo sai ngữ pháp hay nội dung.
- **Hoạt động 24/7** mà không cần can thiệp của con người.
- **Cá nhân hóa hình ảnh bìa** theo tiêu đề bài viết.
- **Tích hợp hoàn hảo với WPML**, không cần viết mã.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản OpenAI** (đăng ký [tại đây](https://platform.openai.com/)) và **API Key**.
2. **WordPress + WPML** đã cài đặt và hoạt động.
3. **Endpoint tùy chỉnh WPML** để liên kết bài viết song ngữ (xem hướng dẫn dưới đây).
4. **Thư viện hình ảnh** (nếu muốn sử dụng hình ảnh từ bên ngoài).
5. **Tài khoản VPS** (n8n Self-hosted) để workflow chạy 24/7 (khuyến nghị sử dụng **VPS TinoHost** hoặc **BNIX**).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể **import workflow từ file JSON** hoặc **copy/paste JSON** vào **n8n Editor**.

#### **Bước 1: Tải workflow từ n8n.io**
- Truy cập [link workflow gốc](https://n8n.io/workflows/16045).
- Nhấn **Export** để tải file JSON về máy.

#### **Bước 2: Import vào n8n**
- Mở **n8n Editor** (trên VPS hoặc n8n.io).
- Nhấn **Import** và chọn file JSON vừa tải.

---
### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **12 node**, các sếp cần **cấu hình cẩn thận** các phần sau:

#### **🔹 Node 1: Manual Trigger (Bắt Đầu Tự Động)**
- **Không cần chỉnh sửa**, chỉ cần kích hoạt workflow khi cần.

#### **🔹 Node 2: Set Prompt Context (Cấu Hình Prompt AI)**
- **Tham số quan trọng**:
  - **Prompt**: Đặt nội dung bài viết, ngôn ngữ (Việt-English), cấu trúc bài viết (tiêu đề, nội dung, hình ảnh).
  - **Dữ liệu mẫu**:
    ```json
    {
      "title_it": "Tiêu đề bài viết tiếng Việt",
      "title_en": "English blog post title",
      "content_it": "Nội dung bài viết tiếng Việt...",
      "content_en": "English blog post content..."
    }
    ```
- **Lưu ý**: Cần **điền đầy đủ thông tin** về cấu trúc bài viết để AI sinh ra nội dung chính xác.

#### **🔹 Node 3-12: Tương Tác Với WordPress & OpenAI**
Các node này **sử dụng API WordPress và OpenAI**, các sếp cần:
1. **Thiết lập credentials**:
   - **openAiApi**: Điền **API Key** từ OpenAI.
   - **wordpressApi**: Điền **URL WordPress** và **credentials** (API Key hoặc JWT).
2. **Cấu hình URL WordPress**:
   - Thay thế tất cả `https://YOUR_URL` trong các node `httpRequest` bằng **URL thực của website WordPress**.
3. **Cấu hình WPML**:
   - **Endpoint `/wp-json/custom/v1/link-translation`** phải hoạt động (xem hướng dẫn PHP dưới đây).

---
### **3. Kích Hoạt ⚡️**
#### **Bước 1: Test Run Dữ Liệu Mẫu**
- Chạy **Manual Trigger** và kiểm tra:
  - AI có sinh ra **bài viết song ngữ** không?
  - **Hình ảnh bìa** có được tạo và upload lên WordPress không?
  - **Bài viết** có được đăng và liên kết song ngữ không?

#### **Bước 2: Bật Active Workflow**
- Sau khi kiểm tra thành công, **bật Active** để workflow chạy tự động.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Tích Hợp Slack/Telegram**:
   - Sau khi tạo bài viết, gửi thông báo lên **Slack/Telegram** để các sếp biết workflow đã hoàn thành.
   - **Cách làm**: Thêm node **Slack Webhook** hoặc **Telegram Bot** vào workflow.

2. **Lưu Log & Báo Cáo**:
   - Sử dụng **Google Sheets** hoặc **Airtable** để lưu lịch sử bài viết đã tạo.
   - **Cách làm**: Thêm node **Google Sheets** sau khi bài viết được đăng.

3. **Tự Động Chọn Ngôn Ngữ**:
   - Nếu website hỗ trợ nhiều ngôn ngữ hơn 2, có thể **tự động phân tách nội dung** sang nhiều ngôn ngữ bằng cách **cập nhật prompt**.

4. **Tối Ưu Hình Ảnh Bìa**:
   - Thay đổi **prompt tạo hình ảnh** để phù hợp với **ngôn ngữ hoặc chủ đề** bài viết.
   - Ví dụ:
     ```json
     "prompt": "Generate a realistic photo for a blog post cover about {{ $('Generate Article Text').item.json.output.title_it }}, photography, 8K resolution, cinematic lighting"
     ```
:::

---
## **📌 Hướng Dẫn Cài Đặt Endpoint WPML (PHP)**
Để **liên kết bài viết song ngữ** tự động, các sếp cần thêm **mã PHP** vào file `functions.php` của theme WordPress.

### **Bước 1: Thêm Endpoint Tùy Chỉnh**
```php
add_action('rest_api_init', function () {
    register_rest_route('custom/v1', '/link-translation', [
        'methods' => 'POST',
        'callback' => 'ew_link_translation',
        'permission_callback' => '__return_true'
    ]);
});

function ew_link_translation($request) {
    $post_it = intval($request->get_param('post_it'));
    $post_en = intval($request->get_param('post_en'));

    if (!$post_it || !$post_en) {
        return new WP_Error('missing_data', 'post_it và post_en bắt buộc', ['status' => 400]);
    }

    if (!get_post($post_it) || !get_post($post_en)) {
        return new WP_Error('invalid_post', 'Một trong hai bài viết không tồn tại', ['status' => 404]);
    }

    if (!has_filter('wpml_element_trid')) {
        return new WP_Error('wpml_missing', 'WPML không hoạt động', ['status' => 500]);
    }

    $element_type = 'post_post';
    $trid = apply_filters('wpml_element_trid', null, $post_it, $element_type);

    if (!$trid) {
        do_action('wpml_set_element_language_details', [
            'element_id' => $post_it,
            'element_type' => $element_type,
            'trid' => false,
            'language_code' => 'vi', // Thay 'it' thành 'vi' cho Việt Nam
            'source_language_code' => null
        ]);

        $trid = apply_filters('wpml_element_trid', null, $post_it, $element_type);
    }

    do_action('wpml_set_element_language_details', [
        'element_id' => $post_it,
        'element_type' => $element_type,
        'trid' => $trid,
        'language_code' => 'vi', // Ngôn ngữ 1 (Việt)
        'source_language_code' => null
    ]);

    do_action('wpml_set_element_language_details', [
        'element_id' => $post_en,
        'element_type' => $element_type,
        'trid' => $trid,
        'language_code' => 'en', // Ngôn ngữ 2 (English)
        'source_language_code' => 'vi'
    ]);

    return [
        'success' => true,
        'trid' => $trid,
        'post_it' => $post_it,
        'post_en' => $post_en
    ];
}
```
- **Lưu ý**:
  - Thay `it` thành `vi` nếu ngôn ngữ chính là **Việt Nam**.
  - Nếu muốn thêm ngôn ngữ khác, **cập nhật `language_code`** tương ứng.

---
## **🎥 Học Từ Nguồn Gốc**
Nếu muốn **hiểu sâu hơn về workflow**, các sếp có thể xem **bài giảng của Davide Boizza** trên [YouTube](https://youtube.com/@n3witalia):
👉 [Subscribe để không bỏ lỡ tutorial mới](https://youtube.com/@n3witalia)

---
## **📌 Kết Luận: Áp Dụng Ngay Hôm Nay!**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **strategy marketing** thay vì **viết bài blog thủ công**. Với **AI OpenAI + WPML**, nội dung song ngữ **chính xác, nhanh chóng và tự động hóa hoàn toàn**.

**Bắt đầu ngay!**
1. **Import workflow** vào n8n.
2. **Cấu hình OpenAI & WordPress**.
3. **Test và kích hoạt**.

🚀 **Hãy tự động hóa nội dung của mình ngay hôm nay!** 🚀