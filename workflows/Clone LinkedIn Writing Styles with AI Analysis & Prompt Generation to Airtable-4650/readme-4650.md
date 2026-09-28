---
title: "🎯 Tự Động Học Học Bài Viết LinkedIn Của Người Khác Với AI & Lưu Trữ Vào Airtable (Không Cần Code)"
description: "Workflow tự động phân tích phong cách viết LinkedIn của các chuyên gia hàng đầu, tạo prompt AI cá nhân hóa và lưu kết quả vào Airtable - giúp các sếp tiết kiệm 10+ giờ/tháng phân tích thủ công."
slug: "tieu-dong-hoc-bai-viet-linkedin-voi-ai"
tags: [n8n, automation, marketing, ai-content, airtable, prompt-engineering, no-code]
keywords: [n8n workflow marketing, tự động hóa phân tích bài viết LinkedIn, AI học phong cách viết, lưu dữ liệu Airtable, prompt generation]
---

# 🚀 **Học Bài Viết LinkedIn Của Người Khác Với AI - Từ Scraping Đến Airtable (Không Cần Code)**

### **Nỗi Đau Của Các Sếp Marketing**
Bạn đã bao giờ mơ ước **học được phong cách viết LinkedIn của các chuyên gia hàng đầu** (như Gary Vee, Neil Patel, hoặc các CEO thành công) mà không phải đọc từng bài một? Hay muốn **tạo ra prompt AI cá nhân hóa** để viết nội dung giống họ? Thì với workflow này, bạn sẽ **tự động hóa toàn bộ quá trình** chỉ trong vài phút!

- **Tiết kiệm 10+ giờ/tháng** phân tích bài viết thủ công.
- **Lấy lại phong cách viết độc đáo** của các nhà lãnh đạo marketing.
- **Lưu dữ liệu phân tích** vào Airtable để theo dõi và sử dụng lâu dài.
- **Tạo prompt AI** để viết nội dung giống họ, áp dụng cho blog, email, hoặc bài viết LinkedIn của riêng bạn.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tự động scrap** bài viết LinkedIn của người dùng theo URL.
✅ **Phân tích phong cách viết** (tôn trọng, chuyên nghiệp, động viên,...) bằng AI (OpenRouter).
✅ **Tạo prompt AI cá nhân hóa** để viết nội dung giống phong cách của họ.
✅ **Lưu kết quả vào Airtable** với định dạng sẵn sàng sử dụng.
✅ **Hoạt động 24/7** trên VPS tự host (không phụ thuộc vào n8n.cloud).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản LinkedIn** (để scrap bài viết - *lưu ý: không vi phạm chính sách LinkedIn*).
2. **API Key của OpenRouter** (để phân tích AI):
   - Đăng ký tại [OpenRouter](https://openrouter.ai/) và lấy API Key.
3. **Airtable API Key** (để lưu dữ liệu):
   - Tạo một **Base mới** trong Airtable và lấy API Key từ **Settings > API**.
4. **VPS tự host n8n** (khuyến nghị):
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
5. **Node LangChain** (n8n Community):
   - Cài đặt từ [n8n Community](https://community.n8n.io/) để sử dụng `chainLlm` và `lmChatOpenRouter`.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1: Import từ file JSON**
  1. Tải workflow từ [đây](https://n8n.io/workflows/4650) (ấn "Export").
  2. Trong n8n Editor, chọn **Import** và chọn file JSON vừa tải.
- **Cách 2: Copy/Paste JSON**
  1. Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/4650).
  2. Trong n8n Editor, chọn **Import** > **Paste JSON**.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này có **2 phần quan trọng** cần cấu hình kỹ:

##### **A. Cấu Hình API & Credentials**
| **Node**               | **Tham Số Cần Chỉnh**                          | **Lưu Ý**                                                                 |
|------------------------|-----------------------------------------------|----------------------------------------------------------------------------|
| **0) Start LinkedIn Analysis** | `formTrigger` (không cần chỉnh)              | Sử dụng để kích hoạt workflow khi người dùng nhập URL LinkedIn.          |
| **1) Fetch LinkedIn Posts** | `httpRequest` (URL API scrap)               | Sử dụng API như [thisonefeed](https://thisonefeed.com/) hoặc [LinkedIn Scraper](https://rapidapi.com/apidojo/api/linkedin-scraper/). |
| **7) Analyze Writing Style** | `chainLlm` (Model: `Style Analysis Model`) | Chọn **OpenRouter** và điền `apiKey` từ OpenRouter.                       |
| **8) Generate Style Prompt** | `chainLlm` (Model: `Prompt Creation Model`) | Giống như trên, chỉ định `apiKey` và cấu hình prompt mẫu.               |
| **9) Save to Airtable**      | `airtable` (API Key + Base Name)             | Điền `apiKey` từ Airtable và chọn **Table Name** (ví dụ: "LinkedIn_Analysis"). |

