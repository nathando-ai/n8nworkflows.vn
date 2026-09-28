---
title: "🤖 **Tự Động Scrape & Tái Lập Lại Bài Đăng LinkedIn AI với Apify, Groq, OpenAI & Google Sheets**"
description: "Workflow tự động hóa 100% không code để scrape bài đăng LinkedIn từ bất kỳ tài khoản nào, lọc nội dung liên quan đến AI, tái lập lại với phong cách chuyên nghiệp và lưu kết quả vào Google Sheets. Giúp content creator, quản lý mạng xã hội và nhà nghiên cứu tiết kiệm thời gian lên đến 80% trong việc curate nội dung chất lượng cao."
slug: "tieu-dong-scrape-tai-lap-lai-bai-dang-linkedin-ai"
tags: [n8n, automation, no-code, content-creation, ai-summarization, apify, groq, openai, google-sheets]
keywords: [tự động hóa scrape linkedin, tái lập lại bài đăng ai, workflow n8n content creation, tự động hóa nội dung ai, scrape bài đăng linkedin không code, google sheets tự động hóa]
---

# 🚀 **Scrape & Tái Lập Lại Bài Đăng LinkedIn AI: Giải Pháp Tự Động Hóa Cho Content Creator**

### **Nỗi Đau Của Các Sếp**
Các sếp trong lĩnh vực **content marketing**, **AI research** hoặc **quản lý mạng xã hội** thường phải mất **giờ đồng hồ** để:
- **Scrape** bài đăng từ LinkedIn (thường phải dùng các công cụ có phí hoặc viết script).
- **Lọc** nội dung chất lượng, đặc biệt là về **AI, công nghệ mới** hay **cập nhật ngành**.
- **Tái lập lại** bài đăng thành văn bản **chuyên nghiệp, dễ hiểu** (không jargon) để phù hợp với **newsletter, blog hay social media**.
- **Lưu trữ** kết quả một cách **đơn giản và dễ theo dõi**.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách tự động hóa toàn bộ quy trình – chỉ cần một lần setup!**

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên **VPS riêng** thay vì dùng phiên bản cloud.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** – giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đảm bảo tốc độ cao, phù hợp cho AI workload)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian lên đến 80%** – Không phải scrape thủ công hoặc viết script.
✅ **Nội dung AI chất lượng cao** – Bài đăng được **lọc, tái lập lại** với phong cách **chuyên nghiệp, không jargon**.
✅ **Lưu trữ tự động** – Kết quả được ghi vào **Google Sheets** với định dạng **sẵn sàng xuất bản**.
✅ **Hoạt động liên tục** – Workflow chạy **24/7** khi được self-host.
✅ **Dễ mở rộng** – Thêm được **Slack/Telegram notification**, **email báo cáo định kỳ** hoặc **kết hợp với Notion**.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
📌 **Tài khoản & API Keys:**
- **Apify** (để scrape LinkedIn) → [Đăng ký miễn phí](https://apify.com/)
- **Groq API Key** (để lọc bài đăng AI) → [Đăng ký Groq](https://console.groq.com/)
- **OpenAI API Key** (để tái lập lại bài đăng) → [Đăng ký OpenAI](https://platform.openai.com/)
- **Google Sheets** (để lưu kết quả) → [Tạo bảng mới](https://sheets.google.com/)

📌 **Bảng Google Sheets chuẩn bị sẵn:**
- **Cột cần thiết:**
  - `Author` (Tác giả)
  - `Date` (Ngày đăng)
  - `Original Post` (Bài đăng gốc)
  - `Rewrite Post` (Bài đăng tái lập lại)

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow:
✅ **Tải file JSON từ n8n.io:**
1. Truy cập [workflow gốc](https://n8n.io/workflows/15453).
2. Nhấp vào **"Export"** (góc trên bên phải).
3. **Upload** file `.json` vào **n8n Editor** của mình.

✅ **Copy/Paste JSON vào Editor:**
1. Mở **n8n Editor** → **"Import"** → **"From JSON"**.
2. Dán toàn bộ mã JSON từ [đây](https://n8n.io/workflows/15453) (hoặc tải file đã export).
3. Nhấp **"Import"**.

---

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Sau khi import, các sếp **phải cấu hình** các node quan trọng sau:

##### **🔹 Node 1: "On form submission" (formTrigger)**
- **Không cần chỉnh** (sẵn sàng sử dụng).
- **Cách sử dụng:**
  - Mở **form** bằng cách nhấp vào **"Open"** trên node này.
  - Nhập:
    - **LinkedIn Profile URL** (ví dụ: `https://www.linkedin.com/in/elonmusk/`)
    - **Number of Posts** (số bài đăng muốn scrape, tối đa 1000/1 lần).

##### **🔹 Node 2: "Run an Actor and get dataset" (Apify)**
- **Cấu hình:**
  - Nhấp **"Add"** → Chọn **"Apify"** → **"OAuth2"**.
  - Đăng nhập **Apify** và cấp quyền.
  - **Actor ID:** `linkedin-post-scraper` (sẵn sàng, không cần thay đổi).
  - **Run Parameters:**
    ```json
    {
      "startUrl": "{{$json["linkedinProfileUrl"]}}",
      "maxPosts": "{{$json["numberOfPosts"]}}"
    }
    ```
  - **Lưu ý:**
    - **Mỗi 1000 bài đăng** ≈ **$1** (do Apify tính phí).
    - **Không cần cookies** – Apify scrape được mà không bị chặn.

##### **🔹 Node 3: "Groq Chat Model" (lmChatGroq)**
- **Cấu hình:**
  - Nhấp **"Add"** → **"Groq"** → **"API Key"**.
  - Dán **API Key** từ Groq vào.
  - **Model:** `llama-3.3-70b-versatile` (sẵn sàng).
  - **Prompt mẫu (không cần chỉnh):**
    ```json
    {
      "verdict": "relevant" if the post is about AI tools, news, agents, or industry updates; otherwise "not_relevant"
    }
    ```

##### **🔹 Node 4: "Structured Output Parser" (outputParserStructured)**
- **Không cần chỉnh** (sẵn sàng với schema JSON).
- **Nó đảm bảo** Groq trả về **cấu trúc JSON chuẩn**:
  ```json
  {"verdict": "relevant"}
  ```

##### **🔹 Node 5: "If" (if)**
- **Không cần chỉnh** (sẽ tự động **bỏ qua** bài đăng không liên quan).

##### **🔹 Node 6: "OpenAI Chat Model" (lmChatOpenAi)**
- **Cấu hình:**
  - Nhấp **"Add"** → **"OpenAI"** → **"API Key"**.
  - Dán **API Key** từ OpenAI vào.
  - **Model:** `gpt-5-mini` (nếu không có, thay bằng `gpt-4o-mini`).
  - **Prompt tái lập lại bài đăng (không cần chỉnh):**
    ```json
    Rewrite the following LinkedIn post in a clear, professional, and jargon-free style. Keep it concise (100-200 words). Maintain the original meaning but make it more engaging for a general audience.
    ```

##### **🔹 Node 7: "Append row in sheet" (googleSheets)**
- **Cấu hình:**
  - Nhấp **"Add"** → **"Google Sheets"** → **"OAuth2"**.
  - Đăng nhập **Google** và cấp quyền.
  - **Chọn Sheet ID** (tìm trong URL của bảng Google Sheets của bạn, ví dụ: `1AbCdEfGhIjKlMnOpQrStUvWxYz`).
  - **Range:** `Sheet1!A1:D1` (đảm bảo cột `A` là `Author`, `B` là `Date`, `C` là `Original Post`, `D` là `Rewrite Post`).

##### **🔹 Node 8-10: "Rewrite post", "Verify The authenticity", "Simple Memory" (agent & memoryBufferWindow)**
- **Không cần chỉnh** (sẵn sàng, sử dụng **LangChain** để tối ưu quá trình tái lập lại).

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run (kiểm tra trước khi chạy thật):**
   - Nhấp **"Execute"** trên node **"On form submission"**.
   - Nhập **URL LinkedIn** và **số bài đăng** (ví dụ: 5 bài).
   - Kiểm tra **Google Sheets** xem kết quả có được ghi không.

2. **Bật Active Workflow:**
   - Nhấp **"Active"** trên node **"On form submission"**.
   - Workflow sẽ **chạy tự động** mỗi khi có form submission.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁCH LÀM NGOÀI THƯỜNG]
🔹 **Gửi thông báo Slack/Telegram khi có bài đăng mới:**
- Thêm **node `webhook`** sau **"Append row in sheet"** để gửi **webhook** đến Slack/Telegram.
- **Cài đặt:** `https://hooks.slack.com/services/...` (Slack) hoặc `https://api.telegram.org/bot/...` (Telegram).

🔹 **Lưu log vào Notion:**
- Thêm **node `notion`** để ghi lại **tất cả bài đăng** vào một **Notion Database**.

🔹 **Gửi báo cáo định kỳ (hàng tuần):**
- Sử dụng **node `set` + `schedule`** để gửi **email tổng hợp** các bài đăng mới qua **Gmail API**.

🔹 **Tái lập lại nhiều ngôn ngữ:**
- Thay đổi **prompt OpenAI** để hỗ trợ **tiếng Việt, tiếng Anh, tiếng Nhật...**.

🔹 **Lọc bài đăng theo từ khóa cụ thể:**
- Thay đổi **prompt Groq** để chỉ lấy bài đăng về **AI, blockchain, hoặc marketing digital**.
:::

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn:
✔ **Tự động scrape** bài đăng LinkedIn **không cần code**.
✔ **Lọc & tái lập lại** nội dung AI **chuyên nghiệp, dễ hiểu**.
✔ **Lưu kết quả** vào **Google Sheets** để **xuất bản nhanh chóng**.

**Hành động ngay:**
1. **Setup** theo hướng dẫn trên.
2. **Chạy test** với 5-10 bài đăng.
3. **Bật Active** và **nhận nội dung AI chất lượng hàng ngày!**

**🚀 CÓ THỂ TỰ ĐỘNG HÓA GÌ KHÁC?** Hãy **share workflow** của mình trên [n8n Community](https://community.n8n.io/) để cùng học hỏi! 🤝