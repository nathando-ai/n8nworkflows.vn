---
title: "🎙️ Tự Động Xử Lý Âm Thanh với ElevenLabs: Chuyển Văn Bản → Âm Thanh, Lọc Âm Thanh & Chuyển Âm Thanh → Văn Bản (KIE.AI)"
description: "Workflow tự động hóa 100% không code giúp các sếp xử lý âm thanh hiệu quả: chuyển văn bản thành âm thanh tự nhiên, tách âm thanh nền, và chuyển âm thanh thành văn bản bằng ElevenLabs qua API KIE.AI. Giúp tiết kiệm thời gian lên đến 80% trong quá trình tạo nội dung đa phương tiện."
slug: "tieu-ly-am-than-voi-elevenlabs"
tags: [n8n, automation, no-code, elevenlabs, kie-ai, content-creation, ai-multimodal]
keywords: [n8n workflow ElevenLabs, tự động hóa xử lý âm thanh, chuyển văn bản thành âm thanh tự nhiên, tách âm thanh nền, chuyển âm thanh thành văn bản, API KIE.AI, tự động hóa nội dung đa phương tiện]
---

# 🚀 **Tự Động Xử Lý Âm Thanh với ElevenLabs: 3 Công Cụ AI Đa Phương Tiện trong Một Workflow**

### **📌 Nỗi Đau Của Các Sếp**
Các sếp thường phải mất **giờ đồng hồ** để:
- Chuyển văn bản thành âm thanh tự nhiên (TTS) cho podcast, quảng cáo, hoặc nội dung video.
- Tách âm thanh nền khỏi file âm thanh để tăng chất lượng.
- Chuyển âm thanh thành văn bản (STT) để transcribe cuộc họp hoặc nội dung video.

