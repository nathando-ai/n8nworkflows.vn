---
title: "🚀 Tự Động Hóa Bài Đăng LinkedIn Từ RSS Với AI Ollama + Xác Nhận Telegram + Theo Dõi PostgreSQL (Human-in-the-Loop)"
description: "Workflow tự động hóa 100% không code giúp các sếp tự động thu thập tin tức từ RSS, tổng hợp nội dung bằng AI Ollama, lấy ý kiến xác nhận qua Telegram, và đăng bài lên LinkedIn chỉ trong vài giây. Giảm thiểu công việc thủ công 90% trong quản lý nội dung xã hội."
slug: "tieu-dong-hoa-bai-dang-linkedin-tu-rss-voi-ollama-telegram-postgres"
tags: [n8n, automation, social-media, ai-summarization, ollama, linkedin, telegram, postgres, human-in-the-loop]
keywords: [n8n workflow tự động hóa, đăng bài LinkedIn tự động, tổng hợp tin tức bằng AI Ollama, xác nhận nội dung qua Telegram, cơ sở dữ liệu PostgreSQL, tự động hóa nội dung xã hội]
---

# 🚀 **Tự Động Hóa Bài Đăng LinkedIn Từ RSS Với AI Ollama + Xác Nhận Telegram + Theo Dõi PostgreSQL**

## **Giải Phẫu Nỗi Đau Của Các Sếp Trong Quản Lý Nội Dung Xã Hội**
Các sếp thường phải:
- **Tốn thời gian** để theo dõi và tổng hợp tin tức từ nhiều nguồn RSS khác nhau.
- **Lo ngại chất lượng nội dung** khi tự động hóa hoàn toàn (AI có thể sai lệch hoặc không phù hợp với brand voice).
- **Không kiểm soát được** khi bài đăng được tự động đăng lên LinkedIn mà không được xác nhận.
- **Không có hệ thống theo dõi** để biết bài nào đã được đăng, bài nào bị từ chối, và lý do tại sao.

