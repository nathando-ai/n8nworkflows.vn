---
title: "🎨 Tự Động Hóa Sinh Thành Anime từ Telegram với LLM & Gemini/Leonardo.AI (Không Cần Code)"
description: "Workflow tự động hóa hoàn toàn miễn phí (trong 90 ngày) giúp các sếp tạo ra **4 bức ảnh anime chất lượng cao** chỉ bằng một tin nhắn Telegram. Sử dụng Gemini (Google) hoặc Leonardo.AI (chất lượng cao hơn) kết hợp với LLM DeepSeek để tối ưu hóa prompt, tiết kiệm thời gian lên đến 90% so với làm thủ công."
slug: "tự-dộng-hoa-sinh-thanh-anime-telegram-llm-gemini-leonardo"
tags: [n8n, automation, anime, ai-image-generator, telegram-bot, gemini-api, leonardo-ai, no-code]
keywords: [tự động hóa anime, tạo hình anime bằng ai, n8n workflow telegram, gemini api miễn phí, leonardo ai api, prompt generator llm, deepseek openrouter]
---

# **🚀 Tự Động Hóa Sinh Thành Anime từ Telegram với LLM & Gemini/Leonardo.AI**

## **💡 Giải Pháp Cho Nỗi Đau Của Các Sếp**
Bạn có bao giờ phải:
- **Tốn thời gian** viết và điều chỉnh prompt để tạo hình anime ấn tượng?
- **Khó tìm kiếm** các công cụ miễn phí hoặc chất lượng cao để sinh ảnh?
- **Muốn tự động hóa** quá trình tạo hình từ Telegram mà không cần code?

Workflow này **giải quyết tất cả** bằng cách:
✅ **Chỉ cần gửi 1 tin nhắn** Telegram, hệ thống tự động sinh **4 bức ảnh anime chất lượng cao** (hoặc 1 bức nếu dùng Leonardo.AI).
✅ **Tối ưu hóa prompt** bằng LLM DeepSeek (OpenRouter) để đảm bảo hình ảnh đẹp và phù hợp với yêu cầu.
✅ **Chọn giữa 2 mô hình miễn phí/paid**:
   - **Gemini (Google)** – Miễn phí 90 ngày với tài khoản GCP.
   - **Leonardo.AI** – Chất lượng cao hơn (phải mua API key).
✅ **Tự động chuyển file** về Telegram, không cần download thủ công.

---

### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ 30 phút/lần xuống còn **5 giây** (chỉ cần gửi tin nhắn).
- **Chất lượng ổn định**: LLM tự động cải thiện prompt để hình ảnh đẹp hơn.
- **Hoạt động 24/7**: Workflow chạy tự động trên VPS, không cần can thiệp.
- **Tùy chỉnh dễ dàng**: Thay đổi số lượng hình ảnh, mô hình AI, hoặc style anime.
- **Miễn phí (tạm thời)**: Sử dụng Gemini trong 90 ngày với tài khoản GCP.
:::

---

