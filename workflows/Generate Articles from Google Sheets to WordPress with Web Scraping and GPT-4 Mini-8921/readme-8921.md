---
title: "🚀 Tự Động Hóa Tạo Bài Viết SEO Từ Google Sheets Sang WordPress Với Web Scraping & GPT-4 Mini (N8n)"
description: "Workflow tự động hóa hoàn toàn không code giúp các sếp lấy dữ liệu từ Google Sheets, web scraping nội dung, sử dụng GPT-4 Mini tạo bài viết SEO hoàn chỉnh và đăng tải lên WordPress chỉ trong vài giây. Giảm thời gian viết bài từ 2-3 tiếng xuống 5 phút/bài!"
slug: "tu-dong-hoa-tao-bai-viet-seo-tu-google-sheets-sang-wordpress"
tags: [n8n, automation, content-creation, ai-gpt, wordpress, google-sheets, seo, no-code]
keywords: [tự động hóa viết bài, n8n workflow, tạo bài viết seo tự động, gpt-4 mini, web scraping, google sheets wordpress, tự động hóa content marketing]
---

# 🚀 **Tự Động Hóa Tạo Bài Viết SEO Từ Google Sheets Sang WordPress Với Web Scraping & GPT-4 Mini**

## **💡 Giải Pháp Cho Các Sếp Bị "Chết" Vì Viết Bài**
Hãy tưởng tượng: Bạn chỉ cần **nhấp chuột**, hệ thống tự động:
✅ **Lấy dữ liệu** từ Google Sheets (đã chuẩn bị sẵn chủ đề, URL nguồn, tiêu đề).
✅ **Scraping nội dung** từ các trang web (báo, blog, forum) mà không cần viết code.
✅ **Tạo bài viết SEO hoàn chỉnh** với GPT-4 Mini (tóm tắt, mở rộng, tối ưu từ khóa).
✅ **Đăng tải tự động** lên WordPress với format chuẩn, tiêu đề SEO, meta description.
✅ **Cập nhật trạng thái** trên Google Sheets (đã xử lý, thành công/thất bại).

**Kết quả?** Từ **2-3 tiếng viết 1 bài** (thủ công) → **5 phút/bài** (tự động). Thời gian dành cho chiến lược content, chứ không phải "chết" với việc viết.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**3 Lợi Ích Cốt Lõi**]
- **Tiết kiệm thời gian**: Viết hàng chục bài/ngày mà không mệt mỏi.
- **Chất lượng cao**: Bài viết được tối ưu SEO, logic, và tránh plagiarism nhờ GPT-4 Mini.
- **Hoạt động 24/7**: Workflow chạy tự động, không cần can thiệp thủ công.
- **Dễ dàng mở rộng**: Thêm chủ đề, nguồn scrap mới chỉ với vài click.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[**Chuẩn Bị Trước Khi "Lên Đồ"**]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản Google Sheets**:
   - Một bảng Google Sheets với **cột chuẩn** (ví dụ: `URL_Nguon`, `TieuDe`, `NoiDung`, `TrangThai`).
   - **Trạng thái ban đầu**: Cột `TrangThai` phải có giá trị `"New"` cho các bài cần xử lý.
   - **Mẫu bảng**:
     | URL_Nguon       | TieuDe               | NoiDung          | TrangThai |
     |-----------------|----------------------|------------------|-----------|
     | `https://vnexpress.net/` | "Cách tự động hóa content" | (trống) | New       |

2. **API Key OpenAI**:
   - Đăng ký tại [OpenAI](https://platform.openai.com/) và lấy **API Key** cho GPT-4 Mini.
   - **Lưu ý**: GPT-4 Mini có giới hạn token, các sếp nên kiểm tra chi phí.

3. **Tài Khoản WordPress**:
   - Một trang WordPress với quyền **API Full Access** (cài plugin **WP REST API**).
   - **Lưu trữ media**: Đảm bảo có thể upload hình ảnh (nếu cần).

4. **VPS Self-Hosted (Khuyến Nghị)**:
   - Workflow này **không chạy được** trên n8n.cloud (do giới hạn node OpenAI).
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).

