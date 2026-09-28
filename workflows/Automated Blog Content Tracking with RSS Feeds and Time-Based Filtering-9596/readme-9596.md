---
title: "🚀 Tự Động Hóa Theo Dõi Nội Dung Blog qua RSS với Lọc Thời Gian - Không Cần Code!"
description: "Workflow này tự động thu thập và lọc nội dung blog mới từ các nguồn RSS theo thời gian (ví dụ: chỉ lấy bài viết trong 60 ngày qua), giúp các sếp tiết kiệm thời gian và tập trung vào nội dung chất lượng cao. Hoàn toàn miễn phí và không cần API key!"
slug: "tieu-dong-ho-tra-cuu-nội-dung-blog-rss"
tags: [n8n, automation, no-code, rss-feed, content-tracking, blog-automation]
keywords: [n8n workflow rss, tự động hóa blog, theo dõi bài viết mới, lọc nội dung theo thời gian, không cần code]
---

# 🚀 **Tự Động Hóa Theo Dõi Nội Dung Blog qua RSS với Lọc Thời Gian**

### **Giải pháp hoàn hảo cho các sếp muốn theo dõi bài viết mới từ các blog chuyên ngành mà không tốn thời gian thủ công!**

Hãy tưởng tượng: Bạn không phải mở từng trang web, tìm kiếm bài viết mới, hoặc lo lắng bỏ lỡ thông tin quan trọng. **Workflow này tự động hóa toàn bộ quá trình** bằng cách:
1. **Thu thập** bài viết mới từ các nguồn RSS (ví dụ: blog n8n, Zapier, hoặc blog của các đối thủ).
2. **Lọc** chỉ giữ lại những bài viết **mới nhất** (ví dụ: trong vòng 60 ngày qua).
3. **Cung cấp** kết quả sạch sẽ, sẵn sàng để bạn **xuất vào Google Sheets, Slack, hoặc email** để phân tích.