### **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Telegram**:
   - Bot Telegram (tạo tại [@BotFather](https://t.me/BotFather)).
   - **Chat ID** của bot (để restrict chỉ cho bot này hoạt động).
   - **User ID** của bạn (để bot gửi hình ảnh về).

2. **API Keys**:
   - **Google Gemini API** (miễn phí 90 ngày với tài khoản GCP):
     - Đăng ký tại [Google Cloud Console](https://console.cloud.google.com/).
     - Tạo **API key** và thêm vào credential `googlePalmApi` trong n8n.
   - **Leonardo.AI API** (nếu muốn chất lượng cao hơn):
     - Đăng ký tại [Leonardo.AI](https://leonardo.ai/).
     - Tạo **API key** và thêm vào credential `httpHeaderAuth` (Header Auth).

3. **LLM Provider (DeepSeek)**:
   - Sử dụng **DeepSeek via OpenRouter** (miễn phí).
   - Không cần API key riêng, chỉ cần đăng ký tại [OpenRouter](https://openrouter.ai/).

4. **VPS Self-Hosted (khuyến nghị)**:
   - Để workflow chạy 24/7 ổn định, các sếp nên cài n8n trên VPS.
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
:::

---

## **🚀 Cách Import & Cấu Hình Workflow**

### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/9102](https://n8n.io/workflows/9102) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON dưới đây và paste vào **Import Workflow** trong n8n:
  ```json
  // (Danh sách JSON đầy đủ sẽ được cung cấp nếu cần)
  ```

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Sau khi import, các sếp cần cấu hình **các node quan trọng** như sau:

#### **🔹 Node 1: Telegram Trigger**
- **Credentials**: Chọn `telegramApi` (đã cấu hình bot token và user ID).
- **Restrict to Chat IDs**: Nhập **Chat ID của bot** (lấy từ [@UserIDBot](https://userbot.org/)).
- **Example**: `/start` (để kích hoạt workflow khi người dùng gửi tin nhắn).

#### **🔹 Node 2: HTTP - Gemini (hoặc Leonardo AI)**
- **Mô hình 1: Gemini (Miễn phí 90 ngày)**
  - **Credentials**: `googlePalmApi` (API key từ Google Cloud).
  - **URL**: `https://generativelanguage.googleapis.com/v1beta/models/gemini-pro:generateContent`.
  - **Headers**:
    ```json
    {
      "Content-Type": "application/json",
      "Authorization": "Bearer YOUR_GOOGLE_API_KEY"
    }
    ```
  - **Body**:
    ```json
    {
      "contents": [{"parts": [{"text": "$json.prompt"}]}]
    }
    ```

- **Mô hình 2: Leonardo AI (Chất lượng cao)**
  - **Thay thế node HTTP-Gemini** bằng một node mới.
  - **Credentials**: `httpHeaderAuth` (API key Leonardo.AI).
  - **URL**: `https://api.leonardo.ai/v1/generations`.
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer YOUR_LEONARDO_API_KEY",
      "Content-Type": "application/json"
    }
    ```
  - **Body**:
    ```json
    {
      "model": "leonardo-ai/leonardo-v1-0",
      "prompt": "$json.prompt",
      "width": 512,
      "height": 512,
      "num_images": 1
    }
    ```

#### **🔹 Node 3: Prompt Generator (LLM)**
- **Credentials**: Không cần (sử dụng DeepSeek miễn phí).
- **Model**: `deepseek/deepseek-chat-v3-0324:free`.
- **Prompt Template**:
  ```plaintext
  Tôi muốn tạo một bức ảnh anime về "{user_prompt}". Hãy viết **4 prompt chi tiết** với các góc độ khác nhau, bao gồm:
  1. Style: Anime 2D truyền thống (như Studio Ghibli).
  2. Style: Anime hiện đại (như Jujutsu Kaisen).
  3. Style: Anime pastel (như K-On!).
  4. Style: Anime fantasy (như Sword Art Online).
  Mỗi prompt phải có:
  - Mô tả chi tiết nhân vật, cảnh quan, ánh sáng.
  - Kỹ thuật vẽ (shading, lighting, details).
  - Thể loại (slice-of-life, action, romance...).
  ```
- **Output Parser**: Chọn `Structured Output Parser` để đảm bảo format JSON chuẩn.

#### **🔹 Node 4: Loop Over Prompts & Convert to File**
- **Image-count**: Đặt số lượng hình ảnh muốn sinh (mặc định 4).
- **Convert to File**: Chọn `toBinary` để chuyển base64 thành file ảnh.

#### **🔹 Node 5: Send pics via Telegram**
- **Credentials**: `telegramApi`.
- **Operation**: `sendPhoto`.
- **File**: Chọn file ảnh từ node `Convert to File`.
- **Caption**: Thêm caption tùy chỉnh (ví dụ: `Dưới đây là 4 bức anime từ prompt của bạn!`).

---

### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run**:
   - Gửi tin nhắn `/start` hoặc tin nhắn văn bản bất kỳ đến bot Telegram.
   - Kiểm tra nếu workflow sinh ra hình ảnh và gửi về Telegram.
2. **Active Workflow**:
   - Chuyển trạng thái từ `Inactive` sang `Active`.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**
:::info[TIPS CHẤT LƯỢNG CAO]
- **Tối ưu prompt**:
  - Nếu prompt ban đầu không rõ ràng, LLM sẽ tự động cải thiện. Ví dụ:
    - **Input**: "Girl with umbrella".
    - **Output LLM**: `"A young anime girl with a vintage-style umbrella, standing in a neon-lit alleyway at night, with soft pastel lighting, inspired by Studio Ghibli's 'Howl's Moving Castle' aesthetic. The girl has long brown hair, wearing a cozy sweater, and the umbrella has intricate watercolor patterns."`
- **Chọn mô hình AI**:
  - **Gemini**: Miễn phí 90 ngày, chất lượng trung bình.
  - **Leonardo.AI**: Chất lượng cao hơn, phù hợp cho anime chi tiết.
- **Tùy chỉnh số lượng hình ảnh**:
  - Thay đổi giá trị trong node `Image-count` (mặc định 4).
- **Lưu log & báo cáo**:
  - Thêm node `StickyNote` để ghi lại lịch sử sinh ảnh.
  - Kết hợp với **Google Sheets** để lưu danh sách prompt và kết quả.
- **Gửi báo cáo định kỳ**:
  - Sử dụng node `Set` + `Telegram` để gửi tổng hợp hình ảnh sinh ra hàng ngày.
:::

---

## **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp trong việc tạo hình anime, đồng thời **tối ưu hóa chất lượng** nhờ LLM và các mô hình AI tiên tiến. Bạn có thể:
✔ **Sử dụng miễn phí** với Gemini trong 90 ngày.
✔ **Nâng cấp lên Leonardo.AI** để có hình ảnh chất lượng cao hơn.
✔ **Tự động hóa hoàn toàn** từ Telegram đến kết quả cuối cùng.

**Hãy thử ngay và chia sẻ kết quả với chúng tôi!** 🚀
Nếu có vấn đề, hãy để lại comment dưới bài viết hoặc liên hệ với tác giả [Diptamoy Barman](https://n8n.io/workflows/9102) để hỗ trợ.

---
**🎁 Bonus**: Các sếp có thể kết hợp workflow này với **Slack/Email** để nhận hình ảnh tự động vào các kênh công việc. Hãy tưởng tượng khi bạn chỉ cần nói "Tôi muốn hình ảnh anime về [mô tả]" và hệ thống tự động sinh ra kết quả!