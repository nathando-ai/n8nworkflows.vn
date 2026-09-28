---
title: "🚀 Tự Động Hóa Sáng Tạo Bài Dẫn Dẫn Game Hàng Ngày Từ Reddit Với AI Gemini - Cho WebApp Của Các Sếp"
description: "Workflow tự động hóa 24/7 lấy top bài hot từ các subreddit game, lọc và viết bài dẫn dẫn SEO hoàn chỉnh bằng AI Gemini, tự động publish lên webapp của các sếp - không cần code!"
slug: "tu-dong-hoa-sang-tao-bai-dan-dan-game-reddit-gemini"
tags: [n8n, automation, content-creation, ai-gemini, no-code, seo, reditt-rss, web-app]
keywords: [n8n workflow reditt ai, tự động hóa bài viết game, gemini ai viết bài, seo tự động, content creation no-code, reditt rss automation]
---

# 🚀 **Tự Động Hóa Sáng Tạo Bài Dẫn Dẫn Game Hàng Ngày Từ Reddit Với AI Gemini**

### **Nỗi Đau Của Các Sếp**
Các sếp đang phải mất **giờ đồng hồ** mỗi ngày để:
- **Tìm kiếm** top bài hot từ các cộng đồng game trên Reddit.
- **Lọc** những bài chất lượng (không phải meme, rant hay fan art).
- **Viết** bài dẫn dẫn SEO hoàn chỉnh từ đầu đến cuối.
- **Cập nhật** nội dung lên webapp một cách thủ công.

**Kết quả?** Nội dung không được cập nhật kịp thời, chất lượng không đồng đều, và mất nhiều thời gian quý giá.

### **🎯 Giải Pháp: Workflow Tự Động Hóa 100% AI**
Workflow này **tự động hóa toàn bộ quy trình** bằng cách:
✅ **Lấy dữ liệu** từ top 10 bài hot trên các subreddit game (ví dụ: r/gaming, r/pcgames).
✅ **Lọc bài chất lượng** bằng AI Gemini (gemini-3-flash-preview).
✅ **Viết bài dẫn dẫn SEO** hoàn chỉnh trong định dạng Markdown.
✅ **Publish tự động** lên webapp của các sếp (thông qua Supabase Edge Function).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải tìm kiếm, lọc và viết bài hàng ngày.
- **Nội dung SEO cao**: AI Gemini tự động viết bài với cấu trúc chuyên nghiệp.
- **Cập nhật liên tục**: Workflow chạy tự động hàng ngày (8h sáng).
- **Chất lượng ổn định**: AI lọc bỏ bài không phù hợp (meme, rant, fan art).
- **Tích hợp hoàn hảo**: Dữ liệu được gửi trực tiếp lên webapp của các sếp.
:::

---