---
## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Từ File JSON**
1. Tải workflow từ [n8n.io/workflows/8921](https://n8n.io/workflows/8921) (chọn **Export JSON**).
2. Trên n8n Editor (trang web hoặc VPS), nhấn **Import** → Chọn file JSON vừa tải.
3. **Kiểm tra cấu trúc**: Workflow sẽ hiển thị 12 node như mô tả.

#### **Phương pháp 2: Copy/Paste JSON**
1. Sao chép toàn bộ JSON từ [n8n.io/workflows/8921](https://n8n.io/workflows/8921) (chọn **Export JSON** → Copy).
2. Trên n8n Editor, nhấn **Import** → Chọn **Paste JSON**.
3. **Lưu ý**: Nếu JSON quá dài, có thể gặp lỗi. Thử phương pháp 1 thay vì.

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này **không chạy được** nếu không cấu hình chính xác các node sau:

#### **🔹 Node "Get New Articles" (Google Sheets)**
- **Credentials**: Chọn `googleSheetsOAuth2Api` (đã cấu hình trước).
- **Sheet Name**: Điền tên bảng Google Sheets của bạn.
- **Range**: Điền `Sheet1!A2:D` (giả sử dữ liệu từ hàng 2).
- **Filter**: Thêm điều kiện:
  ```json
  {
    "TrangThai": "New"
  }
  ```
  (Lọc chỉ các bài có trạng thái "New").

#### **🔹 Node "Fetch HTML" (HTTP Request)**
- **Method**: `GET`.
- **URL**: Điền vào `{{$json["URL_Nguon"]}}` (động).
- **Headers**:
  ```json
  {
    "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36"
  }
  ```
  (Tránh bị chặn bởi server).

#### **🔹 Node "Article Creator" & "Article Summarizer" (OpenAI)**
- **Credentials**: Chọn `openAiApi`.
- **Model**: Chọn `gpt-4-1106-preview` (GPT-4 Mini).
- **Prompt**:
  - **Article Creator**:
    ```json
    "Tóm tắt nội dung từ trang web {{$json["URL_Nguon"]}} và viết bài viết SEO dài {{$json["DoDai"] || 1000}} từ, bao gồm:
    1. Tiêu đề SEO: {{$json["TieuDe"]}}
    2. Mở đầu hấp dẫn
    3. Nội dung chi tiết (sử dụng thông tin từ trang web)
    4. Kết luận + CTA (Call To Action)
    5. Từ khóa liên quan: {{$json["TuKhoa"] || ""}}
    Đảm bảo bài viết không plagiarism và có structure rõ ràng."
    ```
  - **Article Summarizer**:
    ```json
    "Tóm tắt nội dung từ bài viết sau thành 300-500 từ, giữ lại ý chính và tối ưu SEO:
    {{$json["NoiDung"]}}
    Đảm bảo không có plagiarism và có tiêu đề: {{$json["TieuDe"]}}."
    ```

#### **🔹 Node "Create a Draft" (WordPress)**
- **Credentials**: Chọn `wordpressApi`.
- **Action**: `create`.
- **Payload**:
  ```json
  {
    "title": "{{$json["TieuDe"]}}",
    "content": "{{$json["NoiDung"]}}",
    "status": "draft",
    "excerpt": "{{$json["MoTa"] || ""}}",
    "categories": [1] // ID danh mục WordPress
  }
  ```
  (Thay `1` bằng ID danh mục của bạn).

#### **🔹 Node "Update Processing" & "Update Error" (Google Sheets)**
- **Credentials**: `googleSheetsOAuth2Api`.
- **Range**: `Sheet1!D2:D` (cập nhật cột `TrangThai`).
- **Value**:
  - **Thành công**: `"Processing"` → `"Done"`.
  - **Thất bại**: `"Processing"` → `"Error"`.

#### **🔹 Node "Format Article" (Code)**
- **Code JavaScript**:
  ```javascript
  // Chỉ định format bài viết cho WordPress
  return {
    json: {
      NoiDung: `$json["NoiDung"].replace(/<[^>]*>/g, '') // Loại bỏ tag HTML
        .replace(/\s+/g, ' ') // Loại bỏ khoảng trắng thừa
        .trim() // Cắt bỏ khoảng trắng đầu cuối`,
      TieuDe: `$json["TieuDe"]`,
      MoTa: `$json["MoTa"] || ""`
    }
  };
  ```

---
### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với 1 bài mẫu:
   - Chỉnh `Range` của node `Get New Articles` thành `Sheet1!A2:A3` (chỉ lấy 1 dòng).
   - Chạy workflow và kiểm tra:
     - Bài viết có được tạo trên WordPress không?
     - Trạng thái trên Google Sheets có cập nhật không?
2. **Bật Active**:
   - Sau khi test thành công, nhấn **Active** trên workflow.
   - **Lưu ý**: Workflow sẽ chạy liên tục (do node Webhook).

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**
### **1. Thêm Webhook Cho Tự Động Hóa Liên Tục**
- Node `Webhook` cho phép workflow **chạy tự động** khi có thay đổi trên Google Sheets.
- **Cách kích hoạt**:
  1. Trong Google Sheets, mở **Extensions > Apps Script**.
  2. Dán mã sau (thay `YOUR_WEBHOOK_URL` bằng URL Webhook của bạn):
     ```javascript
     function onEdit(e) {
       const sheet = e.source.getActiveSheet();
       const range = e.range;
       if (sheet.getName() === "Sheet1" && range.getColumn() === 4 && range.getValue() === "New") {
         const url = "YOUR_WEBHOOK_URL";
         fetch(url, {
           method: "POST",
           headers: { "Content-Type": "application/json" },
           body: JSON.stringify({ event: "new_article" })
         });
       }
     }
     ```
  3. **Save** và **Deploy** như một **Web App** (Enable "Execute as me" và "Installable On Edit").

### **2. Lưu Log Lỗi Cho Dễ Dàng Debug**
- Thêm node **Slack/Telegram** để báo lỗi:
  ```json
  {
    "name": "Notify Error",
    "type": "slack",
    "credentials": ["slackApi"],
    "keyParameters": {
      "text": "Lỗi khi xử lý bài viết: {{$json["TieuDe"]}} - Lỗi: {{$json["error"]}}"
    }
  }
  ```

### **3. Tối Ưu Prompt Cho GPT-4 Mini**
- **Ví dụ prompt cải tiến**:
  ```json
  "Bài viết phải:
  1. Có structure: H1, H2, H3, danh sách, bảng biểu.
  2. Sử dụng từ khóa: {{$json["TuKhoa"]}} trong tiêu đề và 3 lần trong nội dung.
  3. Tránh plagiarism: So sánh với trang web nguồn và viết lại 100% mới.
  4. Kết thúc với CTA: 'Bạn có thể áp dụng ngay bằng cách...'"
  ```

### **4. Tự Động Chuyển Sang Bài Đăng (Publish)**
- Thêm node `wordpress` với action `update` để chuyển từ `draft` sang `publish` sau 1 ngày:
  ```json
  {
    "name": "Publish After Delay",
    "type": "delay",
    "keyParameters": {
      "time": "1d"
    }
  }
  ```

---
## **📌 Kết Luận**
Workflow này **giải phóng thời gian** của các sếp để tập trung vào **strategy content** thay vì viết bài thủ công. Với **Google Sheets + Web Scraping + GPT-4 Mini + WordPress**, bạn có thể:
✔ **Tạo hàng trăm bài viết/ngày** mà không mệt mỏi.
✔ **Tối ưu SEO** tự động với từ khóa và structure chuẩn.
✔ **Hoạt động 24/7** mà không cần can thiệp.

**Bước đầu tiên**: Đăng ký VPS, import workflow, và **chạy thử với 1 bài**. Sau đó mở rộng cho toàn bộ content team!

---
### **🔗 Tài Liệu Tham Khảo**
- [Cách cấu hình Google Sheets OAuth2](https://docs.n8n.io/integrations/built-in/nodes/googleSheets/)
- [Prompt Engineering cho GPT-4 Mini](https://platform.openai.com/docs/guides/gpt/chat-completion)
- [Cài đặt WordPress REST API](https://kinsta.com/knowledgebase/wordpress-rest-api/)