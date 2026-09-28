---
title: "🚀 **Tự Động Hóa Bài Đăng Tin Tức Tech Hàng Ngày Trên Instagram Với Gemini AI & SerpAPI - Không Cần Code!**"
description: "Workflow tự động tìm kiếm tin tức tech mới nhất từ SerpAPI, tạo nội dung cá nhân hóa và hình ảnh AI bằng Google Gemini, sau đó đăng lên Instagram hàng ngày - tiết kiệm 100% thời gian thủ công cho các sếp Marketing & Content Creator."
slug: "tu-dong-hoa-bai-dang-tin-tuc-tech-hang-ngay-tren-instagram"
tags: [n8n, automation, social-media, ai-multimodal, google-gemini, serpapi, instagram-bot]
keywords: [n8n workflow tự động hóa instagram, tự động hóa tin tức tech, gemini ai instagram, serpapi n8n, đăng bài tự động instagram, content creator ai]
---

# 🚀 **Tự Động Hóa Bài Đăng Tin Tức Tech Hàng Ngày Trên Instagram Với Gemini AI & SerpAPI**

## **💥 Nỗi Đau Của Các Sếp Marketing & Content Creator**
Các sếp đang mất **giờ đồng hồ hàng ngày** để:
✅ Tìm kiếm tin tức tech mới nhất từ nhiều nguồn khác nhau (TechCrunch, Bloomberg, Reuters...)
✅ Tạo **nội dung hấp dẫn** với tiêu đề, mô tả và hashtag phù hợp
✅ **Tạo hình ảnh đẹp** để kèm bài đăng (không phải là ảnh chụp màn hình xấu xí)
✅ **Đăng bài tự động** vào thời điểm tối ưu (9h sáng, khi traffic cao nhất)

