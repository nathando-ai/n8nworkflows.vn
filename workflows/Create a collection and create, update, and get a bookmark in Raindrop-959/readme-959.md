---
title: "🌟 Tự Động Hóa Quản Lý Bookmark Raindrop: Tạo, Cập Nhật & Lấy Dữ Liệu Mọi Lúc, Không Cần Code"
description: "Workflow này giúp các sếp tự động hóa việc quản lý collection và bookmark trên Raindrop.io chỉ với 4 node, tiết kiệm thời gian và tránh mất mát thông tin quan trọng. Hoạt động 24/7, không cần can thiệp thủ công."
slug: "tu-dong-hoa-quan-ly-bookmark-raindrop"
tags: [n8n, automation, no-code, Raindrop, quản lý bookmark]
keywords: [n8n workflow Raindrop, tự động hóa quản lý link, Raindrop API, lưu trữ bookmark tự động, tự động hóa không code]
---

# 🚀 **Tự Động Hóa Quản Lý Bookmark Raindrop: Tạo, Cập Nhật & Lấy Dữ Liệu Mọi Lúc**

### **Nỗi Đau Của Các Sếp**
Các sếp thường phải mất thời gian quý báu để:
- **Tạo collection** mới để phân loại bookmark theo chủ đề (ví dụ: "Marketing", "Tech", "Thời sự").
- **Thêm bookmark** vào collection khi tìm thấy link quan trọng trên mạng.
- **Cập nhật** bookmark cũ khi link bị thay đổi hoặc cần bổ sung thông tin mới.
- **Lấy dữ liệu** bookmark để chia sẻ hoặc phân tích sau này.

Với **Raindrop.io** — một công cụ lưu trữ bookmark mạnh mẽ — việc này trở nên đơn giản hơn, nhưng **tự động hóa hoàn toàn** sẽ giúp các sếp **tiết kiệm thời gian, tránh lỗi thủ công và làm việc hiệu quả hơn**.

