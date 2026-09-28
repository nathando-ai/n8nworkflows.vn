---
title: "🍽️ **Tự Động Hóa Gợi Ý Món Ăn HelloFresh Với AI + Qdrant (Không Cần Code!)**"
description: "Workflow tự động hóa gợi ý món ăn từ HelloFresh dựa trên sở thích cá nhân, sử dụng AI Mistral và công nghệ vector Qdrant để tạo engine khuyến nghị thông minh. Giúp khách hàng tiết kiệm thời gian tìm kiếm món ăn phù hợp hàng tuần."
slug: "tự-dộng-hoa-gợi-ý-món-ăn-hello-fresh-ai-qdrant"
tags: [n8n, automation, ai, qdrant, langchain, no-code, tự động hóa, chatbot, recommendation-engine]
keywords: [n8n workflow tự động hóa, gợi ý món ăn HelloFresh, AI Mistral, Qdrant vectorstore, tự động hóa không code, engine khuyến nghị món ăn, chatbot ẩm thực]
---

# 🚀 **Tự Động Hóa Gợi Ý Món Ăn HelloFresh Với AI + Qdrant (Không Cần Code!)**

## **🔍 Nỗi Đau Của Khách Hàng**
Mỗi tuần, khách hàng phải mất thời gian **quét qua danh sách món ăn HelloFresh**, tìm kiếm món phù hợp với sở thích cá nhân (nhiệt độ, thời gian nấu, khẩu vị). Với **24 món ăn khác nhau**, việc lựa chọn một cách thủ công không chỉ tốn thời gian mà còn dễ bị **quên hoặc chọn sai**. **Workflow này giải quyết vấn đề này bằng cách:**
✅ **Tự động hóa việc thu thập và phân tích** danh sách món ăn từ trang web HelloFresh.
✅ **Xây dựng engine khuyến nghị AI** dựa trên **Qdrant (vector search)** và **Mistral (AI language model)**.
✅ **Tạo chatbot cá nhân hóa** để khách hàng chỉ cần **chat với AI** là nhận được gợi ý món ăn **phù hợp với sở thích** (nhiệt, lạnh, cay, ngọt, nhanh/chậm...).
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm thời gian** (không cần quét danh sách thủ công).
- **Khuyến nghị chính xác** dựa trên sở thích cá nhân (AI học từ phản hồi).
- **Món ăn đa dạng** (AI tránh lặp lại món ăn trong tuần).
- **Hoạt động tự động** (không cần can thiệp người dùng).
- **Cá nhân hóa cao** (AI nhớ sở thích trước đó).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ**]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản API Mistral Cloud** (để tạo embeddings và chatbot).
   - [Đăng ký API Mistral](https://mistral.ai/) (miễn phí hoặc trả phí).
   - **Credentials cần thiết:** `mistralCloudApi` (API Key).
2. **Tài khoản Qdrant Cloud** (để lưu trữ vector store).
   - [Đăng ký Qdrant Cloud](https://cloud.qdrant.tech/) (có phiên bản miễn phí).
   - **Credentials cần thiết:** `qdrantApi` (Endpoint + API Key).
3. **Trang web HelloFresh** (để scrape dữ liệu món ăn).
   - Workflow sẽ tự động lấy dữ liệu từ trang web này.
4. **Cài đặt n8n Self-hosted** (để chạy workflow 24/7).
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).

---
---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/2333](https://n8n.io/workflows/2333) hoặc copy/paste JSON vào **n8n Editor**.
- **Cách import:**
  1. Mở **n8n Editor** → Nhấn **"Import"** → Chọn file JSON.
  2. Hoặc **copy toàn bộ JSON** và dán vào **"Import from JSON"** trong Editor.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **24 node**, các bước quan trọng cần cấu hình:

##### **🔹 Bước 1: Cấu Hình API Mistral & Qdrant**
- **Node `Embeddings Mistral Cloud` & `Mistral Cloud Chat Model`:**
  - Điền **`mistralCloudApi`** vào **Credentials** (API Key từ Mistral).
  - Chọn **Model:** `mistral-large-2402`.
- **Node `Qdrant Vector Store` & `Use Qdrant Recommend API`:**
  - Điền **`qdrantApi`** vào **Credentials** (Endpoint + API Key từ Qdrant).
  - **Lưu ý:** **Phải tạo collection `hello_fresh` trong Qdrant trước!**
    ```bash
    PUT collections/hello_fresh
    {
      "vectors": {
        "distance": "Cosine",
        "size": 1024
      }
    }
    ```

##### **🔹 Bước 2: Scrape Dữ liệu Món Ăn từ HelloFresh**
- **Node `Get This Week's Menu` (HTTP Request):**
  - Điền **URL** của trang web HelloFresh (ví dụ: `https://www.hellofresh.vn/weekly-menu`).
  - **Lưu ý:** Trang web này có thể thay đổi URL, cần kiểm tra và cập nhật.
- **Node `Extract Available Courses` (Code):**
  - **Không cần chỉnh sửa** (n8n tự động parse dữ liệu từ HTML).

##### **🔹 Bước 3: Xây Dựng Vector Store & Engine Khuyến Nghị**
- **Node `Embeddings Mistral Cloud`:**
  - Chuyển dữ liệu món ăn thành **vector embeddings** để Qdrant xử lý.
- **Node `Qdrant Vector Store`:**
  - Lưu vector vào **collection `hello_fresh`** trong Qdrant.
- **Node `Qdrant Recommend API`:**
  - Sử dụng **API Recommend** của Qdrant để tránh lặp lại món ăn.
  - **Cấu hình:**
    - **Positive Query:** Món ăn khách hàng thích (ví dụ: "Roast Dinner").
    - **Negative Query:** Món ăn khách hàng không thích (ví dụ: "Roast Chicken").

##### **🔹 Bước 4: Tạo Chatbot AI Agent**
- **Node `Chat Trigger` (LangChain):**
  - Khởi động **AI Agent** để chat với người dùng.
- **Node `AI Agent`:**
  - **Prompt mẫu:**
    ```
    Bạn là một AI khuyến nghị món ăn HelloFresh. Hỏi người dùng sở thích (nhiệt, lạnh, cay, ngọt, nhanh/chậm) và trả lời với 3 món ăn phù hợp từ danh sách tuần này.
    ```
  - **Lưu ý:** Có thể **cập nhật prompt** để cải thiện chất lượng khuyến nghị.

##### **🔹 Bước 5: Lưu Trữ Dữ liệu Món Ăn (SQLite)**
- **Node `Save Recipes to DB` (Code):**
  - Lưu **dữ liệu nguyên bản** của món ăn vào **SQLite** (để AI Agent lấy thông tin chi tiết).

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run:**
   - Nhấn **"Test Workflow"** để kiểm tra dữ liệu mẫu.
   - Kiểm tra **log** để đảm bảo không có lỗi.
2. **Bật Active:**
   - Sau khi test thành công, **bật workflow** để hoạt động 24/7.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[**CÁCH LÀM ĐẸP HƠN**]
1. **Kết nối với Slack/Telegram:**
   - Sử dụng **node `n8n-nodes-base.slack`** hoặc **`n8n-nodes-base.telegram`** để gửi gợi ý món ăn qua chatbot.
2. **Lưu Log & Báo Cáo:**
   - Sử dụng **node `n8n-nodes-base.set`** để lưu lịch sử khuyến nghị vào **Google Sheets** hoặc **Airtable**.
3. **Cập Nhật Dữ liệu Tuần Hàng:**
   - Sử dụng **node `n8n-nodes-base.cron`** để tự động scrape và cập nhật món ăn **mỗi thứ 2 hàng tuần**.
4. **Tăng Cường AI với Prompt Engineering:**
   - **Cập nhật prompt** của AI Agent để trả lời **tự nhiên hơn** (ví dụ: "Bạn thích món gì? Nếu không thích, tôi sẽ đề xuất khác").
5. **Dùng cho Nhiều Khách Hàng:**
   - Sử dụng **node `n8n-nodes-base.manualTrigger`** để mỗi khách hàng có **một workflow riêng** với sở thích cá nhân.
:::

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho khách hàng bằng cách **tự động hóa việc tìm kiếm món ăn phù hợp** dựa trên sở thích cá nhân. Với **AI Mistral + Qdrant**, hệ thống không chỉ **nhớ lịch sử** mà còn **cải thiện khuyến nghị** theo thời gian.

**🚀 Hãy áp dụng ngay để:**
✔ **Tiết kiệm thời gian** cho khách hàng.
✔ **Tăng trải nghiệm** với gợi ý món ăn cá nhân hóa.
✔ **Hoạt động tự động** mà không cần can thiệp.

**💡 Cần hỗ trợ?**
- **Join Discord n8n:** [https://discord.com/invite/XPKeKXeB7d](https://discord.com/invite/XPKeKXeB7d)
- **Hỏi trên Forum:** [https://community.n8n.io/](https://community.n8n.io/)

**Happy Hacking!** 🍴🤖