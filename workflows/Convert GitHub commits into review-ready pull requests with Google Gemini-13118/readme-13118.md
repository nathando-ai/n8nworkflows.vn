---
title: "🚀 Tự Động Hóa Tạo Pull Request Sẵn Sàng Đánh Giá Từ Commit GitHub Với Google Gemini (N8N)"
description: "Workflow này tự động chuyển đổi các commit từ branch vào PR chuẩn chỉnh với tiêu đề và mô tả được viết bởi AI Google Gemini, giúp devops và team founders tiết kiệm thời gian và giảm thiểu lỗi thủ công. Khắc phục vấn đề PR không chuyên nghiệp, mất thời gian viết mô tả và thiếu tính nhất quán."
slug: "tieu-dong-hoa-tao-pull-request-voi-github-gemini"
tags: [n8n, automation, devops, ai-rag, github, google-gemini]
keywords: [n8n workflow github, tự động hóa pull request, google gemini n8n, devops automation, tạo pr tự động]
---

# 🚀 **Tự Động Hóa Tạo Pull Request Sẵn Sàng Đánh Giá Từ Commit GitHub Với Google Gemini**

### **Giải quyết vấn đề gì?**
Các sếp đã từng phải làm gì sau khi nhận commit từ team?
- **Viết tiêu đề PR dài dòng** để mô tả ý định thay đổi?
- **Tóm tắt commit messages** để tạo mô tả PR chi tiết?
- **Lo lắng PR không chuyên nghiệp** khiến reviewer phải chỉnh sửa nhiều lần?
- **Mất thời gian** vì phải copy-paste commit messages một cách thủ công?

Workflow này **tự động hóa toàn bộ quy trình** bằng AI Google Gemini, giúp tạo PR **chuyên nghiệp, chuẩn chỉnh và sẵn sàng đánh giá** chỉ trong vài giây!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đủ sức mạnh cho workflow AI)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian** – Không cần viết PR thủ công, AI tự động tạo tiêu đề và mô tả.
✅ **PR chuyên nghiệp** – Mô tả rõ ràng, logic và phù hợp với ý định thay đổi.
✅ **Tính nhất quán** – Mọi PR đều được viết theo cùng một tiêu chuẩn AI.
✅ **Hoạt động liên tục** – Không phụ thuộc vào người dev, tự động kích hoạt khi có commit mới.
✅ **Giảm thiểu lỗi** – AI giảm thiểu việc bỏ sót thông tin quan trọng trong commit.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
✔ **Tài khoản GitHub** với quyền:
   - **PR access** (để tạo PR tự động).
   - **Repository access** (để đọc commit và issue).
✔ **API Key Google Gemini** (để sử dụng AI viết PR).
✔ **MCP (Multi-Client Proxy)** được cấu hình và kết nối với repo GitHub.
✔ **Sub-workflow** (nếu sử dụng) đã được tạo và kích hoạt.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/13118](https://n8n.io/workflows/13118) hoặc copy toàn bộ JSON.
- Mở **n8n Editor** → Nhấn **Import** → Dán JSON hoặc chọn file.
- **Kích hoạt workflow** (Active) sau khi import xong.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **15 node**, nhưng các sếp cần chú ý đặc biệt đến các node sau:

##### **A. Cấu hình MCP Trigger (MCP Server Trigger for Github)**
- **Node:** `MCP Server Trigger for Github`
- **Cách làm:**
  1. Đăng ký **MCP** tại [mcp.dev](https://mcp.dev/) và lấy **path UUID** (ví dụ: `a2c1b2dd-32ed-463a-97c0-0f7139719c3c`).
  2. Điền vào `keyParameters.path` trong node này.
  3. Kết nối MCP với repo GitHub của các sếp.

##### **B. Cấu hình GitHub Credentials**
- **Node:** `Fetch GitHub Issues`, `Create Pull Request`, `Repo or Branch Validation`
- **Cách làm:**
  1. Tạo **Personal Access Token (PAT)** trên GitHub với quyền:
     - `repo` (đọc và viết repo).
     - `admin:repo_hook` (nếu cần).
  2. Đăng ký **GitHub OAuth2 API** trong n8n với token này.
  3. Chọn **credentials** trong các node liên quan (`githubOAuth2Api`, `githubApi`).

##### **C. Cấu hình Google Gemini**
- **Node:** `Google Gemini Chat Model`, `LLM PR Writer Model`
- **Cách làm:**
  1. Tạo **API Key Google Gemini** tại [Google Cloud Console](https://console.cloud.google.com/).
  2. Đăng ký **Google Palm API** trong n8n với key này.
  3. Đảm bảo **mô hình Gemini Pro** được chọn (hoặc mô hình khác phù hợp).

##### **D. Cấu hình Sub-workflow (nếu có)**
- **Node:** `create_github_pr` (type: `toolWorkflow`)
- **Cách làm:**
  1. Tạo **sub-workflow** riêng để xử lý logic tạo PR (nếu cần).
  2. Đảm bảo sub-workflow **được kích hoạt (Active)** và có thể gọi được từ workflow chính.

##### **E. Cấu hình Prompt AI (Nếu muốn tùy chỉnh)**
- **Node:** `Generate PR Title & Description` (type: `chainLlm`)
- **Cách làm:**
  - Mặc định, workflow sử dụng **prompt mặc định** của Google Gemini.
  - Nếu muốn **tùy chỉnh**, các sếp có thể chỉnh sửa prompt trong node này để phù hợp với **template PR** của team.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Tạo **issue mới** trên GitHub và kích hoạt MCP để workflow bắt đầu.
   - Kiểm tra **log** trong n8n để đảm bảo workflow chạy đúng.
2. **Bật Active** workflow sau khi test thành công.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram**
   - Sử dụng **node `n8n-nodes-base.slack`** để thông báo khi PR được tạo thành công.
   - Ví dụ: *"PR #123 đã được tạo từ commit `abc123`!"*

2. **Lưu log PR**
   - Sử dụng **node `n8n-nodes-base.stickyNote`** để ghi lại lịch sử PR đã tự động tạo.

3. **Bỏ qua PR draft/WIP**
   - Thêm **node `if`** để kiểm tra tiêu đề PR (ví dụ: nếu tiêu đề chứa `"WIP"` hoặc `"draft"`, workflow sẽ **bỏ qua**).

4. **Tùy chỉnh branch mặc định**
   - Sử dụng **node `set`** để đặt **branch mặc định** (ví dụ: `main`, `develop`) trước khi tạo PR.

5. **Sử dụng AI khác (nếu muốn)**
   - Thay thế **Google Gemini** bằng **Mistral AI**, **Claude** hoặc **OpenAI** bằng cách thay đổi node `lmChatGoogleGemini` thành `lmChatOpenAI` (nếu có node hỗ trợ).

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc viết PR thủ công, đồng thời **tăng chất lượng** của PR nhờ AI Google Gemini. **Chỉ cần import, cấu hình và kích hoạt** là xong!

🚀 **Hành động ngay:**
1. **Import workflow** từ [n8n.io/workflows/13118](https://n8n.io/workflows/13118).
2. **Cấu hình MCP + GitHub + Google Gemini** theo hướng dẫn.
3. **Test và bật Active** để tự động hóa PR!

**Nếu cần hỗ trợ thêm**, các sếp có thể **đặt lịch gọi** với Ahmed Salama (tác giả) để được tư vấn chi tiết:
👉 [Book a n8n build or training call](https://ahmedsalama.dev/n8n-consulting)

---
**Chúc các sếp thành công với tự động hóa PR!** 💻✨