Workflow này **giải quyết tất cả các vấn đề trên chỉ với 4 node**, giúp các sếp **tạo collection, thêm bookmark, cập nhật và lấy dữ liệu một cách tự động**, không cần viết một dòng code nào.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định 24/7**, các sếp nên cài đặt n8n trên **VPS riêng** (Self-hosted) thay vì dùng phiên bản miễn phí trên cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Không cần thủ công tạo collection hoặc thêm bookmark.
✅ **Chính xác 100%**: Không bị lỗi copy-paste hoặc quên cập nhật.
✅ **Hoạt động liên tục**: Workflow chạy tự động, ngay cả khi các sếp ngủ.
✅ **Dữ liệu sẵn sàng**: Lấy bookmark bất kỳ lúc nào để chia sẻ hoặc phân tích.
✅ **Tích hợp Raindrop**: Sử dụng API Raindrop để quản lý bookmark một cách chuyên nghiệp.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần:
1. **Tài khoản Raindrop.io** và **API Key OAuth2** của Raindrop.
   - Cách lấy API Key:
     - Đăng nhập vào [Raindrop.io](https://raindrop.io/).
     - Vào **Settings > API Keys** và tạo một API Key mới.
     - Lưu API Key này để sử dụng trong workflow.
2. **n8n Self-hosted** (không dùng phiên bản cloud).
3. **Dữ liệu đầu vào** (nếu tự động hóa từ nguồn khác, ví dụ: Slack, Google Sheets, hoặc Webhook).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**.

**Bước 1:** Tải file JSON từ [link gốc](https://n8n.io/workflows/959) hoặc sao chép JSON dưới đây:
```json
[
  {
    "name": "Raindrop",
    "type": "raindrop",
    "credentials": ["raindropOAuth2Api"],
    "keyParameters": {
      "operation": "create"
    }
  },
  {
    "name": "Raindrop1",
    "type": "raindrop",
    "credentials": ["raindropOAuth2Api"],
    "keyParameters": {
      "operation": "create",
      "resource": "bookmark"
    }
  },
  {
    "name": "Raindrop2",
    "type": "raindrop",
    "credentials": ["raindropOAuth2Api"],
    "keyParameters": {
      "operation": "update",
      "resource": "bookmark"
    }
  },
  {
    "name": "Raindrop3",
    "type": "raindrop",
    "credentials": ["raindropOAuth2Api"],
    "keyParameters": {
      "resource": "bookmark"
    }
  }
]
```

**Bước 2:** Mở **n8n Editor** và chọn **Import Workflow** > Dán JSON vào.

---

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này bao gồm **4 node Raindrop**, mỗi node thực hiện một chức năng khác nhau. Các sếp cần cấu hình **credentials** và **tham số** như sau:

| **Node**  | **Chức Năng**               | **Cấu Hình Cần Thiết**                                                                 | **Lưu Ý**                                                                 |
|-----------|-----------------------------|---------------------------------------------------------------------------------------|----------------------------------------------------------------------------|
| **Raindrop** | Tạo **collection** mới      | - **Credentials**: Chọn `raindropOAuth2Api` (đã cấu hình trước).                     | Điền tên collection vào `data.name` (ví dụ: `"Marketing"`).               |
| **Raindrop1** | **Thêm bookmark** vào collection | - **Credentials**: `raindropOAuth2Api`. <br> - **Resource**: `bookmark`. <br> - **Operation**: `create`. | Điền `data.url` (link bookmark), `data.title` (tiêu đề), và `data.collectionId` (ID collection). |
| **Raindrop2** | **Cập nhật bookmark**      | - **Credentials**: `raindropOAuth2Api`. <br> - **Resource**: `bookmark`. <br> - **Operation**: `update`. | Cần `data.id` (ID bookmark) và `data.url` (link mới).                     |
| **Raindrop3** | **Lấy bookmark**            | - **Credentials**: `raindropOAuth2Api`. <br> - **Resource**: `bookmark`.               | Chọn `data.id` hoặc `data.collectionId` để lấy dữ liệu.                   |

**Cách cấu hình credentials:**
1. Vào **Settings > Credentials** trong n8n.
2. Tạo một **new credential** với loại `raindropOAuth2Api`.
3. Điền **API Key** từ Raindrop.io vào trường `apiKey`.
4. Lưu và chọn credential này trong các node.

---

#### **3. Kích Hoạt ⚡️**
**Bước 1: Test Run với Dữ Liệu Mẫu**
- Chọn **Run Workflow** và điền dữ liệu mẫu vào các node:
  - **Raindrop (Tạo collection)**:
    ```json
    {
      "name": "Marketing"
    }
    ```
  - **Raindrop1 (Thêm bookmark)**:
    ```json
    {
      "url": "https://example.com/marketing",
      "title": "Bài viết Marketing mới",
      "collectionId": "12345" // ID collection từ node Raindrop
    }
    ```
  - **Raindrop2 (Cập nhật bookmark)**:
    ```json
    {
      "id": "67890", // ID bookmark từ Raindrop
      "url": "https://example.com/marketing-update"
    }
    ```
  - **Raindrop3 (Lấy bookmark)**:
    ```json
    {
      "id": "67890" // ID bookmark cần lấy
    }
    ```

**Bước 2: Bật Active Workflow**
Sau khi test thành công, chọn **Active** để workflow chạy tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tích Hợp với Slack/Telegram**
   - Sử dụng **node Slack** hoặc **Telegram Bot** để thông báo khi bookmark được thêm/cập nhật.
   - Ví dụ: Khi một bookmark mới được thêm vào collection, gửi thông báo đến Slack.

2. **Lưu Log Dữ Liệu**
   - Sử dụng **node Google Sheets** hoặc **node Airtable** để lưu lịch sử thay đổi bookmark.
   - Giúp các sếp theo dõi và phân tích dữ liệu lâu dài.

3. **Tự Động Hóa từ Google Drive/Notion**
   - Sử dụng **node Google Drive** hoặc **Notion API** để lấy danh sách link từ tài liệu và tự động thêm vào Raindrop.

4. **Xử Lý Lỗi & Khôi Phục**
   - Thêm **node Set** hoặc **node If** để kiểm tra lỗi và gửi email thông báo nếu có vấn đề.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tự động hóa quản lý bookmark Raindrop một cách hiệu quả**, không cần viết code. Với chỉ **4 node**, các sếp có thể:
✔ **Tạo collection** tự động.
✔ **Thêm bookmark** vào collection một cách nhanh chóng.
✔ **Cập nhật bookmark** khi cần.
✔ **Lấy dữ liệu bookmark** bất kỳ lúc nào.

**Hãy áp dụng ngay workflow này và làm việc thông minh hơn!** 🚀

---
**💡 Cần hỗ trợ thêm?**
- Trả lời câu hỏi trong [community n8n](https://community.n8n.io/).
- Liên hệ với [TinoHost](https://tino.vn/) để hỗ trợ cài đặt n8n trên VPS.