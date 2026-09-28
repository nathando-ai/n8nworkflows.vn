---
title: "🎨 **Tự Động Hoà Trộn & Ghép Hình Nhiều File Sáng Tạo Với n8n + Gemini AI (Không Cần Code!)**"
description: "Workflow tự động hóa sử dụng Gemini AI để ghép nhiều hình ảnh riêng lẻ thành một bức ảnh mới duy nhất, giữ nguyên phong cách và chi tiết nguồn gốc. Phù hợp cho thiết kế marketing, storyboard, hoặc tạo nội dung sáng tạo cá nhân hóa."
slug: "tự-dộng-hoa-trong-ghep-hinh-nhieu-file-voi-gemini-ai"
tags: [n8n, automation, ai-gemini, design-marketing, google-drive, no-code]
keywords: [n8n workflow ghép hình, tự động hóa thiết kế AI, Gemini Image Editing, tự động hóa marketing, ghép ảnh không code]
---

# 🚀 **Tự Động Ghép Hình Nhiều File Sáng Tạo Với n8n + Gemini AI**

## **🔍 Nỗi Đau Của Các Sếp**
Bạn có bao giờ phải **ghép nhiều hình ảnh nhỏ thành một bức ảnh hoàn chỉnh** để tạo ra:
- **Storyboard** với các nhân vật nhất quán?
- **Tài liệu marketing** với sản phẩm và bối cảnh phù hợp?
- **Nội dung sáng tạo** như "thử đồ" với nhiều góc độ?
- **Báo cáo thiết kế** với các phần tử riêng lẻ cần được sắp xếp logic?

