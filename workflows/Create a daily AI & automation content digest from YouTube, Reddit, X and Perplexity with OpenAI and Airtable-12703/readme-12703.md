---
title: "🚀 Tự Động Hóa Tạo Báo Cáo Nội Dung AI Hàng Ngày Từ YouTube, Reddit, X & Perplexity – Khai Thác Dữ Liệu Trending Cho Content Marketing"
description: "Workflow tự động hóa 100% không code để scrap dữ liệu từ YouTube, Reddit, Twitter/X và Perplexity, phân tích bằng AI (OpenAI/GPT-4), tổng hợp báo cáo hàng ngày và lưu trữ trên Airtable. Giúp các sếp tiết kiệm 10+ giờ/tháng và phát hiện xu hướng nội dung mới mẻ."
slug: "tieu-dong-hoa-tao-bao-cao-noi-dung-ai-hang-ngay"
tags: [n8n, automation, content-marketing, ai-summarization, airtable, openai, no-code]
keywords: [tự động hóa nội dung ai, scrap youtube reddit twitter, báo cáo hàng ngày content marketing, n8n workflow ai, phân tích xu hướng nội dung]
---

# 🚀 **Tự Động Hóa Tạo Báo Cáo Nội Dung AI Hàng Ngày – Giải Pháp "Không Code" Cho Content Creators & Marketers**

### **Nỗi Đau Của Các Sếp Trong Content Marketing**
Các sếp thường phải mất **5-10 giờ/ngày** để:
- **Scrap** dữ liệu từ YouTube, Reddit, Twitter/X và các nguồn web khác để tìm kiếm xu hướng.
- **Phân tích** nội dung trending và so sánh với thị trường.
- **Tổng hợp** báo cáo hàng ngày cho team hoặc khách hàng.
- **Lưu trữ** dữ liệu để theo dõi xu hướng dài hạn.

Kết quả? **Thời gian bị "ăn chậm", dữ liệu không được cập nhật kịp thời, và mất cơ hội khai thác xu hướng sớm.**

---
### **🎯 Kết Quả Các Sếp Nhận Được**
Sau khi triển khai workflow này, các sếp sẽ:
✅ **Tiết kiệm 10+ giờ/tháng** – Dữ liệu tự động scrap và phân tích mỗi ngày lúc 8h sáng.
✅ **Nhận báo cáo AI tổng hợp** – Nội dung được tóm tắt, phân loại và gợi ý ý tưởng mới.
✅ **Lưu trữ dữ liệu chi tiết** – Tất cả thông tin được ghi vào **Airtable** để theo dõi xu hướng dài hạn.
✅ **Cá nhân hóa nội dung** – AI phân tích xu hướng và đề xuất chủ đề phù hợp với niche của doanh nghiệp.
✅ **Hoạt động 24/7** – Không cần can thiệp thủ công, workflow chạy tự động hàng ngày.

---
## 🎯 **Cách Làm Hoạt Động**
Workflow này **scrap** dữ liệu từ **4 nguồn chính**:
1. **YouTube** (top 10 video trending + phân tích transcript).
2. **Reddit** (top 5 post rising trong r/n8n).
3. **Twitter/X** (top 50 tweet + xu hướng từ keywords).
4. **Perplexity AI** (top 3 tin tức AI mới nhất).

Sau đó, **AI (OpenAI/GPT-4)** sẽ:
- Phân tích xu hướng.
- Tóm tắt nội dung.
- Gợi ý ý tưởng bài viết/blog.
- **Tự động gửi báo cáo hàng ngày** qua email.
- **Lưu dữ liệu vào Airtable** để theo dõi dài hạn.

