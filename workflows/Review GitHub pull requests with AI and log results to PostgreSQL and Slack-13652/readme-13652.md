---
title: "🤖 **Tự Động Hóa Đánh Giá PR GitHub Bằng AI + Log Kết Quả Vào PostgreSQL & Slack** – Giúp Dev Team Tiết Kiệm 100h/Năm"
description: "Workflow tự động phân tích PR trên GitHub bằng AI, đánh giá chất lượng mã, an toàn và hiệu suất, sau đó ghi log kết quả vào PostgreSQL và thông báo trên Slack. Giúp dev team giảm thiểu lỗi, cải thiện codebase và tiết kiệm thời gian review thủ công."
slug: "tieu-dong-hoa-danh-gia-pr-github-bang-ai-postgresql-slack"
tags: [n8n, automation, ai-code-review, github, postgresql, slack, no-code, ai-summarization]
keywords: [tự động hóa đánh giá PR GitHub, AI review code, log kết quả PostgreSQL, Slack notification, n8n workflow, tự động hóa devops]
---

# 🚀 **Tự Động Hóa Đánh Giá PR GitHub Bằng AI: Giúp Dev Team Tiết Kiệm 100h/Năm**

### **Nỗi Đau Của Dev Team**
Hàng ngày, các sếp và dev team phải dành **từ 2-5 tiếng** để review PR thủ công, kiểm tra:
✅ **Chất lượng mã** (viết code theo best practice)
✅ **An toàn** (tránh lỗ hổng bảo mật)
✅ **Hiệu suất** (optimize code, tránh bottleneck)
✅ **Tương thích** (check merge conflict, dependency)

Kết quả? **Lỗi tràn vào production**, **codebase trở nên rối loạn**, và **tốc độ phát triển chậm lại**. Với **AI Code Review**, các sếp có thể **tự động hóa 90% công việc review**, giảm thiểu lỗi và cải thiện chất lượng code **một cách liên tục**.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo **tính bảo mật và hiệu suất cao**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100+ giờ/năm** cho dev team (không cần review thủ công).
- **Giảm thiểu lỗi production** nhờ AI phát hiện vấn đề sớm.
- **Cải thiện chất lượng code** theo best practice, an toàn và hiệu suất.
- **Log kết quả vào PostgreSQL** để theo dõi lịch sử review.
- **Thông báo tự động trên Slack** khi có PR cần chú ý.
- **Hoạt động 24/7** mà không cần can thiệp thủ công.
:::

---

