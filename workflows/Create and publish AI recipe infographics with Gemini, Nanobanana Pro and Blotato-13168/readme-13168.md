---
title: "🎨 **Tự Động Hóa Tạo & Đăng Bài Infographic Đồ Án AI Với Gemini, Nanobanana Pro & Blotato – Không Cần Code!**"
description: "Workflow tự động hóa hoàn toàn tạo infographic đồ án ẩm thực từ tên món ăn, nghiên cứu thành phần, tạo caption hấp dẫn, sinh ảnh AI và đăng bài tự động lên Facebook – tiết kiệm 80% thời gian so với thủ công. Phù hợp cho blogger, nhà hàng, và content creator."
slug: "tieu-dong-hoa-tao-dang-bai-infographic-do-an-ai"
tags: [n8n, automation, content-creation, multimodal-ai, facebook-automation, gemini-ai, nanobanana-pro, blotato]
keywords: [n8n workflow tự động hóa, tạo infographic đồ án AI, đăng bài Facebook tự động, Gemini AI, Nanobanana Pro, Blotato API, tự động hóa content ẩm thực]
---

# 🚀 **Tự Động Hóa Tạo & Đăng Bài Infographic Đồ Án AI – Từ Tên Món Đến Bài Đăng Facebook**

### **Giải pháp cho những ai:**
- **Blogger ẩm thực** muốn tiết kiệm thời gian nghiên cứu, thiết kế và đăng bài.
- **Nhà hàng/quán café** cần nội dung hấp dẫn cho mạng xã hội mà không cần designer.
- **Content creator** muốn tự động hóa toàn bộ quy trình từ nghiên cứu đến đăng tải.
- **Người yêu ẩm thực** muốn chia sẻ những món ăn ngon với hình ảnh chuyên nghiệp.

