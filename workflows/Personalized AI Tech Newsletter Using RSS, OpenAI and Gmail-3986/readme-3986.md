---
title: "🚀 Tự Động Hóa Tin Tức Công Nghệ Cá Nhân Hóa Bằng AI - RSS + OpenAI + Gmail (Không Cần Code)"
description: "Workflow tự động hóa gửi tin tức công nghệ cá nhân hóa hàng tuần cho bạn qua email, sử dụng RSS feeds, AI OpenAI và Gmail. Tiết kiệm thời gian theo dõi tin tức hàng ngày và nhận báo cáo tổng hợp thông minh."
slug: "tieu-dong-hoa-tin-tuc-cong-nghe-ai-rss-gmail"
tags: [n8n, automation, ai, marketing, email-automation, rss, openai]
keywords: [n8n workflow tin tức công nghệ, tự động hóa tin tức cá nhân hóa, AI gửi email tin tức hàng tuần, RSS feeds công nghệ, OpenAI tự động hóa]
---

# 🚀 **Tự Động Hóa Tin Tức Công Nghệ Cá Nhân Hóa Bằng AI - Không Cần Code**

### **Giải pháp cho các sếp bận rộn không còn phải theo dõi tin tức công nghệ hàng ngày**
Hàng ngày, các sếp phải mất thời gian quét qua hàng chục trang tin tức công nghệ như *TechCrunch*, *Wired*, *The Verge* để cập nhật xu hướng mới. Nhưng với **workflow này**, bạn chỉ cần **cấu hình 1 lần** và **AI sẽ tự động**:
- **Lấy tin tức mới nhất** từ các nguồn RSS được chọn.
- **Tóm tắt và lọc** những tin tức liên quan đến sở thích của bạn (AI, game, gadget, blockchain...).
- **Gửi báo cáo tổng hợp hàng tuần** trực tiếp vào email, giúp bạn **tiết kiệm thời gian** và **nhận thông tin chính xác, cá nhân hóa**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không phải theo dõi tin tức hàng ngày.
- **Tin tức cá nhân hóa**: AI lọc và tóm tắt những tin tức liên quan đến sở thích của bạn.
- **Báo cáo hàng tuần**: Nhận email tổng hợp với những tin tức mới nhất và quan trọng nhất.
- **Hoạt động tự động**: Khởi động và quên đi, workflow chạy 24/7.
- **Dễ dàng tùy chỉnh**: Thay đổi nguồn tin tức, chủ đề hoặc số lượng tin tức theo ý muốn.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản OpenAI** (API Key) để sử dụng AI tóm tắt và xử lý tin tức.
2. **Tài khoản Gmail** (OAuth2) để gửi email báo cáo hàng tuần.
3. **Danh sách RSS feeds** của các trang tin tức công nghệ bạn quan tâm (ví dụ: *TechCrunch*, *Wired*, *The Verge*).
4. **Sở thích cá nhân** (ví dụ: *AI, game, blockchain, IoT*) để AI lọc tin tức phù hợp.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Bước 1**: Tải workflow từ [đây](https://n8n.io/workflows/3986) hoặc sao chép JSON từ trang gốc.
- **Bước 2**: Mở **n8n Editor** và chọn **Import Workflow** → Dán JSON hoặc tải file `.json`.
- **Bước 3**: Chọn **Active** để kích hoạt workflow.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này gồm **2 phần chính**:
- **Phần 1: Lấy tin tức hàng ngày** (dùng `scheduleTrigger` với tần suất hàng ngày).
- **Phần 2: Gửi báo cáo hàng tuần** (dùng `scheduleTrigger` với tần suất hàng tuần).

##### **A. Cấu hình nguồn tin tức (RSS Feeds)**
- **Node**: *"Set Tech News RSS Feeds"* (type: `set`)
  - **Cách làm**:
    1. Mở node này và thay đổi giá trị `rssFeeds` thành danh sách URL RSS của các trang bạn quan tâm.
    2. Ví dụ:
      ```json
      {
        "rssFeeds": [
          "https://feeds.techcrunch.com/TechCrunch",
          "https://feeds.wired.com/wired/index",
          "https://www.theverge.com/rss/index.xml"
        ]
      }
      ```

##### **B. Cấu hình sở thích cá nhân (Your Topics of Interest)**
- **Node**: *"Your topics of interest"* (type: `set`)
  - **Cách làm**:
    1. Mở node này và thay đổi giá trị `topics` thành danh sách chủ đề bạn quan tâm.
    2. Ví dụ:
      ```json
      {
        "topics": ["AI", "game", "blockchain", "gadget"],
        "numberOfItems": 15
      }
      ```

##### **C. Cấu hình OpenAI & Gmail**
- **Node**: *"Embeddings OpenAI"* và *"OpenAI Chat Model"* (type: `embeddingsOpenAi`, `lmChatOpenAi`)
  - **Cách làm**:
    1. Đăng ký **API Key OpenAI** tại [trang chính thức](https://platform.openai.com/account/api-keys).
    2. Trong **n8n Credentials**, thêm **OpenAI API** với tên `openAiApi` và dán API Key vào.
    3. **Model mặc định**: `gpt-4o` (có thể thay đổi nếu cần).

- **Node**: *"Send Newsletter"* (type: `gmail`)
  - **Cách làm**:
    1. Đăng ký **OAuth2 Gmail** trong **n8n Credentials** với tên `gmailOAuth2`.
    2. Chọn email nhận báo cáo trong node này.

##### **D. Lưu ý về Vector Store (Bộ nhớ vector)**
- **Node**: *"Store News Articles"* (type: `vectorStoreInMemory`)
  - **Lưu ý**:
    - Workflow hiện đang sử dụng **bộ nhớ trong bộ** (`inMemory`), nên dữ liệu sẽ mất khi restart n8n.
    - **Để lưu dài hạn**, các sếp có thể thay thế bằng **Pinecone**, **Weaviate** hoặc **ChromaDB** (hướng dẫn nâng cao ở phần sau).

#### **3. Kích hoạt ⚡️**
- **Bước 1**: Chạy **Test Run** với dữ liệu mẫu để kiểm tra workflow.
- **Bước 2**: Bật **Active** cho cả hai `scheduleTrigger` (hàng ngày và hàng tuần).
- **Bước 3**: Chờ **24h** để nhận email báo cáo đầu tiên!

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Thay đổi nguồn tin tức**:
   - Thay thế RSS feeds bằng **API news** như *NewsAPI* hoặc *Google News RSS*.
   - Ví dụ: `https://newsapi.org/v2/top-headlines?sources=techcrunch&apiKey=YOUR_API_KEY`.

2. **Lưu dữ liệu lâu dài**:
   - Thay thế `vectorStoreInMemory` bằng **Pinecone** hoặc **Weaviate** để lưu tin tức lâu dài.
   - Hướng dẫn: [Cài đặt Pinecone với n8n](https://docs.n8n.io/integrations/built-in/nodes/n8n-nodes-base#vector-store).

3. **Gửi báo cáo qua Telegram**:
   - Thay thế node `gmail` bằng **Telegram Bot** để nhận tin tức trực tiếp trên chat.
   - Hướng dẫn: [Kết nối Telegram với n8n](https://docs.n8n.io/integrations/built-in/nodes/n8n-nodes-base#telegram).

4. **Tùy chỉnh AI tóm tắt**:
   - Thay đổi **prompt** trong node `News reader AI` (type: `agent`) để AI tóm tắt theo phong cách riêng.
   - Ví dụ: Yêu cầu AI viết tóm tắt ngắn gọn hoặc chi tiết hơn.

5. **Lưu log hoạt động**:
   - Thêm node `stickyNote` hoặc `log` để theo dõi lỗi và hoạt động của workflow.

---

### 📌 **Kết luận**
**Workflow này giúp các sếp:**
✅ **Tiết kiệm thời gian** không phải theo dõi tin tức hàng ngày.
✅ **Nhận báo cáo cá nhân hóa** với những tin tức quan trọng nhất.
✅ **Hoạt động tự động** 24/7, không cần can thiệp.

**Hành động ngay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Thêm RSS feeds** và sở thích cá nhân của bạn.
3. **Bật Active** và chờ email báo cáo hàng tuần!

**Nếu cần hỗ trợ**, các sếp có thể tham khảo:
- [Hướng dẫn cài n8n trên VPS](https://docs.n8n.io/hosting/self-hosting-on-vps)
- [Danh sách RSS feeds công nghệ](https://www.feedspot.com/category/technology_rss_feeds/)

---
**Chúc các sếp thành công với tự động hóa tin tức công nghệ cá nhân hóa!** 🚀