Thủ công làm việc này **tốn thời gian, dễ sai sót**, và khó đảm bảo **phong cách nhất quán** giữa các phần. **Workflow này giải quyết tất cả bằng AI Gemini + n8n**, giúp tự động hóa quá trình ghép hình **một cách sáng tạo và chính xác 100%**.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
✅ **Tiết kiệm thời gian** – Ghép hình chỉ với một cú nhấp chuột thay vì làm thủ công.
✅ **Chất lượng cao** – Gemini AI đảm bảo **phong cách nhất quán** giữa các phần tử nguồn.
✅ **Cá nhân hóa** – Đặt **prompt tùy chỉnh** để AI ghép hình theo ý muốn (ví dụ: "hãy ghép nhân vật này vào cảnh sofa").
✅ **Hoạt động 24/7** – Workflow chạy tự động khi kích hoạt, không cần can thiệp.
✅ **Lưu trữ an toàn** – Kết quả được tự động upload lên **Google Drive** (hoặc dịch vụ khác).
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ**]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Google Drive** (để lưu trữ hình ảnh đầu vào và kết quả).
✔ **API Key của Google Gemini** (đăng ký tại [Google AI Studio](https://makersuite.google.com/)).
✔ **Ba hình ảnh hoặc nhiều hơn** (định dạng PNG/JPG) để ghép vào một bức ảnh mới.
✔ **N8n Self-hosted** (để workflow chạy ổn định 24/7).
:::

---
## **🚀 Cách Import & Cấu Hình Workflow**

### **1. Import Workflow 📥**
Các sếp có thể **import workflow từ file JSON** hoặc **copy/paste JSON** vào **n8n Editor**:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/4817).
- Mở **n8n Editor** → Nhấn **"Import"** → Chọn file JSON → **"Import Workflow"**.

:::note[**Lưu ý**]
- Nếu import từ **Google Drive**, các sếp cần **chọn "Manual Trigger"** để bắt đầu workflow.
- **Không cần thay đổi cấu trúc**, chỉ cần **cấu hình các node quan trọng** như hướng dẫn dưới đây.
:::

---

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**

#### **🔹 Node "Upload to Drive" (Google Drive)**
- **Cấu hình OAuth2**:
  - Đăng nhập vào tài khoản **Google Drive** của mình.
  - Tạo **credentials mới** trong **n8n** với tên `"googleDriveOAuth2Api"`.
  - Chọn **scope**: `https://www.googleapis.com/auth/drive.file` (để upload file).
- **Folder upload**: Chọn **folder mục tiêu** để lưu hình ảnh đầu vào và kết quả.

#### **🔹 Node "Gemini Image Compose" (HTTP Request)**
- **Tham số quan trọng**:
  - **URL API**: `https://generativelanguage.googleapis.com/v1beta/models/gemini-pro-vision:generateContent`
  - **Headers**:
    - `Content-Type: application/json`
    - `Authorization: Bearer {API_KEY_GOOGLE_GEMINI}`
  - **Body (JSON)**:
    ```json
    {
      "contents": [
        {
          "parts": [
            {
              "text": "Combine these images into a single cohesive scene. The character should be sitting on the sofa, interacting naturally with the environment. Keep the style consistent with the original images."
            },
            {
              "inlineData": {
                "mimeType": "image/jpeg",
                "data": "{{ $json.base64Character }}"
              }
            },
            {
              "inlineData": {
                "mimeType": "image/jpeg",
                "data": "{{ $json.base64Dalmation }}"
              }
            },
            {
              "inlineData": {
                "mimeType": "image/jpeg",
                "data": "{{ $json.base64Sofa }}"
              }
            }
          ]
        }
      ]
    }
    ```
  - **Lưu ý**:
    - Thay thế `{{ $json.base64Character }}`, `{{ $json.base64Dalmation }}`, `{{ $json.base64Sofa }}` bằng **base64** của hình ảnh tương ứng (tự động lấy từ node trước).
    - **Prompt** có thể thay đổi tùy ý (ví dụ: "ghép nhân vật vào cảnh phố", "tạo một bức ảnh quảng cáo sản phẩm").

#### **🔹 Node "Convert to File" (Binary → File)**
- **Chọn operation**: `toBinary` (để chuyển base64 thành binary).
- **File format**: Chọn **PNG/JPG** tùy ý.

#### **🔹 Node "Extract from File" (Binary → Base64)**
- **Chọn operation**: `binaryToProperty` (để chuyển binary thành base64 cho Gemini xử lý).

---
### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run** với **dữ liệu mẫu**:
   - Nhấn **"Execute Workflow"** → Chọn **3 hình ảnh** (ví dụ: nhân vật, chó Dalmatian, ghế sofa).
   - Kiểm tra **output** trên Google Drive.
2. **Bật Active**:
   - Sau khi test thành công, **bật "Active"** để workflow chạy tự động khi kích hoạt.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **🔹 Kết Hợp Với Slack/Telegram**
- Thêm **node Slack/Telegram** sau khi upload thành công để **báo cáo kết quả** tự động.
- Ví dụ:
  ```json
  {
    "blockKit": {
      "blocks": [
        {
          "type": "section",
          "text": {
            "type": "mrkdwn",
            "text": "🎨 *Hình ảnh ghép mới đã tạo thành công!*\n*Link:* <{{ $json.googleDriveUrl }}|Xem trên Drive>"
          }
        }
      ]
    }
  }
  ```

### **🔹 Lưu Log & Báo Cáo Định Kỳ**
- Thêm **node "Set"** để lưu **thông tin metadata** (tên file, ngày tạo, prompt sử dụng).
- Sử dụng **node "Google Sheets"** để **lưu lịch sử** các lần ghép hình.

### **🔹 Ghép Nhiều Hình Hơn**
- Workflow hiện hỗ trợ **3 hình**, nhưng có thể **tăng số lượng** bằng cách:
  - Thêm **node "Merge"** và **"Aggregate"** để xử lý nhiều base64.
  - **Cảnh báo**: Số lượng hình ảnh nhiều sẽ **tăng chi phí API** và **thời gian xử lý**.

### **🔹 Sử Dụng Prompt Tùy Chỉnh**
- **Cách viết prompt hiệu quả**:
  - **Định vị**: "Hãy đặt nhân vật này ở góc trên bên trái của bức ảnh."
  - **Phong cách**: "Giữ phong cách nghệ thuật của hình ảnh nguồn."
  - **Chi tiết**: "Tăng độ tương phản để nổi bật sản phẩm."

---
## **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp trong việc **tạo nội dung sáng tạo** bằng cách tự động ghép hình với **Gemini AI**, đảm bảo **chất lượng cao và nhất quán**. **Không cần code**, chỉ cần **cấu hình vài bước** là có thể sử dụng ngay!

👉 **Bắt đầu ngay** bằng cách:
1. **Import workflow** từ [đây](https://n8n.io/workflows/4817).
2. **Cấu hình Google Drive & Gemini API**.
3. **Kích hoạt và thử nghiệm** với các hình ảnh của mình!

---
### **🔗 Tài Liệu Tham Khảo**
- [Gemini Image Editing - Google AI](https://ai.google.dev/gemini-api/docs/image-generation#gemini-image-editing)
- [Google Drive Node - n8n Docs](https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.googledrive)
- [Extract from File Node - n8n Docs](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.extractfromfile)

---
### **💡 Cần Hỗ Trợ?**
- **Join Discord n8n**: [https://discord.com/invite/XPKeKXeB7d](https://discord.com/invite/XPKeKXeB7d)
- **Forum Cộng Đồng**: [https://community.n8n.io/](https://community.n8n.io/)

---
:::info[**Gợi Ý Hạ Tầng Cho n8n**]
Để workflow chạy **ổn định 24/7**, các sếp nên **self-host n8n** trên **VPS**:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**Happy Automating!** 🚀