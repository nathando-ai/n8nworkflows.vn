---
title: "🚀 Tự Động Hóa Tóm Tắt Pull Request GitHub Sang Telegram Bằng AI (GPT-4o-mini) - Giúp Các Sếp Theo Dõi Cập Nhật n8n Mỗi Ngày"
description: "Workflow tự động hóa lấy tất cả các Pull Request mới từ repo GitHub của n8n, lọc ra những cập nhật mới nhất trong ngày, tạo tóm tắt bằng AI GPT-4o-mini, và gửi thông báo trực tiếp đến Telegram. Giúp các sếp và dev team tiết kiệm thời gian theo dõi thay đổi, tránh bỏ lỡ các tính năng mới hoặc sửa lỗi quan trọng."
slug: "tu-dong-hoa-tom-tat-pull-request-github-sang-telegram-bang-ai"
tags: [n8n, automation, devops, ai-summarization, github, telegram, openai, gpt-4o-mini]
keywords: [tự động hóa n8n, tóm tắt pull request github, telegram bot n8n, gpt-4o-mini tự động hóa, theo dõi cập nhật n8n, workflow devops]
---

# 🚀 **Tự Động Hóa Tóm Tắt Pull Request GitHub Sang Telegram Bằng AI (GPT-4o-mini)**

