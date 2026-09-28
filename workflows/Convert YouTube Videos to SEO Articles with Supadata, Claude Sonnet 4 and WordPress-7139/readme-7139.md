---
title: "🚀 Chuyển Video YouTube Sang Bài Văn Bản SEO Tự Động Với Claude Sonnet 4 & WordPress (Không Cần Code)"
description: "Tự động hóa chuyển đổi video YouTube thành bài viết SEO chất lượng cao với AI Claude Sonnet 4, Supadata và WordPress - tiết kiệm 80% thời gian viết nội dung."
slug: "chuyen-video-youtube-sang-bai-van-ban-seo-tu-dong"
tags: [n8n, automation, content-creation, ai-multimodal, seo, wordpress, youtube]
keywords: [n8n workflow youtube seo, tự động hóa bài viết từ video, claude sonnet 4 n8n, convert video to article, seo automation]
---

# 🚀 Chuyển Video YouTube Sang Bài Văn Bản SEO Tự Động Với Claude Sonnet 4 & WordPress

### **Giải pháp tự động hóa viết bài từ video YouTube - không cần code!**
Hiện nay, các sếp và marketer phải mất **giờ đồng hồ** để:
- Tìm video mới trên YouTube
- Chuyển đổi nội dung video thành văn bản
- Viết bài SEO từ script
- Đăng bài lên WordPress

**Workflow này tự động hóa toàn bộ quy trình trong 100% tự động hóa**, giúp bạn:
✅ **Tiết kiệm 80% thời gian** viết bài
✅ **Tạo nội dung SEO chất lượng cao** từ video viral
✅ **Cập nhật liên tục** mới nhất từ kênh YouTube
✅ **Hoạt động 24/7** mà không cần can thiệp

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động phát hiện video mới** từ kênh YouTube theo lịch trình
- **Chuyển đổi video thành văn bản** với độ chính xác cao (Supadata)
- **Viết bài SEO hoàn chỉnh** bằng Claude Sonnet 4 (AI đa mô hình)
- **Đăng bài tự động** lên WordPress dưới dạng draft
- **Lọc video viral** dựa trên số like, view và comment
- **Hoạt động liên tục** mà không cần can thiệp
:::

---

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản YouTube** (đăng ký API Key từ [Google Cloud Console](https://console.cloud.google.com/))
2. **Tài khoản Supadata** (dịch vụ chuyển đổi video thành văn bản)
3. **Tài khoản Anthropic** (để sử dụng Claude Sonnet 4)
4. **Tài khoản WordPress** (API Key từ plugin REST API)
5. **Kênh YouTube** muốn theo dõi (đăng ký API Key cho YouTube Data API)
:::

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- **Tải file JSON** từ [n8n.io/workflows/7139](https://n8n.io/workflows/7139)
- **Import vào n8n Editor**:
  - Nhấn `+` → `Import Workflow` → Chọn file JSON
  - Hoặc copy toàn bộ JSON và paste vào `Import Workflow`

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

##### **A. Cấu hình YouTube**
1. **Node "SET YOUTUBE CHANNELS"**:
   - Nhập **danh sách tên kênh YouTube** cần theo dõi (ví dụ: `"TechMaster", "Nghệ Thuật Marketing"`)
   - **Lưu ý**: Tên kênh phải chính xác (không dấu, không khoảng trắng)

2. **Node "Get YouTube Channel Videos"**:
   - Chọn **API Key** từ Google Cloud Console
   - Chọn **Resource** là `video`
   - **Lọc video mới nhất** bằng node `Filter by Date`

3. **Node "Get the Most Viral Video"**:
   - **Cấu hình code** để lọc video có:
     - `viewCount > 10000`
     - `likeCount > 500`
     - `commentCount > 100`

##### **B. Cấu hình AI (Claude Sonnet 4)**
1. **Node "Anthropic Chat Model1"**:
   - Chọn **model**: `claude-sonnet-4-20250514`
   - **API Key**: Nhập từ tài khoản Anthropic
   - **Prompt mẫu** (có thể tùy chỉnh):
     ```json
     {
       "system": "Bạn là một chuyên gia SEO. Chuyển đổi video YouTube thành bài viết SEO hoàn chỉnh với cấu trúc:
       - Tiêu đề SEO (có keyword)
       - Mở đầu hấp dẫn
       - Nội dung chi tiết (cách viết chuyên nghiệp)
       - Kết luận + CTA
       - Từ khóa liên quan",
       "user": "{{$json.video.transcript}}"
     }
     ```

2. **Node "Compose Article" (Agent)**:
   - **Tùy chỉnh PLACEHOLDERS** theo brand:
     - `{{$json.brand_name}}`
     - `{{$json.keyword}}`
     - `{{$json.cta}}`

##### **C. Cấu hình WordPress**
1. **Node "Create WordPress Post"**:
   - Nhập **URL API WordPress** (ví dụ: `https://tudong.vn/wp-json/wp/v2/posts`)
   - **Headers**:
     - `Authorization: Bearer YOUR_WORDPRESS_API_KEY`
     - `Content-Type: application/json`
   - **Body mẫu**:
     ```json
     {
       "title": "{{$json.title}}",
       "content": "{{$json.body}}",
       "status": "draft"
     }
     ```

##### **D. Cấu hình lịch trình**
- **Node "Schedule Trigger"**:
  - Chọn **lịch trình**: `Every 6 hours` (hoặc tùy chỉnh)
  - **Timezone**: Chọn theo múi giờ của bạn

#### 3. Kích hoạt ⚡️
1. **Test run**:
   - Nhấn `Test Workflow` và nhập **một video mẫu** để kiểm tra
   - Kiểm tra **log** để đảm bảo không có lỗi API
2. **Bật Active**:
   - Nhấn `Active` để workflow chạy tự động

---

### ✍️ Mẹo & gợi ý nâng cao
1. **Tối ưu SEO thêm**:
   - Thêm node **Google Keyword Planner** để tự động lấy từ khóa liên quan
   - Sử dụng node **Google Sheets** để lưu lịch sử bài viết

2. **Cập nhật liên tục**:
   - Thêm node **Slack/Telegram** để thông báo khi bài viết được tạo thành công

3. **Lọc video chất lượng cao**:
   - Thêm điều kiện lọc video có **thời lượng > 5 phút** hoặc **tỷ lệ like/dislike > 5:1**

4. **Tự động đăng bài**:
   - Thay đổi `status: "draft"` thành `status: "publish"` khi bài đã được review

---

### 📌 Kết luận
Workflow này **giải phóng hoàn toàn thời gian** của các sếp để tập trung vào chiến lược nội dung thay vì viết bài thủ công. **Chỉ cần cài đặt 1 lần**, nó sẽ tự động:
✔️ Theo dõi video mới từ YouTube
✔️ Chuyển đổi thành văn bản
✔️ Viết bài SEO hoàn chỉnh
✔️ Đăng bài lên WordPress

**Hành động ngay!**
- **Import workflow** và bắt đầu tự động hóa nội dung của bạn!
- **Tùy chỉnh prompt** để phù hợp với brand của doanh nghiệp
- **Monitor log** để đảm bảo workflow hoạt động ổn định

🚀 **Tự động hóa nội dung SEO - không còn phụ thuộc vào con người!** 🚀