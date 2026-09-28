---
title: "🚀 Tự Động Hoà Tạo Tạp Chí Tin Tức Cá Nhân Hóa AI với QWEN & Gemma – Không Cần Code!"
description: "Workflow tự động hóa lấy tin tức từ RSS, phân tích, tóm tắt và gửi newsletter cá nhân hóa hàng ngày qua Gmail bằng AI QWEN & Gemma. Tiết kiệm 5+ giờ/tuần cho các sếp và nhân viên marketing!"
slug: "tap-chi-tin-tuc-ai-personalized-newsletter"
tags: [n8n, automation, ai-summarization, gmail, ollama, postgres, rss-feed]
keywords: [n8n workflow newsletter, tự động hóa tin tức cá nhân hóa, qwen gemma newsletter, rss feed to email, ai summarize articles]
---

# 🚀 **Tự Động Hoà Tạo Tạp Chí Tin Tức Cá Nhân Hóa AI – Không Cần Code!**

### **Giải pháp cho các sếp và marketer:**
Bạn đã bao giờ phải mất **5+ giờ/tuần** để:
- Lọc tin tức từ nhiều nguồn RSS?
- Tóm tắt và chọn lọc nội dung chất lượng?
- Gửi newsletter cá nhân hóa cho khách hàng/đội nhóm?
- Lo lắng về tính chính xác và thời gian thực?

