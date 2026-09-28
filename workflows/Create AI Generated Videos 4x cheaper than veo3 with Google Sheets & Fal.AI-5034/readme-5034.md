---
title: "🎬 Tự Động Hoá Sáng Tạo Video AI 4 Lần Rẻ Hơn Veo3 Với Google Sheets & Fal.AI"
description: "Hướng dẫn chi tiết cách tự động hóa việc tạo video AI 5 giây với chi phí thấp hơn 4 lần so với Veo3, chỉ cần thêm ý tưởng vào Google Sheets và kết hợp với Fal.AI & OpenAI. Giúp các sếp tiết kiệm thời gian và chi phí trong content marketing."
slug: "tu-dong-hoa-tao-video-ai-4-lan-re-hon-veo3"
tags: [n8n, automation, no-code, google-sheets, ai-video-generation, fal-ai, openai, content-marketing]
keywords: [tự động hóa video AI, tạo video với Fal.AI, n8n workflow, google sheets tự động, giảm chi phí video marketing, AI video generation]
---

# 🚀 **Tự Động Hoá Tạo Video AI 4 Lần Rẻ Hơn Veo3 Với Google Sheets & Fal.AI**

### **Giải pháp hoàn hảo cho các sếp muốn tạo video AI chuyên nghiệp mà không cần chi phí cao**

Hiện nay, việc tạo video marketing là một trong những đầu tư quan trọng nhất cho doanh nghiệp, nhưng chi phí lại rất cao. **Veo3** (một dịch vụ tạo video AI nổi tiếng) tính phí lên đến **$1.40 cho mỗi video 5 giây** – một con số khiến nhiều doanh nghiệp phải suy nghĩ hai lần. **Nhưng bạn đã biết chưa?** Với **Fal.AI** và công cụ tự động hóa **n8n**, bạn có thể tạo video AI **4 lần rẻ hơn** – chỉ **$0.35 cho mỗi video 5 giây** – và **tự động hóa toàn bộ quy trình** chỉ bằng cách thêm ý tưởng vào **Google Sheets**!

Không cần viết code, không cần kiến thức kỹ thuật, chỉ cần **cài đặt workflow này** và **điền thông tin vào bảng Google Sheets**, bạn đã có thể tạo video AI chuyên nghiệp, cá nhân hóa và phù hợp với chiến dịch marketing của mình.

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm chi phí**: Chi phí video giảm **4 lần** so với Veo3 (từ $1.40 → $0.35/5s).
- **Tự động hóa hoàn toàn**: Chỉ cần thêm ý tưởng vào Google Sheets, workflow sẽ tự động tạo video và cập nhật kết quả.
- **Cá nhân hóa video**: Mỗi video đều được tạo dựa trên **prompt AI** phù hợp với nội dung của bạn.
- **Hoạt động 24/7**: Không cần can thiệp thủ công, workflow chạy liên tục và cập nhật kết quả vào Google Sheets.
- **Dễ dàng theo dõi**: Tất cả video và prompt được lưu trữ trong bảng Google Sheets, giúp quản lý và phân tích hiệu quả.
:::

---

## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google Cloud** (để kích hoạt **Google Sheets API** và tạo **OAuth 2.0 credentials**).
2. **Tài khoản Google Sheets** (sử dụng **bảng mẫu** được cung cấp hoặc tạo bảng mới với các cột: **Idea, Ratio, Prompt Generated, Video Generated**).
3. **API Key OpenAI** (để tạo **prompt AI** cho video).
4. **Tài khoản Fal.AI** (đăng ký và nạp tiền để tạo video).
5. **API Key Fal.AI** (để gửi yêu cầu tạo video).
6. **n8n Self-hosted** (để workflow chạy 24/7 ổn định).
:::

---

## 🎯 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Bước 1: **Tải workflow JSON** từ [link gốc](https://n8n.io/workflows/5034) hoặc sao chép mã JSON từ đây.

Bước 2: Mở **n8n Editor** và nhấn **"Import"** → **"From JSON"** → Dán mã JSON và nhấn **"Import"**.

:::note[LƯU Ý]
- **Không chỉnh sửa trực tiếp trên canvas** nếu chưa hiểu rõ logic, để tránh lỗi.
- **Kích hoạt mode "Test"** trước khi chạy thực tế.
:::

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **🔹 Node 1: Google Sheets Trigger (n8n-nodes-base.googleSheetsTrigger)**
- **Chọn credentials**: `"googleSheetsTriggerOAuth2Api"` (đã tạo từ Google Cloud).
- **Chọn sheet**: Chọn **bảng mẫu** hoặc bảng mới với cấu trúc:
  | **Idea**       | **Ratio** | **Audio** (true/false) |
  |----------------|-----------|------------------------|
  | "Video giới thiệu sản phẩm" | 9:16 | true |

