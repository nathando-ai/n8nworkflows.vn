---
title: "🎨 **Tự Động Hoà Hợp AI: Tạo Câu Chuyện Động Hình Tự Động Với GPT-4o-mini, Midjourney & Kling (N8N Workflow 45 Node)""
description: "Workflow tự động hóa hoàn chỉnh giúp các sếp tạo **câu chuyện động hình 3D cá nhân hóa** chỉ với 1 cú nhấp chuột, kết hợp AI văn bản (GPT-4o-mini), sinh ảnh (Midjourney) và video (Kling) + kết xuất chuyên nghiệp (Creatomate). Giúp tiết kiệm **100+ giờ/lần** so với cách làm thủ công."
slug: "tạo-câu-chuyện-dộng-hình-tự-dộng-với-n8n"
tags: [n8n, automation, ai-generate, midjourney, kling, creatomate, marketing-automation, no-code]
keywords: [n8n workflow tự động hóa, tạo câu chuyện động hình AI, Midjourney + Kling + Creatomate, tự động hóa content marketing, sinh ảnh động hình tự động, GPT-4o-mini prompt engineering]
---

# 🚀 **Tạo Câu Chuyện Động Hình Tự Động: Từ Văn Bản → Ảnh → Video → Kết Xuất Chuyên Nghiệp**

Hiện nay, việc tạo **câu chuyện động hình cá nhân hóa** cho marketing, training, hoặc content thường tốn **thời gian và chi phí khổng lồ**. Các sếp phải:
- **Viết kịch bản** (hoặc thuê người viết).
- **Sinh ảnh** bằng Midjourney (và chờ đợi).
- **Chỉnh sửa video** bằng Kling (và điều chỉnh lại nhiều lần).
- **Kết xuất** bằng Creatomate (và đảm bảo chất lượng).

**Workflow này giải quyết tất cả trong 1 lần nhấp chuột**, kết hợp **AI văn bản (GPT-4o-mini), sinh ảnh (Midjourney), video (Kling) và kết xuất chuyên nghiệp (Creatomate)** để tạo ra **câu chuyện động hình 3D hoàn chỉnh** chỉ trong **vài phút** thay vì **ngày**.

---
## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**3 Lợi Ích Cốt Lõi**]
✅ **Tiết kiệm 100+ giờ/lần**: Không cần viết kịch bản, chỉnh sửa ảnh, hoặc kết xuất video thủ công.
✅ **Cá nhân hóa hoàn toàn**: Điền **ngôn ngữ, nhân vật, và tình huống** vào **Basic Params**, AI sẽ tự động sinh nội dung phù hợp.
✅ **Chất lượng chuyên nghiệp**: Video kết xuất bằng Creatomate với **động tác mượt mà, âm thanh đồng bộ**, và **chất lượng HD**.
✅ **Hoạt động 24/7**: Chỉ cần **bật workflow**, nó sẽ tự động chạy khi có yêu cầu (hoặc kích hoạt thủ công).
:::