##### **B. Cấu Hình Prompt AI (Quá Trình Phân Tích)**
Workflow sử dụng **hai model OpenRouter** để:
1. **Phân tích phong cách viết** (ví dụ: "Bài viết này có phong cách động viên hay chuyên nghiệp?").
2. **Tạo prompt AI** để viết nội dung giống phong cách đó.

**Ví dụ Prompt mẫu cho Node 7 (Analyze Writing Style):**
```plaintext
Analyze the following LinkedIn post and extract:
1. Tone (Friendly, Professional, Motivational, etc.)
2. Key themes (Leadership, Productivity, Marketing, etc.)
3. Writing style (Short sentences, Long paragraphs, Questions, etc.)
4. Emotional trigger (Fear, Desire, Curiosity, etc.)

Post: {{{$json["postContent"]}}}
Format response as JSON:
{
  "tone": "string",
  "themes": ["array"],
  "style": "string",
  "emotionalTrigger": "string"
}
```

**Ví dụ Prompt mẫu cho Node 8 (Generate Style Prompt):**
```plaintext
Generate a prompt for an AI to write a LinkedIn post in the style of the analyzed post above.
Include:
- Tone and themes from the analysis.
- Key phrases and structure.
- Example opening line.

Analysis: {{{$json["analysis"]}}}
Prompt:
```

##### **C. Cấu Hình Airtable (Lưu Dữ Liệu)**
- **Table Structure** (tạo trước khi chạy workflow):
  | Field Name       | Type      | Example Value                     |
  |------------------|-----------|-----------------------------------|
  | `linkedin_url`   | Text      | "https://linkedin.com/posts/..."  |
  | `tone`           | Single Line| "Motivational"                    |
  | `themes`         | Multi-line| "Leadership, Productivity"        |
  | `writing_style`  | Text      | "Short sentences, Questions"      |
  | `prompt_ai`      | Long Text | "Prompt mẫu để AI viết..."       |
  | `created_at`     | Date      | (Auto)                            |

---

#### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với URL bài viết mẫu:
   - Nhập URL LinkedIn vào `formTrigger` (ví dụ: [Bài viết của Gary Vee](https://www.linkedin.com/posts/activity-7034373726350305280-?utm_source=share&utm_medium=member_desktop)).
   - Chạy workflow và kiểm tra kết quả trong Airtable.
2. **Bật Active**:
   - Đảm bảo tất cả node hoạt động (kiểm tra màu xanh).
   - Lưu workflow và kích hoạt **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁCH DÙNG HIỆU QUẢ HƠN]
1. **Tự động scrap nhiều bài viết**:
   - Sử dụng **n8n Schedule Node** để chạy workflow hàng tuần/month.
   - Ví dụ: Scrap 5 bài viết mới nhất của Gary Vee mỗi tháng.

2. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack/Telegram Bot** để thông báo kết quả phân tích.
   - Ví dụ: "🚀 Phong cách viết của [Tên Người] là **Motivational** với chủ đề **Leadership**."

3. **Lưu log hoạt động**:
   - Thêm node **StickyNote** để ghi lại lỗi hoặc kết quả debug.
   - Ví dụ: "Workflow thất bại vì API OpenRouter hết quota."

4. **Tạo báo cáo định kỳ**:
   - Sử dụng **n8n Airtable Node** để tạo báo cáo tổng hợp (ví dụ: "Top 3 phong cách viết phổ biến trong tháng").

5. **Cải thiện prompt AI**:
   - Thử nghiệm với các model khác trên OpenRouter (ví dụ: `mistral`, `llama2`) để tăng độ chính xác.
   - Ví dụ: "So sánh kết quả phân tích giữa `gpt-4` và `mistral`."
:::

---

### 📌 **Kết Luận: Học Bài Viết LinkedIn Của Người Khác - Ngay Hôm Nay!**
Workflow này **giải phóng thời gian** của các sếp để tập trung vào **strategy** thay vì phân tích thủ công. Bằng cách **tự động scrap, phân tích AI và lưu vào Airtable**, bạn sẽ:
✔ **Học được phong cách viết** của các chuyên gia hàng đầu.
✔ **Tạo prompt AI cá nhân hóa** để viết nội dung chuyên nghiệp.
✔ **Lưu trữ dữ liệu** để theo dõi và sử dụng lâu dài.

**Bắt đầu ngay!**
1. **Cài đặt n8n trên VPS** (khuyến nghị).
2. **Import workflow** và cấu hình API.
3. **Test với URL bài viết mẫu**.
4. **Bật Active và theo dõi kết quả trong Airtable**.

👉 **Mã giảm giá VPS TinoHost (39%)**: [VPSN8N](https://tino.vn/vps-n8n?affid=388)
👉 **Hỗ trợ kỹ thuật**: Nếu gặp vấn đề, comment bên dưới hoặc liên hệ [n8n Community](https://community.n8n.io/).

**Chúc các sếp thành công!** 🚀