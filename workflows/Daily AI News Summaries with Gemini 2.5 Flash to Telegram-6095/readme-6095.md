---
title: "🤖 Tự Động Hóa Tóm Tắt Tin AI Hàng Ngày Với Gemini 2.5 Flash → Telegram (Không Cần Code)"
description: "Workflow tự động hóa lấy tin tức AI mới nhất từ RSS, tóm tắt bằng Gemini 2.5 Flash, và gửi báo cáo định kỳ qua Telegram. Giúp các sếp tiết kiệm 3+ giờ/tuần theo dõi tin tức chuyên ngành."
slug: "tieu-dong-hoa-tom-tat-tin-ai-voi-gemini-telegram"
tags: [n8n, automation, ai-summarization, telegram-bot, gemini-ai, no-code]
keywords: [tự động hóa tin tức AI, gemini 2.5 flash telegram, n8n workflow ai, tóm tắt tin tức tự động, RSS feed telegram, AI news summary]
---

# 🚀 **Tự Động Hóa Tóm Tắt Tin AI Hàng Ngày Với Gemini 2.5 Flash → Telegram**

### **Giải pháp cho các sếp bận rộn:**
Hàng ngày, các sếp phải mất **30-60 phút** để đọc, lọc và tóm tắt tin tức từ các nguồn AI/ML, sau đó chia sẻ với đội nhóm. **Workflow này tự động hóa toàn bộ quy trình** bằng cách:
✅ **Lấy tin tức mới nhất** từ RSS của *Artificial Intelligence News* (một trong những nguồn tin AI uy tín nhất).
✅ **Tóm tắt bằng Gemini 2.5 Flash** (mô hình AI mới nhất của Google) với độ chính xác cao.
✅ **Gửi báo cáo định kỳ** qua Telegram (hoặc Slack) **mỗi khi có tin mới**, không cần can thiệp thủ công.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm 3+ giờ/tuần** theo dõi tin tức AI thủ công.
- **Tóm tắt chính xác** với Gemini 2.5 Flash (không bị lỗi hiểu sai như các mô hình cũ).
- **Cá nhân hóa** bằng cách điều chỉnh prompt để phù hợp với lĩnh vực chuyên môn (AI, ML, Robotics...).
- **Hoạt động 24/7** mà không cần mở máy tính.
- **Dễ dàng mở rộng** để gửi báo cáo qua Slack, Email, hoặc lưu vào Google Sheets.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[**CHUẨN BỊ**]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Telegram** và **Chat ID** của nhóm/đội nhóm (có thể lấy bằng cách gửi `/get_id` trong chat với bot `@rawdata_bot`).
2. **API Key của Google Gemini**:
   - Đăng ký tại [Google AI Studio](https://makersuite.google.com/app/apikey) và tạo một API key.
   - Thêm credential mới trong n8n với tên `googlePalmApi` và gán API key.
3. **API Key của Jina AI** (để scrape nội dung bài viết):
   - Đăng ký tại [Jina AI](https://www.jina.ai/) và lấy API key.
   - Thêm credential mới trong n8n với tên `jinaAiApi`.
4. **n8n Self-hosted** (không dùng phiên bản miễn phí của n8n.io để workflow hoạt động liên tục).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow theo **2 cách**:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/6095) và import vào n8n Editor.
- **Copy/paste JSON** từ [đây](https://n8n.io/workflows/6095) vào n8n Editor (chọn **Import Workflow** → **Paste JSON**).

:::note[**Lưu ý**]
- **Không sử dụng phiên bản n8n.io miễn phí** vì workflow sẽ ngừng hoạt động khi không hoạt động trong 14 ngày.
- **Không cần cài đặt node nào thêm** vì workflow đã sử dụng các node chuẩn (Jina AI, Telegram, Gemini).
:::

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow có **5 node chính**, các sếp cần cấu hình kỹ lưỡng như sau:

#### **🔹 Node 1: `AI-News Feed` (rssFeedReadTrigger)**
- **Không cần chỉnh sửa gì** vì nó tự động lấy tin từ `https://www.artificialintelligence-news.com/feed/` mỗi phút.
- **Lưu ý**: Nếu RSS feed bị thay đổi, các sếp phải cập nhật URL trong **Properties → URL**.

#### **🔹 Node 2: `Read News from AI Website` (jinaAi)**
- **Input**: Node này nhận **`link`** từ node RSS Feed.
- **Cấu hình**:
  - Trong **Credentials**, chọn `jinaAiApi` (đã thêm trước đó).
  - **Lưu ý**: Nếu Jina AI bị giới hạn request, các sếp có thể **thay thế bằng node `http` + `webhook`** để scrape nội dung bằng Python (mô tả chi tiết ở phần **Mẹo nâng cao**).
- **Output**: Nội dung bài viết sạch sẽ (không có HTML tag).

#### **🔹 Node 3: `Gemini 2.5 Flash` (lmChatGoogleGemini)**
- **Input**: Nội dung bài viết từ node Jina AI.
- **Cấu hình**:
  - Trong **Credentials**, chọn `googlePalmApi`.
  - **Prompt mặc định** đã được tối ưu để tóm tắt tin tức AI:
    ```plaintext
    You are an AI assistant specialized in summarizing news articles about Artificial Intelligence.
    Your task is to create a concise, well-structured summary of the latest article.
    Focus on:
    - Key findings or breakthroughs.
    - Implications for the AI industry.
    - Any new technologies or research mentioned.
    - Quotes from experts (if available).
    Format the summary as follows:
    ---
    [Title of the Article]
    ---
    [Summary (3-5 sentences)]
    ---
    [Key Takeaways (bullet points)]
    ---
    [Relevance to AI Industry (1-2 sentences)]
    ---
    ```
  - **Lưu ý**: Các sếp có thể **chỉnh sửa prompt** để phù hợp với lĩnh vực riêng (ví dụ: Robotics, NLP...).
- **Output**: Báo cáo tóm tắt được gửi đến node Telegram.

#### **🔹 Node 4: `Generate Report` (chainLlm)**
- **Input**: Kết quả từ node Gemini.
- **Cấu hình**:
  - **Không cần chỉnh sửa** vì nó tự động kết nối với node Gemini.
  - **Lưu ý**: Nếu muốn thay đổi mô hình AI, các sếp phải **cài đặt node `@n8n/n8n-nodes-langchain`** và chọn mô hình khác (ví dụ: Llama 3).

#### **🔹 Node 5: `Send a text message` (telegram)**
- **Input**: Báo cáo từ node `Generate Report`.
- **Cấu hình**:
  - Trong **Credentials**, chọn `telegramApi`.
  - **Chat ID**: Nhập **Chat ID** của nhóm Telegram (có thể lấy bằng cách gửi `/get_id` trong chat với bot `@rawdata_bot`).
  - **Lưu ý**: Nếu muốn gửi báo cáo qua **Slack**, các sếp phải **thay thế node Telegram bằng node `slack`** và cấu hình tương tự.

---

### **3. Kích hoạt ⚡️**
1. **Test run** với một bài viết mẫu:
   - Chọn **Run Workflow** và kiểm tra kết quả trên Telegram.
2. **Bật Active**:
   - Chuyển trạng thái workflow từ **Inactive** sang **Active** để nó hoạt động liên tục.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::info[**Mở rộng tính năng**]
1. **Gửi báo cáo qua Email**:
   - Thay thế node Telegram bằng node `n8n-nodes-base.email` và cấu hình SMTP.
2. **Lưu báo cáo vào Google Sheets**:
   - Thêm node `n8n-nodes-base.googleSheets` sau node Telegram để lưu lịch sử báo cáo.
3. **Chỉ gửi tin tức mới nhất**:
   - Thêm node `n8n-nodes-base.set` để lọc bỏ tin tức đã gửi trước.
4. **Thay thế Jina AI bằng Python**:
   - Nếu Jina AI bị giới hạn, các sếp có thể:
     - Tạo một **webhook Python** (bằng Flask/FastAPI) để scrape nội dung.
     - Kết nối nó với node `n8n-nodes-base.httpRequest`.
5. **Tùy chỉnh thời gian gửi**:
   - Thay đổi **interval** của node RSS Feed từ **1 phút** sang **5 phút** để giảm tải server.
6. **Dùng nhiều RSS feed**:
   - Thêm node `n8n-nodes-base.split` để lấy tin từ **nhiều nguồn RSS** (ví dụ: VentureBeat, TechCrunch).

---
## 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tự động hóa theo dõi tin tức AI** mà không cần viết code. Với **Gemini 2.5 Flash**, báo cáo sẽ **được tóm tắt chính xác và chuyên nghiệp**, sau đó được gửi trực tiếp qua Telegram (hoặc Slack/Email).

👉 **Hành động ngay**:
1. **Cài đặt n8n Self-hosted** trên VPS (để workflow hoạt động 24/7).
2. **Import workflow** và cấu hình API keys.
3. **Bật Active** và bắt đầu nhận báo cáo AI hàng ngày!

**Cần hỗ trợ?** Đăng ký **VPS n8n** từ [TinoHost](https://tino.vn/vps-n8n?affid=388) và liên hệ với chúng tôi để được tư vấn chi tiết! 🚀