### **Giải Pháp Cho Các Sếp & Dev Team Bỏ Qua Cập Nhật n8n**
Theo dõi thay đổi trong mã nguồn của **n8n** thủ công là một việc tốn thời gian và dễ bỏ lỡ. Các sếp và dev team phải thường xuyên check GitHub để cập nhật về các **tính năng mới, sửa lỗi, hoặc thay đổi quan trọng** trong nền tảng. Workflow này **tự động hóa toàn bộ quá trình** bằng cách:
✅ **Lấy dữ liệu** từ repo GitHub của n8n mỗi ngày (giờ 10h).
✅ **Lọc ra** chỉ những Pull Request mới nhất trong ngày.
✅ **Tạo tóm tắt AI** bằng GPT-4o-mini, dễ đọc và chính xác.
✅ **Gửi thông báo** trực tiếp đến Telegram (hoặc Slack/Email).

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần check thủ công hàng ngày.
- **Chính xác & không bỏ lỡ**: Lọc ra chỉ những cập nhật mới nhất.
- **Tóm tắt AI**: Dễ hiểu, không cần đọc mã nguồn chi tiết.
- **Hoạt động 24/7**: Thông báo tự động vào giờ đã thiết lập.
- **Cá nhân hóa**: Chỉnh sửa prompt AI theo nhu cầu (ví dụ: tóm tắt ngắn gọn, chi tiết kỹ thuật).
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản GitHub** (đăng ký miễn phí tại [github.com](https://github.com)).
2. **API Key OpenAI** (đăng ký tại [openai.com](https://openai.com) và chọn mô hình **GPT-4o-mini**).
3. **Bot Telegram** (tạo tại [@BotFather](https://t.me/BotFather) và lấy **Chat ID** của channel/group).
4. **Repo GitHub của n8n** (đã được cấu hình trong workflow).
:::

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/10585) hoặc copy toàn bộ mã JSON từ đây.
- Mở **n8n Editor** → Nhấn **"Import"** → Dán JSON → Chọn **"Import"**.
- **Lưu ý**: Nếu import từ file, chọn **"Import from File"** và tải file JSON đã tải về.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflows này gồm **7 node chính**, mỗi node đều cần cấu hình kỹ lưỡng:

##### **🔹 Node 1: Daily Check at 10 AM (Schedule Trigger)**
- **Cấu hình**:
  - Thời gian mặc định: **10h sáng** (UTC). **Chỉnh sửa** theo múi giờ của bạn (ví dụ: 7h sáng nếu ở Việt Nam).
  - **Lưu ý**: Nếu muốn chạy vào giờ khác, chỉnh trong **"Schedule"** của node này.

##### **🔹 Node 2: Fetch Latest Pull Request (GitHub)**
- **Cấu hình**:
  - **Credentials**: Chọn **"githubApi"** (đã cấu hình trước khi import).
  - **Parameters**:
    - **Owner**: `n8n-io`
    - **Repository**: `n8n`
    - **Limit**: `1` (chỉ lấy PR mới nhất).
  - **Lưu ý**:
    - Đảm bảo **API Key GitHub** đã được thêm vào **Credentials** (Settings → Credentials → Add GitHub).
    - Nếu muốn lấy nhiều PR hơn, chỉnh **Limit** lên (ví dụ: `5`).

##### **🔹 Node 3: Filter Today's Updates Only (Filter)**
- **Cấu hình**:
  - **Logic**: Chọn **"JSON"** → **"Create new JSON"** → Thêm điều kiện:
    ```json
    {
      "jsonpath": "$[*]",
      "operation": "filter",
      "value": {
        "filter": "$.created_at >= formatDate('{{$datetime(YYYY-MM-DD)}}', 'YYYY-MM-DD')"
      }
    }
    ```
  - **Lưu ý**: Node này **lọc ra chỉ PR được tạo trong ngày hôm nay**, tránh gửi thông báo cũ.

##### **🔹 Node 4: Extract PR Summary (Set)**
- **Cấu hình**:
  - **Action**: Chọn **"Set"** → **"Create new JSON"** → Thêm trường:
    ```json
    {
      "pr_summary": "$[0].body"
    }
    ```
  - **Lưu ý**: Node này **trích xuất nội dung body của PR** để AI xử lý.

##### **🔹 Node 5: Generate AI Summary (ChainLLM + OpenAI)**
- **Cấu hình**:
  - **Node ChainLLM**:
    - **Model**: Chọn **"OpenAI"** (đã cấu hình trước).
    - **Prompt**: Sử dụng mặc định (có thể chỉnh sửa sau):
      ```
      You are an AI assistant that summarizes GitHub pull requests.
      For each pull request, provide a clear, concise summary in bullet points.
      - Translate if needed (keep technical terms in English).
      - Highlight key changes, new features, or bug fixes.
      - Include the date of the PR.
      - Format: "Date: [YYYY-MM-DD] - [Summary in bullet points]".
      ```
  - **Node OpenAI (lmChatOpenAi)**:
    - **Credentials**: Chọn **"openAiApi"** (API Key đã cấu hình).
    - **Model**: Chọn **"gpt-4o-mini"** (mô hình miễn phí, tiết kiệm chi phí).
    - **Lưu ý**:
      - Đảm bảo **API Key OpenAI** đã được thêm vào **Credentials**.
      - **Chi phí**: ~$0.0001/1000 token (rất rẻ).

##### **🔹 Node 6: Send to Telegram Channel (Telegram)**
- **Cấu hình**:
  - **Credentials**: Chọn **"telegramApi"** (Bot Token đã cấu hình).
  - **Chat ID**: Điền **ID của channel/group Telegram** (lấy từ [@userinfobot](https://t.me/userinfobot)).
  - **Message Format**:
    ```markdown
    **New n8n Update - {{ $jsonpath("$.created_at") }}**

    {{ $jsonpath("$.title") }}

    {{ $jsonpath("$.ai_summary") }}
    ```
  - **Lưu ý**:
    - Nếu muốn gửi **rich message** (có hình ảnh, link), bật **"Parse mode"** → Chọn **"HTML".
    - **Test trước**: Gửi tin nhắn mẫu để kiểm tra định dạng.

---
#### **3. Kích Hoạt ⚡️**
- **Test Run**: Nhấn **"Run Workflow"** với dữ liệu mẫu để kiểm tra.
- **Bật Active**: Sau khi kiểm tra thành công, chuyển trạng thái sang **"Active"**.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[TIẾP CẬN HƠN]
1. **Chỉnh sửa Prompt AI**:
   - Muốn tóm tắt **ngắn gọn**? Chỉnh prompt thành:
     ```
     Provide a 3-line summary of the key changes in this PR.
     ```
   - Muốn **chi tiết kỹ thuật**? Thêm:
     ```
     Include technical details like API changes, performance improvements, etc.
     ```

2. **Gửi Email Cùng Telegram**:
   - Thêm **node Email** (ví dụ: Gmail) sau node Telegram để gửi bản sao.

3. **Theo Dõi Nhiều Repo**:
   - **Clone node GitHub** và thay đổi **Owner/Repository** để theo dõi repo khác (ví dụ: `n8n-workflows`).

4. **Báo Cáo Tuần**:
   - Chỉnh **Schedule Trigger** thành **"Every Sunday at 8 AM"** để gửi **tóm tắt tuần**.

5. **Lưu Log**:
   - Thêm **node StickyNote** (đã có trong workflow) để lưu lịch sử tóm tắt.

6. **Kết Nối Slack**:
   - Thay thế node Telegram bằng **node Slack** (cấu hình tương tự).

---
### 📌 **Kết Luận**
Workflow này **giúp các sếp và dev team tự động hóa việc theo dõi cập nhật n8n**, tiết kiệm thời gian và tránh bỏ lỡ các thay đổi quan trọng. **Chỉ cần cấu hình 1 lần**, workflow sẽ hoạt động **mỗi ngày tự động** và gửi tóm tắt AI sang Telegram.

👉 **Bắt đầu ngay!**
1. **Import workflow** từ link trên.
2. **Cấu hình Credentials** (GitHub, OpenAI, Telegram).
3. **Chỉnh sửa giờ** và **prompt AI** theo nhu cầu.
4. **Bật Active** và **theo dõi cập nhật n8n mỗi ngày** một cách thông minh!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**Cần hỗ trợ?** Hãy liên hệ với **Mattis** (tác giả workflow) qua [website PerformAI](https://performai.fr/) để tùy chỉnh thêm! 🚀