### **🔧 Yêu Cầu Cần Thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Reddit**: Không cần API key (sử dụng RSS công khai).
2. **Google Gemini API**:
   - Đăng ký [Google AI Studio](https://makersuite.google.com/) và tạo **API Key**.
   - Thêm **credentials** trong n8n với tên `googlePalmApi`.
3. **WebApp với Supabase Edge Function**:
   - Cung cấp **endpoint** để nhận dữ liệu (ví dụ: `https://api.cacse.com/publish-guide`).
   - *(Nếu cần auth)* Thêm **header Authorization** với `Bearer YOUR_SUPABASE_KEY`.
4. **n8n Self-hosted**: Workflow chạy trên máy chủ riêng (không dùng n8n.cloud).

---

### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/14854](https://n8n.io/workflows/14854).
- **Import vào n8n Editor**:
  - Mở n8n → **Import** → Chọn file JSON → **Import**.
  - *(Hoặc)* Copy toàn bộ JSON và **Paste** vào **Create Workflow** → **Paste JSON**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **9 node**, các sếp cần chú ý cấu hình sau:

##### **🔹 Node 1: Schedule Trigger1 (Đặt lịch chạy)**
- **Schedule**: `0 8 * * *` (chạy hàng ngày lúc 8h sáng, theo giờ máy chủ).
- **Time Zone**: Đặt theo **múi giờ của máy chủ** (ví dụ: `Asia/Ho_Chi_Minh` cho Việt Nam).

##### **🔹 Node 2: List of Subreddits1 (Danh sách subreddit)**
- **Mở node Code** → Sửa mảng JSON để thêm/loại bỏ subreddit:
  ```json
  [
    { "name": "gaming" },
    { "name": "pcgames" },
    { "name": "xbox" }  // Thêm subreddit mới ở đây
  ]
  ```
- **Lưu ý**: Không quá 3-5 subreddit để tránh rate limit của Reddit.

##### **🔹 Node 3: Get Reddit JSON1 (Lấy dữ liệu từ Reddit)**
- **URL**: `https://www.reddit.com/r/{name}/hot.rss?limit=10`
  *(n8n tự động thay thế `{name}` bằng tên subreddit từ node trước).*
- **Method**: `GET`
- **Headers**: Không cần thêm (Reddit RSS công khai).

##### **🔹 Node 4: Code in JavaScript (Xử lý XML)**
- **Mã nguồn** đã được tối ưu, **không cần chỉnh sửa** (nếu muốn thay đổi logic, liên hệ tác giả Flavio Paesano).

##### **🔹 Node 5: Loop Over Items1 (Vòng lặp qua bài post)**
- **Batch Size**: Đặt **1** để xử lý một bài một lần (tránh overloading).

##### **🔹 Node 6: Wait1 (Đợi để tránh rate limit)**
- **Thời gian**: **5-10 giây** (để Reddit không block IP).
- **Mode**: `immediately` (nếu muốn delay, chỉnh `delay` trong node).

##### **🔹 Node 7: Message a Model (Gemini AI)**
- **Credentials**: Chọn `googlePalmApi` (đã cấu hình trước).
- **Model**: `gemini-3-flash-preview` (mặc định).
- **Prompt**:
  ```json
  {
    "candidates": [
      {
        "role": "user",
        "parts": [
          {
            "text": "Analyze the following Reddit posts and pick the best discussion-worthy one. Then, write a detailed SEO gaming guide in Markdown format (2000-3000 words) about the topic. Ignore memes, rants, and fan art."
          }
        ]
      }
    ]
  }
  ```
  *(Prompt này đã được tối ưu, các sếp có thể chỉnh sửa nếu cần).*

##### **🔹 Node 8: Code in JavaScript1 (Xử lý output AI)**
- **Mã nguồn** tự động trích xuất `headline` và `article_body` từ response của Gemini.
- **Không cần chỉnh sửa** (nếu muốn thay đổi, liên hệ tác giả).

##### **🔹 Node 9: Send to WebApp (Gửi dữ liệu lên webapp)**
- **URL**: Điền **endpoint** của Supabase Edge Function (ví dụ: `https://api.cacse.com/publish-guide`).
- **Headers**:
  - `Content-Type: application/json`
  - *(Nếu cần auth)* Thêm `Authorization: Bearer YOUR_SUPABASE_KEY`.
- **Body**:
  ```json
  {
    "title": "{{$json.headline}}",
    "content": "{{$json.article_body}}"
  }
  ```

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Chọn **Run Workflow** → Chọn **Run Once**.
  - Kiểm tra **output** của node cuối (`Send to WebApp`) để đảm bảo dữ liệu đúng.
- **Bật Active**:
  - Sau khi test thành công, **bật Active** để workflow chạy tự động hàng ngày.

---

### **✍️ Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Subreddit Niche**:
   - Thêm subreddit chuyên sâu như `r/playstation`, `r/steam`, `r/gamingdeals` để tăng đa dạng nội dung.

2. **Tích Hợp Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** để thông báo khi bài mới được publish:
     ```json
     {
       "text": "🚀 Bài mới được publish: {{ $json.headline }}"
     }
     ```

3. **Lưu Log Dữ Liệu**:
   - Thêm node **Google Sheets** hoặc **Airtable** để lưu lịch sử bài viết:
     ```json
     {
       "sheetName": "Gaming_Guides",
       "range": "A1",
       "values": [
         ["Tên Bài", "{{ $json.headline }}"],
         ["Nội Dung", "{{ $json.article_body }}"],
         ["Subreddit", "{{ $node["Loop Over Items1"].json["name"] }}"]
       ]
     }
     ```

4. **Báo Cáo Định Kỳ**:
   - Sử dụng node **Google Sheets** hoặc **Email** để gửi báo cáo tổng hợp hàng tuần:
     ```json
     {
       "subject": "Báo cáo bài viết game hàng tuần",
       "html": "<h1>Top 5 bài viết mới</h1><ul>{{ $json.posts }}</ul>"
     }
     ```

5. **Optimize Gemini Prompt**:
   - Nếu muốn bài viết dài hơn hoặc có cấu trúc cụ thể, chỉnh sửa prompt trong node `Message a Model`:
     ```json
     {
       "parts": [
         {
           "text": "Viết bài với cấu trúc: [Tiêu đề H1] -> [Mở đầu] -> [Phần 1: Lợi ích] -> [Phần 2: So sánh] -> [Kết luận]. Sử dụng từ khóa SEO: 'game miễn phí', 'trò chơi online'."
         }
       ]
     }
     ```

---

### **📌 Kết Luận**
Workflow này **giải phóng thời gian** của các sếp để tập trung vào chiến lược nội dung hơn, trong khi AI và tự động hóa đảm bảo **nội dung SEO chất lượng** được publish hàng ngày.

**Hành động ngay**:
1. **Import workflow** vào n8n.
2. **Cấu hình endpoint** của webapp và **API Key Gemini**.
3. **Bật Active** và xem nội dung tự động xuất hiện trên trang web!

**💡 Lưu ý cuối cùng**:
- Nếu gặp **rate limit** từ Reddit, tăng thời gian `Wait1` lên **15-30 giây**.
- Để **tối ưu chi phí**, sử dụng **Gemini Flash** (rẻ hơn Pro) và kiểm tra log để điều chỉnh prompt.

**Chúc các sếp thành công với nội dung tự động hóa!** 🚀