## 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản GitHub** (và **Personal Access Token** với quyền `repo`).
✔ **API Key của OpenAI/Claude** (để AI phân tích code).
✔ **Cổng webhook GitHub** (để n8n nhận được sự kiện PR mới).
✔ **PostgreSQL Database** (đã tạo bảng `code_reviews`).
✔ **Webhook Slack** (nếu muốn nhận thông báo tự động).
✔ **n8n Self-hosted** (để chạy workflow 24/7).

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Cách 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/13652](https://n8n.io/workflows/13652) (chọn **Export as JSON**).
2. Mở **n8n Editor** → Nhấn **Import** → Chọn file JSON vừa tải.
3. Chọn **Create new workflow** và nhấn **Import**.

#### **Cách 2: Copy/Paste JSON**
1. Mở **n8n Editor** → Nhấn **Create new workflow**.
2. Chọn **Import** → Chọn **Paste JSON** và dán nội dung từ file JSON.
3. Nhấn **Import**.

---
### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

#### **🔹 Node 1: GitHub Webhook - PR Events**
- **Credentials**: Chọn `githubApi` (đã cấu hình trước).
- **Repository**: Chọn repo cần review.
- **Events**: Chọn `pull_request` (để nhận tất cả sự kiện PR mới).
- **Webhook URL**: Điền URL webhook của n8n (có thể lấy từ **Settings → Webhooks** trong n8n).

#### **🔹 Node 2 & 3: Fetch Changed Files & Merge PR Details**
- **GitHub API Request**: Sử dụng cùng `githubApi` credentials.
- **Query**: Đảm bảo lấy được `pull_request` và `files` (diff code).

#### **🔹 Node 4 & 5: Extract Code Diffs & Score Review**
- **Code Node (Extract Code Diffs)**:
  - Sử dụng **JavaScript/TypeScript** để trích xuất diff code từ PR.
  - Ví dụ:
    ```javascript
    return {
      diffs: item.json.files.map(file => ({
        filename: file.filename,
        diff: file.patch
      }))
    };
    ```
- **Code Node (Score Review & Categorize Issues)**:
  - Gọi API **OpenAI/Claude** để phân tích code.
  - Ví dụ:
    ```javascript
    const response = await fetch("https://api.openai.com/v1/chat/completions", {
      method: "POST",
      headers: { "Authorization": `Bearer ${$input.all().openaiApiKey}` },
      body: JSON.stringify({
        messages: [{ role: "user", content: `Analyze this code diff:\n${$input.all().diffs}` }],
        model: "gpt-4"
      })
    });
    return await response.json();
    ```

#### **🔹 Node 6: Route by Review Severity**
- **Switch Node**: Chia PR thành **3 mức độ**:
  - **Critical** (lỗi nghiêm trọng → cần fix ngay).
  - **High** (lỗi ảnh hưởng lớn → review lại).
  - **Low** (lỗi nhỏ → có thể chấp nhận).

#### **🔹 Node 7: Post Review to GitHub PR**
- **HTTP Request**: Gửi comment review về PR.
- **Headers**: Đảm bảo có `Authorization: token <GITHUB_TOKEN>`.
- **Body**: Nội dung comment từ AI (đã được xử lý ở Node 5).

#### **🔹 Node 8: Store Review Results in PostgreSQL**
- **Credentials**: Chọn `postgres` (đã cấu hình trước).
- **Query**: Thêm dữ liệu vào bảng `code_reviews`:
  ```sql
  INSERT INTO code_reviews (pr_id, review_score, issues_found, review_time)
  VALUES ('{{$json.nodeData.prId}}', '{{$json.nodeData.score}}', '{{$json.nodeData.issues}}', NOW());
  ```

#### **🔹 Node 9: Send Summary to Slack**
- **HTTP Request**: Gửi thông báo Slack với nội dung:
  ```json
  {
    "text": `🚨 PR #{{$json.nodeData.prNumber}} cần review!\nScore: {{$json.nodeData.score}}\nIssues: {{$json.nodeData.issues}}`,
    "blocks": [...]
  }
  ```
- **URL Webhook**: Điền từ **Slack App → Incoming Webhooks**.

#### **🔹 Node 10: Log Review Completion**
- **Code Node**: Ghi log thời gian hoàn thành review (có thể log vào Slack hoặc PostgreSQL).

---
### **3. Kích Hoạt ⚡️**
1. **Test Run** với một PR mẫu:
   - Tạo PR test trên GitHub → AI sẽ tự động review và gửi comment.
   - Kiểm tra **PostgreSQL** và **Slack** để xác nhận dữ liệu.
2. **Bật Active Workflow**:
   - Nhấn **Active** trên n8n Editor.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với GitHub Actions**:
   - Sử dụng **GitHub Actions** để tự động trigger workflow khi PR được mở.
2. **Lưu Log Chi Tiết**:
   - Thêm **bảng `review_details`** trong PostgreSQL để lưu chi tiết từng issue.
3. **Tự Động Fix Lỗi**:
   - Nếu AI phát hiện lỗi **Critical**, có thể tự động **merge PR** với sửa đổi (nếu cấu hình cho phép).
4. **Báo Cáo Hàng Tuần**:
   - Sử dụng **n8n + Google Sheets** để tự động tạo báo cáo thống kê lỗi trong tuần.
5. **Cá Nhân Hóa Review**:
   - Thêm **AI Chatbot** (n8n + OpenAI) để dev team chat với AI để giải thích lý do review.

---
## 📌 **Kết Luận**
Workflow này **giúp dev team tự động hóa 90% công việc review PR**, giảm thiểu lỗi và cải thiện chất lượng code **một cách liên tục**. Các sếp chỉ cần **cấu hình 1 lần**, sau đó **AI sẽ làm tất cả**!

**Hãy áp dụng ngay và tiết kiệm 100h/năm cho team của mình!** 🚀

---
### **🔗 Tài Liệu Tham Khảo**
- [Workflow gốc trên n8n.io](https://n8n.io/workflows/13652)
- [Docusaurus Callouts](https://docusaurus.io/docs/markdown-features/callouts)
- [Cấu hình PostgreSQL cho n8n](https://docs.n8n.io/integrations/builtins/nodes/n8n-nodes-base.postgres/)