Không cần viết code, không cần API key, và **hoàn toàn miễn phí**!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không phải thủ công tìm kiếm bài viết mới trên từng trang web.
- **Chính xác 100%**: Lọc bài viết theo thời gian (ví dụ: chỉ lấy bài viết trong 30/60/90 ngày qua).
- **Tập trung vào nội dung chất lượng**: Bỏ qua bài viết cũ, tập trung vào thông tin mới nhất.
- **Hoạt động liên tục**: Workflow chạy tự động mỗi khi có bài viết mới (không cần can thiệp).
- **Dễ dàng mở rộng**: Xuất dữ liệu vào Google Sheets, Slack, hoặc email để phân tích sâu hơn.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Danh sách RSS Feed** của các blog muốn theo dõi (ví dụ: `https://blog.n8n.io/feed.xml`).
   - *Lưu ý*: Nếu link RSS không hoạt động, sử dụng **Perplexity AI** hoặc công cụ tìm kiếm RSS như [Feedspot](https://www.feedspot.com/) để tìm link chính xác.
2. **Số ngày lọc** (ví dụ: `60` để chỉ lấy bài viết trong 60 ngày qua).
3. **Tài khoản Google Sheets** (nếu muốn xuất dữ liệu vào bảng tính).

---
:::note[CHUẨN BỊ]
- **Không cần API key**: Workflow hoạt động hoàn toàn với các nguồn RSS công khai.
- **N8n Self-hosted**: Để workflow chạy 24/7, các sếp nên cài n8n trên VPS (không dùng phiên bản miễn phí của n8n.io).
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n Editor](https://n8n.io/editor/) và chọn **"Import Workflow"**.
2. Chọn file JSON đã tải xuống từ [link gốc](https://n8n.io/workflows/9596) hoặc paste JSON vào ô **"Paste JSON"**.
3. Nhấn **"Import"** để workflow xuất hiện trên canvas.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **12 node**, nhưng các sếp chỉ cần chú ý đến **5 node quan trọng** sau:

| **Tên Node**               | **Loại Node**       | **Cách cấu hình**                                                                 | **Lưu ý**                                                                 |
|-----------------------------|---------------------|----------------------------------------------------------------------------------|----------------------------------------------------------------------------|
| **RSS → Items**             | `rssFeedRead`       | Điền **URL RSS Feed** của blog (ví dụ: `https://blog.n8n.io/feed.xml`).          | Nếu link sai, workflow sẽ báo lỗi **403**. Sử dụng Perplexity để tìm link mới nhất. |
| **max_content_age_days**    | `set`               | Đặt giá trị số ngày lọc (ví dụ: `60` để lấy bài viết trong 60 ngày qua).          | Giá trị mặc định là `60`. Các sếp có thể thay đổi theo nhu cầu.             |
| **blogs to track**          | `set`               | Danh sách **URL RSS Feed** của các blog muốn theo dõi (ví dụ: `["https://blog.n8n.io/feed.xml", "https://zapier.com/blog/feed"]`). | Mỗi URL phải là một dòng trong danh sách.                                |
| **Filter Out Old Blogs**    | `if`                | **Không cần chỉnh** (cấu hình sẵn để lọc bài viết cũ).                          | Node này tự động gửi bài viết **mới** vào đường `true`, bài viết **cũ** vào `false`. |
| **Merge3**                  | `merge`             | **Không cần chỉnh** (gộp dữ liệu từ các nguồn RSS).                              | Node này kết hợp dữ liệu từ tất cả các RSS Feed.                          |

##### **Cách thêm node xuất dữ liệu (ví dụ: Google Sheets)**
Sau khi bài viết mới được lọc (đường `true` của node `Filter Out Old Blogs`), các sếp có thể thêm node **Google Sheets** để xuất dữ liệu:
1. Thêm node **`Google Sheets`** vào đường `true` của node `Filter Out Old Blogs`.
2. Chọn **credentials** của tài khoản Google Sheets.
3. Chọn **Sheet Name** và **Range** (ví dụ: `Sheet1!A1`).
4. Chọn **columns** muốn xuất (ví dụ: `title`, `link`, `publishedDate`).

---
#### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **"Execute Workflow"** để kiểm tra workflow có hoạt động không.
   - Kiểm tra **log** để đảm bảo bài viết mới được lọc chính xác.
2. **Bật Active**:
   - Sau khi test thành công, chuyển trạng thái workflow từ **"Inactive"** sang **"Active"**.
   - Workflow sẽ chạy tự động mỗi khi có bài viết mới trên các RSS Feed đã cấu hình.

---
### ✍️ **Mẹo & gợi ý nâng cao**
1. **Xuất dữ liệu vào Slack/Telegram**:
   - Thêm node **`Slack`** hoặc **`Telegram Bot`** vào đường `true` của node `Filter Out Old Blogs` để nhận thông báo khi có bài viết mới.
   - *Cách cấu hình*:
     - Thêm node **`Slack`** và chọn **credentials** của tài khoản Slack.
     - Điền **channel** và **message template** (ví dụ: `New blog post: {{ $node["RSS → Items"].json["title"] }} - {{ $node["RSS → Items"].json["link"] }}`).

2. **Lưu log vào Google Drive**:
   - Thêm node **`Google Drive`** vào đường `false` của node `Filter Out Old Blogs` để lưu bài viết cũ vào một folder riêng.

3. **Tự động gửi báo cáo định kỳ**:
   - Sử dụng node **`Set`** để định nghĩa thời gian (ví dụ: `0 9 * * *` để chạy hàng ngày lúc 9h sáng).
   - Thêm node **`Email`** để gửi báo cáo tổng hợp về email của các sếp.

4. **Tăng tốc độ xử lý**:
   - Nếu có nhiều RSS Feed, sử dụng node **`Split In Batches`** để xử lý từng feed một cách hiệu quả.

---
### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa việc theo dõi bài viết mới từ các blog chuyên ngành **không cần viết code**. Bằng cách cấu hình đơn giản, các sếp có thể:
✅ **Tiết kiệm thời gian** không phải thủ công tìm kiếm bài viết.
✅ **Lọc bài viết mới nhất** theo thời gian (ví dụ: 30/60/90 ngày).
✅ **Xuất dữ liệu vào Google Sheets, Slack, hoặc email** để phân tích.

**Hãy import workflow ngay hôm nay và bắt đầu tự động hóa công việc của mình!** 🚀

---
#### **🔗 Tài liệu tham khảo**
- [Tìm kiếm RSS Feed mới nhất](https://www.feedspot.com/)
- [Perplexity AI - Tìm kiếm thông tin chính xác](https://www.perplexity.ai/)
- [Cách cấu hình Google Sheets trong n8n](https://docs.n8n.io/integrations/builtins/google-sheets/)