#### **🔹 Node 2: Generate prompt for Kling 2.1 model (n8n-nodes-langchain.openAi)**
- **Chọn credentials**: `"openAiApi"` (điền **API Key OpenAI**).
- **Cấu hình OpenAI**:
  - **Model**: `gpt-3.5-turbo` (hoặc model khác phù hợp).
  - **Prompt template**:
    ```plaintext
    Tạo một prompt chi tiết cho video AI với nội dung: "{{$node["Google Sheets Trigger"].json["Idea"]}}".
    Video ratio: "{{$node["Google Sheets Trigger"].json["Ratio"]}}".
    Nếu có audio, yêu cầu audio tự nhiên và phù hợp với nội dung.
    ```
  - **Output format**: Chọn `"json"` để trả về kết quả dễ dàng xử lý.

#### **🔹 Node 3: Set variables for Video generation (n8n-nodes-base.set)**
- **Điền biến cần thiết**:
  - `prompt`: Giá trị từ **Node OpenAI**.
  - `ratio`: Giá trị từ **Google Sheets** (`9:16`, `16:9`, `1:1`).
  - `audio`: `true`/`false` (tùy thuộc vào bảng Google Sheets).

#### **🔹 Node 4: Submit Request to generate video (n8n-nodes-base.httpRequest)**
- **URL**: `https://api.fal.ai/v1/video`
- **Headers**:
  ```json
  {
    "Authorization": "Key YOUR_FAL_AI_API_KEY",
    "Content-Type": "application/json"
  }
  ```
- **Body (JSON)**:
  ```json
  {
    "model": "kling-2.1",
    "prompt": "{{$node["Set variables for Video generation"].json["prompt"]}}",
    "ratio": "{{$node["Set variables for Video generation"].json["ratio"]}}",
    "audio": "{{$node["Set variables for Video generation"].json["audio"]}}"
  }
  ```

#### **🔹 Node 5: Check video status (n8n-nodes-base.httpRequest)**
- **URL**: `https://api.fal.ai/v1/video/status` (sử dụng **ID video** từ response của Node 4).
- **Headers**:
  ```json
  {
    "Authorization": "Key YOUR_FAL_AI_API_KEY"
  }
  ```
- **Thêm Node Wait 5s** để tránh quá tải API.

#### **🔹 Node 6: Get video url (n8n-nodes-base.httpRequest)**
- **URL**: `https://api.fal.ai/v1/video/{{$node["Check video status"].json["id"]}}`
- **Headers**:
  ```json
  {
    "Authorization": "Key YOUR_FAL_AI_API_KEY"
  }
  ```

#### **🔹 Node 7: Update sheet with video url and prompt used (n8n-nodes-base.googleSheets)**
- **Chọn credentials**: `"googleSheetsOAuth2Api"`.
- **Cập nhật cột**:
  - `Prompt Generated`: Giá trị từ **Node OpenAI**.
  - `Video Generated`: Link video từ **Node Get video url**.

---

### **3. Kích hoạt ⚡️**
- **Test run**: Chọn **1 row mẫu** trong Google Sheets và chạy workflow để kiểm tra.
- **Bật Active**: Sau khi kiểm tra thành công, **bật workflow** để chạy tự động khi có dữ liệu mới.

---

## ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁCH LÀM NÂNG CAO]
1. **Tích hợp Slack/Telegram**: Khi video sẵn sàng, gửi thông báo tự động qua Slack/Telegram bằng **n8n-nodes-base.slack** hoặc **n8n-nodes-base.telegram**.
2. **Lưu log hoạt động**: Sử dụng **n8n-nodes-base.set** để lưu lịch sử tạo video vào một sheet riêng.
3. **Gửi báo cáo định kỳ**: Tạo một workflow khác để tổng hợp và gửi báo cáo số liệu video đã tạo hàng tháng.
4. **Cá nhân hóa video**: Sử dụng **OpenAI API** để tạo **prompt khác nhau** cho từng khách hàng hoặc chiến dịch.
5. **Optimize chi phí**: Nếu video dài hơn 5s, chia nhỏ thành nhiều đoạn ngắn để tiết kiệm chi phí.
:::

---

## 📌 **Kết luận**
Với **workflow này**, các sếp không chỉ **giảm chi phí video 4 lần** so với Veo3 mà còn **tự động hóa toàn bộ quy trình** chỉ bằng cách thêm ý tưởng vào Google Sheets. **Không cần kỹ thuật, không cần code**, chỉ cần **cài đặt và chạy** là xong!

:::success[HÀNH ĐỘNG NGÀY HÔM NAY]
1. **Đăng ký VPS** để self-host n8n (để workflow chạy 24/7).
   👉 [TinoHost (Mã giảm giá: **VPSN8N**)](https://tino.vn/vps-n8n?affid=388)
   👉 [BNIX (Xeon 4GB chỉ 50k/tháng)](https://my.bnix.one/aff.php?aff=172)

2. **Import workflow** và **cấu hình API keys** theo hướng dẫn trên.

3. **Thêm ý tưởng đầu tiên** vào Google Sheets và **chờ workflow tự động tạo video**!

**Bắt đầu tự động hóa video AI của bạn ngay hôm nay!** 🚀
:::