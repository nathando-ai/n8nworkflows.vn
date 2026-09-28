---
title: "🎨 Chuyển Ảnh Trắng Trơn Thành Ảnh & Video Đẹp Tự Động Với AI - N8n Workflow Miễn Phí"
description: "Tự động hóa quy trình chỉnh sửa ảnh và tạo video từ ảnh thô bằng AI (OpenAI + Replicate) chỉ với 1 tin nhắn Telegram. Giúp các sếp tiết kiệm thời gian thiết kế, nâng cao chất lượng hình ảnh marketing, và tạo nội dung video chuyên nghiệp 100% tự động hóa."
slug: "chuyen-anh-trang-thon-thanh-anh-video-dep-voi-n8n"
tags: [n8n, automation, ai-image-editing, replicate, openai, telegram-bot, no-code]
keywords: [n8n workflow tự động hóa ảnh, chỉnh sửa ảnh bằng AI, tạo video từ ảnh, OpenAI Replicate API, tự động hóa thiết kế marketing]
---

# 🚀 **Chuyển Ảnh Trắng Trơn Thành Ảnh & Video Đẹp Tự Động Với AI**

### **Giải pháp cho các sếp:**
- **Thiết kế marketing** nhưng không có thời gian chỉnh sửa ảnh thủ công?
- **Cần video ngắn** từ ảnh sản phẩm nhưng không biết code?
- **Mệt mỏi** với quá trình chỉnh sửa ảnh qua lại giữa Photoshop và AI?