---
### **🔧 Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
#### **1. Tài Khoản & API Keys**
| Dịch Vụ | Link Đăng Ký | Ghi Chú |
|---------|------------|---------|
| **YouTube API** | [Google Cloud](https://console.cloud.google.com/) | Cần OAuth 2.0 |
| **Reddit API** | [Reddit Developer](https://www.reddit.com/prefs/apps) | Cần OAuth 2.0 |
| **Airtable** | [Airtable](https://airtable.com/) | Cần API Key |
| **OpenAI API** | [OpenAI](https://platform.openai.com/) | Cần API Key |
| **Perplexity API** | [Perplexity](https://www.perplexity.ai/) | Cần API Key |
| **Apify (Scraper)** | [Apify](https://console.apify.com/) | Cần tài khoản miễn phí |

#### **2. Airtable Template**
- **Tải template** từ [đây](https://airtable.com/appsi00aU0KfhF76Z/shrUtGawO8D1DoaO4) và sao chép vào tài khoản Airtable của mình.

#### **3. Chi Phí (Tính Toàn Bộ)**
| Dịch Vụ | Chi Phí/Lần Chạy |
|---------|------------------|
| **Twitter Scraper** | $0.02 |
| **YouTube Scraper** | $0.07 |
| **Reddit Scraper** | $0.00 |
| **Perplexity AI** | $0.01 |
| **LLM (OpenAI/GPT-4)** | $0.22 |
| **Tổng** | **$0.32/lần chạy** |

---
## 🚀 **Cách Import & Cấu Hình Workflow**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Từ File JSON**
1. **Tải workflow** từ [n8n.io/workflows/12703](https://n8n.io/workflows/12703).
2. **Mở n8n Editor** và nhấn **"Import"** → Chọn file JSON đã tải.
3. **Chọn "Import"** để workflow xuất hiện trên canvas.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Tải JSON** từ link trên và copy toàn bộ nội dung.
2. Trong n8n Editor, nhấn **"Import"** → Chọn **"Paste JSON"** và dán nội dung.
3. **Xác nhận import**.

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này **phức tạp** và cần cấu hình cẩn thận. Dưới đây là **các node quan trọng** cần kiểm tra:

#### **🔹 Node "Daily at 8 AM" (ScheduleTrigger)**
- **Cấu hình lịch chạy**: Đảm bảo workflow chạy **mỗi ngày lúc 8h sáng** (UTC hoặc giờ địa phương tùy chọn).
- **Test run**: Nhấn **"Run"** để kiểm tra lịch chạy.

#### **🔹 Node "Perplexity AI News" & "YouTube"**
- **Kiểm tra API Key**:
  - **Perplexity**: Điền vào `perplexityApi` (tên credentials trong n8n).
  - **YouTube**: Điền `youTubeOAuth2Api` (tạo từ Google Cloud).
- **Tham số YouTube**:
  - **Keywords**: Thay thế bằng **keywords niche** của doanh nghiệp (ví dụ: "AI marketing", "no-code tools").
  - **Lọc Shorts**: Node **"Filter Out Shorts"** sẽ loại bỏ video ngắn.

#### **🔹 Node "Reddit" & "Scrape X"**
- **Reddit**:
  - Điền `redditOAuth2Api` (tạo từ Reddit Developer).
  - **Subreddit**: Thay `r/n8n` thành `r/[tên subreddit]` phù hợp.
- **Twitter/X**:
  - **Keywords**: Thay thế bằng từ khóa liên quan (ví dụ: "AI content", "automation tools").
  - **Scraper Apify**: Cần **tạo tài khoản miễn phí** và **API Key** từ [Apify](https://console.apify.com/).

#### **🔹 Node "OpenAI Chat Model" (LLM)**
- **Model**: Đã cấu hình mặc định là `gpt-4.1-mini` (rẻ hơn GPT-4).
- **API Key**: Điền vào `openAiApi` (tạo từ OpenAI).
- **Prompt**: AI sẽ tự động phân tích dữ liệu, nhưng có thể **cập nhật prompt** trong node `chainLlm` để phù hợp với mục đích cụ thể.

#### **🔹 Node "Airtable" (Lưu Dữ Liệu)**
- **Credentials**: Điền `airtableTokenApi` (tạo từ Airtable).
- **Base & Table**: Chọn **table** tương ứng trong Airtable template đã tải.
- **Fields**: Kiểm tra các trường (`Video Title`, `Reddit Post`, `Twitter Tweet`, `Perplexity News`) có khớp với schema trong Airtable.

#### **🔹 Node "Send a message" (Gmail)**
- **Credentials**: Điền `gmailOAuth2` (tạo từ Gmail).
- **Địa chỉ email**: Thay thế `your-email@example.com` bằng email nhận báo cáo.
- **Tiêu đề & Nội dung**: AI sẽ tự động tạo, nhưng có thể **cập nhật template** trong node `Format Message`.

---
### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run**:
   - Nhấn **"Run"** để chạy workflow với **dữ liệu mẫu**.
   - Kiểm tra **Airtable** và **email** để xác nhận dữ liệu được scrap và gửi đúng.
2. **Bật Active**:
   - Sau khi test thành công, **bật switch "Active"** để workflow chạy tự động hàng ngày.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**
### **1. Cập Nhật Keywords Cho Phù Hợp**
- **YouTube/Reddit/Twitter**: Thay đổi **keywords** trong node `Get Videos`, `n8n Trending`, `Scrape X` để phù hợp với **niche cụ thể** của doanh nghiệp.
- **Ví dụ**:
  - Niche **AI Marketing**: `keywords = ["AI content marketing", "automation tools for marketers"]`
  - Niche **No-Code**: `keywords = ["no-code tools 2024", "low-code platforms"]`

### **2. Tăng Cường Báo Cáo với Slack/Telegram**
- **Thêm node Slack/Telegram** sau `Send a message` để **báo cáo ngay khi có dữ liệu mới**.
- **Cách làm**:
  1. Thêm node `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram`.
  2. Cấu hình `slackWebhookUrl` hoặc `telegramBotToken`.
  3. **Merge** dữ liệu từ Gmail và Slack/Telegram.

### **3. Lưu Log & Theo Dõi Xu Hướng**
- **Thêm node `n8n-nodes-base.set`** để lưu **log hoạt động** vào Airtable.
- **Cách làm**:
  1. Thêm node `Set` sau `Aggregate3`.
  2. Thêm trường `log` với nội dung:
     ```json
     {
       "timestamp": "$node['Daily at 8 AM'].json['$.timestamp']",
       "status": "success",
       "data_count": "$node['Aggregate3'].json['$.data'].length"
     }
     ```
  3. **Merge** với Airtable để theo dõi lịch sử.

### **4. Tự Động Gửi Báo Cáo Cho Nhóm**
- **Thêm node `n8n-nodes-base.email`** để gửi **báo cáo cho nhiều người** cùng lúc.
- **Cách làm**:
  1. Thêm node `Email` sau `Send a message`.
  2. Điền danh sách email trong `to`.
  3. **Merge** với node `Set` để cá nhân hóa nội dung.

### **5. Optimize Chi Phí**
- **Sử dụng model rẻ hơn**:
  - Thay `gpt-4.1-mini` thành `gpt-3.5-turbo` (giá rẻ hơn).
  - **Cập nhật trong node `lmChatOpenAi`**.
- **Lọc dữ liệu trước khi phân tích**:
  - Thêm node `If` để **bỏ qua video/post không liên quan**.

---
## 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn:
✔ **Tự động hóa scrap & phân tích dữ liệu** từ nhiều nguồn.
✔ **Nhận báo cáo hàng ngày** được tổng hợp bởi AI.
✔ **Lưu trữ dữ liệu dài hạn** trên Airtable.
✔ **Tiết kiệm thời gian** và **phát hiện xu hướng sớm**.

**🚀 Hành động ngay!**
1. **Import workflow** và cấu hình API.
2. **Test run** để đảm bảo hoạt động.
3. **Bật Active** và **nhận báo cáo hàng ngày**!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**Chia sẻ & phản hồi:**
Nếu có **vấn đề trong quá trình cấu hình**, hãy để lại comment bên dưới hoặc liên hệ với **Chase Hannegan** (tác giả workflow) qua [Skool](https://www.skool.com/chase-ai). 🚀