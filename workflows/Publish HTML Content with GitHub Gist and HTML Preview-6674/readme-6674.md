---
title: "🚀 Tự Động Tạo Gist GitHub & Preview HTML Cho Báo Cáo - Không Cần Code"
description: "Giải pháp tự động hóa hoàn toàn miễn phí để tạo Gist GitHub từ nội dung HTML và chia sẻ liên kết preview trực tiếp. Phù hợp cho các tổ chức phi lợi nhuận, nhà phát triển và doanh nghiệp cần lưu trữ báo cáo HTML dễ dàng."
slug: "tu-dong-tao-gist-github-html-preview"
tags: [n8n, automation, github, file-management, no-code]
keywords: [n8n workflow github, tự động hóa tạo gist, preview html, lưu trữ báo cáo, tự động hóa không code]
---

# 🚀 **Tự Động Tạo Gist GitHub & Preview HTML Cho Báo Cáo - Không Cần Code**

### **Giải pháp cho những ai đang mệt mỏi với việc copy-paste HTML vào GitHub thủ công**
Các sếp có biết rằng việc chia sẻ báo cáo HTML hoặc tài liệu kỹ thuật với đồng nghiệp, khách hàng hoặc cộng đồng thường phải trải qua quá trình **copy-paste thủ công** vào GitHub Gist? Điều này không chỉ tốn thời gian mà còn dễ gây lỗi, khó theo dõi và không thể tự động hóa.

**Workflow này giúp:**
- **Tự động tạo Gist GitHub** từ nội dung HTML đầu vào.
- **Trả về liên kết preview trực tiếp** để các sếp chia sẻ ngay mà không cần cài đặt gì.
- **Hoạt động 24/7** trên nền tảng tự động hóa n8n (Self-hosted) để đảm bảo tính liên tục.

---
### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần copy-paste thủ công, giảm thiểu lỗi.
- **Chia sẻ nhanh chóng**: Liên kết preview HTML được tạo tự động, chia sẻ một click.
- **Lưu trữ an toàn**: Tất cả nội dung được lưu trên GitHub với tính bảo mật cao.
- **Hoạt động liên tục**: Duy trì hoạt động 24/7 trên VPS tự động hóa.
- **Miễn phí & mở nguồn**: Phù hợp cho tổ chức phi lợi nhuận như Open Paws hoặc các dự án cộng đồng.
:::

---
### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản GitHub** và **GitHub Personal Access Token** (có quyền `gist`).
   - Hướng dẫn tạo Token: [GitHub Docs - Creating a personal access token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens).
