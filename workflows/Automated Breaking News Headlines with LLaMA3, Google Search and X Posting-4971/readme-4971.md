---
title: "🌐 Tự Động Hóa Bài Tin Tức Nổi Bật Với LLaMA3, Google Search & Đăng Trên X (Twitter) - Không Cần Code"
description: "Workflow tự động hóa lấy tin tức mới nhất từ Google, tổng hợp tiêu đề nổi bật bằng LLaMA3, và đăng lên Twitter/X hàng ngày - tiết kiệm thời gian cho các sếp 100%."
slug: "tieu-de-tin-tuc-noi-bat-llama3-google-search-x"
tags: [n8n, automation, ai, twitter, google-search, llm]
keywords: [n8n workflow tự động tin tức, tổng hợp tin tức nổi bật, đăng bài tự động twitter, llama3 google search, tự động hóa xã hội]
---

# 🚀 **Tự Động Hóa Bài Tin Tức Nổi Bật Với LLaMA3, Google Search & Đăng Trên X (Twitter)**

### **Giải pháp hoàn hảo cho các sếp muốn:**
- **Tiết kiệm 30 phút/ngày** để tìm kiếm và tổng hợp tin tức nổi bật.
- **Tự động đăng bài** lên Twitter/X với tiêu đề hấp dẫn, không cần viết tay.
- **Cập nhật liên tục** với tin tức mới nhất từ Google, được phân tích bởi AI LLaMA3.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **24/7** mà không gián đoạn, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ nhanh, không lag)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian** – Không cần tìm kiếm, tổng hợp tin tức thủ công hàng ngày.
✅ **Tiêu đề hấp dẫn** – LLaMA3 tự động chọn ra những tiêu đề nổi bật nhất.
✅ **Đăng tự động** – Tin tức được đăng lên Twitter/X ngay khi có kết quả.
✅ **Hoạt động liên tục** – Workflow chạy hàng ngày, không phụ thuộc vào thời gian làm việc của bạn.
✅ **Cập nhật tin tức mới nhất** – Sử dụng Google Search để lấy kết quả thời gian thực.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Twitter/X** (để đăng bài tự động).
2. **API Key của Groq** (để sử dụng LLaMA3).
3. **Thiết lập Google Search API** (hoặc sử dụng Google Custom Search JSON API).
4. **N8n Self-hosted** (không thể chạy trên n8n.cloud vì giới hạn API).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [link gốc](https://n8n.io/workflows/4971) và import vào **n8n Editor**.
- **Cách 2:** Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/4971) và dán vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này bao gồm **8 node** chính, các sếp cần cấu hình kỹ các phần sau:

##### **🔹 Node "Schedule Trigger" (Động cơ kích hoạt hàng ngày)**
- **Chọn thời gian chạy:** Ví dụ: **8h sáng hàng ngày** (thời gian phù hợp với tin tức mới nhất).
- **Lưu ý:** Nếu không thiết lập, workflow sẽ không chạy tự động.

##### **🔹 Node "Groq AI" (LLaMA3 - Tự động chọn tiêu đề)**
- **Tham số cần điền:**
  - **API Key:** Điền vào `groqApi` (tạo trong **Credentials** của n8n).
  - **Prompt:** Cần chỉnh sửa để phù hợp với yêu cầu của bạn (ví dụ: *"Tóm tắt và chọn 3 tiêu đề nổi bật nhất từ kết quả Google Search này"*).
  - **Model:** Chọn `llama3-70b-8192` (hoặc phiên bản khác của Groq).

##### **🔹 Node "HTTP Request" (Lấy kết quả Google Search)**
- **URL mẫu:**
  ```
  https://www.googleapis.com/customsearch/v1?q={query}&key={API_KEY}&cx={SEARCH_ENGINE_ID}
  ```
  - **Thay thế:**
    - `{query}` → Đặt vào `Set Topic` (ví dụ: "tin tức kinh tế Việt Nam").
    - `{API_KEY}` → API Key của Google Custom Search.
    - `{SEARCH_ENGINE_ID}` → ID của Google Custom Search Engine (mua trên [Google Program](https://programmablesearchengine.google.com/about/)).

##### **🔹 Node "Function" (Xử lý dữ liệu)**
- **Mã JavaScript cần chỉnh sửa (nếu cần):**
  ```javascript
  // Ví dụ: Lọc và chọn ra 3 tin tức nổi bật nhất
  return {
    json: {
      headlines: data.json.items.slice(0, 3).map(item => ({
        title: item.title,
        link: item.link
      }))
    }
  };
  ```
  - **Lưu ý:** Nếu không hiểu code, có thể để mặc định và chỉnh sửa trong **Groq AI** thay vì node này.

##### **🔹 Node "Post to X" (Đăng bài lên Twitter/X)**
- **Thiết lập OAuth2:**
  - Đăng nhập vào **Twitter Developer Account** và tạo **App**.
  - Thêm **Credentials** trong n8n với tên `twitterOAuth2Api`.
  - Điền **API Key, API Secret, Access Token, Access Token Secret**.

##### **🔹 Node "Google Config" & "Set Topic" (Cấu hình tìm kiếm)**
- **Google Config:**
  - Điền `cx` (ID của Google Custom Search Engine).
- **Set Topic:**
  - Đặt chủ đề tìm kiếm (ví dụ: "tin tức công nghệ mới nhất").

##### **🔹 Node "Build Query" (Xây dựng query tìm kiếm)**
- **Tham số cần điền:**
  - `query` → Liên kết với `Set Topic` (ví dụ: `{{$node["Set Topic"].json["topic"]}}`).

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chạy **Manual Trigger** để kiểm tra kết quả.
   - Kiểm tra **Groq AI** có trả về tiêu đề hay không.
   - Kiểm tra **Twitter** có đăng bài thành công không.
2. **Bật Active workflow** sau khi test thành công.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tăng tính cá nhân hóa:**
   - Sử dụng **node "Function"** để thêm **hashtag** hoặc **mô tả ngắn** vào bài đăng.
   - Ví dụ: `{{$node["Function"].json["hashtags"]}}` → `#TinTức #CôngNghe`.

2. **Lưu log tin tức:**
   - Thêm **node "Google Sheets"** để lưu tất cả tin tức đã đăng vào bảng tính.
   - Cách thêm: `n8n-nodes-base.googleSheets` → Chọn sheet và cấu hình API.

3. **Gửi báo cáo định kỳ:**
   - Sử dụng **node "Email"** (n8n-nodes-base.email) để gửi báo cáo tin tức hàng tuần cho team.

4. **Tối ưu query Google Search:**
   - Nếu kết quả không tốt, thử thay đổi **keyword** trong `Set Topic` hoặc sử dụng **Google Search API Advanced**.

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào công việc quan trọng hơn, đồng thời **tự động hóa hoàn toàn** quá trình tổng hợp và đăng tin tức nổi bật. **Chỉ cần setup 1 lần**, workflow sẽ chạy tự động hàng ngày!

👉 **Bắt đầu ngay bằng cách:**
1. **Import workflow** từ [đây](https://n8n.io/workflows/4971).
2. **Cấu hình API Key** (Groq, Google, Twitter).
3. **Bật Active** và **chờ tin tức tự động đăng lên Twitter!**

**Cần hỗ trợ?** Để lại comment bên dưới hoặc chat với tôi trên [n8n Community](https://community.n8n.io/).

---