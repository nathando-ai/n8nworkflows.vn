---
title: "🔍 Tự Động Hóa Tìm Kiếm & Phân Tích Cộng Đồng Skool Với AI Claude + Google Docs (N8N)"
description: "Workflow này biến cộng đồng Skool thành cơ sở dữ liệu tìm kiếm được, tự động trích xuất, tổng hợp và phân tích hàng trăm bài đăng cũ bằng AI Claude, trả kết quả chi tiết trong Google Docs và trình bày dưới dạng HTML. Giúp các sếp tiết kiệm hàng giờ tìm kiếm thủ công mỗi ngày."
slug: "tu-dong-hoa-tim-kiem-phan-tich-skool-voi-ai-claude-google-docs"
tags: [n8n, automation, ai-rag, market-research, skool, google-docs, anthropic-claude]
keywords: [n8n workflow skool, tự động hóa tìm kiếm cộng đồng, phân tích AI Claude, google docs tự động, n8n market research]
---

# 🚀 **Tự Động Hóa Tìm Kiếm & Phân Tích Cộng Đồng Skool Với AI Claude + Google Docs**

## **💡 Giải Pháp Cho Nỗi Đau Của Các Sếp**
Hàng ngày, các sếp phải **quét thủ công** hàng trăm bài đăng trong tab "Cộng Đồng" của Skool để tìm câu trả lời cho các câu hỏi phức tạp như:
- *"Ai trong cộng đồng đang làm dự án tương tự với chúng tôi?"*
- *"Có bao nhiêu người đã chia sẻ kinh nghiệm về [chủ đề]?"*
- *"Trend nào đang nổi trong cộng đồng gần đây?"*