**Workflow này tự động hóa toàn bộ quy trình:**
1. **Nhập tên món ăn** → AI nghiên cứu thành phần, cách chế biến.
2. **Tạo caption** hấp dẫn, SEO-friendly cho Facebook.
3. **Sinh infographic** đồ án ẩm thực bằng AI (Nanobanana Pro).
4. **Upload ảnh** lên Blotato và **đăng bài tự động** lên Facebook.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[**Lợi ích cốt lõi**]
✅ **Tiết kiệm 80% thời gian** so với thủ công (không cần thiết kế, viết caption, đăng bài).
✅ **Nội dung chuyên nghiệp** với infographic AI sinh, caption tối ưu hóa engagement.
✅ **Hoạt động 24/7** – không cần can thiệp thủ công.
✅ **Cá nhân hóa** – mỗi món ăn đều có infographic và caption riêng.
✅ **Tăng tương tác** – caption được AI tối ưu hóa cho Facebook.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[**Chuẩn bị trước khi chạy workflow**]
Các sếp cần có:
1. **Tài khoản Blotato** (đăng ký [tại đây](https://blotato.com/?ref=giang9s)) và **Facebook Business Manager** kết nối.
2. **API Key của Nanobanana Pro** (đăng ký [tại đây](https://geminigen.ai/) hoặc [Kie.ai](https://kie.ai?ref=f8cec88ea15f9ecbff52ccbafa41dd6e)).
3. **API Key của Google Gemini** (đăng ký [tại đây](https://makersuite.google.com/)).
4. **API Key của Perplexity AI** (nếu muốn sử dụng node `perplexityTool`).
5. **n8n Self-hosted** (không dùng phiên bản miễn phí của n8n.io).
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/13168](https://n8n.io/workflows/13168) và import vào **n8n Editor**.
- **Cách 2:** Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/13168) và paste vào **Import Workflow** trong n8n.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **17 node** với các bước quan trọng sau. **Các sếp phải cấu hình kỹ các node sau:**

#### **🔹 Node 1: Submit Dish Name (formTrigger)**
- **Cấu hình:**
  - Thêm **form input** với trường `Dish Name` (kiểu text).
  - **Lưu ý:** Nếu không có form, workflow sẽ không nhận được đầu vào.

#### **🔹 Node 2-3: AI Research (Perplexity Tool & Agent)**
- **Cấu hình:**
  - Điền **`perplexityApi`** vào credentials (API Key của Perplexity).
  - **Prompt mẫu** (có thể chỉnh sửa):
    ```
    Research the recipe for {dishName}. Return structured data including:
    - Ingredients (with quantities)
    - Step-by-step instructions
    - Cooking time
    - Difficulty level (Easy/Medium/Hard)
    - Origin/country
    ```

#### **🔹 Node 4-5: Gemini LLM (2 lần sử dụng)**
- **Cấu hình:**
  - Điền **`googlePalmApi`** vào credentials (API Key của Google Gemini).
  - **Prompt cho Node "AI Agent: Recipe Analyzer":**
    ```
    Analyze the recipe data for {dishName} and generate a detailed infographic prompt.
    Include:
    - Visual style (minimalist/colorful)
    - Layout (ingredients on left, steps on right)
    - Fonts and colors
    - Key highlights (e.g., "Quick & Easy")
    ```
  - **Prompt cho Node "AI Agent: Facebook Caption Generator":**
    ```
    Write a Facebook caption for {dishName} that:
    - Is engaging and food-related
    - Includes emojis (🍳🔥)
    - Mentions key ingredients
    - Has a call-to-action (e.g., "Try this recipe today!")
    ```

#### **🔹 Node 6-7: Infographic Prompt Builder**
- **Cấu hình:**
  - **Node "AI Agent: Infographic Prompt Generator"** sẽ tự động tạo prompt cho Nanobanana Pro.
  - **Lưu ý:** Nếu muốn chỉnh sửa, mở node này và xem **input/output** để điều chỉnh.

#### **🔹 Node 8-9: Generate Infographic (Nanobanana Pro)**
- **Cấu hình:**
  - **Credentials:** Điền `httpHeaderAuth` (API Key của Nanobanana Pro).
  - **Endpoint:** `https://api.nanobanana.pro/v1/generate` (hoặc API của Kie.ai).
  - **Headers:**
    ```
    Authorization: Bearer {API_KEY}
    Content-Type: application/json
    ```
  - **Payload:**
    ```json
    {
      "prompt": "{{$node["AI Agent: Infographic Prompt Generator"].json["prompt"]}}",
      "model": "gemini-pro-vision",
      "size": "1024x1024"
    }
    ```

#### **🔹 Node 10-11: Upload Media & Post to Facebook (Blotato)**
- **Cấu hình:**
  - **Credentials:** Điền `blotatoApi` (API Key của Blotato).
  - **Node "Upload media on Blotato":**
    - **Resource:** `media`
    - **File:** Chọn file từ node `Fetch Generated Image`.
  - **Node "Facebook: Create Post":**
    - **Caption:** Lấy từ node `Prepare Facebook Post Data`.
    - **Media:** Lấy từ node `Upload media on Blotato`.

#### **🔹 Node 12-13: Switch & Wait (Image Status Check)**
- **Cấu hình:**
  - **Switch:** Kiểm tra trạng thái ảnh (`Processing` → `Done` → `Failed`).
  - **Wait:** Thời gian chờ mặc định là **30 giây** (có thể điều chỉnh).

---
### **3. Kích hoạt ⚡️**
1. **Test Run:**
   - Nhập tên món ăn (ví dụ: "Bánh Mì Trứng") vào form.
   - Kiểm tra từng node để đảm bảo không có lỗi.
2. **Bật Active:**
   - Chuyển trạng thái workflow sang **Active**.
   - **Lưu ý:** Nếu dùng n8n self-hosted, cần **cài đặt cron job** để chạy định kỳ (nếu muốn tự động hóa hoàn toàn).

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::info[**Cách tối ưu workflow**]
1. **Kết hợp với Slack/Telegram:**
   - Thêm node **Slack Webhook** để thông báo khi bài đăng thành công.
   - **Prompt mẫu:**
     ```
     "🚀 Bài đăng {dishName} đã được đăng lên Facebook thành công! Link: {{$node["Facebook: Create Post"].json["postUrl"]}}"
     ```

2. **Lưu log hoạt động:**
   - Thêm node **Google Sheets** để ghi lại lịch sử các món ăn đã tự động hóa.

3. **Tăng cường cá nhân hóa:**
   - Sử dụng **node `set`** để thêm thông tin cá nhân (ví dụ: tên quán, logo) vào caption.

4. **Chạy định kỳ:**
   - Sử dụng **n8n Triggers** (n8n.io) để tự động nhập tên món ăn từ một danh sách.

5. **Chỉnh sửa AI Prompt:**
   - Mở node **Gemini LLM** và chỉnh sửa prompt để phù hợp với phong cách của các sếp.
:::

---
## 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc nghiên cứu, thiết kế và đăng bài thủ công. **Chỉ cần nhập tên món ăn, AI sẽ tự động:**
✔ Tạo infographic chuyên nghiệp.
✔ Viết caption hấp dẫn.
✔ Đăng bài lên Facebook tự động.

**Hành động ngay:**
1. **Đăng ký Blotato** ([tại đây](https://blotato.com/?ref=giang9s)) và kết nối Facebook.
2. **Đăng ký Nanobanana Pro** ([tại đây](https://geminigen.ai/)).
3. **Import workflow** và chạy thử với tên món ăn yêu thích!

**🎁 Mã giảm giá cho các sếp:**
- **VPS TinoHost (n8n Self-hosted):** [Đăng ký với mã **VPSN8N**](https://tino.vn/vps-n8n?affid=388) (giảm tới 39%).
- **VPS Xeon 4GB:** [Đăng ký với mã **BNIXN8N**](https://my.bnix.one/aff.php?aff=172) (chỉ 50k/tháng).

**🚀 Hãy tự động hóa content của mình ngay hôm nay!**