**Workflow này tự động hóa toàn bộ quy trình** bằng AI QWEN & Gemma, giúp bạn:
✅ **Tiết kiệm 90% thời gian** trong việc tổng hợp tin tức.
✅ **Cá nhân hóa nội dung** dựa trên sở thích của từng người nhận.
✅ **Lọc tin chất lượng** (điểm số ≥7/10) bằng AI.
✅ **Gửi tự động hàng ngày** qua Gmail (hoặc định kỳ theo lịch).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Không cần can thiệp thủ công.
- **Nội dung cá nhân hóa**: AI phân tích sở thích và gửi tin tức phù hợp.
- **Chất lượng cao**: Chỉ giữ lại tin tức được đánh giá ≥7/10.
- **Hoạt động liên tục**: Gửi newsletter hàng ngày (hoặc theo lịch).
- **Dữ liệu lưu trữ**: Tất cả tin tức được lưu vào cơ sở dữ liệu PostgreSQL.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Ollama** (để chạy mô hình AI QWEN & Gemma):
   - Cài đặt [Ollama](https://ollama.com/) và tải mô hình:
     ```bash
     ollama pull qwen3:14b-q4_K_M
     ollama pull gemma3:latest
     ```
2. **Tài khoản Gmail** (để gửi newsletter):
   - **Enable Gmail API** và tạo **OAuth 2.0 Credentials** (trong [Google Cloud Console](https://console.cloud.google.com/)).
3. **Cơ sở dữ liệu PostgreSQL**:
   - Tạo một cơ sở dữ liệu mới và lưu trữ thông tin tin tức.
4. **RSS Feeds**:
   - Danh sách các nguồn RSS bạn muốn theo dõi (ví dụ: TechCrunch, BBC News, Forbes).
5. **Sở thích cá nhân hóa**:
   - Danh sách từ khóa/ngành nghề mà người nhận quan tâm (ví dụ: "AI", "Tin tức công nghệ", "Thể thao").

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/5400](https://n8n.io/workflows/5400) hoặc copy toàn bộ JSON từ canvas.
- Mở **n8n Editor** → Nhấn **"Import"** → Dán JSON và nhấn **"Import Workflow"**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **25 node**, nhưng các bước quan trọng nhất cần chú ý:

##### **A. Cấu hình AI (QWEN & Gemma)**
- **Node `Model QWEN3 14B-q4`** và `Model Gemma3 4B`:
  - Đảm bảo đã **tải mô hình** trên Ollama (như hướng dẫn trên).
  - **Credentials**: Chọn `"ollamaApi"` (đã cấu hình trong n8n).
  - **Key Parameters**:
    - `model`: Đặt theo mô hình đã tải (ví dụ: `qwen3:14b-q4_K_M`).

##### **B. Cấu hình Gmail**
- **Node `Send Email Newsletter`**:
  - **Credentials**: Chọn `"gmailOAuth2"` (đã cấu hình OAuth 2.0).
  - **Điền địa chỉ email** của người nhận (ví dụ: `nguyenvan@doanhnghiep.com`).
  - **Chủ đề email**: Thay thế `"Your Newsletter Subject"` bằng tiêu đề cá nhân hóa (ví dụ: `"Tin tức AI hàng ngày cho bạn - [Ngày]"`).

##### **C. Cấu hình RSS Feeds**
- **Node `RSS Read`**:
  - **Điền URL RSS** của các nguồn tin bạn muốn theo dõi (ví dụ: `https://feeds.bbci.co.uk/news/rss.xml`).
  - **Lưu ý**: Nếu muốn theo dõi nhiều nguồn, thêm nhiều node `RSS Read` và sử dụng `Merge` để kết hợp dữ liệu.

##### **D. Cấu hình PostgreSQL**
- **Node `Create DB and Schema if not exists`**:
  - **Credentials**: Chọn `"postgres"` (đã cấu hình trong n8n).
  - **Query SQL**:
    ```sql
    CREATE TABLE IF NOT EXISTS articles (
      id SERIAL PRIMARY KEY,
      title TEXT,
      summary TEXT,
      rating INTEGER,
      url TEXT,
      word_count INTEGER,
      created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
    );
    ```
- **Node `Postgres` (lấy dữ liệu)**:
  - **Operation**: Chọn `"select"` và điền query:
    ```sql
    SELECT * FROM articles WHERE rating >= 7;
    ```

##### **E. Cấu hình Sở thích cá nhân hóa**
- **Node `Set your Interests`**:
  - Thay thế giá trị `{{$json["interests"]}}` bằng danh sách từ khóa (ví dụ: `["AI", "Tin tức công nghệ", "Startup"]`).
  - **Node `Rating & Tagging Articles`** (LLM Chain):
    - AI sẽ đánh giá tin tức dựa trên sở thích này.

##### **F. Đặt lịch tự động (Schedule Trigger)**
- **Node `Schedule Trigger`**:
  - **Default**: Đang tắt (`deactivated`).
  - **Bật và cấu hình**:
    - Nhấn **"Edit"** → Chọn **"Active"**.
    - Thiết lập thời gian gửi (ví dụ: **8h sáng hàng ngày**).
    - **Lưu ý**: Nếu muốn gửi thủ công, giữ `Manual Trigger` (node đầu tiên) hoạt động.

##### **G. Thay đổi style newsletter**
- **Node `Format HTML Email`**:
  - Mở **Code Editor** và thay thế nội dung HTML để phù hợp với brand của bạn (ví dụ: thay đổi màu sắc, logo).

---

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhấn **"Execute Workflow"** để kiểm tra.
   - Kiểm tra **Gmail** và **PostgreSQL** để xác nhận dữ liệu.
2. **Bật Active**:
   - Đảm bảo tất cả node hoạt động (màu xanh).
   - Nếu sử dụng **Schedule Trigger**, bật nó và kiểm tra lịch.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node `slack` hoặc `telegram` để thông báo khi có tin tức mới.
2. **Lưu log hoạt động**:
   - Sử dụng node `stickyNote` để ghi lại lỗi hoặc tiến trình.
3. **Báo cáo định kỳ**:
   - Tạo một **dashboard** (ví dụ: Metabase) kết nối với PostgreSQL để theo dõi thống kê.
4. **Cá nhân hóa thêm**:
   - Thêm node `if` để gửi tin tức khác nhau cho từng nhóm người nhận (ví dụ: nhân viên marketing vs. CEO).

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp và marketer bằng cách tự động hóa việc tổng hợp, phân tích và gửi newsletter cá nhân hóa. **Không cần code**, chỉ cần cấu hình vài bước đơn giản.

**Hành động ngay!**
1. **Cài đặt n8n** trên VPS (để đảm bảo ổn định).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Bật Schedule Trigger** để nhận newsletter hàng ngày!

**Cảm ơn các sếp đã đọc đến cuối!** Nếu có vấn đề, hãy để lại comment hoặc liên hệ với Falk (tác giả) qua [n8n Community](https://community.n8n.io/). 🚀