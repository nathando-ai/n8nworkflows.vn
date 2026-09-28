---
title: "🤖 **Tự Động Chỉnh Sửa Bài Blog Markdown với AI Gemini + Groq + Commit Auto GitHub**"
description: "Workflow tự động hóa hoàn toàn không cần code để phân tích, chỉnh sửa và commit bài blog Markdown lên GitHub với AI Gemini (Google) và Groq (fallback), tiết kiệm thời gian và nâng cao chất lượng nội dung."
slug: "tieu-dong-hoa-chinh-sua-blog-markdown-voi-ai-github"
tags: [n8n, automation, ai, github, markdown, no-code, ai-chatbot, gemini, groq]
keywords: [n8n workflow markdown, tự động hóa blog, ai chỉnh sửa bài viết, gemini groq github, tự động commit git]
---

# 🚀 **Tự Động Chỉnh Sửa Bài Blog Markdown với AI Gemini + Groq + Commit Auto GitHub**

### **Giải pháp AI tự động hóa chỉnh sửa bài blog Markdown**
Các sếp đã từng phải mất **giờ đồng hồ** để đọc lại bài blog, sửa lỗi ngữ pháp, cải thiện logic, và commit lên GitHub? Hay thậm chí phải **tìm kiếm và sửa lỗi** trong nội dung dài hàng trang? **Workflow này sẽ tự động hóa toàn bộ quá trình** với AI Gemini (Google) và Groq (fallback) để phân tích, sửa lỗi, và commit tự động lên GitHub.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: AI tự động phân tích và sửa lỗi trong bài blog chỉ trong **vài giây**.
- **Chất lượng nội dung cao**: Gemini và Groq cải thiện **tôn ngữ, logic, và ngữ pháp** theo tiêu chuẩn chuyên nghiệp.
- **Commit tự động**: Bài blog được sửa và commit lên GitHub **không cần can thiệp thủ công**.
- **Báo cáo chi tiết**: Tạo ra **báo cáo QA** (Quality Assurance) để theo dõi lỗi và tiến trình sửa chữa.
- **Hỗ trợ fallback**: Nếu Gemini không hoạt động, Groq sẽ tự động thay thế.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản GitHub** với quyền **write** vào repository chứa bài blog Markdown.
2. **API Key Google Gemini** (từ [Google AI Studio](https://aistudio.google/)).
3. **API Key Groq** (từ [Groq API](https://console.groq.com/)).
4. **File Markdown** cần chỉnh sửa được đặt trong repository GitHub.
5. **n8n Self-hosted** (không dùng phiên bản cloud để đảm bảo tính riêng tư và ổn định).
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Bước 1**: Tải workflow từ [n8n.io/workflows/14207](https://n8n.io/workflows/14207) (chọn **Export as JSON**).
- **Bước 2**: Mở **n8n Editor** và chọn **Import** → Dán JSON vào.
- **Bước 3**: Chọn **Active** để kích hoạt workflow.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **22 node** với các bước chính sau:

##### **A. Cấu hình GitHub**
- **Node "Github Config" (n8n-nodes-base.set)**:
  - Điền **repoOwner**, **repoName**, và **filePath** của bài blog Markdown cần sửa.
  - Ví dụ:
    ```json
    {
      "repoOwner": "ten-taikhoan-github",
      "repoName": "ten-repo",
      "filePath": "docs/blog/ten-bai-blog.md"
    }
    ```
- **Node "Fetch Blog Post from GitHub"**:
  - Chọn **credentials** GitHub OAuth2 đã cấu hình trước đó.

##### **B. Cấu hình AI (Gemini + Groq)**
- **Node "QA Agent LLM" và "Editor Agent LLM"**:
  - Điền **API Key Google Gemini** vào **Authentication** (nếu không, Groq sẽ tự động fallback).
- **Node "Fallback Chat Model"**:
  - Điền **API Key Groq** vào **Authentication** (sử dụng model `openai/gpt-oss-20b`).

##### **C. Cấu hình Prompt (Tùy chọn)**
- **Node "QA Agent - Analyze Content"** và **"Editor Agent - Generate Edit Ops"**:
  - Các sếp có thể **cập nhật prompt** trong **Agent Configuration** để phù hợp với **tiêu chuẩn brand** của mình.
  - Ví dụ:
    ```json
    {
      "role": "You are a professional content editor. Follow these rules: [Điền quy tắc chỉnh sửa của công ty]",
      "system": "Analyze the markdown content for grammar, clarity, and tone issues."
    }
    ```

##### **D. Kích hoạt & Test**
- **Bước 1**: Chọn **Execute workflow** (node `manualTrigger`).
- **Bước 2**: Chọn **file Markdown** cần sửa từ GitHub.
- **Bước 3**: Kiểm tra **báo cáo QA** và **bài blog đã sửa** trong repository.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tự động chạy định kỳ**:
   - Sử dụng **n8n Cron Trigger** để chạy workflow hàng ngày/ngày nào đó (ví dụ: `0 0 * * *` để chạy lúc 00:00 hàng ngày).
2. **Gửi báo cáo qua Slack/Email**:
   - Thêm **node Slack/Email** sau khi tạo **QA Report** để thông báo kết quả.
3. **Lưu log sửa đổi**:
   - Sử dụng **node StickyNote** để ghi lại **lịch sử sửa đổi** của từng bài blog.
4. **Thay đổi model AI**:
   - Nếu muốn sử dụng **OpenAI/GPT-4**, thay thế **Gemini/Groq** bằng **n8n-nodes-base.llmOpenAI**.

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** của các sếp khỏi công việc **sửa chữa bài blog thủ công**, đồng thời **nâng cao chất lượng nội dung** với AI Gemini và Groq. **Chỉ cần import, cấu hình và kích hoạt** là xong!

👉 **Hãy thử ngay và chia sẻ kết quả với chúng tôi!** 🚀
**#n8n #AIAutomation #GitHubAutoCommit #MarkdownQA**