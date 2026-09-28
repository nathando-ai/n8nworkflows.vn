---
title: "🚀 Tự Động Hóa Bài Đăng LinkedIn Từ Xu Hướng Tech Với AI Ollama - Chất Lượng 100% (Không Cần Code)"
description: "Workflow tự động hóa hoàn chỉnh giúp các sếp tìm kiếm xu hướng tech hàng ngày từ Hacker News, Reddit và Product Hunt, tạo bài viết LinkedIn chất lượng cao với AI Ollama, sau đó tự động lựa chọn và đăng bài vào thời điểm tối ưu. Giúp tiết kiệm 10+ giờ/tuần và nâng cao hiệu quả marketing cá nhân."
slug: "tu-dong-hoa-bai-dang-linkedin-ai-ollama"
tags: [n8n, automation, ai-ollama, linkedin-automation, social-media, no-code]
keywords: [tự động hóa linkedin, ai ollama n8n, tự động viết bài linkedin, workflow linkedin tự động, tự động hóa marketing cá nhân]
---

# 🚀 **Tự Động Hóa Bài Đăng LinkedIn Từ Xu Hướng Tech Với AI Ollama - Chất Lượng 100% (Không Cần Code)**

Hiện nay, việc tạo nội dung LinkedIn chất lượng hàng ngày là một thách thức lớn đối với các chuyên gia kỹ thuật và marketer cá nhân. Thường xuyên phải:
- Tìm kiếm xu hướng tech mới từ nhiều nguồn khác nhau (Hacker News, Reddit, Product Hunt).
- Viết bài đăng chất lượng, phù hợp với giọng điệu cá nhân.
- Lựa chọn bài đăng tốt nhất và đăng vào thời điểm tối ưu.
- Quản lý và theo dõi hiệu quả của từng bài đăng.

Workflow này **giải quyết tất cả những vấn đề trên** bằng cách tự động hóa toàn bộ quy trình từ tìm kiếm xu hướng đến đăng bài, với sự hỗ trợ của **AI Ollama** để đảm bảo chất lượng cao nhất. Các sếp chỉ cần **cài đặt một lần**, workflow sẽ hoạt động **24/7**, tiết kiệm **10+ giờ/tuần** và nâng cao hiệu quả marketing cá nhân.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted) để đảm bảo tính liên tục và bảo mật.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động tìm kiếm xu hướng và viết bài, chỉ cần review cuối cùng.
- **Chất lượng bài viết cao**: AI Ollama viết bài với giọng điệu cá nhân hóa, phù hợp với chuyên môn của các sếp.
- **Tối ưu thời điểm đăng bài**: Chỉ đăng bài vào Thứ 2, 3, 4 vào 9:30 AM (thời điểm có engagement cao nhất).
- **Quản lý và theo dõi**: Tất cả bài viết được lưu trong Google Sheets với trạng thái (draft, approved, rejected) và thông báo tự động qua Telegram.
- **Tự động hóa hoàn chỉnh**: Không cần can thiệp thủ công sau khi cài đặt.
:::

---

### 🔧 **Yêu cầu cần thiết**
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets**:
   - Tạo một bảng Google Sheets với các cột sau:
     - Post ID, Angle, Hook Line, Full Post, Hashtags, Trend Referenced, Word Count, Best Day, Posting Notes, Status, Created Date, Published Date, LinkedIn URL, AI Review, Revised Post, Dedup Stats, Generated At.
   - **Chia sẻ bảng với n8n** để workflow có quyền đọc/ghi.
2. **Ollama AI**:
   - Cài đặt Ollama trên máy chủ hoặc VPS và pull mô hình AI (ví dụ: `ollama pull mistral`).
   - **Mô hình AI mặc định**: `mistral` (có thể thay đổi trong workflow).