---
## 🔧 **Yêu Cầu Cần Thiết**
Để workflow hoạt động, các sếp cần chuẩn bị:
### **1. API Keys & Credentials**
| Dịch vụ/API          | Thông tin cần thiết                                                                 | Làm thế nào để lấy?                                                                 |
|----------------------|--------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| **Midjourney**       | API Key (hoặc token)                                                               | [Đăng ký Midjourney API](https://www.midjourney.com/app/) (nếu sử dụng API chính thức) |
| **Kling**           | API Key                                                                             | [Đăng ký Kling](https://kling.ai/) và lấy từ **Settings > API Keys**                  |
| **Creatomate**       | API Key + Template ID (để kết xuất video)                                           | [Đăng ký Creatomate](https://creatomate.com/) và tạo **template video** trước khi chạy workflow |
| **GPT-4o-mini**     | API Key (hoặc sử dụng n8n-proxy với OpenAI)                                        | [Đăng ký OpenAI](https://platform.openai.com/) và lấy từ **API Keys**                |

### **2. Cấu Hình Trước Khi Chạy**
- **Basic Params**: Điền **3 thông tin cơ bản** trong node **"Basic Params"** (type: `set`):
  - **Style**: Phong cách của câu chuyện (ví dụ: *"Phong cách anime 3D, màu sắc tươi sáng"*).
  - **Character**: Nhân vật chính (ví dụ: *"Một nhân vật doanh nhân trẻ, mặc áo sơ mi trắng, có biểu cảm động viên"*).
  - **Situation_keyword**: Tình huống (ví dụ: *"Trong một cuộc họp marketing, đang trình bày chiến lược mới"*).
- **Template Creatomate**: Tạo **1 template video** trong Creatomate để kết xuất (ví dụ: *"Chuyển động từ ảnh đến video với hiệu ứng zoom-in"*).

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/3655](https://n8n.io/workflows/3655) (chọn **Export as JSON**).
2. **Mở n8n Editor** (trên n8n.io hoặc self-hosted).
3. Nhấn **Import** → Chọn file JSON vừa tải → **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ JSON** từ [n8n.io/workflows/3655](https://n8n.io/workflows/3655) (chọn **Export as JSON**).
2. Trong **n8n Editor**, nhấn **Import** → Chọn **Paste JSON** → **Import**.

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này **phức tạp** (45 node) vì phải **quản lý đồng bộ** giữa Midjourney, Kling và Creatomate. Dưới đây là **các node quan trọng cần cấu hình**:

#### **🔹 Node "Basic Params" (type: set)**
- **Điền 3 trường**:
  ```json
  {
    "style": "Phong cách anime 3D, màu sắc tươi sáng, hiệu ứng ánh sáng neon",
    "character": "Một nhân vật doanh nhân trẻ, 25-30 tuổi, mặc áo sơ mi trắng, có biểu cảm động viên và tay chỉ về phía trước",
    "situation_keyword": "Trong một cuộc họp marketing, đang trình bày chiến lược mới với biểu đồ tăng trưởng"
  }
  ```
- **Lưu ý**: GPT-4o-mini sẽ **tự động sinh mô tả ảnh** từ 3 thông tin này.

#### **🔹 Node "GPT-4o-mini Generate Image Scenario Prompt" (type: httpRequest)**
- **Tham số cần thiết**:
  - **URL**: `https://api.openai.com/v1/chat/completions`
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer YOUR_OPENAI_API_KEY",
      "Content-Type": "application/json"
    }
    ```
  - **Body (JSON)**:
    ```json
    {
      "model": "gpt-4o-mini",
      "messages": [
        {
          "role": "user",
          "content": "Tạo mô tả chi tiết cho 3 cảnh động hình dựa trên các tham số sau:\n- Style: {{ $node["Basic Params"].json("style") }}\n- Character: {{ $node["Basic Params"].json("character") }}\n- Situation: {{ $node["Basic Params"].json("situation_keyword") }}\n\nMỗi cảnh phải có:\n1. Mô tả chi tiết nhân vật và cảnh quay.\n2. Gợi ý camera angle (góc quay).\n3. Hiệu ứng đặc biệt (nếu có).\n\nĐảm bảo mô tả phù hợp với phong cách anime 3D."
        }
      ]
    }
    ```
- **Lưu ý**:
  - Thay thế `YOUR_OPENAI_API_KEY` bằng API key của bạn.
  - **Test run** trước khi chạy workflow toàn bộ.

#### **🔹 Node "Midjourney Generator" (type: httpRequest)**
- **Tham số cần thiết**:
  - **URL**: `https://api.midjourney.com/v1/image/generate` (hoặc API Midjourney khác nếu sử dụng proxy).
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer YOUR_MIDJOURNEY_API_KEY",
      "Content-Type": "application/json"
    }
    ```
  - **Body (JSON)**:
    ```json
    {
      "prompt": "{{ $node["GPT-4o-mini Generate Image Scenario Prompt"].json("content") }}",
      "style": "3D anime",
      "quality": "high"
    }
    ```
- **Lưu ý**:
  - **Chờ đợi** (node `Wait for the First Image Generation`) để Midjourney hoàn thành.
  - **Kiểm tra trạng thái** bằng node `Verify the first image generation status` (type: `if`).

#### **🔹 Node "Kling Video Generator" (type: httpRequest)**
- **Tham số cần thiết**:
  - **URL**: `https://api.kling.ai/v1/video/generate`
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer YOUR_KLING_API_KEY",
      "Content-Type": "application/json"
    }
    ```
  - **Body (JSON)**:
    ```json
    {
      "input": {
        "images": ["{{ $node["Get three Image URLs"].json("image1") }}", "{{ $node["Get three Image URLs"].json("image2") }}", "{{ $node["Get three Image URLs"].json("image3") }}"],
        "transition": "fade",
        "duration": 10
      }
    }
    ```
- **Lưu ý**:
  - **Chờ đợi** (node `Wait for Video Generation for at Least 4 min`) vì Kling cần thời gian xử lý.
  - **Kiểm tra trạng thái** bằng node `Verify the First Video Generation` (type: `if`).

#### **🔹 Node "Final Video Combination" (type: httpRequest)**
- **Tham số cần thiết**:
  - **URL**: `https://api.creatomate.com/v1/video/combine`
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer YOUR_CREATOMATE_API_KEY",
      "Content-Type": "application/json"
    }
    ```
  - **Body (JSON)**:
    ```json
    {
      "template_id": "YOUR_TEMPLATE_ID",
      "video_urls": ["{{ $node["Get the First Video URL"].json("url") }}", "{{ $node["Get the Second Video URL"].json("url") }}", "{{ $node["Get the Third Video URL"].json("url") }}"],
      "output_format": "mp4"
    }
    ```
- **Lưu ý**:
  - **Điền `YOUR_TEMPLATE_ID`** từ Creatomate.
  - **Kết quả cuối cùng** sẽ là **file video MP4** được kết xuất từ 3 cảnh.

---
### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run**:
   - Nhấn **Test Workflow** (node `When clicking Test workflow`).
   - Điền **Basic Params** và chạy.
   - **Kiểm tra log** để đảm bảo không có lỗi.

2. **Bật Active**:
   - Sau khi test thành công, **bật switch Active** trên workflow.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**
### **1. Tự Động Hoá Gửi Video Sang Slack/Email**
- **Thêm node `n8n-nodes-base.slack`** sau node `Final Video Combination` để gửi **link video** vào Slack.
- **Thêm node `n8n-nodes-base.email`** để gửi **file video** cho khách hàng.

### **2. Lưu Log & Theo Dõi Lịch Sử**
- **Thêm node `n8n-nodes-base.googleSheets`** để lưu **tất cả thông tin** (prompt, URL ảnh, URL video) vào Google Sheets.
- **Cấu hình** để tự động **xóa file tạm** sau khi hoàn thành.

### **3. Tối Ưu Hóa Prompt cho GPT-4o-mini**
- **Cập nhật node `GPT-4o-mini Generate Image Scenario Prompt`** với **các gợi ý cụ thể**:
  ```json
  {
    "role": "user",
    "content": "Tạo mô tả chi tiết cho 3 cảnh động hình **phù hợp với phong cách anime 3D hiện đại**, với các yêu cầu sau:\n\n1. **Cảnh 1**: {{ $node["Basic Params"].json("situation_keyword") }} với **góc quay close-up** vào nhân vật ({{ $node["Basic Params"].json("character") }}).\n   - Yêu cầu: Ánh sáng tập trung vào mặt nhân vật, hiệu ứng **glow** xung quanh.\n\n2. **Cảnh 2**: Nhân vật **di chuyển** trong không gian (ví dụ: phòng họp) với **camera angle wide shot**.\n   - Yêu cầu: Hiệu ứng **motion blur** khi nhân vật chuyển động.\n\n3. **Cảnh 3**: **Kết thúc** với **camera zoom-in** vào biểu đồ tăng trưởng.\n   - Yêu cầu: Hiệu ứng **particle effect** khi biểu đồ hiện ra.\n\n**Đảm bảo mô tả phù hợp với style**: {{ $node["Basic Params"].json("style") }}."
  }
  ```

### **4. Sử Dụng Workflow cho Marketing**
- **Tạo nhiều biến thể** (ví dụ: *"Câu chuyện về sản phẩm A"*, *"Câu chuyện về sản phẩm B"*).
- **Kết hợp với node `n8n-nodes-base.manualTrigger`** để **bật workflow khi có yêu cầu mới**.

---
## 📌 **Kết Luận: Áp Dụng Ngay & Tiết Kiệm Thời Gian**
Workflow này **giải phóng các sếp** khỏi việc **viết kịch bản, sinh ảnh, và chỉnh sửa video thủ công**. Với **chỉ 1 cú nhấp chuột**, bạn có thể tạo ra **câu chuyện động hình 3D chuyên nghiệp** trong **vài phút** thay vì **ngày**.

:::success[**Hành Động Ngay**]
1. **Cài đặt n8n trên VPS** (để workflow hoạt động 24/7).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

2. **Import workflow** và **cấu hình API keys**.
3. **Test run** và **bật