**Giải pháp?** Workflow này **tự động hóa toàn bộ quá trình** với **ElevenLabs** (qua API KIE.AI), giúp tiết kiệm **80% thời gian** và đảm bảo **chất lượng cao**.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
✅ **Tiết kiệm thời gian**: Xử lý âm thanh chỉ trong vài giây thay vì giờ đồng hồ.
✅ **Chất lượng chuyên nghiệp**: Âm thanh tự nhiên (TTS) và văn bản chính xác (STT).
✅ **Tách âm thanh nền**: Loại bỏ tiếng ồn, tiếng nền để âm thanh sạch hơn.
✅ **Hoạt động 24/7**: Workflow tự động kiểm tra trạng thái và hoàn thành nhiệm vụ.
✅ **Dễ dàng mở rộng**: Kết hợp với Slack, Telegram, hoặc lưu log cho quản lý.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ**]
Trước khi sử dụng, các sếp cần:
✔ **API Key KIE.AI** (miễn phí hoặc trả phí tùy chọn):
   - [Đăng ký tại KIE.AI](https://kie.ai/) (sử dụng mã giảm giá **N8NAI** để giảm 20% phí đầu tiên).
✔ **Tài khoản n8n Self-hosted** (không dùng n8n.cloud vì API KIE.AI có giới hạn request).
✔ **File âm thanh hoặc văn bản** (URL hoặc nội dung trực tiếp).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/12203](https://n8n.io/workflows/12203) hoặc copy/paste JSON vào **n8n Editor**.
- **Cách import nhanh**:
  ```bash
  curl -o workflow.json https://raw.githubusercontent.com/mfarooqone/n8n/master/workflows/12203.json
  ```
  Sau đó nhấn **Import** trong n8n Editor.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này gồm **3 phần độc lập** (có thể sử dụng riêng lẻ hoặc kết hợp):
- **Phần 1: Chuyển Văn Bản → Âm Thanh (TTS)**
- **Phần 2: Tách Âm Thanh Nền (Audio Isolation)**
- **Phần 3: Chuyển Âm Thanh → Văn Bản (STT)**

##### **🔹 Cấu Hình API KIE.AI (Bắt Buộc)**
1. **Tạo Credential HTTP Bearer Auth**:
   - Trong n8n, đi đến **Credentials** → **Add Credential** → **HTTP Bearer Auth**.
   - **Name**: `KIE.AI`
   - **Bearer Token**: Dán **API Key** từ KIE.AI vào đây.
   - Lưu và chọn credential này cho tất cả các node `httpRequest` trong workflow.

##### **🔹 Cấu Hình Mỗi Phần**
| **Phần**               | **Node Cần Chỉnh**               | **Tham Số Cần Điền**                          |
|-------------------------|-----------------------------------|-----------------------------------------------|
| **TTS (Văn Bản → Âm Thanh)** | `Set Text Input`                  | `Text`: Nhập văn bản muốn chuyển thành âm thanh. |
| **Audio Isolation**     | `Set Audio URL 1`                 | `Audio URL`: URL file âm thanh (MP3/WAV).     |
| **STT (Âm Thanh → Văn Bản)** | `Set Audio URL`                  | `Audio URL`: URL file âm thanh cần transcribe. |

##### **🔹 Cấu Hình Node Quan Trọng**
- **Node `httpRequest`**:
  - **Method**: `POST`
  - **URL**: `https://kie.ai/api/v1/...` (sử dụng URL API từ KIE.AI).
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer {{ $credentials.KIE.AI.token }}"
    }
    ```
  - **Body**: JSON theo định dạng của KIE.AI (ví dụ:
    ```json
    {
      "text": "{{ $node["Set Text Input"].json["text"] }}"
    }
    ```
    cho phần TTS).

- **Node `code` (Extract URL/Text)**:
  - Sử dụng JavaScript để trích xuất URL âm thanh hoặc văn bản từ phản hồi API.
  - Ví dụ:
    ```javascript
    // Trong node "Extract Audio URL" (TTS)
    return { audioUrl: JSON.parse($input.all()["json"]).data.audio_url };
    ```

##### **🔹 Thiết Lập Thời Gian Chờ (Wait Nodes)**
- Workflow tự động **kiểm tra trạng thái** mỗi **5 giây** (được cấu hình trong `Wait` nodes).
- Nếu cần thay đổi, chỉnh `Interval` trong node `Wait`.

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Execute Workflow** và kiểm tra phản hồi.
   - Kiểm tra **Log** để đảm bảo không có lỗi.
2. **Bật Active**:
   - Sau khi test thành công, **bật Active** để workflow chạy tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[**TẠO NỘI DUNG HIỆU QUẢ HƠN**]
- **Kết hợp với Slack/Telegram**:
  - Sử dụng node `slack` hoặc `telegram` để thông báo kết quả xử lý.
  - Ví dụ: Khi TTS hoàn thành, gửi tin nhắn "Âm thanh đã tạo xong: [URL]".
- **Lưu Log**:
  - Sử dụng node `googleSheets` hoặc `airtable` để lưu lịch sử xử lý.
- **Tự động hóa định kỳ**:
  - Sử dụng `n8n-trigger` để chạy workflow hàng ngày (ví dụ: transcribe podcast mới).
- **Tối ưu API Key**:
  - Nếu dùng nhiều workflow, chia API Key thành nhiều credential để tránh bị block.
:::

---

### 📌 **Kết Luận**
Workflow này là **công cụ mạnh mẽ** để tự động hóa **3 công việc âm thanh quan trọng** với **ElevenLabs** trên n8n. Các sếp có thể:
✔ **Tiết kiệm thời gian** trong việc tạo nội dung đa phương tiện.
✔ **Tăng chất lượng** âm thanh và văn bản.
✔ **Hoạt động 24/7** mà không cần can thiệp thủ công.

**🚀 Hãy thử ngay!**
- **Import workflow** và bắt đầu xử lý âm thanh trong vài giây.
- **Mở rộng** với các tính năng như gửi báo cáo tự động hoặc tích hợp với CRM.

---
:::note[**LƯU Ý CUỐI CUNG**]
- **Không dùng n8n.cloud** vì API KIE.AI có giới hạn request.
- **N8n Self-hosted** là lựa chọn tối ưu cho hiệu suất và bảo mật.
- **Nếu gặp vấn đề**, liên hệ tác giả:
  - **Email**: [mfarooqiqbal143@gmail.com](mailto:mfarooqiqbal143@gmail.com)
  - **Portfolio**: [mfarooqone.github.io/n8n](https://mfarooqone.github.io/n8n/)
:::