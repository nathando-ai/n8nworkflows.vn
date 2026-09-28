---
title: "🚀 Chuyển GitHub Code Sang Bài Đăng LinkedIn Tự Động Với AI Gemini & Hình Ảnh Code Đẹp"
description: "Workflow tự động hóa chuyển đổi commit code từ GitHub thành bài đăng LinkedIn chuyên nghiệp, kèm hình ảnh code đẹp và nội dung AI viết sẵn - tiết kiệm thời gian cho các dev/tech leader 100% không cần code."
slug: "chuyen-github-code-sang-linkedin-post-voi-ai"
tags: [n8n, automation, no-code, linkedin-automation, ai-content-creation, github-integration]
keywords: [n8n workflow github linkedin, tự động hóa bài đăng linkedin, ai viết bài cho devops, hình ảnh code từ commit, gemini ai cho devops]
---

# 🚀 **Tự Động Hóa: Chuyển Commit Code GitHub Thành Bài Đăng LinkedIn Đẹp Mắt**

## **💡 Nỗi Đau Của Các Sếp Dev/Tech Leader**
Mỗi lần push code mới lên GitHub, các sếp phải:
- **Tìm kiếm** commit mới trong lịch sử thay đổi.
- **Viết bài đăng** LinkedIn để chia sẻ kiến thức, nhưng thường bị "chán" vì nội dung lặp lại, thiếu sáng tạo.
- **Tạo hình ảnh code** đẹp mắt để làm bài đăng hấp dẫn, mất thời gian thiết kế HTML/CSS hoặc sử dụng tool ngoài.
- **Quên đăng** vì bận rộn, dẫn đến mất cơ hội chia sẻ kiến thức và tăng visibility.