**Workflow này giải quyết tất cả!** Nó kết hợp **AI Ollama** để tổng hợp tin tức nhanh chóng, **Telegram** để các sếp xác nhận nội dung trước khi đăng, và **PostgreSQL** để theo dõi toàn bộ quá trình. Kết quả? **Nội dung chất lượng cao, tự động hóa hoàn toàn, nhưng vẫn có sự kiểm soát con người.**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính bảo mật và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian** lên đến **90%** trong việc thu thập và tổng hợp tin tức.
✅ **Nội dung chất lượng cao** nhờ AI Ollama tổng hợp và các sếp xác nhận trước khi đăng.
✅ **Kiểm soát hoàn toàn** qua Telegram, tránh đăng bài không phù hợp.
✅ **Theo dõi toàn diện** tất cả bài đăng, trạng thái, và lý do từ chối trong PostgreSQL.
✅ **Tự động hóa hoàn toàn** sau khi cấu hình, không cần can thiệp thủ công.
✅ **Phù hợp với brand voice** của doanh nghiệp, tránh nội dung không chuyên nghiệp.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
#### **1. Tài Khoản & API Keys**
| Tài Khoản/Dịch Vụ          | Mô Tả                                                                 | Làm Thế Nào Để Lấy?                                                                 |
|----------------------------|------------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| **Ollama Local AI**        | Máy chủ Ollama cài đặt trên máy hoặc VPS để chạy mô hình AI.          | [Tải Ollama](https://ollama.ai/) và cài đặt mô hình `qwen2.5:3b`.                     |
| **PostgreSQL Database**    | Cơ sở dữ liệu để lưu trữ bài viết, trạng thái, và metadata.           | [Cài đặt PostgreSQL](https://www.postgresql.org/download/) hoặc sử dụng VPS có sẵn. |
| **Telegram Bot**           | Bot Telegram để nhận và gửi yêu cầu xác nhận.                        | Tạo bot trên [@BotFather](https://t.me/BotFather) và lấy `API Token`.                |
| **LinkedIn OAuth2**        | Tài khoản LinkedIn để đăng bài tự động.                              | [Tạo ứng dụng LinkedIn](https://www.linkedin.com/developers/) và lấy `Client ID/Secret`. |
| **RSS Feed Sources**       | Các nguồn tin tức RSS (ví dụ: TechCrunch, BBC News, Forbes).          | Lấy từ trang web hoặc sử dụng công cụ như [Feedly](https://feedly.com/).              |

#### **2. Database Schema (PostgreSQL)**
Workflow yêu cầu **bảng `rss_feed_articles`** với cấu trúc như sau:
```sql
CREATE TABLE rss_feed_articles (
    id SERIAL PRIMARY KEY,
    creator TEXT,
    title TEXT NOT NULL,
    link TEXT NOT NULL,
    published_date TIMESTAMP,
    summary TEXT,
    category VARCHAR(100),
    keywords TEXT[],
    sentiment VARCHAR(20),
    important_points TEXT[],
    is_approved BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```
**Lưu ý:** Các sếp có thể thêm cột tùy chỉnh như `brand_voice` hoặc `post_schedule` nếu cần.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/15720](https://n8n.io/workflows/15720) và import vào **n8n Editor**.
- **Cách 2:** Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/15720) và dán vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **3 lớp chính**:
1. **AI Processing Layer** (Tự động hóa)
2. **Human Governance Layer** (Xác nhận con người)
3. **PostgreSQL Audit Tracking** (Theo dõi)

##### **A. Cấu Hình Credentials (Tất Cả Các Node)**
| Node Name               | Loại Node          | Credentials Cần Chỉnh                          | Tham Số Khóa (Key Parameters)          |
|-------------------------|--------------------|-----------------------------------------------|----------------------------------------|
| **Ollama Chat Model**   | `lmChatOllama`     | `ollamaApi` (API Key Ollama)                  | `model: qwen2.5:3b`                   |
| **Telegram Trigger**    | `telegramTrigger`  | `telegramApi` (Token Telegram Bot)            | -                                      |
| **Send message and wait for response** | `telegram` | `telegramApi` (Token Telegram Bot) | `operation: sendAndWait` |
| **Create a post**       | `linkedIn`         | `linkedInOAuth2Api` (Client ID/Secret)        | -                                      |
| **PostgreSQL Nodes**    | `postgres`         | `postgres` (Tên DB, Host, Port, Username, Password) | `operation: select/insert/update` |

**Hướng dẫn chi tiết:**
1. **Ollama:**
   - Đảm bảo mô hình `qwen2.5:3b` đã được cài đặt trên Ollama.
   - Trong **Credentials**, chọn `ollamaApi` và điền `host: http://localhost:11434` (nếu Ollama chạy trên máy chủ local).

2. **Telegram:**
   - Tạo bot Telegram và lấy `API Token`.
   - Trong **Credentials**, chọn `telegramApi` và điền `token: YOUR_TELEGRAM_BOT_TOKEN`.
   - **Node "Send message and wait for response"** cần cấu hình:
     - `chatId`: ID chat của bot (lấy từ Telegram khi gửi tin nhắn cho bot).
     - `text`: Nội dung yêu cầu xác nhận (ví dụ: `Xác nhận bài viết này? [TÍT LE: {{ $node["RSS Read"].json()["title"] }}]`).

3. **LinkedIn:**
   - Đăng ký ứng dụng trên LinkedIn Developer và lấy `Client ID` và `Client Secret`.
   - Trong **Credentials**, chọn `linkedInOAuth2Api` và điền thông tin OAuth2.

4. **PostgreSQL:**
   - Đảm bảo bảng `rss_feed_articles` đã được tạo.
   - Trong **Credentials**, điền:
     - `host`: IP hoặc địa chỉ máy chủ PostgreSQL.
     - `port`: 5432 (mặc định).
     - `database`: Tên cơ sở dữ liệu.
     - `username` và `password`: Thông tin đăng nhập.

##### **B. Cấu Hình Node Quan Trọng**
1. **RSS Feed Read Trigger (`rssFeedReadTrigger`):**
   - Điền **URL RSS** của nguồn tin tức (ví dụ: `https://feeds.bbci.co.uk/news/rss.xml`).
   - Chọn **Item Path**: `$` (truy cập toàn bộ item).

2. **Split In Batches (`splitInBatches`):**
   - Đặt **Batch Size**: 1 (để xử lý một bài viết một lần).

3. **AI Agent (`agent`):**
   - Node này kết hợp với **Ollama Chat Model** để tổng hợp tin tức.
   - **Không cần cấu hình thêm**, chỉ cần đảm bảo `ollamaApi` đã được thiết lập.

4. **If Conditions (Xác Nhận Trạng Thái):**
   - Node `If` và `If1` kiểm tra:
     - `is_approved` trong PostgreSQL.
     - Trạng thái phản hồi từ Telegram.
   - **Cấu hình:**
     - `If`: Kiểm tra `{{ $json["is_approved"] }} === true`.
     - `If1`: Kiểm tra phản hồi từ Telegram (`{{ $json["text"] }} === "Approved"`).

5. **Update Rows in a Table (`postgres`):**
   - Khi bài viết được **xác nhận**, cập nhật `is_approved = true`.
   - Khi **bị từ chối**, cập nhật `is_approved = false` và thêm cột `reason` (nếu cần).

##### **C. Test Run & Active Workflow**
1. **Test Run:**
   - Chọn **Test Tab** trong n8n Editor.
   - Chọn **RSS Feed Trigger** và nhấn **Execute**.
   - Kiểm tra:
     - AI có tổng hợp tin tức không?
     - Telegram có gửi yêu cầu xác nhận không?
     - PostgreSQL có lưu bài viết không?

2. **Active Workflow:**
   - Sau khi test thành công, chuyển **Active** và **Save**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tự Động Xóa Bài Viêt Trước Khi Đăng:**
   - Thêm node `If` sau `Select rows from a table` để kiểm tra `is_approved = false` và **xóa bài viết** từ PostgreSQL trước khi đăng.

2. **Gửi Báo Cáo Hàng Tuần:**
   - Sử dụng **n8n Scheduler** để chạy workflow hàng tuần và gửi báo cáo thống kê (số bài đăng, tỷ lệ xác nhận, bài bị từ chối) qua **Email** hoặc **Telegram**.

3. **Lưu Log Chi Tiết:**
   - Thêm node `stickyNote` để lưu log của mỗi bước (ví dụ: thời gian tổng hợp, phản hồi Telegram, trạng thái đăng).

4. **Kết Hợp Với Slack:**
   - Thay vì Telegram, các sếp có thể sử dụng **Slack** để xác nhận bằng cách:
     - Thêm node `slack` và cấu hình `sendAndWait`.
     - Tạo **Slack App** và lấy `Token` từ [API Slack](https://api.slack.com/apps).

5. **Tùy Chỉnh Brand Voice:**
   - Trong **Ollama Prompt**, thêm yêu cầu về **tone của brand**:
     ```json
     "prompt": "Tóm tắt bài viết này với tone chuyên nghiệp và phù hợp với brand của {{ $json["creator"] }}. Không sử dụng từ ngữ quá kỹ thuật."
     ```

6. **Lưu Trữ Bài Viêt Trước Khi Đăng:**
   - Thêm node `noOp` để lưu bài viết vào **Google Drive** hoặc **Dropbox** trước khi đăng, để có thể khôi phục nếu cần.

---

### 📌 **Kết Luận: Đăng Bài LinkedIn Chỉ Với Nhấn Chữa**
Workflow này **giải phóng thời gian** của các sếp để tập trung vào nội dung chất lượng cao hơn, trong khi tự động hóa phần thủ công. **Kết hợp AI Ollama, xác nhận con người qua Telegram, và theo dõi PostgreSQL** tạo ra một hệ thống **tự động hóa hoàn toàn nhưng vẫn kiểm soát được**.

**Bước đầu tiên:**
1. **Cài đặt Ollama** và cài mô hình `qwen2.5:3b`.
2. **Import workflow** và cấu hình credentials.
3. **Test run** và **active** workflow.
4. **Theo dõi và tối ưu** qua PostgreSQL.

**Kết quả?** **Nội dung LinkedIn được đăng tự động, chất lượng cao, và hoàn toàn an toàn cho brand!**

---
**🚀 Hãy áp dụng ngay và giảm thiểu công việc thủ công trong quản lý nội dung xã hội!**