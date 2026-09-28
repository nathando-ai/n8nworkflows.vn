---
title: "🚀 Tự Động Hóa Bài Đăng LinkedIn Hàng Ngày Từ Notion - Giảm Thời Gian Làm Thủ Công 90%!"
description: "Workflow tự động hóa hoàn toàn không cần code để lấy bài viết từ Notion, xử lý nội dung, tải hình ảnh và đăng lên LinkedIn hàng ngày. Giúp các sếp tiết kiệm thời gian, duy trì nội dung liên tục và tối ưu hóa chiến dịch marketing."
slug: "tu-dong-hoa-bai-dang-linkedin-tu-notion"
tags: [n8n, automation, marketing, notion, linkedin, no-code]
keywords: [tự động hóa bài đăng LinkedIn, workflow n8n marketing, tự động hóa content marketing, tự động hóa từ Notion, đăng bài LinkedIn tự động]
---

# 🚀 **Tự Động Hóa Bài Đăng LinkedIn Hàng Ngày Từ Notion - Không Cần Code!**

## **🔥 Nỗi Đau Của Các Sếp Marketing**
Hàng ngày, các sếp phải:
- **Tìm kiếm và chuẩn bị nội dung** từ Notion, Google Docs hay các công cụ khác.
- **Chỉnh sửa và định dạng** bài viết để phù hợp với LinkedIn.
- **Tải hình ảnh** và xử lý để đáp ứng yêu cầu kích thước của LinkedIn.
- **Đăng bài thủ công**, mất thời gian và dễ quên.

**Kết quả?** Nội dung không được đăng đều, hiệu quả marketing giảm, và thời gian quý giá bị "chôn vùi" trong công việc thủ công.

