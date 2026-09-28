---
title: "🤖 Tự Động Hóa Đánh Giá Mã Lập Trình Bằng ChatGPT Trong GitLab Merge Requests (N8n)"
description: "Giải pháp tự động hóa đánh giá code bằng AI (ChatGPT) trong GitLab Merge Requests, giúp các sếp tiết kiệm thời gian review, giảm lỗi và cải thiện chất lượng mã nguồn chỉ với 1 workflow n8n. Hoạt động 24/7, không cần code."
slug: "tieu-dong-hoa-danh-gia-code-chatgpt-gitlab-n8n"
tags: [n8n, automation, engineering, ai, gitlab, chatgpt, code-review]
keywords: [tự động hóa đánh giá code, n8n workflow gitlab, chatgpt tự động review, tự động hóa lập trình, giảm thời gian review code]
---

# 🚀 **Tự Động Hóa Đánh Giá Mã Lập Trình Bằng ChatGPT Trong GitLab Merge Requests**

### **Giải pháp cho các sếp:**
Bạn đã bao giờ cảm thấy **mệt mỏi** khi phải review hàng chục Merge Requests (MR) trên GitLab mỗi ngày? Hay **lo lắng** về việc bỏ lỡ lỗi nhỏ nhưng quan trọng trong code? Hoặc **chán ngấy** việc phải đọc từng dòng code để tìm ra những phần cần cải thiện?

**Workflow này sẽ giúp bạn:**
✅ **Tự động đánh giá code** bằng ChatGPT (GPT-4o-mini) ngay khi có Merge Request mới trên GitLab.
✅ **Lọc bỏ thay đổi không quan trọng** (ví dụ: thay đổi file README, comment, hoặc file không liên quan).
✅ **Tạo phản hồi chi tiết** về chất lượng code, đề xuất cải tiến, và cảnh báo lỗi tiềm ẩn.
✅ **Gửi phản hồi tự động vào Merge Request** dưới dạng **Discussion**, giúp team phát triển không phải mất thời gian review thủ công.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này **ổn định và hoạt động liên tục**, các sếp nên **self-host n8n** trên một VPS ổn định. N8n chạy trên máy chủ riêng sẽ tránh tình trạng **timeout** hoặc **ngắt kết nối** khi xử lý nhiều Merge Request cùng lúc.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đủ sức mạnh để chạy n8n + ChatGPT)
:::

---

## 🎯 **Kết quả các sếp nhận được**
### **Lợi ích thực tế khi áp dụng workflow này:**
1. **Tiết kiệm thời gian review**
   - Thay vì phải đọc từng Merge Request, AI sẽ **tự động đánh giá** và gửi phản hồi chi tiết.
   - Các sếp có thể **focusing** vào những phần code **phức tạp** hoặc **đòi hỏi sự chuyên môn cao** hơn.

2. **Chất lượng code được cải thiện**
   - ChatGPT sẽ **phân tích logic**, **cảnh báo lỗi tiềm ẩn**, và **đề xuất cách viết code tốt hơn**.
   - Giảm thiểu **bugs** và **việc làm lại** do lỗi nhỏ trong code.

3. **Cá nhân hóa phản hồi**
   - Các sếp có thể **tùy chỉnh prompt** để AI **phù hợp với tiêu chuẩn code** của team.
   - Ví dụ: Nếu team **ưa thích** một cách viết code nhất định, AI sẽ **tuân thủ** và đề xuất tương tự.

4. **Hoạt động liên tục (24/7)**
   - Workflow **chạy tự động** ngay khi có Merge Request mới, **không cần can thiệp** của con người.
   - **Không lo bỏ lỡ** bất kỳ Merge Request nào, kể cả vào ban đêm hoặc ngày nghỉ.

5. **Tăng cường cộng tác trong team**
   - Phản hồi từ AI được **gửi dưới dạng Discussion** trong GitLab, giúp **team dễ dàng theo dõi** và **thảo luận**.
   - Các developer có thể **trả lời AI** hoặc **cải tiến code** ngay lập tức.

---