**Kết quả?** Bài đăng không được cá nhân hóa, mất thời gian, và không tối ưu hóa cho engagement.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS chuyên dụng.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ nhanh, không lag)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✔ **Tiết kiệm 5-10 giờ/tuần** (không cần tìm kiếm, viết bài, tạo hình ảnh thủ công)
✔ **Nội dung cá nhân hóa** với tiêu đề, mô tả và hashtag được tối ưu bởi AI
✔ **Hình ảnh chuyên nghiệp** được tạo bởi Google Gemini (không cần skill design)
✔ **Đăng bài tự động** vào 9h sáng hàng ngày (khi engagement cao nhất)
✔ **Tăng tương tác** với nội dung mới mẻ, hấp dẫn và định kỳ
✔ **Không phụ thuộc vào thời gian** (chạy 24/7, không cần can thiệp thủ công)
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
🔹 **Tài khoản Instagram Business** (đã kết nối với Meta Business Suite)
🔹 **API Key của Google Gemini** (miễn phí trong giới hạn)
🔹 **API Key của SerpAPI** (đăng ký tại [serpapi.com](https://serpapi.com/))
🔹 **Tài khoản n8n Self-hosted** (để workflow chạy liên tục)

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/13151](https://n8n.io/workflows/13151) (chọn **Download JSON**)
2. Trên **n8n Editor**, nhấn **Import** → Chọn file JSON vừa tải
3. Chọn **Workflow Configuration** → **Import**

#### **Phương pháp 2: Copy/Paste JSON**
1. Mở **n8n Editor** → Nhấn **Create New Workflow**
2. Chọn **Import** → **Paste JSON** → Dán toàn bộ mã JSON từ [n8n.io/workflows/13151](https://n8n.io/workflows/13151)
3. Chọn **Workflow Configuration** → **Import**

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

#### **🔹 Node 1: Schedule Daily Posts (n8n-nodes-base.scheduleTrigger)**
- **Cài đặt thời gian chạy:** 9h sáng hàng ngày (hoặc thời gian phù hợp với audience)
- **Lưu ý:** Đảm bảo **n8n chạy liên tục** (không bị ngắt kết nối)

#### **🔹 Node 2: Workflow Configuration (n8n-nodes-base.set)**
- **Cấu hình tin tức muốn theo dõi:**
  - **Search Query:** `"tech news 2024"`, `"AI breakthroughs"`, `"startup funding Vietnam"`
  - **Content Preferences:** Chọn **tiêu đề ngắn gọn**, **mô tả chi tiết**, **hashtag phù hợp**
  - **Instagram Handle:** Điền **@tên_tài_khoản_instagram**

#### **🔹 Node 3: AI Agent - News Research & Prompt Generation (@n8n/n8n-nodes-langchain.agent)**
- **Kết nối với SerpAPI:**
  - Điền **API Key** từ SerpAPI vào **Credentials**
  - Thiết lập **search engine** là **Google News** (hoặc Bing)
- **Kết nối với Google Gemini:**
  - Điền **API Key** từ Google Gemini vào **Credentials**
  - Chọn **model** là `gemini-pro` (hoặc `gemini-1.5` nếu có)

#### **🔹 Node 4: Google Gemini Chat Model (n8n-nodes-langchain.lmChatGoogleGemini)**
- **Prompt mẫu:**
  ```plaintext
  Tìm kiếm tin tức tech mới nhất về {{searchQuery}}.
  Trả về:
  1. Tiêu đề hấp dẫn (dưới 30 ký tự)
  2. Mô tả chi tiết (dưới 280 ký tự)
  3. 5 hashtag phù hợp
  4. Một prompt để tạo hình ảnh kèm bài đăng (ví dụ: "Một hình ảnh hiện đại về AI và blockchain")
  ```
- **Lưu ý:** Đảm bảo **API Key** được điền chính xác.

#### **🔹 Node 5: SerpAPI News Search Tool (@n8n/n8n-nodes-langchain.toolSerpApi)**
- **Tham số cần thiết:**
  - `q`: Từ khóa tìm kiếm (ví dụ: `"AI startup Vietnam 2024"`)
  - `engine`: `google`
  - `hl`: `vi` (để kết quả tiếng Việt)
- **Lưu ý:** Nếu kết quả không đủ, tăng **`num`** lên 10-20.

#### **🔹 Node 6: Generate an image (n8n-nodes-langchain.googleGemini)**
- **Prompt tự động lấy từ Node 3:**
  ```plaintext
  =={{ $('AI Agent - News Research & Prompt Generation').item.json.output.imagePrompt }}
  ```
- **Tham số hình ảnh:**
  - **Format:** `PNG` (phù hợp với Instagram)
  - **Style:** `Realistic` (hoặc `Modern`)
  - **Resolution:** `1080x1080` (định dạng chuẩn Instagram)

#### **🔹 Node 7: Upload file to tmpfiles (n8n-nodes-tmpfiles.tmpfiles)**
- **Lưu ý:** Node này tạo **URL tạm thời** để Instagram upload hình ảnh.
- **Thời gian hết hạn:** ~15 phút (đảm bảo **Node 8** chạy trước khi URL hết hạn).

#### **🔹 Node 8: Post to Instagram (@mookielianhd/n8n-nodes-instagram.instagram)**
- **Kết nối Instagram API:**
  1. Tạo **Facebook Developer Account** → Đăng ký **Instagram Graph API**
  2. Điền **Access Token** vào **Credentials**
  3. Chọn **Page ID** của tài khoản Instagram
- **Tham số cần thiết:**
  - `image_url`: URL từ Node 7
  - `caption`: Tiêu đề + mô tả từ Node 4
  - `hashtags`: Hashtag từ Node 4

#### **🔹 Node 9: Structured Output Parser (n8n-nodes-langchain.outputParserStructured)**
- **Lưu ý:** Node này **tách dữ liệu** thành các phần riêng (tiêu đề, mô tả, hashtag, URL hình ảnh).
- **Không cần chỉnh sửa** nếu workflow đã cấu hình đúng.

---

### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Run Workflow** (chọn **Manual Execution**)
   - Kiểm tra **các node** có chạy thành công không (kiểm tra **JSON output**)
2. **Bật Schedule Trigger:**
   - Đi đến **Node 1 (Schedule Daily Posts)**
   - Nhấn **Active** → Chọn **9:00 AM hàng ngày**
3. **Kiểm tra Instagram:**
   - Sau 1 ngày, kiểm tra **tài khoản Instagram** có bài đăng tự động không.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **🔹 1. Tăng Tính Cá Nhân Hóa với AI**
- **Sử dụng LangChain Prompt Engineering** để tạo **tiêu đề động** dựa trên:
  - **Thời gian** (ví dụ: `"Tin tức tech hôm nay - 10/10/2024"`)
  - **Tình trạng thị trường** (ví dụ: `"AI sụt giá? Đọc tin tức này!"`)
- **Mẫu prompt nâng cao:**
  ```plaintext
  Tạo một tiêu đề hấp dẫn cho tin tức tech về {{topic}} với:
  - Tôn chỉ: {{tone}} (ví dụ: "Học thuật", "Thương mại", "Phê phán")
  - Kết hợp từ khóa: {{keywords}}
  - Sử dụng emoji: {{emoji}}
  ```

### **🔹 2. Lưu Log & Theo Dõi Performance**
- **Thêm Node `n8n-nodes-base.httpRequest`** sau Node 8 để:
  - Gửi **báo cáo thành công/thất bại** về **Google Sheets** hoặc **Slack**
  - Ví dụ: `https://api.slack.com/webhook/...` (để báo lỗi nếu workflow crash)
- **Mẫu JSON gửi Slack:**
  ```json
  {
    "text": "🚀 Bài đăng tự động thành công! Tin tức: {{title}}",
    "attachments": [
      {
        "title": "Chi tiết",
        "fields": [
          {"title": "Tiêu đề", "value": "{{title}}", "short": true},
          {"title": "Hashtag", "value": "{{hashtags}}", "short": true},
          {"title": "Link", "value": "{{image_url}}", "short": true}
        ]
      }
    ]
  }
  ```

### **🔹 3. Tối Ưu Hóa Thời Gian Đăng Bài**
- **Sử dụng Node `n8n-nodes-base.dateTime`** để:
  - Đăng bài vào **thời điểm traffic cao nhất** (không phải 9h cố định)
  - Ví dụ: **Từ 8h-10h sáng** (thời gian người dùng mở Instagram nhiều nhất)
- **Mẫu cấu hình:**
  ```plaintext
  ={{ $datetime.now().format('YYYY-MM-DD') }} + " 08:00:00"
  ```

### **🔹 4. Tạo Bài Đăng Video (Nâng Cao)**
- **Sử dụng Node `n8n-nodes-langchain.googleGemini`** để tạo **script video** từ tin tức
- **Kết hợp với Node `n8n-nodes-base.youtube`** để tự động upload video
- **Mẫu prompt:**
  ```plaintext
  Tạo một script video 30 giây về tin tức {{topic}} với:
  - Diễn viên: "AI Voice" (ngôn ngữ Việt)
  - Bối cảnh: "Phòng làm việc hiện đại"
  - Kết thúc: "Like & Follow để cập nhật tin tức tech mới nhất!"
  ```

### **🔹 5. Xử Lý Lỗi & Khôi Phục Tự Động**
- **Thêm Node `n8n-nodes-base.if`** để:
  - Nếu **SerpAPI trả về lỗi**, thì **tìm kiếm từ khóa khác**
  - Nếu **Google Gemini lỗi**, thì **sử dụng model khác** (ví dụ: `gemini-1.5`)
- **Mẫu logic:**
  ```plaintext
  IF (error in SerpAPI response)
    THEN search with alternative query
  ELSE proceed to image generation
  ```

---

## 📌 **Kết Luận: Đăng Bài Tự Động Với AI - Không Cần Code!**

Workflow này **giải phóng thời gian** cho các sếp Marketing & Content Creator để:
✅ **Tập trung vào chiến lược nội dung** thay vì làm thủ công
✅ **Tăng engagement** với bài đăng định kỳ và chuyên nghiệp
✅ **Tiết kiệm chi phí** so với việc thuê designer hoặc copywriter

**Bước đầu tiên:** **Import workflow ngay hôm nay** và **cấu hình theo hướng dẫn**!
Sau đó, **bật Schedule Trigger** và **đợi AI làm việc cho bạn** mỗi sáng.

---
**🚀 Cần hỗ trợ thêm?** Đăng ký **VPS n8n** từ [TinoHost](https://tino.vn/vps-n8n?affid=388) và **khám phá thêm workflow tự động hóa** khác trên [n8n.io](https://n8n.io/).