2. **n8n Self-hosted** (không thể chạy trên n8n.cloud vì yêu cầu API key GitHub).
3. **Nội dung HTML đầu vào** (có thể là kết quả từ một workflow khác hoặc file HTML đã chuẩn bị).
:::

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Bước 1:** Tải workflow từ [n8n.io/workflows/6674](https://n8n.io/workflows/6674) hoặc copy JSON từ trang này.
- **Bước 2:** Mở **n8n Editor** và chọn **"Import"** → Dán JSON hoặc tải file `.json`.
- **Bước 3:** Workflow sẽ hiển thị 3 node chính:
  - `When Executed by Another Workflow` (Trigger)
  - `Set URL` (Xử lý URL đầu ra)
  - `Create Gist` (Tạo Gist GitHub)

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **A. Cấu hình Node `Create Gist`**
- **Thêm API Key GitHub**:
  1. Vào node `Create Gist`, chọn tab **"Credentials"**.
  2. Chọn **"httpHeaderAuth"** và điền:
     - **Name**: `GitHub Token` (hoặc tên tùy ý).
     - **Token**: Dán **GitHub Personal Access Token** (không chia sẻ cho ai!).
  3. Trong tab **"Main"**, cấu hình:
     - **Method**: `POST`
     - **URL**: `https://api.github.com/gists`
     - **Headers**:
       - `Authorization`: `token {{{ $json["token"] }}}` (điền token từ credentials).
       - `Accept`: `application/vnd.github.v3+json`
     - **Body**:
       - Chọn **"Raw"**, điền JSON như sau (điền `{{{ $json["html"] }}}` vào trường `description` và `{{{ $json["html"] }}}` vào trường `files`):
         ```json
         {
           "description": "{{{ $json["html"] }}}",
           "public": true,
           "files": {
             "report.html": {
               "content": "{{{ $json["html"] }}}"
             }
           }
         }
         ```
     - **Note**: Nếu không truyền HTML từ workflow khác, các sếp có thể **set default** trong node `Set URL` (xem phần sau).

##### **B. Cấu hình Node `Set URL`**
- Node này **xử lý URL đầu ra** của Gist được tạo.
- Trong tab **"Main"**, cấu hình:
  - **Set**: `{{$json["html"]}}` → `{{$json["url"]}}` (đổi tên biến `html` thành `url` để lưu URL Gist).
  - **Example**: Nếu đầu vào là `{"html": "<h1>Hello</h1>"}`, sau khi chạy, output sẽ là `{"url": "https://gist.github.com/username/123456789"}`.

##### **C. Cấu hình Node `When Executed by Another Workflow`**
- Node này **khởi động workflow** khi nhận được input từ một workflow khác.
- Các sếp có thể **bỏ qua node này** nếu muốn chạy workflow **manual** (bấm nút "Run Workflow" trong n8n Editor).
- **Lưu ý**: Nếu muốn tự động hóa, các sếp cần **kết nối với workflow khác** (ví dụ: sau khi tạo HTML từ một report).

---
#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Điền **dữ liệu mẫu** vào input (ví dụ: `{"html": "<h1>Test HTML</h1>"}`).
   - Chạy workflow và kiểm tra output:
     - Nếu thành công, sẽ có URL Gist như: `https://gist.github.com/username/report.html`.
     - Mở URL trên trình duyệt để preview HTML.
2. **Bật Active**:
   - Sau khi test thành công, **bật switch "Active"** ở góc trên bên phải.

---
### ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁCH SỬ DỤNG THỰC TẾ]
1. **Kết hợp với Slack/Telegram**:
   - Sau khi tạo Gist, **gửi thông báo** về Slack/Telegram với liên kết preview bằng node `slack` hoặc `telegramBot`.
   - Ví dụ: `Tạo thành công báo cáo HTML! Preview: [{{$json["url"]}}]({{$json["url"]}})`.
2. **Lưu log hoạt động**:
   - Sử dụng node `set` hoặc `googleSheets` để **lưu lịch sử** các Gist được tạo (ngày tạo, tên file, URL).
3. **Tự động tạo từ report**:
   - Nếu các sếp có **workflow tạo report HTML** (ví dụ: từ Google Sheets, Notion, hoặc LLM), hãy **kết nối nó với workflow này** để tự động hóa toàn bộ quy trình.
4. **Chia sẻ công khai**:
   - Đặt `public: true` trong JSON của node `Create Gist` để Gist **không cần xác thực** khi chia sẻ.
:::

---
### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp cần **tự động hóa việc chia sẻ báo cáo HTML** một cách nhanh chóng và không cần code. Với chỉ **3 node đơn giản**, các sếp có thể:
✅ **Tạo Gist GitHub tự động** từ HTML.
✅ **Chia sẻ preview ngay** mà không cần cài đặt gì.
✅ **Hoạt động 24/7** trên VPS tự động hóa.

**Hãy thử ngay!** Nếu các sếp đang quản lý nhiều báo cáo HTML hoặc tài liệu kỹ thuật, **tự động hóa này sẽ tiết kiệm thời gian và giảm thiểu lỗi**.

---
:::note[CHÚ Ý]
- **GitHub Personal Access Token** phải có **quyền `gist`** và **không chia sẻ** với ai.
- Workflow **không hoạt động trên n8n.cloud** vì yêu cầu API key GitHub.
- Để **tối ưu hiệu suất**, các sếp nên cài **n8n trên VPS** (Self-hosted) để tránh giới hạn của phiên bản cloud.
:::