3. **Tài khoản LinkedIn**:
   - Đăng ký ứng dụng trên [LinkedIn Developer Portal](https://developer.linkedin.com/) với scope `w_member_social`.
   - Lấy **Person URN** của tài khoản LinkedIn (thông tin này sẽ được sử dụng để đăng bài).
4. **Bot Telegram**:
   - Tạo bot Telegram qua [@BotFather](https://tbotfather.com/) và lấy **token bot**.
   - Lấy **chat ID** của tài khoản Telegram để nhận thông báo.
5. **API Keys**:
   - Không cần API key nào ngoài các thông tin trên (Google Sheets, LinkedIn OAuth, Telegram Bot Token).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### 1. **Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/13465](https://n8n.io/workflows/13465) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** và nhấn **Import Workflow** → Dán JSON hoặc tải file JSON.
- **Không cần chỉnh sửa gì** nếu đã import hoàn chỉnh.

#### 2. **Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này được chia thành **hai phần chính**:
- **Phần 1: Nghiên cứu hàng ngày (6:00 AM)** → Tìm xu hướng và tạo bài viết.
- **Phần 2: Đăng bài (Thứ 2-4, 9:30 AM)** → Lựa chọn và đăng bài.

##### **2.1. Cấu hình Google Sheets**
- **Node "📋 Save to Queue" và "✅ Mark Published"**:
  - Đảm bảo **credentials Google Sheets** được cấu hình chính xác.
  - **Sheet Name**: Đặt tên bảng là `LinkedIn Posts Queue` (hoặc tên khác nhưng phải khớp với cấu trúc cột trong workflow).
  - **Range**: `Sheet1!A1:Z` (hoặc tùy chỉnh theo cấu trúc cột).

##### **2.2. Cấu hình LinkedIn OAuth**
- **Node "📤 Publish to LinkedIn"**:
  - Thay thế `YOUR_LINKEDIN_PERSON_ID` trong **URL** bằng **Person URN** của tài khoản LinkedIn.
  - Ví dụ:
    ```plaintext
    https://api.linkedin.com/v2/ugcPosts?q=urn:li:person:YOUR_LINKEDIN_PERSON_ID&format=json
    ```
  - **Headers**:
    - `Authorization`: `Bearer YOUR_ACCESS_TOKEN` (lấy từ LinkedIn OAuth).
    - `X-Restli-Protocol-Version`: `2.0.0`.

##### **2.3. Cấu hình Telegram Bot**
- **Node "📲 Published ✅" và "📲 Rejected ❌"**:
  - Thay thế `YOUR_TELEGRAM_BOT_TOKEN` và `YOUR_TELEGRAM_CHAT_ID` trong **URL**:
    ```plaintext
    https://api.telegram.org/botYOUR_TELEGRAM_BOT_TOKEN/sendMessage?chat_id=YOUR_TELEGRAM_CHAT_ID&text=...
    ```

##### **2.4. Cấu hình AI Ollama**
- **Node "Ollama Writer", "Ollama Selector", "Ollama Reviewer"**:
  - **Mô hình AI**:
    - `Ollama Writer`: Đặt mặc định là `mistral`.
    - `Ollama Selector` và `Ollama Reviewer`: Thay thế `YOUR_MODEL_NAME` bằng mô hình muốn sử dụng (ví dụ: `llama3`).
  - **Prompt AI**:
    - **BẮT BUỘC** chỉnh sửa **tất cả 3 hệ thống prompt** (Writer, Selector, Quality Gate) trong **Sticky Notes** của workflow để phù hợp với:
      - **Tên và chuyên môn** của các sếp.
      - **Giọng điệu** muốn truyền tải (chuyên nghiệp, thân thiện, giáo dục...).
    - Ví dụ prompt cho **AI Writer**:
      ```plaintext
      Tôi là [Tên của các sếp], chuyên gia về [chuyên môn]. Viết bài LinkedIn với:
      - Đầu bài hấp dẫn (Hook Line).
      - Nội dung chi tiết, phân tích xu hướng [tên xu hướng].
      - Kết thúc với call-to-action (CTA) phù hợp.
      ```

##### **2.5. Cấu hình Lịch trình (Schedule Trigger)**
- **Node "⏰ Daily 6 AM — Research"**:
  - Cron expression mặc định là `0 6 * * *` (6:00 AM hàng ngày).
  - **Không cần chỉnh** nếu muốn chạy đúng giờ.
- **Node "⏰ Tue-Thu 9:30 AM — Publish"**:
  - Cron expression mặc định là `0 9.30 2-4 * *` (9:30 AM Thứ 2-4).
  - **Không cần chỉnh** nếu muốn đăng bài vào thời điểm này.

---

#### 3. **Kích hoạt ⚡️**
1. **Test Run**:
   - Chạy **Flow 1 (Daily Research)** thủ công để kiểm tra:
     - AI có viết bài không?
     - Bài viết có được lưu vào Google Sheets không?
   - Chạy **Flow 2 (Smart Publish)** thủ công để kiểm tra:
     - AI có lựa chọn bài viết tốt nhất không?
     - Bài viết có được đăng lên LinkedIn không?
2. **Bật Active**:
   - Sau khi test thành công, **bật Active** cho cả hai Flow.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tăng cường chất lượng bài viết**:
   - Thêm **các mô hình AI khác** (ví dụ: `llama3`, `phi3`) vào `Ollama Selector` và `Ollama Reviewer` để so sánh kết quả.
   - Sử dụng **prompt engineering** để AI viết bài dài hơn hoặc ngắn hơn tùy thuộc vào xu hướng.

2. **Thêm nguồn dữ liệu**:
   - Thêm **Twitter API** hoặc **Medium RSS** để lấy xu hướng từ nhiều nguồn khác.
   - Sử dụng **node `httpRequest`** để fetch dữ liệu từ các API khác.

3. **Tự động hóa báo cáo**:
   - Thêm **node `googleSheets`** để tạo báo cáo hàng tuần về số lượng bài đăng, engagement, và xu hướng phổ biến.
   - Gửi báo cáo qua **email** hoặc **Slack** bằng node `n8n-nodes-base.email` hoặc `n8n-nodes-base.slack`.

4. **Tối ưu thời điểm đăng bài**:
   - Sử dụng **node `dateTime`** để phân tích thời điểm đăng bài có engagement cao nhất và điều chỉnh cron expression.

5. **Quản lý lại bài viết bị loại**:
   - Thêm **node `telegram`** để thông báo lại bài viết bị loại và lý do (ví dụ: "Bài viết không đủ chất lượng").
   - Cho phép **review thủ công** bằng cách thêm **node `manualApproval`** (nếu cần).

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn chỉnh** để các sếp tự động hóa toàn bộ quy trình tạo và đăng bài LinkedIn, từ tìm kiếm xu hướng đến đăng bài, với sự hỗ trợ của **AI Ollama** để đảm bảo chất lượng cao nhất. **Không cần code**, chỉ cần **cài đặt và chạy**, workflow sẽ hoạt động tự động hàng ngày.

**Hành động ngay hôm nay**:
1. **Cài đặt n8n** trên VPS và import workflow.
2. **Cấu hình Google Sheets, LinkedIn, Telegram** theo hướng dẫn.
3. **Chỉnh sửa prompt AI** để phù hợp với giọng điệu cá nhân.
4. **Bật Active** và bắt đầu tiết kiệm **10+ giờ/tuần**!

**🚀 Cùng tự động hóa marketing cá nhân của mình ngay bây giờ!**