**Giải pháp?** **Workflow này tự động hóa toàn bộ quy trình** - từ lấy nội dung từ Notion đến đăng bài lên LinkedIn, **với chỉ một lần setup!**

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian** lên đến **90%** so với cách làm thủ công.
✅ **Nội dung đăng đều đặn**, không bị quên hoặc bỏ quên.
✅ **Tối ưu hóa hình ảnh** tự động, phù hợp với LinkedIn.
✅ **Cập nhật trạng thái** bài viết trong Notion, theo dõi hiệu quả.
✅ **Hoạt động 24/7**, không phụ thuộc vào thời gian làm việc của cá nhân.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Notion** và **API Key Notion** (đăng ký tại [Notion API](https://www.notion.so/my-integrations)).
   - **Database Notion** chứa bài viết hàng ngày (cấu trúc: `Title`, `Content`, `Image URL`, `Status`).
2. **Tài khoản LinkedIn** và **OAuth 2.0 API Key** (cài đặt tại [LinkedIn Developer Portal](https://www.linkedin.com/developers/)).
   - **Chú ý:** Để đăng bài lên **trang công ty** (không chỉ cá nhân), cần có **trang LinkedIn Company Page** và liên kết với tài khoản cá nhân.
3. **VPS Self-hosted n8n** (không dùng phiên bản miễn phí trên cloud).
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
:::

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/2273](https://n8n.io/workflows/2273) (chọn **Export as JSON**).
2. **Mở n8n Editor** trên VPS của bạn.
3. Nhấn **Import** → Chọn file JSON vừa tải → **Import**.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ mã JSON** từ file export.
2. Trong n8n Editor, nhấn **Import** → Chọn **Paste JSON** → Dán và **Import**.

---
### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **9 node**, mỗi node đều cần cấu hình kỹ lưỡng. Dưới đây là **các bước chỉnh sửa quan trọng**:

#### **🔹 Node 1: Schedule Trigger (Khởi động hàng ngày)**
- **Cấu hình:**
  - **Schedule:** Chọn **Daily** (hàng ngày).
  - **Time:** Đặt giờ phù hợp (ví dụ: 8h sáng).
  - **Time Zone:** Chọn múi giờ của bạn (ví dụ: `Asia/Ho_Chi_Minh`).
  - **Active:** Bật **Active** để workflow chạy tự động.

#### **🔹 Node 2 & 3: Lấy Dữ liệu từ Notion**
- **Node "Filter the table for the day's post" (Lọc bài viết ngày hôm nay):**
  - **Credentials:** Chọn `notionApi` (đã setup trước).
  - **Database ID:** Điền **ID của Database Notion** chứa bài viết (tìm trong URL Notion: `https://www.notion.so/your-database-ID`).
  - **Filter:** Cấu hình để lấy bài viết có `Status = "Pending"` (hoặc tùy chỉnh theo logic của bạn).
    ```json
    {
      "property": "Status",
      "operator": "equals",
      "value": "Pending"
    }
    ```

- **Node "Fetch the content on the page" (Lấy nội dung chi tiết):**
  - **Credentials:** Chọn `notionApi`.
  - **Page ID:** Sử dụng **`{{$node["Filter the table for the day's post"].json | filterBy("Status", "Pending") | first | "id" }}`** (để lấy ID bài viết từ node trước).
  - **Operation:** Chọn `getAll` (lấy toàn bộ block).

#### **🔹 Node 4: Aggregate the Notion blocks (Kết hợp block Notion)**
- **Cấu hình mặc định** (không cần thay đổi) để ghép các block (text, image, rich text) thành một nội dung duy nhất.

#### **🔹 Node 5: Format the post (Định dạng bài viết)**
- **Mã JavaScript trong node Code:**
  ```javascript
  // Dữ liệu đầu vào từ Notion (cần xử lý)
  const notionData = $input.all();

  // Lấy nội dung và hình ảnh
  const content = notionData[0].properties.body.map(block => {
    if (block.type === "text") return block.text.content;
    if (block.type === "image") return `[![Image](${block.image.file.url})]`;
    return "";
  }).join("\n\n");

  // Lấy URL hình ảnh (nếu có)
  const imageUrl = notionData[0].properties.image?.url || null;

  // Trả về đối tượng định dạng
  return {
    json: {
      content: content,
      imageUrl: imageUrl,
      title: notionData[0].properties.title || "No Title"
    }
  };
  ```
  - **Lưu ý:**
    - Nếu nội dung Notion có **rich text**, cần điều chỉnh mã để trích xuất đúng.
    - **Hình ảnh** sẽ được xử lý ở node tiếp theo.

#### **🔹 Node 6: Download image (Tải hình ảnh)**
- **Cấu hình:**
  - **Method:** `GET`.
  - **Url:** `{{$node["Format the post"].json.imageUrl}}` (URL hình ảnh từ node trước).
  - **Response Format:** Chọn `Binary` (để tải file hình ảnh).
  - **Output:** Lưu vào biến `imageBinary`.

#### **🔹 Node 7: Publish on LinkedIn (Đăng bài)**
- **Credentials:** Chọn `linkedInOAuth2Api` (đã setup trước).
- **Operation:** Chọn `createPost`.
- **Post Content:**
  ```json
  {
    "author": "your-linkedin-profile-id",
    "lifecycleState": "PUBLISHED",
    "specificContent": {
      "com.linkedin.ugc.ShareContent": {
        "shareCommentary": {
          "text": "{{$node["Format the post"].json.content}}"
        },
        "shareMediaCategory": "NONE",
        "shareMedia": [
          {
            "status": "PUBLISHED",
            "media": {
              "status": "PUBLISHED",
              "description": {
                "text": "Image for post"
              },
              "media": {
                "status": "PUBLISHED",
                "fileName": "post-image.jpg",
                "mimeType": "image/jpeg",
                "base64Content": "{{$node["Download image"].json | base64Encode}}"
              }
            }
          }
        ]
      }
    }
  }
  ```
  - **Lưu ý:**
    - **`your-linkedin-profile-id`** thay bằng **ID của trang LinkedIn Company Page** (tìm trong URL: `https://www.linkedin.com/company/your-company-id/`).
    - **`base64Content`** được tạo từ node **Download image**.

#### **🔹 Node 8: Update post status in notion (Cập nhật trạng thái)**
- **Credentials:** Chọn `notionApi`.
- **Page ID:** Sử dụng **`{{$node["Filter the table for the day's post"].json | filterBy("Status", "Pending") | first | "id" }}`**.
- **Update Data:**
  ```json
  {
    "Status": "Published"
  }
  ```
  - **Lưu ý:** Cập nhật trạng thái từ `Pending` → `Published` để tránh đăng lại.

---
### **3. Kích Hoạt ⚡️**
1. **Test Run (Kiểm tra thử):**
   - Chạy **manual test** với dữ liệu mẫu để kiểm tra:
     - Nội dung có được lấy từ Notion không?
     - Hình ảnh có tải được không?
     - Bài viết có đăng lên LinkedIn thành công không?
     - Trạng thái trong Notion có được cập nhật không?

2. **Bật Active:**
   - Sau khi test thành công, **bật Active** cho **Schedule Trigger** để workflow chạy tự động hàng ngày.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Gửi thông báo Slack/Telegram khi đăng bài thành công:**
   - Thêm **node Slack/Telegram** sau **Publish on LinkedIn** để báo cáo.
   - Ví dụ:
     ```json
     {
       "text": "🚀 Bài viết đã đăng thành công!\nTitle: {{$node["Format the post"].json.title}}"
     }
     ```

2. **Lưu log hoạt động:**
   - Thêm **node StickyNote** (hoặc Google Sheets) để ghi lại lịch sử đăng bài, trạng thái và thời gian.

3. **Tùy chỉnh nội dung trước khi đăng:**
   - Sử dụng **node Code** thêm logic để:
     - Thêm **hashtag** tự động.
     - Chèn **link** từ URL trong Notion.
     - Xóa **kí tự đặc biệt** không phù hợp.

4. **Chia sẻ bài viết trên các nền tảng khác:**
   - Thêm **node Facebook/Instagram** để đăng bài trên nhiều nền tảng cùng lúc.

5. **Tự động tạo thumbnail cho bài viết:**
   - Sử dụng **node ImageMagick** (nếu self-hosted) để tạo thumbnail từ hình ảnh.
:::

---
## 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp để tập trung vào **strategy marketing** thay vì làm thủ công. Với **chỉ một lần setup**, nội dung sẽ được đăng tự động hàng ngày, **mang lại sự nhất quán và hiệu quả cao hơn**.

**👉 Hãy áp dụng ngay và bắt đầu tự động hóa marketing của bạn!**
Nếu có vấn đề, hãy **comment bên dưới** hoặc liên hệ với cộng đồng n8n tại [n8n Community](https://community.n8n.io/).

---
### **🔗 Tài Liệu tham khảo:**
- [Notion API Documentation](https://developers.notion.com/)
- [LinkedIn Marketing API](https://developer.linkedin.com/)
- [n8n Schedule Trigger](https://docs.n8n.io/integrations/builtins/n8n-nodes-base.scheduleTrigger/)