**Workflow này sẽ tự động:**
✅ **Chỉnh sửa ảnh** theo yêu cầu bằng AI (OpenAI)
✅ **Tạo video biến thể** từ ảnh gốc (Replicate)
✅ **Gửi kết quả** trực tiếp qua Telegram (không cần cài phần mềm nào)

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động 24/7 ổn định, các sếp nên **self-host n8n** trên VPS. Dưới đây là 2 lựa chọn tối ưu:
👉 **[VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 **[VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ xử lý AI nhanh)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** so với chỉnh sửa thủ công (AI làm việc 24/7).
- **Chất lượng cao** với ảnh/video chuyên nghiệp, không cần kỹ năng thiết kế.
- **Tự động hóa marketing** (tạo banner, mockup sản phẩm, video demo).
- **Cá nhân hóa** theo yêu cầu từ caption trong tin nhắn Telegram.
- **Không giới hạn số lượng** (khác với các công cụ AI trả phí).
:::

---

## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng, các sếp cần:
1. **Tài khoản Telegram** và **bot Telegram** (để nhận ảnh và gửi kết quả).
2. **API Key OpenAI** (để chỉnh sửa ảnh).
3. **API Key Replicate** (để tạo video biến thể).
4. **File ảnh gốc** (gửi qua Telegram với caption mô tả yêu cầu chỉnh sửa).

**Cách lấy API Key:**
- [OpenAI API Key](https://platform.openai.com/account/api-keys)
- [Replicate API Token](https://replicate.com/account/api-tokens)
:::

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/4275](https://n8n.io/workflows/4275) hoặc copy/paste JSON vào **n8n Editor**.
- **Cách import:**
  1. Mở **n8n Editor** (trang chủ của workflow).
  2. Nhấn **"Import"** và chọn file JSON.
  3. Hoặc nhấn **"Create"** → **"Import"** → **"From JSON"**.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **9 node** chính. Dưới đây là hướng dẫn cấu hình chi tiết:

#### **📱 Node 1: Telegram Bot Trigger**
- **Chức năng:** Nhận ảnh từ Telegram và lấy caption (mô tả yêu cầu chỉnh sửa).
- **Cấu hình:**
  - **Bot Token:** Điền `YOUR_TELEGRAM_BOT_TOKEN` (tìm trong `@BotFather` trên Telegram).
  - **Chat ID:** Để trống (n8n sẽ tự động lấy từ tin nhắn).
  - **Lọc tin nhắn:** Chỉ nhận ảnh (`media_type: photo`).

#### **🖼️ Node 2: Edit Image (OpenAI)**
- **Chức năng:** Chỉnh sửa ảnh bằng AI (OpenAI).
- **Cấu hình:**
  - **URL API:** `https://api.openai.com/v1/images/edits`
  - **Headers:**
    - `Authorization: Bearer YOUR_OPENAI_API_KEY`
    - `Content-Type: multipart/form-data`
  - **Body (JSON):**
    ```json
    {
      "image": "{{ $node["Convert to Binary Image"].json.data }}",
      "prompt": "{{ $json.caption }}",
      "n": 1,
      "size": "1024x1024"
    }
    ```
  - **Lưu ý:**
    - Thay `YOUR_OPENAI_API_KEY` bằng API Key của bạn.
    - **Caption** trong tin nhắn Telegram sẽ được dùng làm **prompt** cho AI.

#### **📤 Node 3: Convert to Binary Image**
- **Chức năng:** Chuyển dữ liệu ảnh từ OpenAI thành binary để gửi lại.
- **Cấu hình:**
  - **Input:** `{{ $json.data[0].b64_json }}` (dữ liệu ảnh từ OpenAI).
  - **Output:** Binary image (sẵn sàng gửi qua Telegram).

#### **📤 Node 4: Send Edited Image**
- **Chức năng:** Gửi ảnh đã chỉnh sửa về Telegram.
- **Cấu hình:**
  - **Chat ID:** `{{ $json.message.chat.id }}` (tự động lấy từ tin nhắn gốc).
  - **Photo:** `{{ $node["Convert to Binary Image"].json.data }}`.
  - **Caption:** `{{ $json.caption }}` (giữ nguyên caption gốc).

#### **🎨 Node 5: Generate Variation (Replicate)**
- **Chức năng:** Tạo video biến thể từ ảnh gốc (sử dụng Replicate).
- **Cấu hình:**
  - **URL API:** `https://api.replicate.com/v1/predictions`
  - **Headers:**
    - `Authorization: Bearer YOUR_REPLICATE_API_TOKEN`
    - `Content-Type: application/json`
  - **Body (JSON):**
    ```json
    {
      "version": "a104a7e4102547e2a7c77a06b722970e66876090563e5578",
      "input": {
        "image": "{{ $json.file_path }}",
        "prompt": "Enhanced version of the image with cinematic lighting"
      }
    }
    ```
  - **Lưu ý:**
    - Thay `YOUR_REPLICATE_API_TOKEN` bằng API Key của bạn.
    - **`file_path`** sẽ được lấy từ Node **Get File Path** (xem dưới).

#### **⏱️ Node 6: Wait for Processing (45s)**
- **Chức năng:** Đợi Replicate xử lý xong (tránh timeout).
- **Cấu hình:**
  - Thời gian chờ: **45 giây** (đủ cho Replicate hoàn thành).

#### **📤 Node 7: Get File Path**
- **Chức năng:** Lấy đường dẫn ảnh từ Telegram để Replicate xử lý.
- **Cấu hình:**
  - **URL API:** `https://api.telegram.org/botYOUR_TELEGRAM_BOT_TOKEN/getFile?file_id={{ $json.photo[0].file_id }}`
  - **Output:** `{{ $json.result.file_path }}` (đường dẫn để Replicate tải ảnh).

#### **📡 Node 8: Retrieve Generated Image**
- **Chức năng:** Lấy kết quả từ Replicate (video biến thể).
- **Cấu hình:**
  - **URL API:** `https://api.replicate.com/v1/predictions/PREDICTION_ID/output`
  - **Headers:**
    - `Authorization: Bearer YOUR_REPLICATE_API_TOKEN`
  - **Lưu ý:**
    - Thay `PREDICTION_ID` bằng ID từ Node **Generate Variation**.

#### **📤 Node 9: Send Variation Image**
- **Chức năng:** Gửi video biến thể về Telegram.
- **Cấu hình:**
  - **Chat ID:** `{{ $json.message.chat.id }}`.
  - **Document:** `{{ $node["Retrieve Generated Image"].json }}`.

---

### **3. Kích hoạt ⚡️**
1. **Test Run:** Nhấn **"Execute"** trên n8n Editor và gửi ảnh + caption qua Telegram.
2. **Bật Active:** Sau khi kiểm tra thành công, chuyển workflow sang **Active**.

---

## ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁCH LÀM NÂNG CAO]
1. **Tự động lưu ảnh/video** vào Google Drive/OneDrive:
   - Thêm **Node `google-drive`** sau khi chỉnh sửa ảnh.
   - Cấu hình folder lưu trữ tự động.

2. **Gửi báo cáo định kỳ** (ví dụ: hàng tuần):
   - Sử dụng **Node `email`** hoặc **Slack** để thông báo kết quả.

3. **Tối ưu prompt** cho AI:
   - Thay đổi caption trong tin nhắn để điều chỉnh kết quả:
     - *"Make this product photo look premium"* → Ảnh sang trọng.
     - *"Add neon lights to this image"* → Ảnh hiệu ứng neon.

4. **Kết hợp với Notion/Google Sheets:**
   - Lưu danh sách ảnh đã chỉnh sửa vào bảng Excel/Notion để theo dõi.

5. **Tạo bot Telegram riêng cho team:**
   - Sử dụng `@BotFather` tạo bot mới và chia sẻ link cho đồng nghiệp.
:::

---

## 📌 **Kết luận**
Workflow này **giải phóng thời gian** của các sếp khỏi công việc chỉnh sửa ảnh thủ công, đồng thời **nâng cao chất lượng nội dung marketing** với ảnh/video chuyên nghiệp. **Chỉ cần 1 tin nhắn Telegram**, AI sẽ tự động:
✔ Chỉnh sửa ảnh theo yêu cầu.
✔ Tạo video biến thể.
✔ Gửi kết quả ngay về cho bạn.

**Hành động ngay:**
1. **Self-host n8n** trên VPS (để workflow hoạt động 24/7).
2. **Import workflow** và cấu hình API Key.
3. **Gửi ảnh + caption** qua Telegram và xem kết quả!

**🚀 CÓ THỂ THỬ NGHIỆM TRONG 5 PHÚT!** 🚀

---
**💡 Cần hỗ trợ thêm?**
- **Đăng ký VPS n8n** với mã giảm giá: **[VPSN8N](https://tino.vn/vps-n8n?affid=388)**
- **Hỏi đáp nhanh** trên [Community n8n](https://community.n8n.io/)