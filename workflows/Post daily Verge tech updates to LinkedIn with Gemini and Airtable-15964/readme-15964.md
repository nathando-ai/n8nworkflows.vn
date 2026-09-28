---
title: "🚀 Tự Động Hóa Bài Tech Update Hàng Ngày Từ The Verge Sang LinkedIn Với Gemini AI & Airtable"
description: "Workflow này tự động chuyển đổi tin tức tech từ RSS (như The Verge) thành bài viết LinkedIn sẵn sàng đăng, tối ưu hóa bằng AI, đồng thời tạo hình ảnh minh họa và lưu trữ dữ liệu trong Airtable. Giúp các sếp tiết kiệm 10+ giờ công mỗi tuần, đồng thời nâng cao hiệu quả marketing với nội dung cá nhân hóa và chuyên nghiệp."
slug: "tieu-dong-hoa-bai-tech-update-hang-ngay-them-verge-sang-linkedin"
tags: [n8n, automation, social-media, ai-multimodal, airtable, linkedin, gemini-ai, no-code]
keywords: [tự động hóa linkedin, gemini ai n8n, workflow rss linkedin, tự động hóa bài viết tech, airtable n8n, tự động hóa marketing digital]
---

# 🚀 **Tự Động Hóa Bài Tech Update Hàng Ngày Từ The Verge Sang LinkedIn Với Gemini AI & Airtable**

