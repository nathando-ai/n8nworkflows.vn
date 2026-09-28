---
title: "🚀 Tự Động Hóa Email Tóm Tắt Tin Tức AI Hàng Tuần - Từ RSS Đến Inbox (Gmail + OpenAI)"
description: "Workflow tự động hóa giúp các sếp founder, marketer và nhà nghiên cứu nhận được email tóm tắt tin tức hàng tuần được AI curate từ các nguồn RSS ưa thích, tiết kiệm thời gian đọc thủ công và tối ưu hóa thông tin. Kết quả: Inbox sạch sẽ, nội dung cá nhân hóa và được sắp xếp logic."
slug: "tieu-dong-hoa-email-tom-tat-tin-tuc-ai-hang-tuan"
tags: [n8n, automation, no-code, content-creation, ai-curation, gmail, openai, rss]
keywords: [tự động hóa email AI, curate tin tức hàng tuần, RSS feed automation, OpenAI Gmail n8n, tự động hóa content marketing, email tóm tắt tin tức]
---

# 🚀 **Tự Động Hóa Email Tóm Tắt Tin Tức AI Hàng Tuần - Từ RSS Đến Inbox**

## **Nỗi Đau Của Các Sếp: Đọc RSS Thủ Công Làm Mất Thời Gian & Thông Tin Tràn Lan**
Hàng ngày, các sếp founder, marketer hoặc nhà nghiên cứu phải **quét qua hàng chục nguồn tin tức** (tech, marketing, startup, finance...) để tìm ra những tin tức **cần thiết, mới nhất và liên quan**. Kết quả?
- **Thời gian bị "đoạt đi"** bởi việc đọc lướt, không tập trung.
- **Thông tin tràn lan** khiến các sếp **quên bỏ** những tin tức quan trọng sau khi đọc.
- **Không có sự tổng hợp logic** → phải tự phân loại, tóm tắt và lưu trữ.

**Workflow này giải quyết tất cả!** Nó **tự động hóa toàn bộ quy trình**:
✅ **Chọn lọc** tin tức từ các nguồn RSS ưa thích.
✅ **Tóm tắt & phân loại** bằng AI (OpenAI) thành **2-4 chủ đề**.
✅ **Gửi email HTML sẵn sàng** vào inbox hàng tuần (thứ Hai 8h sáng).

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**3 Lợi Ích Cốt Lõi**]
- **Tiết kiệm 5-10 giờ/tuần** đọc tin tức thủ công.
- **Nhận email tóm tắt AI** với **nội dung được sắp xếp logic**, không phải quét lướt.
- **Cá nhân hóa hoàn toàn** → Chỉ lấy tin tức từ các nguồn **của chính mình**.
- **Hoạt động 24/7** → Không cần nhớ hoặc nhắc nhở.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản OpenAI** (API Key) → Để AI tóm tắt và phân loại tin tức.
2. **Tài khoản Gmail** (OAuth2) → Để gửi email tự động.
3. **Danh sách các nguồn RSS** (ví dụ: TechCrunch, Hacker News, Forbes, hoặc blog cá nhân).
4. **Email nhận** (của chính mình hoặc team) → Để nhận email tóm tắt hàng tuần.

---
### 🚀 **Cách Import & Cấu Hình Workflow**