## 🔧 **Yêu cầu cần thiết**
Trước khi **lên đồ**, các sếp cần chuẩn bị:
### **1. Tài khoản và API Key**
- **Tài khoản GitLab** (có quyền **MR Reviewer** hoặc **Maintainer**).
- **Token GitLab Personal Access Token** (có quyền `api` và `read_repository`).
- **Tài khoản OpenAI** (để sử dụng ChatGPT).
- **API Key OpenAI** (có thể lấy từ [trang tài khoản OpenAI](https://platform.openai.com/account/api-keys)).

### **2. Cấu hình GitLab**
- **Cài đặt Webhook** trong GitLab để n8n có thể **nghe** khi có Merge Request mới.
  - **URL Webhook**: `https://[your-n8n-instance]/webhook/[path-from-workflow]`
  - **Event**: `Merge Request Events` (hoặc `Push Events` nếu muốn review khi có commit mới).

### **3. Cấu hình n8n**
- **Cài đặt node `@n8n/n8n-nodes-langchain`** (để sử dụng ChatGPT).
- **Cài đặt node `@n8n/n8n-nodes-base.httpRequest`** (để gọi API GitLab).

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/2167](https://n8n.io/workflows/2167).
2. **Mở n8n Editor** và nhấn **Import** (icon `...` → **Import**).
3. **Chọn file JSON** đã tải và nhấn **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Mở n8n Editor** và nhấn **Create New Workflow**.
2. **Nhấn `...` → Import** và **dán JSON** từ workflow gốc.
3. **Nhấn Import**.

---

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này **có 3 phần chính cần chỉnh sửa**:

#### **A. Cấu hình Webhook (Node: "Webhook")**
- **Path**: Đã được cung cấp (`e21095c0-1876-4cd9-9e92-a2eac737f03e`), **không cần thay đổi**.
- **HTTP Method**: Đặt là **POST**.
- **Triggers**: Chọn **Merge Request Events** (hoặc **Push Events** nếu muốn review khi có commit mới).

#### **B. Cấu hình GitLab (Node: "Get Changes" và "Post Discussions")**
1. **Node "Get Changes" (HTTP Request)**
   - **Method**: `GET`
   - **URL**: `https://gitlab.com/api/v4/projects/[project-id]/merge_requests/[mr-id]/diff`
     - Thay `[project-id]` và `[mr-id]` bằng **ID dự án** và **ID Merge Request** từ GitLab.
     - **Lưu ý**: Có thể sử dụng **variable** trong n8n để **tự động lấy** ID từ Webhook.
   - **Headers**:
     - `PRIVATE-TOKEN`: Điền **GitLab Personal Access Token**.
     - `Content-Type`: `application/json`

2. **Node "Post Discussions" (HTTP Request)**
   - **Method**: `POST`
   - **URL**: `https://gitlab.com/api/v4/projects/[project-id]/merge_requests/[mr-id]/discussions`
   - **Headers**:
     - `PRIVATE-TOKEN`: Điền **GitLab Personal Access Token**.
     - `Content-Type`: `application/json`
   - **Body**:
     ```json
     {
       "body": "{{ $json.output.body }}", // Thay thế bằng phản hồi từ ChatGPT
       "note": true
     }
     ```

#### **C. Cấu hình ChatGPT (Node: "OpenAI Chat Model")**
- **Credentials**: Chọn **openAiApi** (đã được cấu hình trước).
- **Model**: Đặt là **`gpt-4o-mini`** (mặc định).
- **Prompt**: **Chỉnh sửa theo tiêu chuẩn code của team** (xem phần **Mẹo & gợi ý nâng cao**).

#### **D. Cấu hình Logic (Node: "If", "Split Out", "Code")**
1. **Node "Need Review" (If)**
   - **Condition**: Chọn **`jsonpath`** và điền:
     ```json
     $['object_attributes']['state'] == 'opened'
     ```
     (Đảm bảo chỉ review **Merge Request mới mở**).

2. **Node "Skip File Changes" (If)**
   - **Condition**: Chọn **`jsonpath`** và điền:
     ```json
     $['object_attributes']['title'].includes('docs') || $['object_attributes']['title'].includes('README')
     ```
     (Bỏ qua **Merge Request liên quan đến docs** hoặc **README**).

3. **Node "Parse Last Diff Line" (Code)**
   - **Mã JavaScript**:
     ```javascript
     // Lấy dòng cuối cùng của diff
     const lastDiffLine = $input.all()[0].diff.split('\n').pop();
     return { json: { lastDiffLine } };
     ```

4. **Node "Basic LLM Chain" (ChainLlm)**
   - **Prompt**: **Chỉnh sửa theo yêu cầu** (xem phần **Mẹo & gợi ý nâng cao**).
   - **Example Prompt**:
     ```
     Bạn là một developer chuyên nghiệp. Hãy phân tích đoạn code sau và trả lời:
     1. Có lỗi nào trong logic không?
     2. Có cách viết tốt hơn không?
     3. Có điểm nào cần cải thiện về performance không?
     4. Nếu có, hãy đề xuất cách sửa và lý do.
     ---
     Code:
     {{ $input.all()[0].lastDiffLine }}
     ```

---

### **3. Kích hoạt ⚡️**
1. **Test Run với dữ liệu mẫu**
   - **Tạo một Merge Request test** trên GitLab.
   - **Kích hoạt Webhook** để n8n nhận được request.
   - **Chạy workflow** và kiểm tra phản hồi từ ChatGPT.

2. **Bật Active workflow**
   - Sau khi **test thành công**, nhấn **Active** để workflow **chạy tự động** khi có Merge Request mới.

---

## ✍️ **Mẹo & gợi ý nâng cao**

### **1. Tùy chỉnh Prompt cho phù hợp với team**
- **Ví dụ prompt cơ bản**:
  ```plaintext
  Bạn là một developer chuyên nghiệp trong lĩnh vực [ngành nghề của team]. Hãy phân tích đoạn code sau và trả lời:
  1. Có lỗi nào trong logic không? Nếu có, hãy mô tả và đề xuất cách sửa.
  2. Có cách viết tốt hơn không? Nếu có, hãy so sánh và lý giải.
  3. Có điểm nào cần cải thiện về performance, security, hoặc readability không?
  4. Nếu code liên quan đến API, hãy kiểm tra xem có lỗi request/response nào không?
  ---
  Code:
  {{ $input.all()[0].lastDiffLine }}
  ```
- **Cách tùy chỉnh**:
  - Thêm **tiêu chuẩn code** riêng của team (ví dụ: **naming convention**, **logging standard**).
  - Nếu team **sử dụng một framework** nhất định (React, Django, Spring), hãy **nhắc nhở AI** về những quy tắc đặc biệt.

### **2. Lọc bỏ Merge Request không cần review**
- **Cách 1**: Sử dụng **Node "Skip File Changes"** để bỏ qua:
  - Merge Request liên quan đến **docs**, **README**, **test files**.
  - Merge Request từ **bot** hoặc **CI/CD**.
- **Cách 2**: Thêm **Node If** mới để kiểm tra:
  ```json
  $['object_attributes']['author']['username'] == 'bot'
  ```

### **3. Gửi phản hồi vào Slack/Telegram**
- **Thêm Node Slack/Telegram** sau **Node "Post Discussions"** để:
  - **Báo động** khi có Merge Request cần review.
  - **Gửi tóm tắt phản hồi** từ AI cho team.

### **4. Lưu log phản hồi để theo dõi**
- **Thêm Node "StickyNote"** để lưu **tất cả phản hồi** từ AI.
- **Cách sử dụng**:
  - Node **StickyNote** sẽ lưu **tất cả phản hồi** vào một **file JSON** hoặc **database**.
  - Sau đó, các sếp có thể **xem lịch sử** để **cải thiện chất lượng code** theo thời gian.

### **5. Chạy workflow cho nhiều dự án GitLab**
- **Sử dụng variable** trong n8n để:
  - **Lấy danh sách dự án** từ GitLab.
  - **Lặp qua từng dự án** và **review tất cả Merge Requests**.

---

## 📌 **Kết luận**
### **Bắt tay vào tự động hóa review code ngay hôm nay!**
Workflow này **giúp các sếp**:
✔ **Tiết kiệm thời gian** review code thủ công.
✔ **Cải thiện chất lượng mã nguồn** nhờ AI ChatGPT.
✔ **Tăng cường hiệu suất team** với phản hồi tự động.
✔ **Hoạt động 24/7** mà không cần can thiệp.

**Hành động ngay:**
1. **Chuẩn bị** tài khoản GitLab và OpenAI.
2. **Import workflow** và **cấu hình** theo hướng dẫn.
3. **Test run** với một Merge Request mẫu.
4. **Bật Active** và **nhận phản hồi tự động** cho tất cả Merge Request!

**Nếu có vấn đề**, các sếp có thể:
- **Trao đổi trên cộng đồng n8n** ([n8n Community](https://community.n8n.io/)).
- **Liên hệ với tác giả** ([assert](https://n8n.io/workflows/2167)) để hỗ trợ.

**Chúc các sếp thành công với tự động hóa review code!** 🚀💻