## **🔥 Nỗi Đau Của Các Sếp Và Giải Pháp Tự Động Hóa**
Các sếp trong lĩnh vực **marketing tech, content creation, hoặc social media** thường phải:
- **Tìm kiếm và lọc tin tức tech** từ nguồn RSS như The Verge, TechCrunch hàng ngày.
- **Chỉnh sửa và tối ưu hóa nội dung** để phù hợp với LinkedIn (loại bỏ HTML, tracking code, viết ngắn gọn).
- **Tạo hình ảnh minh họa** cho bài viết (thường mất thời gian với các công cụ design).
- **Đăng bài thủ công** và quản lý lịch trình, dẫn đến **sự chậm trễ và thiếu nhất quán**.
- **Không có hệ thống lưu trữ** để theo dõi hiệu suất của từng bài viết.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động lấy tin tức tech** từ RSS (The Verge) và lọc ra những bài viết tốt nhất.
✅ **Sử dụng AI Gemini** để **tự động viết bài LinkedIn** với phong cách chuyên nghiệp, tối ưu hashtag và tạo **mô tả hình ảnh** (prompt) cho AI tạo ảnh.
✅ **Tạo hình ảnh minh họa** từ mô tả bằng AI (Gemini Image).
✅ **Đăng bài tự động** lên LinkedIn và **lưu trữ dữ liệu** trong Airtable để theo dõi hiệu suất.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**Lợi Ích Cốt Lõi**]
- **Tiết kiệm 10+ giờ công mỗi tuần** (không cần tìm kiếm, viết, thiết kế hình ảnh).
- **Nội dung chuyên nghiệp** với phong cách viết tự động nhưng gần giống con người.
- **Hình ảnh minh họa tự động** phù hợp với bài viết (không cần skill design).
- **Đăng bài tự động** vào thời gian cố định (6:35 PM hàng ngày).
- **Lưu trữ dữ liệu** trong Airtable để phân tích hiệu suất (likes, shares, engagement).
- **Tối ưu SEO** với hashtag và mô tả tự động.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**Chuẩn Bị Trước Khi Bắt Đầu**]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản LinkedIn** (để đăng bài tự động).
2. **API Key Google Gemini** (để sử dụng AI viết bài và tạo hình ảnh).
3. **Airtable Personal Access Token** (để lưu trữ dữ liệu bài viết).
4. **RSS Feed URL** (mặc định là The Verge, có thể thay đổi).
5. **Thời gian kích hoạt** (mặc định là 6:35 PM hàng ngày).
6. **Màu sắc hex code** (để tạo hình ảnh: `#f39f1c`, `#364250`, `#fefbf6`).
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/15964](https://n8n.io/workflows/15964) (chọn **Export as JSON**).
2. Trên n8n Editor, nhấn **Import** → **Paste JSON** và dán nội dung file vào.
3. Chọn **Import** để thêm workflow vào hệ thống.

#### **Phương pháp 2: Copy/Paste JSON**
1. Copy toàn bộ mã JSON từ [n8n.io/workflows/15964](https://n8n.io/workflows/15964).
2. Trên n8n Editor, nhấn **Import** → **Paste JSON** và dán vào.
3. Chọn **Import**.

---

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này có **13 node** quan trọng, các sếp cần cấu hình kỹ lưỡng:

#### **🔹 Node 1: Schedule Trigger (Daily @ 6:35PM)**
- **Cấu hình:**
  - Thời gian mặc định: **6:35 PM hàng ngày**.
  - Có thể thay đổi theo nhu cầu (ví dụ: 8:00 AM).
- **Lưu ý:**
  - Nếu workflow chạy trên **VPS**, đảm bảo máy chủ hoạt động 24/7.

#### **🔹 Node 2: RSS Feed Read**
- **Cấu hình:**
  - **RSS URL:** `https://feeds.theverge.com/rss/tech` (mặc định).
  - **Limit:** 10 bài viết mới nhất (có thể điều chỉnh).
- **Lưu ý:**
  - Nếu muốn theo dõi nguồn khác (TechCrunch, Wired), thay đổi URL tương ứng.

#### **🔹 Node 3: Aggregate Fields**
- **Cấu hình:**
  - **Fields to aggregate:** `title`, `url`, `date`, `content`.
  - **Lưu ý:** Node này kết hợp dữ liệu từ RSS thành một mảng duy nhất để AI xử lý.

#### **🔹 Node 4: AI Agent (Advanced AI Evaluation)**
- **Cấu hình:**
  - **Model:** `Google Gemini` (đã được cấu hình sẵn).
  - **Prompt mặc định:**
    ```json
    "Select the best article from the aggregated data based on relevance to tech automation, AI, and customer experience. Clean the HTML and generate a LinkedIn post with hashtags and a minimal image prompt."
    ```
  - **Lưu ý:**
    - Nếu muốn thay đổi logic lựa chọn bài viết, chỉnh sửa **prompt** trong node **Think**.

#### **🔹 Node 5: Google Gemini Chat Model (Viết Bài)**
- **Cấu hình:**
  - **Credentials:** `googlePalmApi` (API Key Google Gemini).
  - **Prompt:** Sử dụng mô tả từ AI Agent.
  - **Lưu ý:**
    - Đảm bảo **API Key** được thêm vào **Credentials** của n8n.

#### **🔹 Node 6: Google Gemini (Tạo Hình Ảnh)**
- **Cấu hình:**
  - **Credentials:** `googlePalmApi`.
  - **Prompt:** `={{ $json.output.airtable_records[0].image_prompt }}` (mô tả hình ảnh từ AI).
  - **Lưu ý:**
    - Mô tả hình ảnh phải rõ ràng (ví dụ: *"A minimalist tech illustration with colors #f39f1c, #364250, and #fefbf6"*).

#### **🔹 Node 7: LinkedIn Post**
- **Cấu hình:**
  - **Credentials:** `linkedInOAuth2Api` (OAuth2 từ LinkedIn).
  - **Content:** Nội dung bài viết từ AI.
  - **Image:** Hình ảnh từ node Gemini Image.
  - **Lưu ý:**
    - **Cần đăng ký OAuth2 LinkedIn** trước:
      1. Tạo ứng dụng trên [LinkedIn Developer Portal](https://www.linkedin.com/developers/).
      2. Thêm `r_email_address`, `r_liteprofile`, `w_member_social` vào **Permissions**.
      3. Sau đó, thêm **Client ID & Secret** vào **Credentials** của n8n.

#### **🔹 Node 8: Airtable (Lưu Trữ Dữ liệu)**
- **Cấu hình:**
  - **Credentials:** `airtableTokenApi` (Personal Access Token).
  - **Workspace Base:** Chọn **Workspace** và **Table** (mặc định là "Daily News").
  - **Operation:** `create` (tạo bản ghi mới).
  - **Lưu ý:**
    - **Cách lấy Token Airtable:**
      1. Mở Airtable → **Settings** → **API**.
      2. Copy **Personal Access Token**.
      3. Thêm vào **Credentials** của n8n.

---

### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Run Workflow** để kiểm tra từng node.
   - Kiểm tra **LinkedIn Post** và **Airtable** để đảm bảo dữ liệu đúng.
2. **Bật Active:**
   - Sau khi test thành công, chuyển **Status** từ **Inactive** sang **Active**.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[**Cách Tối Ưu Hiệu Quả Hơn**]
1. **Thay đổi RSS Feed:**
   - Nếu muốn theo dõi **TechCrunch** thay vì The Verge, thay đổi URL thành:
     ```json
     "https://feeds.techcrunch.com/techcrunch"
     ```

2. **Tùy Chỉnh AI Agent:**
   - Muốn AI **ưu tiên bài viết về AI/Automation** hơn, chỉnh sửa **prompt** trong node **Think**:
     ```json
     "Focus on articles about AI automation, no-code tools, and workflow optimization."
     ```

3. **Thêm Slack/Telegram Notification:**
   - Sử dụng **n8n-nodes-base.slack** hoặc **n8n-nodes-base.telegram** để thông báo khi bài viết được đăng thành công.

4. **Lưu Log & Báo Cáo Hiệu Suất:**
   - Sử dụng **n8n-nodes-base.stickyNote** để lưu log lỗi hoặc **n8n-nodes-base.email** để gửi báo cáo hàng tuần.

5. **Sử Dụng Màu Sắc Khác:**
   - Nếu muốn hình ảnh khác, thay đổi **hex code** trong **image_prompt**:
     ```json
     "A futuristic tech background with colors #00ff88, #ff00ff, #00ffff"
     ```

6. **Chạy Trên VPS Để 24/7:**
   - Để workflow hoạt động liên tục, **cài n8n trên VPS** (Self-hosted).
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc lặp lại như **tìm kiếm tin tức, viết bài, thiết kế hình ảnh và đăng bài**. Với **AI Gemini** và **Airtable**, nội dung được **tự động tối ưu hóa**, **đăng bài chính xác** và **lưu trữ dữ liệu** để phân tích.

**Hành động ngay:**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test run** để đảm bảo mọi thứ hoạt động.
3. **Bật Active** và để AI làm việc cho bạn!

**🚀 Cùng tự động hóa marketing tech của mình ngay hôm nay!** 🚀