#### **1. Import Workflow 📥**
Các sếp có thể **import** workflow từ file JSON hoặc **copy/paste** mã JSON vào **n8n Editor**:
- **Bước 1:** Mở [n8n.io](https://n8n.io/) và tạo một **workflow mới**.
- **Bước 2:** Nhấn **"Import"** và chọn **"From JSON"**.
- **Bước 3:** Dán mã JSON từ [workflow gốc](https://n8n.io/workflows/16037) hoặc tải file JSON từ link này.

#### **2. Các Lưu Ý Bắt Buộc Phải Chỉnh 📌**
Workflow này có **7 node chính**, nhưng **3 node quan trọng nhất** cần cấu hình cẩn thận:

##### **🔹 Node 1: Define Feed Sources (Code)**
- **Mục đích:** Xác định danh sách các nguồn RSS cần theo dõi.
- **Cách chỉnh:**
  - Mở node **"Define Feed Sources"** (type: `code`).
  - Thay đổi biến `FEEDS` trong mã JavaScript để thêm/loại bỏ nguồn RSS.
  - **Ví dụ:**
    ```javascript
    const FEEDS = [
      "https://feeds.feedburner.com/TechCrunch",
      "https://feeds.feedburner.com/HackerNews",
      "https://feeds.feedburner.com/ForbesTech",
      // Thêm các nguồn RSS của bạn
    ];
    ```
  - **Lưu ý:** Các nguồn RSS phải **cung cấp dữ liệu XML** (không phải JSON).

##### **🔹 Node 5: Curate & Summarize Digest (OpenAI)**
- **Mục đích:** AI tóm tắt và phân loại tin tức thành **2-4 chủ đề**.
- **Cách chỉnh:**
  - Đảm bảo **credential OpenAI** đã được thiết lập (sử dụng `gpt-4o-mini` hoặc mô hình khác).
  - **Tùy chỉnh Prompt** (nếu cần) trong node này để điều chỉnh cách AI xử lý:
    ```json
    {
      "prompt": "Tóm tắt và phân loại {articles} thành 2-4 chủ đề. Mỗi chủ đề bao gồm:\n1. Tiêu đề tin tức\n2. Link nguồn\n3. Một câu tóm tắt ngắn (under 3 sentences)\n4. Đánh giá tính liên quan (high/medium/low)\n\nĐịnh dạng output theo HTML sẵn sàng gửi email."
    }
    ```
  - **Lưu ý:** Nếu API OpenAI bị giới hạn, có thể **tăng thời gian chờ** hoặc **giảm số lượng tin tức** trong `MAX_ARTICLES`.

##### **🔹 Node 7: Send Digest Email (Gmail)**
- **Mục đích:** Gửi email HTML tự động vào inbox.
- **Cách chỉnh:**
  - Đảm bảo **credential Gmail OAuth2** đã được thiết lập.
  - Trong node **"Build Email HTML"** (type: `set`), chỉnh sửa:
    - **Tiêu đề email** (ví dụ: `"Weekly AI Digest - {date}"`).
    - **Người nhận** (điền email của mình hoặc team).
    - **Nội dung HTML** (có thể tùy chỉnh logo, màu sắc, hoặc footer).
  - **Lưu ý:** Nếu email bị đánh dấu là spam, có thể **thêm "From Name"** và **cấu hình SPF/DKIM** cho domain.

#### **3. Kích Hoạt ⚡️**
- **Bước 1:** Nhấn **"Test Run"** để kiểm tra workflow với **dữ liệu mẫu**.
- **Bước 2:** Sau khi test thành công, **bật Active** workflow.
- **Bước 3:** Chờ đến **thứ Hai 8h sáng** (thời gian mặc định) để nhận email đầu tiên.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[**Tăng Cường Hiệu Quả**]
1. **Thêm Slack/Telegram Notifications**
   - Sử dụng node **Slack** hoặc **Telegram Bot** để **báo động** khi email được gửi.
   - **Cách làm:** Thêm node `slack` sau node `gmail` và cấu hình webhook.

2. **Lưu Log & Theo Dõi**
   - Sử dụng node **StickyNote** để **ghi lại** các tin tức quan trọng.
   - **Cách làm:** Thêm node `stickyNote` sau node `openAi` và lưu dữ liệu vào **Google Sheets** hoặc **Notion**.

3. **Tùy Chỉnh Thời Gian & Số Lượng Tin Tức**
   - Trong node **"Merge, Filter & Rank Articles"**, chỉnh `LOOKBACK_DAYS` (ví dụ: 7 ngày) và `MAX_ARTICLES` (ví dụ: 10 tin/tuần).
   - **Cách làm:** Mở node `code` và sửa biến:
     ```javascript
     const LOOKBACK_DAYS = 7;
     const MAX_ARTICLES = 10;
     ```

4. **Kết Hợp Với Notion/Google Docs**
   - Thay vì chỉ gửi email, **tự động lưu tin tức vào Notion** hoặc **Google Docs** để **dễ dàng chia sẻ** với team.
   - **Cách làm:** Thêm node `notion` hoặc `google-drive` sau node `openAi`.
:::

---
### 📌 **Kết Luận: Đừng Đọc RSS Thủ Công Nữa!**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **các quyết định chiến lược** thay vì **quét tin tức thủ công**. Với **AI curate**, email hàng tuần sẽ **luôn được sắp xếp logic**, **tóm tắt ngắn gọn** và **cá nhân hóa** theo sở thích của bạn.

**🚀 Hành động ngay:**
1. **Import workflow** từ [link gốc](https://n8n.io/workflows/16037).
2. **Cấu hình OpenAI & Gmail** trong 5 phút.
3. **Chờ thứ Hai 8h sáng** để nhận email tóm tắt đầu tiên!

---
:::info[**Gợi Ý Hạ Tầng Cho n8n**]
Để workflow **chạy ổn định 24/7**, các sếp nên **self-host n8n** trên VPS:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**💡 Câu hỏi thường gặp:**
❓ **"Workflow này có miễn phí không?"**
→ **Vâng!** Nếu sử dụng **n8n Cloud** (miễn phí cho 1000 credit/tháng). Nếu self-host, chỉ cần **VPS rẻ** như trên.

❓ **"AI có thể tóm tắt sai không?"**
→ Có thể, nhưng **các sếp có thể chỉnh sửa Prompt** trong node OpenAI để **tăng độ chính xác**.

❓ **"Có thể thêm nhiều nguồn RSS hơn không?"**
→ **Vâng!** Chỉ cần **thêm link RSS** vào biến `FEEDS` trong node `Define Feed Sources`.