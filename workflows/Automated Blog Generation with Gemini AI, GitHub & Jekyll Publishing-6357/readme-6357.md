---
title: "🚀 Tự Động Hóa Viết Blog Tự Động Với Gemini AI, GitHub & Jekyll – Không Cần Code!"
description: "Workflow tự động hóa viết blog chuyên nghiệp từ chủ đề đến công bố trên trang web Jekyll/GitHub Pages chỉ trong vài phút. Giúp các sếp tiết kiệm thời gian viết nội dung, duy trì blog liên tục và tối ưu SEO."
slug: "tieu-dong-hoa-viet-blog-voi-gemini-ai-github-jekyll"
tags: [n8n, automation, content-creation, ai-gemini, github-actions, jekyll, seo, no-code]
keywords: [tự động hóa viết blog, gemini ai viết bài, n8n workflow blog, jekyll tự động hóa, content marketing tự động, viết bài blog không code]
---

# 🚀 **Tự Động Hóa Viết Blog Chuyên Nghiệp Với Gemini AI, GitHub & Jekyll**

### **Giải pháp cho các sếp muốn:**
- **Tiết kiệm hàng giờ viết blog** mỗi tuần.
- **Duy trì blog liên tục** mà không lo quên deadline.
- **Tối ưu SEO** với nội dung được AI nghiên cứu từ nguồn tin tức mới nhất.
- **Công bố blog tự động** lên trang web Jekyll/GitHub Pages chỉ với một nhấp chuột.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản miễn phí.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: AI viết blog trong vài phút thay vì mất cả ngày.
✅ **Nội dung chuyên nghiệp**: Gemini AI nghiên cứu từ Wikipedia, Tavily (tìm kiếm web) và tạo bài viết có cấu trúc SEO.
✅ **Công bố tự động**: Blog được commit lên GitHub và tự động build lên trang web Jekyll/GitHub Pages.
✅ **Quản lý chủ đề**: Dùng Google Sheets để theo dõi chủ đề đã viết và chưa viết.
✅ **Hoạt động 24/7**: Workflow chạy tự động theo lịch trình (ví dụ: mỗi sáng 7h).
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
- **Tài khoản n8n** (cài đặt trên máy chủ riêng hoặc dùng phiên bản cloud).
- **API Key Tavily** (dùng để tìm kiếm web):
  👉 [Đăng ký Tavily](https://www.tavily.com/) (miễn phí 5000 credit/tháng).
- **Google Sheets** (để quản lý danh sách chủ đề):
  - Tạo một sheet với cột `Topic` và `Status` (đang chờ/đã hoàn thành).
- **API Key Google Gemini** (hoặc LLM khác):
  👉 [Đăng ký Google AI Studio](https://aistudio.google/) (miễn phí 300$ credit/tháng).
- **Tài khoản GitHub** với:
  - **Personal Access Token** (cho phép commit tự động).
  - **Repository Jekyll** (cấu hình GitHub Pages).
- **Repository Jekyll** (để host blog):
  - Tạo repo `<username>.github.io` và cấu hình Jekyll.

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [workflow gốc](https://n8n.io/workflows/6357) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/6357) và paste vào **Import Workflow** trong n8n.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
#### **A. Cấu hình Node "Schedule Trigger" (Đặt lịch chạy)**
- Mở node **Schedule Trigger** → Chọn **Cron expression** phù hợp (ví dụ: `0 7 * * *` để chạy mỗi sáng 7h).
- **Lưu ý**: Nếu muốn chạy thủ công, có thể bỏ qua node này và kích hoạt từ **Webhook** hoặc **Manual Trigger**.

#### **B. Cấu hình Node "Get Topic from Google Sheet"**
- **Credentials**: Chọn `googleSheetsOAuth2Api` (đã cấu hình trước).
- **Sheet Name**: Điền tên sheet chứa danh sách chủ đề (ví dụ: `Blog Topics`).
- **Range**: Điền `Sheet1!A2:B` (giả sử cột A là `Topic`, cột B là `Status`).
- **Filter**: Chỉ lấy dòng có `Status = "Chưa viết"` (sử dụng `=ARRAYFORMULA(IF(B2:B="Chưa viết", A2:A, ""))`).

#### **C. Cấu hình Node "Google Gemini Chat Model"**
- **Credentials**: Chọn `googlePalmApi` (đã điền API Key).
- **Prompt**: Workflow đã cấu hình sẵn, nhưng các sếp có thể tùy chỉnh để phù hợp với phong cách viết của mình.
  **Ví dụ prompt mặc định**:
  ```
  Tôi là một nhà viết blog chuyên nghiệp. Viết một bài blog chi tiết về chủ đề "{topic}" với cấu trúc:
  1. Tiêu đề hấp dẫn (SEO-friendly).
  2. Mở đầu (hook).
  3. 3-5 phần nội dung chi tiết (sử dụng thông tin từ Tavily).
  4. Kết luận + CTA (Call to Action).
  Đảm bảo bài viết có từ 800-1200 từ và được format Markdown.
  ```

#### **D. Cấu hình Node "Commit Blog Post to GitHub"**
- **Credentials**: Chọn `githubOAuth2Api` (đã cấu hình trước).
- **Repository**: Điền đường dẫn repo Jekyll (ví dụ: `username/repo-name`).
- **Branch**: Chọn `main` (hoặc `master`).
- **File Path**: Đặt là `posts/{YYYY}-{MM}-{DD}-{title}.md` (để tự động tạo tên file theo định dạng Jekyll).

#### **E. Cấu hình Node "Mark Topic as Done in Sheet"**
- **Credentials**: Chọn `googleSheetsOAuth2Api`.
- **Range**: Điền `Sheet1!B2:B` (cột `Status`).
- **Value**: Điền `"Đã viết"` để cập nhật trạng thái khi blog đã được commit.

---

### **3. Kích hoạt ⚡️**
1. **Test Run** với một chủ đề mẫu:
   - Chọn node **Get Topic from Google Sheet** → Nhấn **Execute**.
   - Kiểm tra các node sau đó (Tavily, Gemini, GitHub) có hoạt động không.
2. **Bật Active**:
   - Sau khi test thành công, bật **Active** cho workflow.

---

## ✍️ **Mẹo & gợi ý nâng cao**
### **1. Tối ưu SEO cho blog**
- **Sử dụng Tavily để lấy từ khóa**:
  - Thêm node **Code** sau Tavily để trích xuất từ khóa từ kết quả tìm kiếm.
  - Ví dụ:
    ```javascript
    // Trích xuất từ khóa từ URL và tiêu đề
    const keywords = $input.all().map(item => {
      const urls = item.data.links.map(link => link.url);
      const titles = item.data.links.map(link => link.title);
      return [...new Set([...urls, ...titles])];
    });
    $output.set("keywords", keywords);
    ```
- **Thêm meta tags** trong file Markdown:
  ```markdown
  ---
  layout: post
  title: "Tên Blog SEO-friendly"
  date: {{ date }}
  tags: [tag1, tag2, tag3]
  keywords: keyword1, keyword2
  ---
  ```

### **2. Gửi thông báo khi blog được viết**
- **Thêm node Slack/Telegram**:
  - Sau node **Commit Blog Post to GitHub**, thêm node **Slack Webhook** hoặc **Telegram Bot** để thông báo:
    ```
    📢 Blog mới được viết: "{topic}" - Link: https://username.github.io/{post-url}
    ```

### **3. Lưu log hoạt động**
- **Thêm node StickyNote**:
  - Sau node **Commit Blog Post**, thêm node **StickyNote** để ghi log:
    ```
    - Chủ đề: {topic}
    - Ngày viết: {date}
    - Trạng thái: Thành công
    ```

### **4. Cập nhật Jekyll tự động**
- **Sử dụng GitHub Actions**:
  - Tạo file `.github/workflows/deploy.yml` trong repo Jekyll:
    ```yaml
    name: Deploy Jekyll
    on:
      push:
        branches: [ main ]
    jobs:
      deploy:
        runs-on: ubuntu-latest
        steps:
          - uses: actions/checkout@v2
          - uses: actions/jekyll-build-pages@v1
            with:
              token: ${{ secrets.GITHUB_TOKEN }}
    ```
  - Workflow sẽ tự động build và deploy khi có commit mới.

---

## 📌 **Kết luận**
Workflow này là **giải pháp hoàn chỉnh** để các sếp tự động hóa viết blog, từ nghiên cứu chủ đề đến công bố trên trang web. **Không cần code**, chỉ cần cấu hình các API và credentials là xong!

👉 **Bắt đầu ngay**:
1. Import workflow.
2. Cấu hình các credentials.
3. Chạy thử với một chủ đề.
4. Đặt lịch tự động và **blog của bạn sẽ tự viết mỗi sáng!**

**Cần hỗ trợ?** Để lại comment bên dưới hoặc liên hệ qua [n8n Community](https://community.n8n.io/). 🚀