**Workflow này giải quyết tất cả!** Dùng AI Gemini viết bài tự động, tạo hình ảnh code "Mac-window" đẹp mắt, và đăng lên LinkedIn chỉ với **một commit code mới**.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 30 phút/ngày** cho việc viết bài và tạo hình ảnh.
- **Nội dung chuyên nghiệp** do AI Gemini phân tích code và viết bài theo phong cách dev/tech leader.
- **Hình ảnh code đẹp mắt** (style Mac terminal) tự động sinh ra từ HTML/CSS.
- **Hoạt động 24/7** khi có commit mới, không cần can thiệp thủ công.
- **Tăng visibility** trên LinkedIn với bài đăng tự động, chia sẻ kiến thức hiệu quả.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản & API Keys**:
   - **GitHub**: Tài khoản với quyền truy cập repo (để workflow theo dõi commit).
   - **LinkedIn**: Tài khoản cá nhân (để đăng bài tự động).
   - **OpenRouter API**: Đăng ký [OpenRouter](https://openrouter.ai/) để sử dụng model **Gemini 2.5 Flash** (miễn phí cho số lượng nhỏ).
   - **HCTI API** (nếu sử dụng node `httpRequest` để generate image): [Đăng ký tại đây](https://hcti.com/) (hoặc thay thế bằng API khác như Replicate, DALL·E).

2. **Tham số repo GitHub**:
   - `owner` và `repository` trong node **Github Trigger** và **GitHub File Download** (điền tên repo của các sếp).

3. **URN LinkedIn**:
   - Trong node **Post to LinkedIn**, điền **URN** của tài khoản LinkedIn (thường là `urn:li:person:<ID>`). Để lấy ID:
     - Mở trang cá nhân LinkedIn.
     - Nhấn **F12** > **Network** > Reload.
     - Tìm URL chứa `urn:li:person:<ID>` (ví dụ: `urn:li:person:123456789`).

4. **Credentials cho API**:
   - **GitHub API**: Tạo [Personal Access Token](https://github.com/settings/tokens) với quyền `repo`.
   - **OpenRouter API**: API Key từ [OpenRouter Dashboard](https://openrouter.ai/).
   - **HCTI API** (nếu cần): API Key từ tài khoản HCTI.
:::

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Từ file JSON**
1. Tải workflow từ [n8n.io/workflows/12131](https://n8n.io/workflows/12131) (chọn **Export as JSON**).
2. Trên n8n Editor, nhấn **Import** > Chọn file JSON vừa tải.
3. Chọn **Create new workflow** và nhấn **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. Copy toàn bộ JSON từ [n8n.io/workflows/12131](https://n8n.io/workflows/12131) (chọn **Export as JSON**).
2. Trên n8n Editor, nhấn **Import** > **Paste JSON** > Chọn **Create new workflow**.

---

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **15 node**, nhưng các node quan trọng cần cấu hình kỹ như sau:

#### **🔹 Node "Github Trigger1" (Github Trigger)**
- **Credentials**: Chọn `githubApi` (đã cấu hình trước).
- **Update tham số**:
  - `owner`: Tên owner của repo (ví dụ: `tino-vn`).
  - `repository`: Tên repo (ví dụ: `my-repo`).
  - `event`: Đặt thành `push` để theo dõi commit mới.

#### **🔹 Node "LinkedIn Content Creator" (Agent)**
- **Prompt AI**: Workflow đã cấu hình sẵn prompt cho Gemini AI, nhưng các sếp có thể **tùy chỉnh** trong node này để:
  - Thay đổi phong cách bài viết (ví dụ: chuyên nghiệp hơn hoặc thân thiện hơn).
  - Đính kèm yêu cầu cụ thể (ví dụ: "Viết bài ngắn gọn dưới 300 từ").
- **Model**: Đã sử dụng `google/gemini-2.5-flash` (miễn phí). Nếu muốn nâng cấp, thay đổi trong `keyParameters`.

#### **🔹 Node "OpenRouter Chat Model" (lmChatOpenRouter)**
- **Credentials**: Chọn `openRouterApi` (API Key đã cấu hình).
- **Model**: Đảm bảo chọn `google/gemini-2.5-flash` (hoặc model khác nếu có).
- **Prompt**: Workflow đã cấu hình sẵn, nhưng các sếp có thể **sửa lại** để:
  ```json
  "prompt": "Analyze this code commit and write a LinkedIn post in Vietnamese. Highlight the key changes, improvements, and technical details. Keep it engaging and under 300 words. Also, extract the most relevant code snippet to include in the post."
  ```

#### **🔹 Node "Generate Code Image" (httpRequest)**
- **Credentials**: Chọn `httpBasicAuth` hoặc `httpHeaderAuth` (nếu dùng HCTI API).
- **URL API**: Đảm bảo điền đúng URL API của HCTI (hoặc thay thế bằng API khác như Replicate).
- **Tham số request**:
  - `body`: Nội dung HTML/CSS để generate hình ảnh (workflow tự động tạo từ code).
  - Ví dụ body:
    ```json
    {
      "html": "<div style='font-family: monospace; background: #1a1a1a; color: #e0e0e0; padding: 10px; border-radius: 5px;'>{{$code}}</div>"
    }
    ```

#### **🔹 Node "Post to LinkedIn" (linkedIn)**
- **Credentials**: Chọn `linkedInOAuth2Api` (đã cấu hình OAuth2).
- **URN**: Điền **URN** của tài khoản LinkedIn (xem phần **Yêu cầu cần thiết**).
- **Content**: Workflow tự động merge text từ AI + hình ảnh code vào bài đăng.

---

### **3. Kích Hoạt ⚡️**
1. **Test Run** với một commit mẫu:
   - Thêm một commit nhỏ vào repo (ví dụ: `git commit -m "Test workflow"`).
   - Chạy workflow bằng nút **Run Workflow** trên n8n Editor.
   - Kiểm tra:
     - Bài đăng có xuất hiện trên LinkedIn không?
     - Hình ảnh code có được generate đúng không?
     - Nội dung bài viết có logic không?

2. **Bật Active**:
   - Sau khi test thành công, nhấn **Active** trên workflow.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**

### **🔹 Kết hợp với Slack/Telegram để thông báo**
- Thêm node **Slack/Telegram** sau node **Post to LinkedIn** để nhận thông báo khi bài đăng thành công:
  ```json
  {
    "name": "Notify Slack",
    "type": "slack",
    "credentials": ["slackApi"],
    "keyParameters": {
      "channel": "#devops",
      "text": "🚀 Bài đăng LinkedIn mới được tự động tạo từ commit: {{$json.commit.message}}"
    }
  }
  ```

### **🔹 Lưu log hoạt động vào Google Sheets**
- Thêm node **Google Sheets** để ghi lại lịch sử bài đăng:
  ```json
  {
    "name": "Log to Google Sheets",
    "type": "googleSheets",
    "credentials": ["googleSheetsApi"],
    "keyParameters": {
      "sheetName": "LinkedIn Posts",
      "range": "A1",
      "values": [
        ["Date", "Commit Message", "Post URL", "Status"],
        [{{$json.date}}, {{$json.commit.message}}, {{$json.postUrl}}, "Success"]
      ]
    }
  }
  ```

### **🔹 Tùy chỉnh hình ảnh code**
- Nếu không muốn dùng HCTI, thay thế bằng **Replicate API** (dùng để generate image từ code):
  - Thay đổi node `Generate Code Image` thành API của Replicate.
  - Cài đặt node **Replicate** trong n8n (nếu chưa có).

### **🔹 Gửi báo cáo định kỳ**
- Thêm node **Set** để tính toán số bài đăng/ngày và gửi báo cáo qua email:
  ```json
  {
    "name": "Send Daily Report",
    "type": "set",
    "keyParameters": {
      "count": "{{$json.posts.length}}",
      "date": "{{$json.date}}"
    }
  }
  ```
  Sau đó kết nối với node **Email** để gửi báo cáo.

---

## 📌 **Kết Luận: Tự Động Hóa Bài Đăng LinkedIn Cho DevOps - Không Cần Code!**

Workflow này **giải phóng thời gian** cho các sếp dev/tech leader để tập trung vào công việc chiến lược hơn, trong khi bài đăng LinkedIn vẫn được tự động hóa, chuyên nghiệp và hấp dẫn.

**👉 Hành động ngay:**
1. **Cài n8n Self-hosted** trên VPS để workflow chạy 24/7 (không phụ thuộc vào n8n.io).
2. **Import workflow** và cấu hình theo hướng dẫn trên.
3. **Test với một commit** và bật Active!

**💡 Mẹo cuối:**
- Nếu muốn **tăng tính cá nhân hóa**, chỉnh sửa prompt trong node **LinkedIn Content Creator** để AI viết bài theo phong cách riêng của các sếp.
- Dùng **n8n Dashboard** để theo dõi hoạt động của workflow.

**Chia sẻ kết quả với #DevOpsAutomation trên LinkedIn để cùng học hỏi!** 🚀