**Kết quả?** Tốn **hàng giờ** mỗi tuần, dễ bỏ lỡ thông tin quan trọng, và không thể tổng hợp được cảm xúc chung của cộng đồng. **Workflow này giải quyết tất cả bằng AI + tự động hóa 100% không cần code!**

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 10-20 giờ/tuần** so với tìm kiếm thủ công.
✅ **Trả kết quả chính xác** từ hàng ngàn bài đăng bằng AI Claude (Anthropic).
✅ **Tự động tổng hợp cảm xúc cộng đồng** (trend, ý kiến, kinh nghiệm).
✅ **Lưu báo cáo định kỳ** trong Google Docs để theo dõi lâu dài.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản Skool** (để lấy cookie và Community Slug).
2. **API Key Claude (Anthropic)** – [Đăng ký miễn phí tại đây](https://console.anthropic.com/).
3. **Google Docs OAuth2 Credentials** – [Cài đặt tại đây](https://developers.google.com/docs/api/quickstart/docs).
4. **Folder ID trong Google Drive** – Dùng để lưu báo cáo tự động.
5. **n8n Self-hosted** (không dùng phiên bản cloud để đảm bảo ổn định).
:::

---
## **🚀 Cách Import & Cấu Hình Workflow**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/12180](https://n8n.io/workflows/12180) hoặc copy toàn bộ JSON dưới đây vào **n8n Editor**:
  ```json
  // (File JSON đầy đủ sẽ được cung cấp sau khi import thành công)
  ```
- **Cách import**:
  - Mở **n8n Editor** → Nhấn **Import** → Chọn file JSON hoặc dán JSON vào ô `Paste JSON`.
  - Chọn **Import** để tạo workflow.

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow có **23 node** phức tạp, nhưng chỉ cần chú ý đến **5 node quan trọng** sau:

#### **🔹 Node 1: Form Trigger (Đầu vào)**
- **Cấu hình**:
  - **Path**: `skool-search` (không thay đổi).
  - **Fields**:
    - `query` (Câu hỏi của người dùng, ví dụ: *"Ai đang làm dự án SaaS tại Việt Nam?"*).
    - `depth` (Số trang tìm kiếm, mặc định `5`).

#### **🔹 Node 2: Config (Cấu hình API & Cookie)**
- **Mở node `Config` (type: code)** và điền:
  ```javascript
  // Thay thế các giá trị sau:
  const config = {
    skoolCookie: "YOUR_SKOOL_COOKIE_VALUE", // Copy từ DevTools → Application → Cookies → www.skool.com
    anthropicApiKey: "sk-...", // API Key Claude từ Anthropic
    communitySlug: "your-community-slug", // Slug của cộng đồng Skool (ví dụ: "my-business-network")
    googleDocsCredentials: "YOUR_GOOGLE_DOCS_CREDENTIALS", // Credentials OAuth2 từ n8n
    defaultFolderId: "YOUR_GOOGLE_DRIVE_FOLDER_ID" // Folder ID trong Google Drive
  };
  return config;
  ```
  - **Lấy Cookie Skool**:
    1. Mở trình duyệt → Đăng nhập Skool.
    2. Nhấn **F12** → Tab **Application** → **Cookies** → Copy giá trị của `www.skool.com`.
  - **Lấy Folder ID Google Drive**:
    1. Mở Google Drive → Tạo 1 folder mới.
    2. Nhấn **Chia sẻ** → Sao chép **Link chia sẻ** → Trích xuất `folderId` từ URL (ví dụ: `https://drive.google.com/drive/folders/1AbCdE...`).

#### **🔹 Node 3: Claude - Extract Keywords (Trích xuất từ khóa)**
- **Cấu hình API Request**:
  - **URL**: `https://api.anthropic.com/v1/messages`
  - **Headers**:
    - `anthropic-version`: `2023-06-01`
    - `content-type`: `application/json`
    - `x-api-key`: `YOUR_ANTHROPIC_API_KEY`
  - **Body (JSON)**:
    ```json
    {
      "model": "claude-3-haiku-20240307",
      "max_tokens_to_sample": 1000,
      "messages": [
        {
          "role": "user",
          "content": `Analyze the following user query and suggest 3-5 relevant keywords for searching Skool community:
          Query: ${$node["Form Trigger"].json["query"]}
          Suggest keywords that would help find the most relevant posts.`
        }
      ]
    }
    ```

#### **🔹 Node 4: Fetch All Pages (Lấy tất cả trang kết quả)**
- **Cấu hình HTTP Request**:
  - **URL**: `https://www.skool.com/community/${config.communitySlug}/search?q=${keywords}&page=${page}`
  - **Headers**:
    - `cookie`: `${config.skoolCookie}`
  - **Variables**:
    - `keywords`: Từ khóa từ node `Claude - Extract Keywords`.
    - `page`: Từ `1` đến `depth` (định nghĩa trong Form Trigger).

#### **🔹 Node 5: Create Google Doc (Tạo báo cáo)**
- **Cấu hình Google Docs**:
  - **File ID**: Tự động tạo khi chạy lần đầu.
  - **Folder ID**: Điền `defaultFolderId` từ node `Config`.
  - **Tiêu đề**: `"Báo cáo phân tích cộng đồng Skool - ${new Date().toLocaleDateString()}"`.

---
### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhập vào Form Trigger:
     - `query`: *"Ai đang làm dự án AI tại Việt Nam?"*
     - `depth`: `3`
   - Chạy workflow và kiểm tra:
     - **Kết quả HTML** (trả về trong response).
     - **Google Doc** (được tạo tự động).
2. **Bật Active**:
   - Nhấn **Active** trên tab workflow.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**
### **1. Tối Ưu Hóa AI Claude**
- **Sử dụng Claude Sonnet** cho phân tích sâu (mặc định trong workflow).
- **Đổi sang Claude Haiku** để tiết kiệm token (nhưng kết quả ít chi tiết hơn):
  ```javascript
  // Trong node `Claude - Analyze`, thay đổi model:
  "model": "claude-3-haiku-20240307" // Thay thế bằng "claude-3-opus-20240229" nếu muốn Sonnet
  ```

### **2. Tự Động Gửi Báo Cáo Định Kỳ**
- **Kết hợp với Node `Set Interval`** (n8n Premium) để chạy workflow hàng tuần:
  ```javascript
  // Thêm node Set Interval (1 tuần/lần)
  const interval = setInterval(() => {
    n8n.triggerWorkflow("skool-search", {
      query: "Tổng hợp trend mới trong cộng đồng",
      depth: 10
    });
  }, 7 * 24 * 60 * 60 * 1000);
  ```

### **3. Lưu Log & Theo Dõi Lỗi**
- **Thêm Node `Sticky Note`** để ghi lại lịch sử chạy:
  ```javascript
  // Trong node Sticky Note, lưu:
  {
    timestamp: new Date().toISOString(),
    query: $node["Form Trigger"].json["query"],
    status: "success" // hoặc "error"
  }
  ```
- **Kết hợp với Slack/Telegram** để báo lỗi:
  - Thêm node `Slack` hoặc `Telegram Bot` sau node `Respond with Error`.

### **4. Cập Nhật Cookie & API Key**
- **Cookie Skool** có thể hết hạn sau 30 ngày → **Tự động hóa refresh**:
  - Thêm node `HTTP Request` để kiểm tra cookie:
    ```javascript
    // Gửi request đến Skool và kiểm tra cookie
    const response = await fetch("https://www.skool.com", {
      headers: { cookie: config.skoolCookie }
    });
    if (response.status !== 200) {
      throw new Error("Cookie đã hết hạn!");
    }
    ```

---
## **📌 Kết Luận**
Workflow này **giải phóng hàng giờ mỗi tuần** cho các sếp bằng cách:
✔ **Tự động trích xuất** từ hàng ngàn bài đăng Skool.
✔ **Phân tích bằng AI Claude** để tổng hợp cảm xúc cộng đồng.
✔ **Lưu báo cáo** trong Google Docs để theo dõi lâu dài.
✔ **Hoạt động 24/7** mà không cần can thiệp.

**👉 Hành động ngay!**
1. **Cài n8n Self-hosted** trên VPS (để ổn định 24/7).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
2. **Import workflow** và cấu hình theo hướng dẫn trên.
3. **Nhập câu hỏi đầu tiên** và xem AI trả kết quả như thế nào!

**🚀 Chúc các sếp tự động hóa thành công!** 🚀